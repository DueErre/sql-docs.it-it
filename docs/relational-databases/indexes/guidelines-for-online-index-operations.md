---
title: Linee guida per le operazioni sugli indici online | Microsoft Docs
ms.custom: 
ms.date: 07/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.technology: dbe-indexes
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- clustered indexes, online operations
- online index operations
- indexes [SQL Server], online operations
- disk space [SQL Server], indexes
- nonclustered indexes [SQL Server], online operations
- transaction logs [SQL Server], indexes
ms.assetid: d82942e0-4a86-4b34-a65f-9f143ebe85ce
caps.latest.revision: "64"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.suite: sql
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: indexes
ms.workload: On Demand
ms.openlocfilehash: 2c5e3f669cd2789676e334beedb4e8ee410c5cd6
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/18/2018
---
# <a name="guidelines-for-online-index-operations"></a>Linee guida per operazioni di indice online
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Quando si eseguono operazioni sugli indici online sono da ritenersi valide le linee guida seguenti:  
  
-   Gli indici cluster devono essere creati, ricompilati o eliminati offline se la tabella sottostante contiene i seguenti tipi di dati dell'oggetto LOB: **image**, **ntext**e **text**.  
  
-   È possibile creare indici non cluster non univoci online quando la tabella contiene tipi di dati LOB ma nessuna di queste colonne è utilizzata nella definizione di indice come colonna chiave o non chiave (inclusa).  
  
-   Non è possibile creare, ricompilare o eliminare online indici su tabelle temporanee locali. Questa limitazione non è valida per gli indici su tabelle temporanee globali.
- Gli indici possono essere ripresi dal punto di interruzione dopo un errore imprevisto, il failover del database o l'esecuzione di un comando **PAUSE**. Vedere [Alter Index](../../t-sql/statements/alter-index-transact-sql.md). 

