---
title: Creare un modello di traccia (SQL Server Profiler) | Documenti Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: sql-server-profiler
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- templates [SQL Server], traces
- trace templates [SQL Server]
- saving trace template
ms.assetid: 025868b0-3790-4cda-8757-5a58327bfba0
caps.latest.revision: "24"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 23a7719304b70e0c981a3bfbc9ad780d45cdd721
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/17/2018
---
# <a name="create-a-trace-template-sql-server-profiler"></a>Creare un modello di traccia (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]In questo argomento viene descritto come creare un nuovo modello di traccia tramite [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
### <a name="to-create-a-trace-template"></a>Per creare un modello di traccia  
  
1.  Scegliere **Modelli** dal menu **File**e quindi fare clic su **Nuovo modello**.  
  
2.  Nella finestra di dialogo **Proprietà modello di traccia** selezionare il tipo di server nell'elenco **Tipo server**.  
  
3.  Nella casella **Nome nuovo modello** immettere un nome per il modello.  
  
4.  Facoltativamente, selezionare la casella di controllo **Basa il nuovo modello sul seguente modello esistente**e quindi fare clic su un modello nell'elenco.  
  
     Tutti gli eventi, le colonne di dati e i filtri vengono impostati inizialmente come specificato nel modello selezionato.  
  
5.  Facoltativamente, selezionare la casella di controllo **Usa come modello predefinito per il tipo di server selezionato**.  
  
6.  Nella scheda **Selezione eventi** aggiungere, rimuovere o modificare eventi, colonne di dati o filtri.  
  
7.  Nella scheda **Selezione eventi**usare il controllo griglia per aggiungere o rimuovere eventi e colonne di dati dal file di traccia, nel modo seguente:  
  
    -   Per aggiungere un evento, espandere la categoria di eventi appropriata nella colonna **Eventi** e quindi selezionare il nome dell'evento.  
  
    -   Quando si aggiunge un evento, tutte le colonne di dati significative vengono incluse per impostazione predefinita. Per rimuovere una colonna di dati per un evento da una traccia, deselezionare la casella di controllo nella colonna di dati per l'evento.  
  
    -   Per aggiungere i filtri, fare clic sul nome della colonna di dati e specificare i criteri del filtro nella finestra di dialogo **Modifica filtro** . È anche possibile fare clic con il pulsante destro del mouse sul nome della colonna di dati e scegliere **Modifica filtro colonne** per avviare la finestra di dialogo **Modifica filtro** . Fare clic su **OK** per aggiungere il filtro.  
  
8.  Fare clic su **Salva**.  
  
## <a name="see-also"></a>Vedere anche  
 [Specificare eventi e colonne di dati per un File di traccia &#40; SQL Server Profiler &#41;](../../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)   
 [Derivare un modello da una traccia in esecuzione &#40; SQL Server Profiler &#41;](../../tools/sql-server-profiler/derive-a-template-from-a-running-trace-sql-server-profiler.md)   
 [Derivare un modello da un File di traccia o tabella di traccia &#40; SQL Server Profiler &#41;](../../tools/sql-server-profiler/derive-a-template-from-a-trace-file-or-trace-table-sql-server-profiler.md)   
 [Modelli e autorizzazioni di SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
