---
title: sp_helptracertokens (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/14/2017
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
- sp_helptracertokens
- sp_helptracertokens_TSQL
helpviewer_keywords: sp_helptracertokens
ms.assetid: 61f27234-531d-4b37-8fa3-fe4c32e6f521
caps.latest.revision: "16"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 71cc327ba10d62f1e11b922a3e8680134a913d59
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="sphelptracertokens-transact-sql"></a>sp_helptracertokens (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce una riga per ogni token di traccia che è stato inserito in una pubblicazione per determinare la latenza. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione o nel database di distribuzione del server di distribuzione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_helptracertokens [ @publication = ] 'publication'   
    [ , [ @publisher = ] 'publisher' ]   
    [ , [ @publisher_db = ] 'publisher_db' ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@publication=** ] **'***pubblicazione***'**  
 Nome della pubblicazione in cui sono stati inseriti i token di traccia. *pubblicazione* è **sysname**, non prevede alcun valore predefinito.  
  
 [  **@publisher=** ] **'***publisher***'**  
 Nome del server di pubblicazione. *server di pubblicazione* è **sysname**, con un valore predefinito è NULL.  
  
> [!NOTE]  
>  Questo parametro deve essere specificato solo per non[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i server di pubblicazione.  
  
 [  **@publisher_db=** ] **'***publisher_db***'**  
 Nome del database di pubblicazione. *publisher_db* è **sysname**, con un valore predefinito null. Questo parametro viene ignorato se la stored procedure viene eseguita nel server di pubblicazione.  
  
## <a name="result-set"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|**tracer_id**|**int**|Identifica un record di token di traccia.|  
|**publisher_commit**|**datetime**|Data e ora in cui è stato eseguito il commit del record del token nel database di pubblicazione del server di pubblicazione.|  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_helptracertokens** viene utilizzata nella replica transazionale.  
  
 **sp_helptracertokens** viene utilizzata per ottenere gli ID dei token traccia durante l'esecuzione [sp_helptracertokenhistory &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql.md).  
  
## <a name="example"></a>Esempio  
 [!code-sql[HowTo#sp_tracertokens](../../relational-databases/replication/codesnippet/tsql/sp-helptracertokens-tran_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server, il **db_owner** ruolo predefinito del database nel database di pubblicazione o **db_owner** predefiniti del database o  **replmonitor** ruoli nel database di distribuzione possono eseguire **sp_helptracertokenhistory**.  
  
## <a name="see-also"></a>Vedere anche  
 [Misurare la latenza e convalidare le connessioni per la replica transazionale](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)   
 [sp_deletetracertokenhistory &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-deletetracertokenhistory-transact-sql.md)  
  
  
