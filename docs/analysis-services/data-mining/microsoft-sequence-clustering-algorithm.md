---
title: Algoritmo Microsoft Sequence Clustering | Documenti Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- clusters [Analysis Services]
- algorithms [data mining]
- sequence clustering algorithms [Analysis Services]
- sequence [Analysis Services]
ms.assetid: ae779a1f-0adb-4857-afbd-a15543dff299
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 181b95753ac004aef4da9134ce46347c4cffa304
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/15/2018
---
# <a name="microsoft-sequence-clustering-algorithm"></a>Algoritmo Microsoft Sequence Clustering
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
[!INCLUDE[msCoName](../../includes/msconame-md.md)] Sequence Clustering è un algoritmo di tipo unico che combina l'analisi delle sequenze con il clustering. È possibile usare questo algoritmo per esplorare i dati contenenti eventi da collegare in una *sequenza*. L'algoritmo consente di individuare le sequenze più comuni ed esegue il clustering per individuare le sequenze simili. Gli esempi seguenti illustrano i tipi di sequenze che possono essere acquisite come dati per il Machine Learning, al fine di ottenere informazioni su problemi o scenari aziendali comuni:  
  
-   Clickstream or percorsi di navigazione generati dagli utenti durante l'uso di un sito Web.  
  
-   Log in cui vengono elencati eventi che precedono un incidente, ad esempio errori del disco rigido o deadlock del server.  
  
-   Record di transazioni in cui viene descritto l'ordine in base al quale un cliente aggiunge articoli al carrello durante gli acquisti online.  
  
-   Record in cui si seguono le interazioni del cliente (o paziente) nel tempo, per stimare annullamenti del servizio o altri risultati insufficienti.  
  
 Questo algoritmo è simile per molti versi all'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Clustering. ma, anziché rilevare cluster di case contenenti attributi simili, l'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Sequence Clustering individua i cluster di case contenenti percorsi simili in una sequenza.  
  
## <a name="example"></a>Esempio  
 Nel sito Web di [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] vengono raccolte informazioni sulle pagine visitate dagli utenti del sito e sul relativo ordine di esplorazione. Poiché l'azienda accetta solo ordini online, i clienti devono accedere al sito. In questo modo, l'azienda ottiene informazioni di esplorazione per il profilo di ogni cliente. Tramite l'applicazione dell'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Sequence Clustering a tali dati, l'azienda può individuare gruppi o cluster di clienti con schemi di acquisto o sequenze di selezioni simili. In seguito, l'azienda può utilizzare tali cluster per analizzare gli spostamenti degli utenti nel sito Web, identificare le pagine più strettamente correlate alla vendita di un prodotto specifico ed eseguire la stima delle pagine che con maggiore probabilità verranno visitate successivamente.  
  
## <a name="how-the-algorithm-works"></a>Funzionamento dell'algoritmo  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Sequence Clustering è un algoritmo ibrido che combina tecniche di clustering e l'analisi delle catene di Markov per identificare i cluster e le relative sequenze.  Una delle caratteristiche distintive dell'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Sequence Clustering è l'utilizzo dei dati in sequenza. Questi dati rappresentano in genere una serie di eventi o transizioni tra stati in un set di dati, ad esempio una serie di acquisti di prodotti o di clic sul Web per un determinato utente. Per determinare le sequenze migliori da usare come input per il clustering, l'algoritmo esamina tutte le probabilità di transizione e misura le differenze, o distanze, tra tutte le sequenze possibili del set di dati. Dopo la creazione dell'elenco di sequenze candidate, l'algoritmo usa le informazioni sulla sequenza come input per il clustering tramite EM (Expectation Maximization).  
  
 Per una descrizione dettagliata dell'implementazione, vedere [Riferimento tecnico per l'algoritmo Microsoft Sequence Clustering](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm-technical-reference.md).  
  
## <a name="data-required-for-sequence-clustering-models"></a>Dati necessari per i modelli Sequence Clustering  
 Quando si preparano dati da utilizzare nel training di un modello Sequence Clustering, è importante comprendere i requisiti per l'algoritmo specifico, tra cui la quantità di dati necessari e la modalità di utilizzo dei dati.  
  
 I requisiti per un modello Sequence Clustering sono i seguenti:  
  
-   **Una colonna a chiave singola** Un modello Sequence Clustering richiede una chiave che identifica i record.  
  