> [!NOTE]  
>  Le operazioni sugli indici online sono disponibili solo in alcune edizioni di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per un elenco delle funzionalità supportate dalle edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Funzionalità supportate dalle edizioni](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 Nella tabella seguente sono riportate le operazioni sugli indici che è possibile eseguire online, gli indici che sono esclusi da queste operazioni online e le restrizioni per gli indici ripristinabili. Sono inoltre incluse ulteriori limitazioni.  
  
| Operazione su indice online | Indici esclusi | Altre limitazioni |  
|----------------------------|----------------------|------------------------|  
|ALTER INDEX REBUILD|Indice cluster disabilitato o vista indicizzata disabilitata<br /><br /> Indice XML<br /><br />Indice columnstore <br /><br /> Indice di una tabella temporanea locale|L'operazione può avere esito negativo se la tabella contiene un indice escluso e si utilizza la parola chiave ALL.<br /><br /> Sono applicabili ulteriori restrizioni nella ricompilazione di indici disabilitati. Per altre informazioni, vedere [Disabilitazione di indici e vincoli](../../relational-databases/indexes/disable-indexes-and-constraints.md).|  
|CREATE INDEX|Indice XML<br /><br /> Indice cluster univoco iniziale su una vista<br /><br /> Indice di una tabella temporanea locale||  
|CREATE INDEX WITH DROP_EXISTING|Indice cluster disabilitato o vista indicizzata disabilitata<br /><br /> Indice di una tabella temporanea locale<br /><br /> Indice XML||  
|DROP INDEX|Indice disabilitato<br /><br /> Indice XML<br /><br /> Indice non cluster<br /><br /> Indice di una tabella temporanea locale|Non è possibile specificare più indici in una singola istruzione.|  
|ALTER TABLE ADD CONSTRAINT (PRIMARY KEY o UNIQUE)|Indice di una tabella temporanea locale<br /><br /> Indice cluster|È consentito l'utilizzo di una sola clausola secondaria alla volta. Ad esempio, non è possibile aggiungere ed eliminare vincoli PRIMARY KEY o UNIQUE nella stessa istruzione ALTER TABLE.|  
|ALTER TABLE DROP CONSTRAINT (PRIMARY KEY o UNIQUE)|Indice cluster||  
  
 Non è possibile modificare, troncare o eliminare la tabella sottostante mentre è in corso un'operazione su un indice online.  
  
 L'impostazione di un'opzione online (ON oppure OFF) specificata durante la creazione o l'eliminazione di un indice cluster viene applicata a tutti gli indici non cluster che devono essere ricompilati. Ad esempio, se l'indice cluster viene compilato online utilizzando CREATE INDEX WITH DROP_EXISTING, ONLINE=ON, anche tutti gli indici non cluster associati vengono ricreati online.  
  
 Quando si crea o si ricompila un indice UNIQUE online, il generatore dell'indice e una transazione utente simultanea potrebbero tentare di inserire la stessa chiave, causando una violazione di univocità. Se una riga immessa da un utente viene inserita nel nuovo indice (destinazione) prima che la riga originale della tabella di origine venga spostata nel nuovo indice, l'operazione sull'indice online avrà esito negativo.  
  
 Un'operazione su un indice online può in rari casi provocare un deadlock quando interagisce con aggiornamenti al database a causa di attività dell'utente o dell'applicazione. In questi rari casi, il [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] selezionerà l'attività dell'utente o dell'applicazione come vittima del deadlock.  
  
 È possibile eseguire operazioni DDL sugli indici online simultanee sulla stessa tabella o vista solo quando si stanno creando più indici nuovi non cluster oppure si stanno riorganizzando indici non cluster. Qualsiasi altra operazione sugli indici online eseguita nello stesso istante avrà esito negativo. Ad esempio, non è possibile creare un nuovo indice online durante la ricompilazione di un indice online esistente sulla stessa tabella.  
  
 Non è possibile eseguire un'operazione online se un indice contiene una colonna di tipo di oggetti di grandi dimensioni e nella stessa transazione sono presenti operazioni di aggiornamento prima di questa operazione online. Per risolvere questo problema, posizionare l'operazione online all'esterno della transazione o prima degli aggiornamenti all'interno della transazione.  
  
## <a name="disk-space-considerations"></a>Considerazioni sullo spazio su disco  
 Le operazioni sugli indici online hanno requisiti di spazio su disco maggiori rispetto alle operazioni sugli indici offline. 
 - Durante le operazioni di creazione dell'indice e di ricompilazione dell'indice, è necessario spazio aggiuntivo per l'indice in corso di ricompilazione o ricompilato. 
 - È richiesto anche spazio su disco aggiuntivo per l'indice di mapping temporaneo. Questo indice temporaneo è utilizzato nelle operazioni sugli indici online che creano, ricompilano o eliminano un indice cluster.
- L'eliminazione di un indice cluster online richiede lo stesso spazio che è necessario per la creazione o la ricompilazione di un indice cluster online. 

Per altre informazioni, vedere [Disk Space Requirements for Index DDL Operations](../../relational-databases/indexes/disk-space-requirements-for-index-ddl-operations.md).  
  
## <a name="performance-considerations"></a>Considerazioni sulle prestazioni  
 Sebbene le operazioni sugli indici online consentano l'esecuzione di attività simultanee di aggiornamento utente, le operazioni sugli indici impiegheranno più tempo se l'attività di aggiornamento genera un notevole carico. Le operazioni sugli indici online saranno generalmente più lente delle operazioni sugli indici offline equivalenti, indipendentemente dal livello di attività di aggiornamento simultanee.  
  
 Dato che durante le operazioni sugli indici online vengono mantenute sia la struttura di origine che quella di destinazione, l'utilizzo di risorse per l'inserimento, l'aggiornamento e l'eliminazione delle transazioni viene aumentato, potenzialmente fino al doppio. Ciò può causare una riduzione delle prestazioni e un maggior utilizzo di risorse durante l'operazione sugli indici, specialmente del tempo CPU. Le operazioni sugli indici online vengono registrate completamente.  
  
 Sebbene le operazioni online siano consigliabili, è opportuno valutare l'ambiente e i requisiti specifici, in base ai quali l'esecuzione delle operazioni sugli indici offline potrebbe essere la soluzione ottimale. In quest'ultimo caso gli utenti avrebbero un accesso limitato ai dati durante l'operazione, la quale però terminerebbe più rapidamente e utilizzerebbe meno risorse.  
  
 Nei computer multiprocessore che eseguono SQL Server 2016 le istruzioni per gli indici, analogamente ad altre query, possono usare più processori per eseguire le operazioni di analisi e ordinamento associate all'istruzione. È possibile utilizzare l'opzione dell'indice MAXDOP per controllare il numero di processori dedicati all'operazione di indice online. In questo modo è possibile bilanciare le risorse utilizzate dall'operazione sugli indici con quelle occupate dagli utenti simultanei. Per altre informazioni, vedere [Configurazione di operazioni parallele sugli indici](../../relational-databases/indexes/configure-parallel-index-operations.md). Per altre informazioni sulle edizioni di SQL Server che supportano le operazioni indicizzate parallele, vedere [Funzionalità supportate dalle edizioni](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 Poiché al termine dell'esecuzione dell'operazione sugli indici viene mantenuto un blocco S o Sch-M, è necessario prestare particolare attenzione quando si esegue un'operazione sugli indici online all'interno di una transazione utente esplicita, ad esempio un blocco BEGIN TRANSACTION...COMMIT. Una tale operazione causa il mantenimento del blocco fino alla fine della transazione, impedendo quindi la concorrenza degli utenti.  
  
 La ricompilazione degli indici online può aumentare la frammentazione quando è consentita l'esecuzione con le opzioni `MAX DOP > 1` e `ALLOW_PAGE_LOCKS = OFF` . Per altre informazioni, vedere [Funzionamento: Ricompilazione di indici online - Possibilità di aumento della frammentazione](http://blogs.msdn.com/b/psssql/archive/2012/09/05/how-it-works-online-index-rebuild-can-cause-increased-fragmentation.aspx).  
  
## <a name="transaction-log-considerations"></a>Considerazioni sul log delle transazioni  
 Operazioni sugli indici su larga scala, eseguite online oppure offline, possono generare volumi di dati elevati i quali possono esaurire rapidamente lo spazio disponibile nel log delle transazioni. Per garantire la possibilità di eseguire il rollback dell'operazione sugli indici, non è possibile troncare il log delle transazioni fino al completamento dell'operazione. È tuttavia possibile eseguire il backup del log durante l'operazione sugli indici. È pertanto necessario che il log delle transazioni abbia spazio sufficiente per archiviare sia le transazioni dell'operazione sugli indici sia tutte le transazioni utente simultanee per l'intera durata dell'operazione sugli indici. Per altre informazioni, vedere [Spazio su disco per il log delle transazioni per operazioni sugli indici](../../relational-databases/indexes/transaction-log-disk-space-for-index-operations.md).  

## <a name="resumable-index-rebuild-considerations"></a>Considerazioni sulla ricompilazione degli indici ripristinabili

> [!NOTE]
> L'opzione dell'indice ripristinabile è valida per SQL Server (a partire da SQL Server 2017) e per il database SQL. Vedere [Alter Index](../../t-sql/statements/alter-index-transact-sql.md). 

Per eseguire la ricompilazione di un indice online ripristinabile, attenersi alle seguenti linee guida:
-   Gestione, pianificazione ed estensione delle finestre di manutenzione degli indici. È possibile sospendere e riavviare un'operazione di ricompilazione dell'indice più volte in base alle finestre di manutenzione.
- Recupero da errori di ricompilazione degli indici, ad esempio failover del database o esaurimento dello spazio su disco.
- Quando un'operazione sull'indice è sospesa, sia l'indice originale sia quello appena creato richiedono spazio su disco e devono essere aggiornati durante le operazioni DML.

- È consentito il troncamento dei log delle transazioni durante le operazioni di ricompilazione dell'indice (non possono invece essere eseguiti per le normali operazioni sull'indice online).
- L'opzione SORT_IN_TEMPDB=ON non è supportata

