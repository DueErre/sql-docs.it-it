---
title: sys.dm_os_process_memory (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
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
- sys.dm_os_process_memory_TSQL
- dm_os_process_memory_TSQL
- dm_os_process_memory
- sys.dm_os_process_memory
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_process_memory dynamic management view
ms.assetid: e838130c-95d4-4605-9e3b-eb0ab71cd250
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3031089c848bf8afeac9eeb464dee551aecd771e
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmosprocessmemory-transact-sql"></a>sys.dm_os_process_memory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  La maggior parte delle allocazioni di memoria attribuite allo spazio di processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono controllati tramite interfacce che consentono la registrazione e la contabilità delle allocazioni. Tuttavia, le allocazioni di memoria possono essere eseguite nello spazio degli indirizzi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che ignora le routine interne di gestione memoria. I valori sono ottenuti tramite chiamate al sistema operativo di base. Non sono modificati dai metodi interni a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], tranne quando si regola per bloccare o allocazioni di pagine di grandi dimensioni.  
  
 Tutti i valori restituiti che indicano dimensioni della memoria sono espressi in kilobyte (KB). La colonna **total_virtual_address_space_reserved_kb** è un duplicato di **virtual_memory_in_bytes** da **Sys.dm os_sys_info**.  
  
 Nella tabella seguente è inclusa un'immagine completa dello spazio degli indirizzi di processo.  
  
> [!NOTE]  
>  Per chiamare questo metodo dal [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], utilizzare il nome **sys.dm_pdw_nodes_os_process_memory**.  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|**physical_memory_in_use_kb**|**bigint**|Indica il working set del processo in KB, come riportato dal sistema operativo, nonché le allocazioni registrate utilizzando API per pagine di grandi dimensioni. Non ammette i valori NULL.|  
|**large_page_allocations_kb**|**bigint**|Indica la memoria fisica allocata utilizzando API per pagine di grandi dimensioni. Non ammette i valori NULL.|  
|**locked_page_allocations_kb**|**bigint**|Indica le pagine di memoria bloccate nella memoria. Non ammette i valori NULL.|  
|**total_virtual_address_space_kb**|**bigint**|Indica le dimensioni totali della parte della modalità utente dello spazio degli indirizzi virtuali. Non ammette i valori NULL.|  
|**virtual_address_space_reserved_kb**|**bigint**|Indica la quantità totale di spazio degli indirizzi virtuali riservato dal processo. Non ammette i valori NULL.|  
|**virtual_address_space_committed_kb**|**bigint**|Indica la quantità di spazio degli indirizzi virtuali riservato di cui è stato eseguito il commit o il mapping a pagine fisiche. Non ammette i valori NULL.|  
|**virtual_address_space_available_kb**|**bigint**|Indica la quantità di spazio degli indirizzi virtuali attualmente libera. Non ammette i valori NULL.<br /><br /> **Nota:** libero aree che sono minori della granularità di allocazione può essere presente. Tali aree non sono disponibili per le allocazioni.|  
|**page_fault_count**|**bigint**|Indica il numero di errori di pagina causati dal processo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Non ammette i valori NULL.|  
|**memory_utilization_percentage**|**int**|Specifica la percentuale di memoria di cui è stato eseguito il commit nel working set. Non ammette i valori NULL.|  
|**available_commit_limit_kb**|**bigint**|Indica la quantità di memoria disponibile per il commit da parte del processo. Non ammette i valori NULL.|  
|**process_physical_memory_low**|**bit**|Indica che il processo risponde a una notifica di memoria fisica insufficiente. Non ammette i valori NULL.|  
|**process_virtual_memory_low**|**bit**|Indica che è stata rilevata una condizione di memoria virtuale insufficiente. Non ammette i valori NULL.|  
|**pdw_node_id**|**int**|**Si applica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> L'identificatore per il nodo che utilizza questo tipo di distribuzione.|  
  
## <a name="permissions"></a>Autorizzazioni  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è necessaria l'autorizzazione VIEW SERVER STATE nel server.  
  
 In [!INCLUDE[ssSDS](../../includes/sssds-md.md)] livelli Premium richiede l'autorizzazione VIEW DATABASE STATE nel database. In [!INCLUDE[ssSDS](../../includes/sssds-md.md)] livelli Standard e Basic richiede il [!INCLUDE[ssSDS](../../includes/sssds-md.md)] account amministratore.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni e viste a gestione dinamica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Relative al sistema operativo SQL Server viste a gestione dinamica &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


