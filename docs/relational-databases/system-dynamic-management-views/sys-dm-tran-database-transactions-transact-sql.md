---
title: Sys.dm tran_database_transactions (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 06/09/2017
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
- dm_tran_database_transactions
- sys.dm_tran_database_transactions_TSQL
- dm_tran_database_transactions_TSQL
- sys.dm_tran_database_transactions
dev_langs: TSQL
helpviewer_keywords: sys.dm_tran_database_transactions dynamic management view
ms.assetid: 82a44295-4cbc-4a5b-891a-8ebaf307b8f5
caps.latest.revision: "33"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 56421d77a4ca75f75f87667d6a52c42de4f817b6
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmtrandatabasetransactions-transact-sql"></a>sys.dm_tran_database_transactions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Restituisce informazioni sulle transazioni a livello di database.  
  
> [!NOTE]  
>  Chiamare questa DMV da [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], utilizzare il nome **sys.dm_pdw_nodes_tran_database_transactions**.  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|transaction_id|**bigint**|ID della transazione a livello di istanza, non a livello di database. L'ID è univoco solo in tutti i database all'interno di un'istanza specifica, ma non tra tutte le istanze del server.|  
|database_id|**int**|ID del database associato alla transazione.|  
|database_transaction_begin_time|**datetime**|Ora in cui il database viene coinvolto nella transazione. In particolare, si tratta dell'ora del primo record di log nel database per la transazione.|  
|database_transaction_type|**int**|1 = Transazione di lettura/scrittura<br /><br /> 2 = Transazione di sola lettura<br /><br /> 3 = Transazione di sistema|  
|database_transaction_state|**int**|1 = La transazione non è stata inizializzata.<br /><br /> 3 = La transazione è stata inizializzata ma non ha generato alcun record di log.<br /><br /> 4 = La transazione ha generato record di log.<br /><br /> 5 = La transazione è stata preparata.<br /><br /> 10 = È stato eseguito il commit della transazione.<br /><br /> 11 = È stato eseguito il rollback della transazione.<br /><br /> 12 = L'esecuzione del commit della transazione è in corso. (Il record del log viene generato, ma non è stato materializzato o persistente.)|  
|database_transaction_status|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|database_transaction_status2|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|database_transaction_log_record_count|**bigint**|**Si applica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Numero di record di log generati nel database per la transazione.|  
|database_transaction_replicate_record_count|**int**|**Si applica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Numero di record di log generati nel database per la transazione che viene replicata.|  
|database_transaction_log_bytes_used|**bigint**|**Si applica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Numero di byte finora utilizzati nel log del database per la transazione.|  
|database_transaction_log_bytes_reserved|**bigint**|**Si applica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Numero di byte riservati all'utilizzo nel log del database per la transazione.|  
|database_transaction_log_bytes_used_system|**int**|**Si applica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Numero di byte finora utilizzati nel log del database per le transazioni di sistema per conto della transazione.|  
|database_transaction_log_bytes_reserved_system|**int**|**Si applica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Numero di byte riservati per l'utilizzo nel log del database per le transazioni di sistema per conto della transazione.|  
|database_transaction_begin_lsn|**Numeric(25,0)**|**Si applica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Numero di sequenza del file di log (LSN) del record di inizio per la transazione nel log del database.|  
|database_transaction_last_lsn|**Numeric(25,0)**|**Si applica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> LSN del log registrato più di recente per la transazione nel log del database.|  
|database_transaction_most_recent_savepoint_lsn|**Numeric(25,0)**|**Si applica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> LSN del punto di salvataggio più recente per la transazione nel log del database.|  
|database_transaction_commit_lsn|**Numeric(25,0)**|**Si applica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> LSN del record di log del commit per la transazione nel log del database.|  
|database_transaction_last_rollback_lsn|**Numeric(25,0)**|**Si applica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> LSN fino al quale è stato eseguito il rollback più recente. Se nessun rollback ha avuto luogo, il valore sarà MaxLSN.|  
|database_transaction_next_undo_lsn|**Numeric(25,0)**|**Si applica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> LSN del record successivo da annullare.|  
|pdw_node_id|**int**|**Si applica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> L'identificatore per il nodo che utilizza questo tipo di distribuzione.|  
  
## <a name="permissions"></a>Permissions  
In [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], richiede `VIEW SERVER STATE` autorizzazione.   
In [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] livelli Premium, è necessario il `VIEW DATABASE STATE` autorizzazione per il database. In [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] livelli Standard e Basic, è necessario il **amministratore del Server** o **amministratore di Azure Active Directory** account.  
 

  
## <a name="see-also"></a>Vedere anche  
 [Sys.dm tran_active_transactions &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-active-transactions-transact-sql.md)   
 [Sys.dm tran_session_transactions &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-session-transactions-transact-sql.md)   
 [Funzioni e viste a gestione dinamica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funzioni e viste a gestione dinamica relative alle transazioni &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  

