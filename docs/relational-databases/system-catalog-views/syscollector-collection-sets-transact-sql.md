---
title: syscollector_collection_sets (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- syscollector_collection_sets_TSQL
- syscollector_collection_sets
dev_langs:
- TSQL
helpviewer_keywords:
- data collector view
- syscollector_collection_sets view
ms.assetid: db0def92-f25b-45da-9709-eab972b33800
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e9f33a49eef6a80e058a12ff032322bb9060c7af
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/03/2018
---
# <a name="syscollectorcollectionsets-transact-sql"></a>syscollector_collection_sets (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Fornisce informazioni su un set di raccolta, inclusa pianificazione, modalità di raccolta e stato.  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|collection_set_id|**int**|Identificatore locale del set di raccolta. Non ammette i valori Null.|  
|collection_set_uid|**uniqueidentifier**|Identificatore univoco globale del set di raccolta. Non ammette i valori Null.|  
|name|**nvarchar(4000)**|Nome del set di raccolta. Ammette i valori Null.|  
|target|**nvarchar(max)**|Identifica la destinazione per il set di raccolta. Ammette i valori Null.|  
|is_system|**bit**|Attivato (1) o disattivato (0) per indicare se il set di raccolta è stato fornito con l'agente di raccolta dati o se è stato aggiunto in seguito da dc_admin. Potrebbe trattarsi di un set di raccolta personalizzato sviluppato internamente o da terze parti. Non ammette i valori Null.|  
|is_running|**bit**|Indica se il set di raccolta è in esecuzione o no. Non ammette i valori Null.|  
|collection_mode|**smallint**|Specifica la modalità di raccolta per il set di raccolta. Non ammette i valori Null.<br /><br /> La modalità di raccolta è una delle seguenti:<br /><br /> 0 - Modalità cache. La raccolta e il caricamento dei dati seguono una pianificazione differente.<br /><br /> 1 - Modalità non in cache. La raccolta e il caricamento dei dati seguono la stessa pianificazione.|  
|proxy_id|**int**|Identifica il proxy utilizzato per eseguire il passaggio processo del set di raccolta. Ammette i valori Null.|  
|schedule_uid|**uniqueidentifier**|Fornisce un puntatore alla pianificazione del set di raccolta. Ammette i valori Null.|  
|collection_job_id|**uniqueidentifier**|Identifica il processo di raccolta. Ammette i valori Null.|  
|upload_job_id|**uniqueidentifier**|Identifica il processo di caricamento raccolta. Ammette i valori Null.|  
|logging_level|**smallint**|Specifica il livello di registrazione (0, 1 o 2). Non ammette i valori Null.|  
|days_until_expiration|**smallint**|Numero di giorni durante i quali i dati raccolti vengono salvati nel data warehouse di gestione. Non ammette i valori Null.|  
|description|**nvarchar(4000)**|Descrive il set di raccolta. Ammette i valori Null.|  
|dump_on_any_error|**bit**|Attivato (1) o disattivato (0) per indicare se creare un [!INCLUDE[ssIS](../../includes/ssis-md.md)] file di dump su qualsiasi errore. Non ammette i valori Null.|  
|dump_on_codes|**nvarchar(max)**|Contiene l'elenco di [!INCLUDE[ssIS](../../includes/ssis-md.md)] i codici di errore utilizzati per attivare il file di dump. Ammette i valori Null.|  
  
## <a name="permissions"></a>Autorizzazioni  
 Richiede SELECT per dc_operator, dc_proxy.  
  
## <a name="remarks"></a>Osservazioni  
 L'API dell'agente di raccolta dati consente di modificare o eliminare solo i set di raccolta da essi creati. I set di raccolta forniti con il sistema non possono essere modificati o eliminati. Tuttavia, è possibile abilitare o disabilitare un set di raccolta del sistema e modificare la configurazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure dell'agente di raccolta dati &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [Viste dell'agente di raccolta dati &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [Raccolta dati](../../relational-databases/data-collection/data-collection.md)  
  
  
