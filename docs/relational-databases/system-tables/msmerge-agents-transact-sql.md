---
title: MSmerge_agents (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/14/2017
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
- MSmerge_agents
- MSmerge_agents_TSQL
dev_langs: TSQL
helpviewer_keywords: MSmerge_agents system table
ms.assetid: 639d2ebb-2c37-4fe0-b14b-1637bc5fc221
caps.latest.revision: "28"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 301961fe3940105c7acdf29fcb30fc734c67fece
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="msmergeagents-transact-sql"></a>MSmerge_agents (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Il **MSmerge_agents** tabella contiene una riga per ogni agente di Merge eseguito nel Sottoscrittore. Questa tabella è archiviata nel database di distribuzione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**id**|**int**|ID dell'agente di merge.|  
|**name**|**nvarchar (100)**|Nome dell'agente di merge.|  
|**publisher_id**|**smallint**|ID del server di pubblicazione.|  
|**publisher_db**|**sysname**|Nome del database del server di pubblicazione.|  
|**pubblicazione**|**sysname**|Nome della pubblicazione.|  
|**subscriber_id**|**smallint**|ID del Sottoscrittore.|  
|**subscriber_db**|**sysname**|Nome del database di sottoscrizione.|  
|**local_job**|**bit**|Specifica se nel server di distribuzione locale è presente un processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|  
|**job_id**|**Binary (16)**|Numero di identificazione del processo.|  
|**profile_id**|**int**|L'ID di configurazione di **MSagent_profiles** tabella.|  
|**anonymous_subid**|**uniqueidentifier**|ID di un agente anonimo.|  
|**subscriber_name**|**sysname**|Nome del Sottoscrittore.|  
|**creation_date**|**datetime**|Data e ora di creazione dell'agente di distribuzione o di merge.|  
|**offload_enabled**|**bit**|Specifica se è possibile o meno attivare l'agente in remoto.<br /><br /> **0** specifica l'agente non può essere attivato in remoto.<br /><br /> **1** specifica l'agente verrà attivato in remoto nel computer remoto specificato nella proprietà offload_server.|  
|**offload_server**|**sysname**|Nome di rete del server da utilizzare per l'attivazione remota dell'agente.|  
|**SID**|**varbinary (85)**|ID di sicurezza (SID) dell'agente di distribuzione o di merge durante la prima esecuzione dell'agente.|  
|**subscriber_security_mode**|**smallint**|Modalità di sicurezza utilizzata dall'agente per la connessione al Sottoscrittore. I possibili valori sono i seguenti:<br /><br /> **0**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'autenticazione.<br /><br /> **1**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] l'autenticazione di Windows.|  
|**subscriber_login**|**sysname**|Account di accesso utilizzato per la connessione al Sottoscrittore.|  
|**subscriber_password**|**nvarchar (524)**|Valore crittografato della password utilizzata per la connessione al Sottoscrittore.|  
|**publisher_security_mode**|**smallint**|Modalità di sicurezza utilizzata dall'agente per la connessione al server di pubblicazione. I possibili valori sono i seguenti:<br /><br /> **0**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'autenticazione.<br /><br /> **1**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] l'autenticazione di Windows.|  
|**publisher_login**|**sysname**|Account di accesso utilizzato per la connessione al server di pubblicazione.|  
|**publisher_password**|**nvarchar (524)**|Valore crittografato della password utilizzata per la connessione al server di pubblicazione.|  
|**job_step_uid**|**uniqueidentifier**|ID univoco del passaggio di processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent in cui viene avviato l'agente.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
