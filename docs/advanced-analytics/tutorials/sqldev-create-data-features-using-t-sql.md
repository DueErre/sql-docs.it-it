---
title: "Lezione 4: Creare funzionalità di dati con T-SQL | Documenti Microsoft"
ms.custom: 
ms.date: 07/26/2016
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2016
dev_langs:
- R
- TSQL
ms.assetid: 5b2f4c44-6192-40df-abf1-fc983844f1d0
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 5802fe172f8476d11a776b15fd2038ebc6917eaf
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2018
---
# <a name="lesson-4-create-data-features-using-t-sql"></a>Lezione 4: Creare funzionalità di dati con T-SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

In questo articolo fa parte di un'esercitazione per gli sviluppatori SQL su come usare il linguaggio R in SQL Server.

In questo passaggio si apprenderà come creare funzionalità dai dati non elaborati tramite una funzione [!INCLUDE[tsql](../../includes/tsql-md.md)] . Tale funzione verrà quindi chiamata da una stored procedure per creare una tabella contenente i valori della funzionalità.

## <a name="about-feature-engineering"></a>Sulla progettazione di funzionalità

Dopo varie sessioni di esplorazione dei dati si sono raccolte alcune informazioni relative ai dati e si è pronti a passare alla *progettazione di funzionalità*. Questo processo di creazione di funzionalità significative dai dati non elaborati è un passaggio critico per la creazione di modelli analitici.

In questo set di dati, i valori di distanza sono in base alla distanza misuratore segnalati e non necessariamente distanza geografica o la distanza effettiva percorsa. Pertanto è necessario calcolare la distanza diretta tra i punti di inizio e fine della corsa, usando le coordinate disponibili nel set di dati di origine NYC Taxi. È possibile farlo usando la [formula dell'emisenoverso](https://en.wikipedia.org/wiki/Haversine_formula) in una funzione [!INCLUDE[tsql](../../includes/tsql-md.md)] personalizzata.

Si userà una funzione T-SQL personalizzata, _fnCalculateDistance_, per calcolare la distanza con la formula dell'emisenoverso e una seconda funzione T-SQL personalizzata, _fnEngineerFeatures_, per creare una tabella contenente tutte le funzionalità.

Il processo generale è il seguente:

- Creare la funzione di T-SQL che esegue i calcoli

- Chiamare la funzione per generare i dati della funzionalità

- Salvare i dati della funzionalità in una tabella

## <a name="calculate-trip-distance-using-fncalculatedistance"></a>Calcolare distanza di andata e ritorno utilizzando fnCalculateDistance

La funzione _fnCalculateDistance_ deve sono stati scaricati e registrato con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] come parte della preparazione per questa esercitazione. È opportuno esaminare il codice.
  
1. In [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]espandere **Programmabilità**, **Funzioni** e quindi **Funzioni a valori scalari**.   

2. Fare clic con il pulsante destro del mouse su _fnCalculateDistance_e selezionare **Modifica** per aprire lo script [!INCLUDE[tsql](../../includes/tsql-md.md)] in una nuova finestra Query.
  
    ```SQL
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)  
    -- User-defined function that calculates the direct distance between two geographical coordinates.  
    RETURNS float  
    AS  
    BEGIN  
      DECLARE @distance decimal(28, 10)  
      -- Convert to radians  
      SET @Lat1 = @Lat1 / 57.2958  
      SET @Long1 = @Long1 / 57.2958  
      SET @Lat2 = @Lat2 / 57.2958  
      SET @Long2 = @Long2 / 57.2958  
      -- Calculate distance  
      SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))  
      --Convert to miles  
      IF @distance <> 0  
      BEGIN  
        SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);  
      END  
      RETURN @distance  
    END
    GO
    ```
  
    - La funzione è una funzione con valori scalari che restituisce un singolo valore di dati di un tipo predefinito.
  
    - Accetta come input valori di latitudine e longitudine, ottenuti dalle località di inizio e fine della corsa. La formula dell'emisenoverso converte le posizioni in radianti e usa tali valori per calcolare la distanza diretta in miglia tra queste due posizioni.

## <a name="generate-the-features-using-fnengineerfeatures"></a>Generare le funzionalità usando _fnEngineerFeatures_

Per aggiungere i valori calcolati in una tabella che può essere utilizzata per il training del modello, si userà un'altra funzione, _fnEngineerFeatures_. La nuova funzione chiama la funzione di T-SQL creata in precedenza, _fnCalculateDistance_, per ottenere la distanza tra i percorsi di ritiro e deposito diretta. 

1. Osservare il codice della funzione T-SQL personalizzata _fnEngineerFeatures_, creata in preparazione a questa procedura dettagliata.
  
    ```SQL
    CREATE FUNCTION [dbo].[fnEngineerFeatures] (  
    @passenger_count int = 0,  
    @trip_distance float = 0,  
    @trip_time_in_secs int = 0,  
    @pickup_latitude float = 0,  
    @pickup_longitude float = 0,  
    @dropoff_latitude float = 0,  
    @dropoff_longitude float = 0)  
    RETURNS TABLE  
    AS
      RETURN
      (
      -- Add the SELECT statement with parameter references here
      SELECT
        @passenger_count AS passenger_count,
        @trip_distance AS trip_distance,
        @trip_time_in_secs AS trip_time_in_secs,
        [dbo].[fnCalculateDistance](@pickup_latitude, @pickup_longitude, @dropoff_latitude, @dropoff_longitude) AS direct_distance
  
      )
    GO
    ```

    + Questa funzione con valori di tabella che accetta più colonne come input e restituisce una tabella con più colonne di funzionalità.

    + Lo scopo di questa funzione consiste nel creare nuove funzionalità per l'utilizzo nella compilazione di un modello.

2.  Per verificare il funzionamento di questa funzione, utilizzarla per calcolare la distanza geografica per tali percorsi in cui la distanza a consumo era 0 ma i percorsi di ritiro e deposito erano diversi.
  
    ```SQL
        SELECT tipped, fare_amount, passenger_count,(trip_time_in_secs/60) as TripMinutes,
        trip_distance, pickup_datetime, dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) AS direct_distance
        FROM nyctaxi_sample
        WHERE pickup_longitude != dropoff_longitude and pickup_latitude != dropoff_latitude and trip_distance = 0
        ORDER BY trip_time_in_secs DESC
    ```
  
    Come si può notare, la distanza indicata dal tassametro non corrisponde sempre alla distanza geografica. Ecco perché la progettazione delle funzionalità è così importante. È possibile utilizzare queste funzionalità migliorate di dati per eseguire il training di un modello di machine learning con R.

## <a name="next-lesson"></a>Lezione successiva

[Lezione 5: Eseguire il training e salvare un modello utilizzando T-SQL](../r/sqldev-train-and-save-a-model-using-t-sql.md)

## <a name="previous-lesson"></a>Lezione precedente

[Lezione 3: Esplorare e visualizzare i dati](../tutorials/sqldev-explore-and-visualize-the-data.md)
