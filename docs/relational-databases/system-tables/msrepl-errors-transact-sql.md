---
title: MSrepl_errors (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- MSrepl_errors
- MSrepl_errors_TSQL
dev_langs: TSQL
helpviewer_keywords: MSrepl_errors system table
ms.assetid: c6e023c1-2c32-4269-8d76-e442ea309e4b
caps.latest.revision: "16"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 66c276d57f2df480d1d3977304911c2826068cce
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="msreplerrors-transact-sql"></a>MSrepl_errors (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Il **MSrepl_errors** tabella contiene righe con informazioni di errore estese agente di distribuzione e agente di Merge. Questa tabella è archiviata nel database di distribuzione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**id**|**int**|ID dell'errore.|  
|**time**|**datetime**|Ora in cui si è verificato l'errore.|  
|**error_type_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**source_type_id**|**int**|ID del tipo di origine dell'errore.|  
|**source_name**|**nvarchar (100)**|Nome dell'origine dell'errore.|  
|**error_code**|**sysname**|Codice di errore.|  
|**testo_errore**|**ntext**|Messaggio di errore.|  
|**xact_seqno**|**varbinary (16)**|Numero di sequenza iniziale del log delle transazioni per il batch con errori di esecuzione. Viene utilizzato solo dagli agenti di distribuzione e corrisponde al numero di sequenza del log delle transazioni per la prima transazione nel batch con errori di esecuzione.|  
|**command_id**|**int**|ID di comando del batch che ha avuto esito negativo. Viene utilizzato solo dagli agenti di distribuzione e corrisponde all'ID del primo comando di tale batch.|  
|**session_id**|**int**|ID della sessione dell'agente in cui si è verificato l'errore.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
