---
title: Definire le partizioni nei modelli DirectQuery | Documenti Microsoft
ms.custom: 
ms.date: 02/22/2018
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5f179ba9-6efb-46ae-90e5-945bbfddb719
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 21e629bbac90f30562c6b8434e2a73a71fdea4ed
ms.sourcegitcommit: d8ab09ad99e9ec30875076acee2ed303d61049b7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/23/2018
---
# <a name="define-partitions-in-directquery-models"></a>Definire le partizioni nei modelli DirectQuery
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
In questa sezione viene illustrato come utilizzare le partizioni nei modelli DirectQuery. Per ulteriori informazioni generali sulle partizioni nei modelli tabulari, vedere [partizioni](../../analysis-services/tabular-models/partitions-ssas-tabular.md).  
  
> [!NOTE]  
>  Anche se una tabella può includere più partizioni, nella modalità DirectQuery è possibile impostarne una sola per l'utilizzo durante l'esecuzione di query. Il requisito della partizione singola si applica ai modelli DirectQuery a tutti i livelli di compatibilità.  
  
## <a name="using-partitions-in-directquery-mode"></a>Utilizzo di partizioni in modalità DirectQuery  
 Per ogni tabella, è necessario specificare una sola partizione da utilizzare come origine dati DirectQuery.  In presenza di più partizioni, quando si abilita la modalità DirectQuery per il modello, per impostazione predefinita la prima partizione creata nella tabella viene contrassegnata come partizione DirectQuery. Questa impostazione potrà essere modificata in seguito tramite Gestione partizioni in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Perché consentire una sola partizione nella modalità DirectQuery?  
  
 Nei modelli tabulari, come nei modelli OLAP, le partizioni di una tabella sono definite tramite query SQL. È responsabilità dello sviluppatore che crea la definizione della partizione assicurarsi che le partizioni non si sovrappongano. In Analysis Services non viene controllato se i record fanno parte di una o più partizioni.  
  
 Le partizioni in un modello tabulare memorizzato nella cache si comportano allo stesso modo. Se si utilizza un modello in memoria, durante l'accesso alla cache, le formule DAX vengono valutate per ogni partizione e i risultati vengono combinati. Tuttavia, quando un modello tabulare utilizza la modalità DirectQuery, sarebbe impossibile valutare più partizioni, combinare i risultati e convertirli in un'istruzione SQL per l'invio all'archivio dati relazionale. Questa operazione potrebbe causare una calo inaccettabile delle prestazioni, nonché imprecisioni potenziali durante l'aggregazione dei dati.  
  
 Quindi, per query risposte in modalità DirectQuery, il server usa una sola partizione contrassegnata come partizione primaria per l'accesso DirectQuery, denominata *partizione DirectQuery*.  La query SQL specificata nella definizione di questa partizione definisce il set completo di dati che possono essere usati per rispondere alle query in modalità DirectQuery.  
  
 Se non si definisce in modo esplicito una partizione, il motore emette una query SQL sull'intera origine dati relazionale, esegue eventuali operazioni basate su set imposte dalla formula DAX e restituisce i risultati della query.  
  
  
