---
title: Sys. query_store_plan (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 09/12/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- QUERY_STORE_PLAN_TSQL
- SYS.QUERY_STORE_PLAN
- SYS.QUERY_STORE_PLAN_TSQL
- QUERY_STORE_PLAN
dev_langs: TSQL
helpviewer_keywords:
- query_store_plan catalog view
- sys.query_store_plan catalog view
ms.assetid: b4d05439-6360-45db-b1cd-794f4a64935e
caps.latest.revision: "18"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0950cf33d112d299de615a702d0fbac7cbfdc0e2
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="sysquerystoreplan-transact-sql"></a>Sys. query_store_plan (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Contiene informazioni su ogni piano di esecuzione associata a una query.  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|**plan_id**|**bigint**|Chiave primaria.|  
|**query_id**|**bigint**|Chiave esterna. Crea un join tra [query_store_query &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md).|  
|**plan_group_id**|**bigint**|ID del gruppo di piano. Query basate su cursori richiedono in genere più (compilare e recuperare) piani. Compilare e si applica ai piani di recupero vengono compilati insieme nello stesso gruppo.<br /><br /> 0 significa piano non è presente in un gruppo.|  
|**engine_version**|**nvarchar(32)**|Versione del motore utilizzata per compilare il piano in **'revisione'** formato.|  
|**COMPATIBILITY_LEVEL**|**smallint**|Livello di compatibilità del database del database a cui fa riferimento nella query.|  
|**valore query_plan_hash**|**Binary (8)**|Hash MD5 del piano individuale.|  
|**query_plan**|**nvarchar(max)**|Showplan XML per il piano di query.|  
|**is_online_index_plan**|**bit**|Piano è stato utilizzato durante la compilazione di un indice online.|  
|**is_trivial_plan**|**bit**|Piano è un semplice piano (output in fase di query Optimizer è 0).|  
|**is_parallel_plan**|**bit**|Piano è parallelo.|  
|**is_forced_plan**|**bit**|Piano viene contrassegnato come forzata quando l'utente esegue una stored procedure **sys.sp_query_store_force_plan**. Meccanismo di utilizzo forzato *non garantisce* esattamente questo piano verrà utilizzato per la query a cui fa riferimento **query_id**. Utilizzo forzato del piano fa sì che una query da compilare nuovamente e in genere produce esattamente il piano identici o simile per il piano a cui fa riferimento **plan_id**. Se l'utilizzo forzato del piano non riesce, **force_failure_count** viene incrementato e **last_force_failure_reason** viene popolato con il motivo dell'errore.|  
|**is_natively_compiled**|**bit**|Piano include le procedure di ottimizzazione per la memoria compilate in modo nativo. (0 = FALSE, 1 = TRUE).|  
|**force_failure_count**|**bigint**|Numero di volte in cui è Impossibile forzare l'utilizzo di questo piano. Può essere incrementato solo quando la query viene ricompilata (*non a ogni esecuzione*). Viene reimpostato su 0 ogni volta **is_plan_forced** viene modificato da **FALSE** a **TRUE**.|  
|**last_force_failure_reason**|**int**|Motivo di utilizzo forzato del piano perché non è riuscita.<br /><br /> 0: nessun errore, il numero di errore in caso contrario dell'errore che ha causato l'imposizione esito negativo<br /><br /> 8637: ONLINE_INDEX_BUILD<br /><br /> 8683: INVALID_STARJOIN<br /><br /> 8684: TIME_OUT<br /><br /> 8689: NO_DB<br /><br /> 8690: HINT_CONFLICT<br /><br /> 8691: SETOPT_CONFLICT<br /><br /> 8694: DQ_NO_FORCING_SUPPORTED<br /><br /> 8698: NO_PLAN<br /><br /> 8712: NO_INDEX<br /><br /> 8713: VIEW_COMPILE_FAILED<br /><br /> \<altro valore >: GENERAL_FAILURE|  
|**last_force_failure_reason_desc**|**nvarchar (128)**|Descrizione testuale last_force_failure_reason_desc.<br /><br /> ONLINE_INDEX_BUILD: query tenta di modificare i dati mentre la tabella di destinazione dispone di un indice viene compilato online<br /><br /> INVALID_STARJOIN: piano contiene specifica StarJoin non valida<br /><br /> TIME_OUT: Numero di Query Optimizer ha superato di operazioni consentite durante la ricerca del piano specificato dal piano forzato<br /><br /> NO_DB: Un database specificato nel piano non esiste.<br /><br /> HINT_CONFLICT: Impossibile compilare la Query perché il piano è in conflitto con un hint di query<br /><br /> DQ_NO_FORCING_SUPPORTED: Impossibile eseguire query piano è in conflitto con l'utilizzo di query distribuite o operazioni full-text.<br /><br /> NO_PLAN: Query processor Impossibile generare il piano di query perché non è stato possibile verificare il piano forzato risulti valida per la query<br /><br /> NO_INDEX: L'indice specificato nel piano non esiste<br /><br /> VIEW_COMPILE_FAILED: Impossibile forzare il piano di query a causa di un problema in una vista indicizzata a cui fa riferimento nel piano<br /><br /> GENERAL_FAILURE: errore generale di forzatura (non descritte con motivi sopra)|  
|**count_compiles**|**bigint**|Pianificare le statistiche di compilazione.|  
|**initial_compile_start_time**|**datetimeoffset**|Pianificare le statistiche di compilazione.|  
|**last_compile_start_time**|**datetimeoffset**|Pianificare le statistiche di compilazione.|  
|**last_execution_time**|**datetimeoffset**|Ora dell'ultima esecuzione fa riferimento all'ultima ora di fine del piano di query /.|  
|**avg_compile_duration**|**float**|Pianificare le statistiche di compilazione.|  
|**last_compile_duration**|**bigint**|Pianificare le statistiche di compilazione.|  
  
## <a name="plan-forcing-limitations"></a>Limitazioni di utilizzo forzato del piano
Query Store è dotato di un meccanismo per imporre a Query Optimizer l'uso di determinati piani di esecuzione. Esistono tuttavia alcune limitazioni che possono impedire l'imposizione di un piano. 

In primo luogo, se il piano contiene i costrutti seguenti:
* Istruzione Insert bulk.
* Istruzione Insert bulk.
* Riferimento a una tabella esterna
* Query distribuita o operazioni full-text
* Uso di query globali 
* Cursori
* Specifica di join a stella non valida 

In secondo luogo, quando gli oggetti su cui si basa il piano non sono più disponibili:
* Database (se il database da cui ha avuto origine il piano non esiste più)
* Indice (non più esistente o disabilitato)

Infine, problemi del piano stesso:
* Piano non valido per query
* Numero di operazioni consentite per Query Optimizer superato
* XML del piano formato in modo non corretto

## <a name="permissions"></a>Permissions  
 Richiede il **VIEW DATABASE STATE** autorizzazione.  
  
## <a name="see-also"></a>Vedere anche  
 [database_query_store_options &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [Sys.query_context_settings &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [query_store_query &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [query_store_query_text &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [query_store_runtime_stats &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [Sys.query_store_runtime_stats_interval &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [Monitoraggio delle prestazioni tramite Archivio query](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Archivio query Stored procedure &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
  
  
