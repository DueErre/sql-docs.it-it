---
title: Sys.dm os_nodes (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 07/19/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_os_nodes
- dm_os_nodes_TSQL
- dm_os_nodes
- sys.dm_os_nodes_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_os_nodes dynamic management view
ms.assetid: c768b67c-82a4-47f5-850b-0ea282358d50
caps.latest.revision: "33"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5cf36f7156f9297231fc232e8fecafee5e77427c
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmosnodes-transact-sql"></a>sys.dm_os_nodes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Un componente interno denominato SQLOS crea le strutture di nodi che imitano la località del processore hardware. Queste strutture possono essere modificate utilizzando soft-NUMA per creare layout di nodo personalizzati.  
  
 Nella tabella seguente sono incluse informazioni su questi nodi.  
  
> **Nota:** per chiamare questa DMV da [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], utilizzare il nome **sys.dm_pdw_nodes_os_nodes**.  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|node_id|**smallint**|ID del nodo.|  
|node_state_desc|**nvarchar(256)**|Descrizione dello stato del nodo. I valori sono visualizzati con i valori reciprocamente esclusivi all'inizio, seguiti dai valori combinabili. Esempio:<br /><br /> Online, Thread Resources Low, Lazy Preemptive<br /><br /> Esistono quattro valori node_state_desc reciprocamente esclusivi. Elencati di seguito con le relative descrizioni.<br /><br /> ONLINE: Il nodo è online<br /><br /> OFFLINE: Nodo è offline<br /><br /> INATTIVO: Nodo non dispone di alcuna richiesta di lavoro in sospeso e ha attivato uno stato di inattività.<br /><br /> IDLE_READY: Nodo non è in attesa di richieste di lavoro ed è pronto per lo stato inattivo.<br /><br /> Esistono cinque valori node_state_desc combinabili, elencati di seguito con le relative descrizioni.<br /><br /> Applicazione livello dati: Questo nodo è riservato per la connessione amministrativa dedicata.<br /><br /> THREAD_RESOURCES_LOW: Nessun nuovo thread è possibile creare nel nodo a causa di una condizione di memoria insufficiente.<br /><br /> AGGIUNTA a caldo: Indica l'aggiunta di nodi in risposta a un caldo evento della CPU.|  
|memory_object_address|**varbinary (8)**|Indirizzo dell'oggetto memoria associato al nodo. Vi è una relazione uno-a-uno con sys.dm_os_memory_objects.memory_object_address.|  
|memory_clerk_address|**varbinary (8)**|Indirizzo del clerk di memoria associato al nodo. Vi è una relazione uno-a-uno con sys.dm_os_memory_clerks.memory_clerk_address.|  
|io_completion_worker_address|**varbinary (8)**|Indirizzo del thread di lavoro assegnato al completamento I/O per il nodo. Vi è una relazione uno-a-uno con sys.dm_os_workers.worker_address.|  
|memory_node_id|**smallint**|ID del nodo di memoria al quale questo nodo appartiene. Vi è una relazione molti-a-uno con sys.dm_os_memory_nodes.memory_node_id.|  
|cpu_affinity_mask|**bigint**|Bitmap che identifica le CPU alle quali questo nodo è associato.|  
|online_scheduler_count|**smallint**|Numero di utilità di pianificazione online gestite da questo nodo.|  
|idle_scheduler_count|**smallint**|Numero di utilità di pianificazione online che non dispongono di thread di lavoro attivi.|  
|active_worker_count|**int**|Numero di thread di lavoro attivi su tutte le utilità di pianificazione gestite da questo nodo.|  
|avg_load_balance|**int**|Media del numero di attività per utilità di pianificazione su questo nodo.|  
|timer_task_affinity_mask|**bigint**|Bitmap che identifica le utilità di pianificazione che possono avere attività di timer assegnate.|  
|permanent_task_affinity_mask|**bigint**|Bitmap che identifica le utilità di pianificazione che possono avere attività permanenti assegnate.|  
|resource_monitor_state|**bit**|A ogni nodo viene assegnato un monitoraggio risorse. Il monitoraggio risorse può essere in esecuzione o inattivo. Il valore 1 indica che è in esecuzione, il valore 0 indica che è inattivo.|  
|online_scheduler_mask|**bigint**|Identifica la maschera di affinità del processo per questo nodo.|  
|processor_group|**smallint**|Identifica il gruppo di processori per questo nodo.|  
|cpu_count |**int** |Numero di CPU disponibili per questo nodo. |
|pdw_node_id|**int**|L'identificatore per il nodo che utilizza questo tipo di distribuzione.<br /><br /> **Si applica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]|  
  
## <a name="permissions"></a>Permissions  
In [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], richiede `VIEW SERVER STATE` autorizzazione.   
In [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] livelli Premium, è necessario il `VIEW DATABASE STATE` autorizzazione per il database. In [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] livelli Standard e Basic, è necessario il **amministratore del Server** o **amministratore di Azure Active Directory** account.  
  
## <a name="see-also"></a>Vedere anche  
  
 [Relative al sistema operativo SQL Server viste a gestione dinamica &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [Soft-NUMA &#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md)  
  
  

