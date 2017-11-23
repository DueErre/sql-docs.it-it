---
title: Sys.dm exec_cached_plan_dependent_objects (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_cached_plan_dependent_objects
- dm_exec_cached_plan_dependent_objects_TSQL
- sys.dm_exec_cached_plan_dependent_objects_TSQL
- dm_exec_cached_plan_dependent_objects
dev_langs: TSQL
helpviewer_keywords: sys.dm_exec_cached_plan_dependent_objects dynamic management function
ms.assetid: 9b6cf5f7-b267-44fb-aac8-f49c9aa10cc1
caps.latest.revision: "19"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b6e044c20434b7aa8a0f927d4c626984309f7a29
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmexeccachedplandependentobjects-transact-sql"></a>sys.dm_exec_cached_plan_dependent_objects (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Restituisce una riga per ogni piano di esecuzione [!INCLUDE[tsql](../../includes/tsql-md.md)] o CLR (Common Language Runtime) e ogni cursore associato a un piano.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
dm_exec_cached_plan_dependent_objects(plan_handle)  
```  
  
## <a name="arguments"></a>Argomenti  
 *plan_handle*  
 Identifica in modo univoco un piano di esecuzione di query per un batch eseguito il cui piano risiede nella cache dei piani. *plan_handle* è **varbinary(64)**. Il *plan_handle* può essere ottenuto dagli oggetti a gestione dinamica seguenti:  
  
-   [Sys.dm exec_cached_plans &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
  
-   [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  
-   [Sys.dm exec_requests &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
## <a name="table-returned"></a>Tabella restituita  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|**usecounts**|**int**|Numero di volte in cui è stato utilizzato il contesto di esecuzione o il cursore.<br /><br /> La colonna non ammette i valori Null.|  
|**memory_object_address**|**varbinary (8)**|Indirizzo di memoria del contesto di esecuzione o del cursore.<br /><br /> La colonna non ammette i valori Null.|  
|**cacheobjtype**|**nvarchar(50)**|Il tipo di oggetto della cache di piano. La colonna non ammette i valori Null. I possibili valori sono i seguenti:<br /><br /> Piano eseguibile<br /><br /> Funzione CLR compilata<br /><br /> Procedura CLR compilata<br /><br /> Cursore|  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione VIEW SERVER STATE per il server.  
  
## <a name="physical-joins"></a>Join fisici  
 ![Diagramma delle relazioni tra](../../relational-databases/system-dynamic-management-views/media/dm-dependent-objects.gif "diagramma delle relazioni")  
  
## <a name="relationship-cardinalities"></a>Cardinalità delle relazioni  
  
|Da|Per|Il|Relazione|  
|----------|--------|--------|------------------|  
|**dm_exec_cached_plan_dependent_objects**|**dm_os_memory_objects**|**memory_object_address**|Uno-a-uno|  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni e viste a gestione dinamica &#40; relative all'esecuzione Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [Funzioni e viste a gestione dinamica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Sys. syscacheobjects &#40; Transact-SQL &#41;](../../relational-databases/system-compatibility-views/sys-syscacheobjects-transact-sql.md)  
  
  