## <a name="change-a-directquery-partition"></a>Modificare una partizione DirectQuery  
 Poiché è possibile designare come partizione DirectQuery solo una partizione di una tabella, per impostazione predefinita in Analysis Services viene utilizzata la prima partizione creata nella tabella. Durante la creazione del progetto di modello, è possibile modificare la partizione DirectQuery tramite la finestra di dialogo Gestione partizioni di [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Per i modelli distribuiti, tale partizione può essere modificata tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
#### <a name="change-the-directquery-partition-for-a-tabular-model-project"></a>Modificare la partizione DirectQuery per un progetto di modello tabulare  
  
1.  In Progettazione modelli di [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]fare clic sulla tabella (scheda) in cui è contenuta la tabella partizionata.  
  
2.  Fare clic sul menu **Tabella** , quindi scegliere **Partizioni**.  
  
3.  In **Gestione partizioni**nel nome della partizione attualmente designata come partizione DirectQuery è contenuto il prefisso **(DirectQuery)** .  
  
     Selezionare una partizione diversa dall'elenco **Partizioni** , quindi fare clic su **Imposta come DirectQuery**. Il pulsante **Imposta come DirectQuery** non è abilitato quando è selezionata la partizione DirectQuery corrente e non è visibile se il modello non è stato abilitato per la modalità DirectQuery.  
  
4.  Se necessario, modificare le opzioni di elaborazione, quindi fare clic su **OK**.  
  
#### <a name="change-the-directquery-partition-for-a-deployed-tabular-model"></a>Modificare la partizione DirectQuery per un modello tabulare distribuito  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]aprire il database modello in Esplora oggetti.  
  
2.  Espandere il nodo **Tabelle** , fare clic con il pulsante destro del mouse sulla tabella partizionata e selezionare **Partizioni**.  
  
     Nel nome della partizione designata per l'utilizzo nella modalità DirectQuery è contenuto il prefisso (DirectQuery).  
  
3.  Per cambiare la partizione, fare clic sull'icona della barra degli strumenti **DirectQuery** per aprire la finestra di dialogo **Imposta partizione DirectQuery** . L'icona della barra degli strumenti DirectQuery non è disponibile per i modelli che non sono stati abilitati per DirectQuery.  
  
4.  Scegliere una partizione diversa dall'elenco a discesa **Nome partizione** e modificare le opzioni di elaborazione sulla partizione, se necessario.  
  
## <a name="partitions-in-cached-models-and-in-directquery-models"></a>Partizioni nei modelli memorizzati nella cache e nei modelli DirectQuery  
 Quando si configura una partizione DirectQuery, è necessario specificare le opzioni di elaborazione per la partizione.  
  
 Sono disponibili due opzioni di elaborazione per la partizione DirectQuery: Per impostare questa proprietà, utilizzare **Gestore partizioni** in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e selezionare la proprietà **Opzione di elaborazione** . Nella tabella seguente vengono elencati i valori di questa proprietà e vengono illustrati gli effetti di ciascun valore combinato alla proprietà DirectQueryUsage nella stringa di connessione:  
  
|Proprietà della**stringa di connessione** |Proprietà**Opzione di elaborazione** |Note|  
|------------------------------------|------------------------------------|-----------|  
|DirectQuery|Non elaborare mai questa partizione|Se il modello utilizza solo DirectQuery, l'elaborazione non è mai necessaria.<br /><br /> Nei modelli ibridi è possibile configurare la partizione DirectQuery in modo che non venga mai elaborata. Ad esempio, se si lavora su un set di dati di grandi dimensioni e non si desidera che i risultati completi vengano aggiunti alla cache, è possibile specificare che la partizione DirectQuery includa l'unione dei risultati di tutte le altre partizioni nella tabella e quindi non elaborare mai l'unione. Le query dirette all'origine relazionale non saranno interessate, mentre le query sui dati memorizzati nella cache combineranno i dati delle altre partizioni.|  
|DataView=Sample<br /><br /> Si applica ai modelli tabulari usano le visualizzazioni di dati di esempio|Consenti l'elaborazione della partizione|Se il modello usa i dati di esempio, è possibile elaborare la tabella per restituire un set di dati filtrati che fornisce indicazioni visive durante la progettazione del modello.|  
|DirectQueryUsage=InMemory con DirectQuery<br /><br /> Si applica ai modelli tabulari 1100 o 1103 in esecuzione in combinazioni di modalità in memoria e DirectQuery|Consenti l'elaborazione della partizione|Se il modello usa la modalità ibrida, è necessario usare la stessa partizione per le query nell'origine dati in memoria e DirectQuery.|  
  
## <a name="see-also"></a>Vedere anche  
 [Partizioni](../../analysis-services/tabular-models/partitions-ssas-tabular.md)  
  
  