> [!IMPORTANT]
> Per la ricompilazione ripristinabile non è necessario tenere aperta una transazione con esecuzione prolungata ed è possibile eseguire il troncamento del log durante l'operazione ottimizzando la gestione dello spazio del log. Con la nuova progettazione è possibile mantenere i dati necessari in un database insieme a tutti i riferimenti richiesti per riavviare l'operazione ripristinabile.

In generale non vi sono differenze di prestazioni tra la ricompilazione degli indici online ripristinabili e quella degli indici non ripristinabili. Quando si aggiorna un indice ripristinabile mentre un'operazione di ricompilazione di indice è in pausa:
- Per i carichi di lavoro prevalentemente di lettura, l'impatto sulle prestazioni è trascurabile. 
- Per i carichi di lavoro con intensa attività di aggiornamento, è possibile riscontrare una riduzione delle prestazioni in termini di velocità effettiva (i test indicano una riduzione inferiore al 10%).

In generale non vi sono differenze di qualità della deframmentazione nella ricompilazione degli indici online ripristinabili rispetto agli indici non ripristinabili.
 
## <a name="related-content"></a>Contenuto correlato  
 [Funzionamento delle operazioni sugli indici online](../../relational-databases/indexes/how-online-index-operations-work.md)  
  
 [Eseguire operazioni online sugli indici](../../relational-databases/indexes/perform-index-operations-online.md)  
  
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)  
  
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)  
  
  