-   **Una colonna della sequenza** Per i dati in sequenza, il modello deve disporre di una tabella annidata contenente una colonna di ID sequenza. L'ID sequenza può essere qualsiasi tipo di dato ordinabile. Ad esempio, è possibile utilizzare un identificatore di pagina Web, un numero intero o una stringa di testo, purché la colonna identifichi gli eventi in una sequenza. Per ogni sequenza è consentito un unico identificatore di sequenza e per ogni modello è consentito un unico tipo di sequenza.  
  
-   **Attributi fuori sequenza facoltativi** L'algoritmo supporta l'aggiunta di altri attributi non correlati alle sequenze. Questi attributi possono includere le colonne nidificate.  
  
 Nell'esempio del sito Web di [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] riportato in precedenza, un modello Sequence Clustering potrebbe includere informazioni sull'ordine come tabella del case, dati demografici sul cliente specifico per ogni ordine come attributi fuori sequenza e una tabella nidificata contenente la sequenza in cui il cliente ha esplorato il sito o ha inserito gli articoli nel carrello acquisti come informazioni sulla sequenza.  
  
 Per informazioni più dettagliate sui tipi di contenuto e i tipi di dati supportati per i modelli Sequence Clustering, vedere la sezione Requisiti di [Riferimento tecnico per l'algoritmo Microsoft Sequence Clustering](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm-technical-reference.md).  
  
## <a name="viewing-a-sequence-clustering-model"></a>Visualizzazione di un modello Sequence Clustering  
 Il modello di data mining creato da questo algoritmo contiene le descrizioni delle sequenze più comuni incluse nei dati. Per esplorare il modello, è possibile usare il **Visualizzatore Microsoft Sequence Clustering**. Quando si visualizza un modello Sequence Clustering, in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] vengono visualizzati i cluster che contengono più transizioni. È inoltre possibile visualizzare statistiche pertinenti. Per altre informazioni, vedere [Visualizzare un modello usando il Visualizzatore Microsoft Sequence Clustering](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md).  
  
 Per maggiori dettagli, è possibile esplorare il modello in [Microsoft Generic Content Tree Viewer](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md). Il contenuto archiviato per il modello include la distribuzione per tutti i valori in ogni nodo, la probabilità di ogni cluster e altre informazioni sulle transizioni. Per altre informazioni, vedere [Contenuto dei modelli di data mining per i modelli Sequence Clustering &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md).  
  
## <a name="creating-predictions"></a>Creazione di stime  
 Dopo il training del modello, i risultati vengono archiviati come set di modelli. È possibile utilizzare le descrizioni delle sequenze più comuni nei dati per la stima del probabile passaggio successivo di una nuova sequenza. Poiché tuttavia l'algoritmo include altre colonne, è possibile utilizzare il modello risultante per individuare le relazioni tra i dati in sequenza e gli input non sequenziali. Ad esempio, se si aggiungono dati demografici al modello, è possibile eseguire stime per gruppi specifici di clienti. È possibile personalizzare le query di stima per restituire un numero variabile di stime o statistiche descrittive.  
  
 Per informazioni sulla creazione di query in base a un modello di data mining, vedere [Query di data mining](../../analysis-services/data-mining/data-mining-queries.md). Per alcuni esempi su come usare le query con un modello Sequence Clustering, vedere [Esempi di query sul modello di cluster di sequenza](../../analysis-services/data-mining/sequence-clustering-model-query-examples.md).  
  
## <a name="remarks"></a>Osservazioni  
  
-   Non supporta l'utilizzo del linguaggio PMML (Predictive Model Markup Language) per la creazione di modelli di data mining.  
  
-   Supporta il drill-through.  
  
-   Supporta l'utilizzo di modelli di data mining OLAP e la creazione di dimensioni di data mining.  
  
## <a name="see-also"></a>Vedere anche  
 [Algoritmi di Data Mining &#40; Analysis Services - Data Mining &#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Riferimento tecnico algoritmo Microsoft Sequence Clustering](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm-technical-reference.md)   
 [Sequence Clustering Model Query Examples](../../analysis-services/data-mining/sequence-clustering-model-query-examples.md)   
 [Visualizzare un modello utilizzando il visualizzatore Microsoft Sequence Clustering](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)  
  
  
