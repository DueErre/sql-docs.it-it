---
title: sp_help_log_shipping_primary_database (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_help_log_shipping_primary_database_TSQL
- sp_help_log_shipping_primary_database
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_log_shipping_primary_database
ms.assetid: e711b01c-ef29-4eb6-a016-0e647e337818
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 56de87e340bc9bd6006208754451c54c145fbdba
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/03/2018
---
# <a name="sphelplogshippingprimarydatabase-transact-sql"></a>sp_help_log_shipping_primary_database (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Recupera le impostazioni del database primario.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_help_log_shipping_primary_database  
[ @database = ] 'database' OR  
[ @primary_id = ] 'primary_id'  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@database =** ] '*database*'  
 Nome del database primario per il log shipping. *database* è **sysname**, senza impostazione predefinita e non può essere NULL.  
  
 [ **@primary_id =** ] '*primary_id*'  
 ID del database primario nella configurazione per il log shipping. *primary_id* è **uniqueidentifier** e non può essere NULL.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Description|  
|-----------------|-----------------|  
|**primary_id**|ID del database primario nella configurazione per il log shipping.|  
|**primary_database**|Nome del database primario nella configurazione di log shipping.|  
|**backup_directory**|Directory in cui vengono archiviati i file di backup del log delle transazioni dal server primario.|  
|**backup_share**|Percorso di rete o UNC della directory di backup.|  
|**backup_retention_period**|Intervallo di tempo, espresso in minuti, di conservazione del file di backup dei log nella directory di backup trascorso il quale il file viene eliminato.|  
|**backup_compression**|Indica se la configurazione di log shipping utilizza [compressione dei backup](../../relational-databases/backup-restore/backup-compression-sql-server.md).<br /><br /> **0** = Disabled. I backup del log non vengono mai compressi.<br /><br /> **1** = abilitato. I backup del log vengono sempre compressi.<br /><br /> **2** = utilizzare l'impostazione di [consente di visualizzare o configurare l'opzione di configurazione del Server di backup compression default](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md). Si tratta del valore predefinito.<br /><br /> La compressione dei backup è supportata solo in [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] o versione successiva. Nelle altre edizioni il valore è sempre 2.|  
|**backup_job_id**|Il [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ID processo dell'agente associato il processo di backup nel server primario.|  
|**monitor_server**|Nome dell'istanza di [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] utilizzata come server di monitoraggio nella configurazione del log shipping.|  
|**monitor_server_security_mode**|Modalità di sicurezza utilizzata per connettersi al server di monitoraggio.<br /><br /> 1 = Autenticazione di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.<br /><br /> 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'autenticazione.|  
|**backup_threshold**|Numero di minuti consentiti tra le operazioni di backup prima che venga generato un avviso.|  
|**threshold_alert**|Avviso da generare quando viene superata la soglia per il backup.|  
|**threshold_alert_enabled**|Determina se sono abilitati gli avvisi relativi alla soglia per il backup.<br /><br /> **1** = abilitato.<br /><br /> **0** = Disabled.|  
|**last_backup_file**|Percorso assoluto del backup del log delle transazioni più recente.|  
|**last_backup_date**|Data e ora dell'ultima operazione di backup dei log.|  
|**last_backup_date_utc**|Data e ora dell'ultima operazione di backup del log delle transazioni nel database primario in base all'ora UTC (Coordinated Universal Time).|  
|**history_retention_period**|Intervallo di tempo, espresso in minuti, di conservazione dei record relativi alla cronologia di log shipping per un database primario specifico trascorso il quale i record vengono eliminati.|  
  
## <a name="remarks"></a>Osservazioni  
 **sp_help_log_shipping_primary_database** deve essere eseguita la **master** database nel server primario.  
  
## <a name="permissions"></a>Autorizzazioni  
 Solo i membri del **sysadmin** ruolo predefinito del server possono eseguire questa procedura.  
  
## <a name="examples"></a>Esempi  
 In questo esempio viene illustrato l'utilizzo **sp_help_log_shipping_primary_database** per recuperare le impostazioni di database primario per il database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```  
EXEC master.dbo.sp_help_log_shipping_primary_database @database=N'AdventureWorks2012';  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni sul Log Shipping &#40; SQL Server &#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
