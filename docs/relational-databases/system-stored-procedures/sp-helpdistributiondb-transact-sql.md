---
title: sp_helpdistributiondb (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_helpdistributiondb_TSQL
- sp_helpdistributiondb
helpviewer_keywords: sp_helpdistributiondb
ms.assetid: a2917020-26d1-4011-99f8-9212d120fd2d
caps.latest.revision: "26"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 040970c34e8154538135e355744746e3ee1e3cb6
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="sphelpdistributiondb-transact-sql"></a>sp_helpdistributiondb (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce le proprietà del database di distribuzione specificato. La stored procedure viene eseguita nel database di distribuzione del server di distribuzione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_helpdistributiondb [ [ @database= ] 'database_name' ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@database=**] **'***database_name***'**  
 Nome del database di cui vengono restituite le proprietà. *database_name* è **sysname**, il valore predefinito è  **%**  per tutti i database associati al server di distribuzione in cui l'utente dispone delle autorizzazioni.  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome del database di distribuzione.|  
|**min_distretention**|**int**|Periodo di memorizzazione minimo espresso in ore che deve trascorrere prima dell'eliminazione delle transazioni.|  
|**max_distretention**|**int**|Periodo di memorizzazione massimo espresso in ore trascorso il quale le transazioni vengono eliminate.|  
|**periodo di memorizzazione cronologia**|**int**|Numero di ore di memorizzazione della cronologia.|  
|**history_cleanup_agent**|**sysname**|Nome dell'agente di pulizia del contenuto della cronologia.|  
|**distribution_cleanup_agent**|**sysname**|Nome dell'agente di pulizia dei riferimenti alla distribuzione.|  
|**status**|**int**|Solo per uso interno.|  
|**data_folder**|**nvarchar(255)**|Nome della directory utilizzata per archiviare i file di database.|  
|**data_file**|**nvarchar(255)**|Nome del file di database.|  
|**data_file_size**|**int**|Dimensioni iniziali del file di dati in MB.|  
|**log_folder**|**nvarchar(255)**|Nome della directory per il file di log del database.|  
|**file_registro**|**nvarchar(255)**|Nome del file di log.|  
|**log_file_size**|**int**|Dimensioni iniziali del file di log in MB.|  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_helpdistributiondb** viene utilizzata in tutti i tipi di replica.  
  
## <a name="permissions"></a>Permissions  
 I membri del **db_owner** ruolo predefinito del database o **replmonitor** possono eseguire in un database di distribuzione e gli utenti nell'elenco di accesso alla pubblicazione di una pubblicazione che utilizza il database di distribuzione **sp_helpdistributiondb** per restituire informazioni relative ai file. I membri del **pubblica** ruolo può eseguire **sp_helpdistributiondb** per restituire informazioni non relative ai file per i database di distribuzione a cui hanno accesso.  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzare e modificare le proprietà del server di pubblicazione e del database di distribuzione](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_adddistributiondb &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md)   
 [sp_changedistributiondb &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-changedistributiondb-transact-sql.md)   
 [sp_dropdistributiondb &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropdistributiondb-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
