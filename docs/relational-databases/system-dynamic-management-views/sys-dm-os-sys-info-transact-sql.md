---
title: sys.dm_os_sys_info (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 04/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_os_sys_info_TSQL
- dm_os_sys_info
- dm_os_sys_info_TSQL
- sys.dm_os_sys_info
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_sys_info dynamic management view
- time [SQL Server], instance started
- starting time
ms.assetid: 20f6bc9c-839a-4fa4-b3f3-a6c47d1b69af
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 21fe61d34a9b8823af499b64aef0eaef95c1a92e
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmossysinfo-transact-sql"></a>sys.dm_os_sys_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Restituisce svariate informazioni utili sul computer e sulle risorse disponibili e utilizzate da [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].  
  
> **Nota:** da chiamare [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], utilizzare il nome **sys.dm_pdw_nodes_os_sys_info**.  
  
|Nome colonna|Tipo di dati|Descrizione e note sulla versione specifiche |  
|-----------------|---------------|-----------------|  
|**cpu_ticks**|**bigint**|Specifica il conteggio corrente dei tick della CPU. I tick della CPU vengono recuperati dal contatore RDTSC del processore. Si tratta di un contatore a incremento progressivo costante. Non ammette i valori NULL.|  
|**ms_ticks**|**bigint**|Specifica il numero di millisecondi dall'avvio del computer. Non ammette i valori NULL.|  
|**cpu_count**|**int**|Specifica il numero di CPU logiche nel sistema. Non ammette i valori NULL.|  
|**hyperthread_ratio**|**int**|Specifica il rapporto del numero dei core logici o fisici esposti da un pacchetto del processore fisico. Non ammette i valori NULL.|  
|**physical_memory_in_bytes**|**bigint**|**Si applica a: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]** .<br /><br /> Specifica la quantità totale di memoria fisica disponibile nel computer. Non ammette i valori NULL.|  
|**physical_memory_kb**|**bigint**|**Si applica a: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> Specifica la quantità totale di memoria fisica disponibile nel computer. Non ammette i valori NULL.|  
|**virtual_memory_in_bytes**|**bigint**|**Si applica a: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]** .<br /><br /> Quantità di memoria virtuale disponibile per il processo in modalità utente. Questo valore può essere utilizzato per determinare se SQL Server è stato avviato tramite il parametro /3gb.|  
|**virtual_memory_kb**|**bigint**|**Si applica a: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> Specifica la quantità totale di spazio degli indirizzi virtuali disponibile per il processo in modalità utente. Non ammette i valori NULL.|  
|**bpool_commited**|**int**|**Si applica a: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]** .<br /><br /> Rappresenta la memoria di cui è stato eseguito il commit in kilobyte (KB) nel gestore della memoria. Non include la memoria riservata nel gestore della memoria. Non ammette i valori NULL.|  
|**committed_kb**|**int**|**Si applica a: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> Rappresenta la memoria di cui è stato eseguito il commit in kilobyte (KB) nel gestore della memoria. Non include la memoria riservata nel gestore della memoria. Non ammette i valori NULL.|  
|**bpool_commit_target**|**int**|**Si applica a: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]** .<br /><br /> Rappresenta la quantità di memoria, in kilobyte (KB), che può essere utilizzata dal gestore della memoria di SQL Server.|  
|**committed_target_kb**|**int**|**Si applica a: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> Rappresenta la quantità di memoria, in kilobyte (KB), che può essere utilizzata dal gestore della memoria di SQL Server. La quantità di destinazione viene calcolata tramite una vasta gamma di input quali:<br /><br /> -lo stato corrente del sistema, incluso il relativo carico<br /><br /> -la memoria richiesta dai processi correnti<br /><br /> -la quantità di memoria installata nel computer<br /><br /> -i parametri di configurazione<br /><br /> Se **committed_target_kb** è maggiore di **committed_kb**, il gestore della memoria tenterà di ottenere memoria aggiuntiva. Se **committed_target_kb** inferiori **committed_kb**, il gestore della memoria tenterà di compattare la quantità di memoria riservata. Il **committed_target_kb** include sempre la memoria prelevata e riservata. Non ammette i valori NULL.|  
|**bpool_visible**|**int**|**Si applica a: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]** .<br /><br /> Numero di buffer da 8 KB nel pool di buffer a cui è possibile accedere direttamente nello spazio degli indirizzi virtuali di processo. Se non si utilizza AWE (Address Windowing Extensions), quando il pool di buffer raggiunge la memoria massima (bpool_committed = bpool_commit_target) il valore di bpool_visible è uguale al valore di bpool_committed. Quando si utilizza AWE in una versione a 32 bit di SQL Server, bpool_visible rappresenta la dimensione della finestra di mapping AWE utilizzata per accedere alla memoria fisica allocata dal pool di buffer. Poiché le dimensioni di questa finestra di mapping sono associate allo spazio degli indirizzi di processo, la quantità visibile sarà inferiore a quella di cui è stato eseguito il commit ed è possibile che risulti ulteriormente ridotta dai componenti interni che utilizzano la memoria per fini diversi dalla visualizzazione delle pagine di database. Se il valore di bpool_visible è troppo basso, è possibile che vengano visualizzati errori di memoria insufficiente.|  
|**visible_target_kb**|**int**|**Si applica a: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> È identico **committed_target_kb**. Non ammette i valori NULL.|  
|**stack_size_in_bytes**|**int**|Specifica le dimensioni dello stack di chiamate per ogni thread creato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Non ammette i valori NULL.|  
|**os_quantum**|**bigint**|Rappresenta il quantum per un'attività non preemptive misurato in millisecondi. Quantum (in secondi) = **os_quantum** / velocità del clock della CPU. Non ammette i valori NULL.|  
|**os_error_mode**|**int**|Viene specificata la modalità di errore per il processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Non ammette i valori NULL.|  
|**os_priority_class**|**int**|Specifica la classe di priorità per il processo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ammette valori Null.<br /><br /> 32 = Normale (nel log degli errori viene indicato che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene avviato con valore base di priorità normale (=7).)<br /><br /> 128 = Alta (nel log degli errori viene indicato che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è in esecuzione con valore base di priorità alta.  (=13).)<br /><br /> Per altre informazioni, vedere [Configurare l'opzione di configurazione del server priority boost](../../database-engine/configure-windows/configure-the-priority-boost-server-configuration-option.md).|  
|**max_workers_count**|**int**|Rappresenta il numero massimo di thread di lavoro che è possibile creare. Non ammette i valori NULL.|  
|**scheduler_count**|**int**|Rappresenta il numero di utilità di pianificazione utente configurate nel processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Non ammette i valori NULL.|  
|**scheduler_total_count**|**int**|Rappresenta il numero totale di utilità di pianificazione in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Non ammette i valori NULL.|  
|**deadlock_monitor_serial_number**|**int**|Specifica l'ID della sequenza corrente di monitoraggio dei deadlock. Non ammette i valori NULL.|  
|**sqlserver_start_time_ms_ticks**|**bigint**|Rappresenta il **ms_tick** numero quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ultimo avvio. Da confrontare con la colonna ms_ticks corrente. Non ammette i valori NULL.|  
|**sqlserver_start_time**|**datetime**|Vengono specificate la data e l'ora dell'ultimo avvio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Non ammette i valori NULL.|  
|**affinity_type**|**int**|**Si applica a: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]**  tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Viene specificato il tipo di affinità di processo CPU server attualmente in uso. Non ammette i valori NULL. Per ulteriori informazioni, vedere [ALTER SERVER CONFIGURATION &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-server-configuration-transact-sql.md).<br /><br /> 1 = MANUAL<br /><br /> 2 = AUTO|  
|**affinity_type_desc**|**varchar(60)**|**Si applica a: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> Viene descritto il **affinity_type** colonna. Non ammette i valori NULL.<br /><br /> MANUAL = l'affinità è stata impostata per almeno una CPU.<br /><br /> AUTO = in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è possibile spostare liberamente i thread tra CPU.|  
|**process_kernel_time_ms**|**bigint**|**Si applica a: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] tramite [! Includi [ssCurrent]**(... /Token/ssCurrent_md.MD)].<br /><br /> Tempo totale in millisecondi impiegato da tutti i thread di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in modalità kernel. Questo valore può essere maggiore di un singolo clock del processore perché è incluso il tempo di tutti i processori nel server. Non ammette i valori NULL.|  
|**process_user_time_ms**|**bigint**|**Si applica a: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> Tempo totale in millisecondi impiegato da tutti i thread di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in modalità utente. Questo valore può essere maggiore di un singolo clock del processore perché è incluso il tempo di tutti i processori nel server. Non ammette i valori NULL.|  
|**time_source**|**int**|**Si applica a: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> Indica l'API utilizzata da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per recuperare il tempo di clock. Non ammette i valori NULL.<br /><br /> 0 = QUERY_PERFORMANCE_COUNTER<br /><br /> 1 = MULTIMEDIA_TIMER|  
|**time_source_desc**|**nvarchar(60)**|**Si applica a: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> Viene descritto il **time_source** colonna. Non ammette i valori NULL.<br /><br /> QUERY_PERFORMANCE_COUNTER = il [QueryPerformanceCounter](http://go.microsoft.com/fwlink/?LinkId=163095) API recupera il tempo di clock.<br /><br /> MULTIMEDIA_TIMER = il [timer multimediale](http://go.microsoft.com/fwlink/?LinkId=163094) API che consente di recuperare il tempo di clock.|  
|**virtual_machine_type**|**int**|**Si applica a: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> Indica se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è in esecuzione in un ambiente virtualizzato.  Non ammette i valori NULL.<br /><br /> 0 = NONE<br /><br /> 1 = HYPERVISOR<br /><br /> 2 = OTHER|  
|**virtual_machine_type_desc**|**nvarchar(60)**|**Si applica a: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> Viene descritto il **virtual_machine_type** colonna. Non ammette i valori NULL.<br /><br /> NONE = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non è in esecuzione all'interno di una macchina virtuale.<br /><br /> HYPERVISOR = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è in esecuzione in un hypervisor, pertanto è implicata un virtualizzazione assistita da hardware. Quando viene installato il ruolo Hyper_V, l'hypervisor ospita il sistema operativo, così che un'istanza in esecuzione nel sistema operativo host viene eseguita nell'hypervisor.<br /><br /> OTHER = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è in esecuzione in una macchina virtuale in cui non viene utilizzato alcun assistente hardware, ad esempio Microsoft Virtual PC.|  
|**softnuma_configuration**|**int**|**Si applica a: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> Specifica che i nodi NUMA modo configurati. Non ammette i valori NULL.<br /><br /> 0 = OFF indica predefinito hardware<br /><br /> 1 = soft-NUMA automatica<br /><br /> 2 = soft-NUMA manuale tramite del Registro di sistema|  
|**softnuma_configuration_desc**|**nvarchar(60)**|**Si applica a: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> OFF = Soft-NUMA funzionalità è disattivata<br /><br /> ON = automaticamente SQL Server determina le dimensioni del nodo NUMA per Soft-NUMA<br /><br /> MANUAL = configurata manualmente soft-NUMA|
|**process_physical_affinity**|**nvarchar(3072)** |**Si applica a: a partire da [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]** .<br /><br />Informazioni ancora disponibili in. |
|**sql_memory_model**|**int**|**Si applica a: [!INCLUDE[sssql11](../../includes/sssql11-md.md)] SP4 e a partire da [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1**.<br /><br />Specifica il modello di memoria usato da SQL Server per allocare memoria. Non ammette i valori NULL.<br /><br />1 = modello di memoria convenzionale<br />2 = blocco di pagine in memoria<br /> 3 = pagine di grandi dimensioni in memoria|
|**sql_memory_model_desc**|**nvarchar(120)**|**Si applica a: [!INCLUDE[sssql11](../../includes/sssql11-md.md)] SP4 e a partire da [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1**.<br /><br />Specifica il modello di memoria usato da SQL Server per allocare memoria. Non ammette i valori NULL.<br /><br />**CONVENZIONALE** = SQL Server utilizza il modello di memoria convenzionale di allocazione della memoria. Si tratta di modello di memoria di sql predefinita, quando account del servizio SQL Server non dispone di blocco di pagine dei privilegi di memoria durante l'avvio.<br />**LOCK_PAGES** = SQL server utilizza blocco di pagine in memoria per allocare memoria. Questo è il gestore della memoria di sql predefinita quando l'account del servizio SQL Server disporre di privilegi di memoria di blocco di pagine durante l'avvio di SQL Server.<br /> **LARGE_PAGES** = SQL Server utilizza le pagine di grandi dimensioni in memoria per allocare memoria. SQL Server utilizza l'allocatore di pagine di grandi dimensioni di allocazione della memoria solo con Enterprise edition quando l'account del servizio SQL Server possedere Lock Pages in privilegio di memoria durante l'avvio del server e quando 834 Flag di traccia è attivata.|
|**pdw_node_id**|**int**|**Si applica a: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]**<br /><br /> L'identificatore per il nodo che utilizza questo tipo di distribuzione.|  
|**socket_count** |**int** | **Si applica a: a partire da [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]** .<br /><br />Specifica il numero di socket di processore disponibile nel sistema. |  
|**cores_per_socket** |**int** | **Si applica a: a partire da [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)].**.<br /><br />Specifica il numero di processori per ogni socket disponibile nel sistema. |  
|**numa_node_count** |**int** | **Si applica a: a partire da [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)].**.<br /><br />Specifica il numero di nodi numa disponibili nel sistema. Questa colonna include nodi numa fisici, nonché i nodi soft-numa. |  
  
## <a name="permissions"></a>Autorizzazioni  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] richiede `VIEW SERVER STATE` autorizzazione nel server.  
  
 In [!INCLUDE[ssSDS](../../includes/sssds-md.md)] richiede livelli Premium di `VIEW DATABASE STATE` autorizzazione per il database. In [!INCLUDE[ssSDS](../../includes/sssds-md.md)] livelli Standard e Basic richiede il [!INCLUDE[ssSDS](../../includes/sssds-md.md)] account amministratore.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni e viste a gestione dinamica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Relative al sistema operativo SQL Server viste a gestione dinamica &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  



