---
title: ALTER SERVER AUDIT SPECIFICATION (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 05/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER SERVER AUDIT SPECIFICATION
- ALTER_SERVER_AUDIT_SPECIFICATION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- server audit [SQL Server]
- audits [SQL Server], specification
- ALTER SERVER AUDIT SPECIFICATION statement
ms.assetid: 9cac288b-940e-4c16-88d6-de06aeed2b47
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 217bc5ba66cfe376a2e970f82714d5ef447b1789
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="alter-server-audit-specification-transact-sql"></a>ALTER SERVER AUDIT SPECIFICATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Modifica un oggetto specifica controllo server utilizzando la funzionalità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Audit. Per altre informazioni, vedere [SQL Server Audit &#40;Motore di database&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
ALTER SERVER AUDIT SPECIFICATION audit_specification_name  
{  
    [ FOR SERVER AUDIT audit_name ]  
    [ { { ADD | DROP } ( audit_action_group_name )  
      } [, ...n] ]  
    [ WITH ( STATE = { ON | OFF } ) ]  
}  
[ ; ]  
```  
  
## <a name="arguments"></a>Argomenti  
 *audit_specification_name*  
 Nome della specifica del controllo.  
  
 *audit_name*  
 Nome del controllo al quale viene applicata questa specifica.  
  
 *audit_action_group_name*  
 Nome di un gruppo di azioni controllabili a livello di server. Per un elenco di gruppi di azioni di controllo, vedere [azioni e gruppi di azioni di SQL Server Audit](../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md).  
  
 CON **(** STATO  **=**  {ON | OFF} **)**  
 Abilita o disabilita la raccolta di record mediante il controllo per questa specifica del controllo.  
  
## <a name="remarks"></a>Osservazioni  
 È necessario impostare lo stato di una specifica del controllo sull'opzione OFF per apportare modifiche a una specifica del controllo. Se ALTER DATABASE AUDIT SPECIFICATION viene eseguita quando una specifica del controllo è abilitata con qualsiasi altra opzione diversa da STATE=OFF, verrà visualizzato un messaggio di errore.  
  
## <a name="permissions"></a>Permissions  
 Gli utenti che dispongono dell'autorizzazione ALTER ANY SERVER AUDIT possono modificare specifiche del controllo del server e associarle a qualsiasi controllo.  
  
 Dopo essere stata creata, la specifica del controllo del server può essere visualizzata dalle entità che dispongono dell'autorizzazione CONTROL SERVER oALTER ANY SERVER AUDIT o dell'account sysadmin oppure dalle entità che possono accedere esplicitamente al controllo.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene crea una specifica del controllo del server denominata `HIPPA_Audit_Specification`. Elimina il gruppo di azioni di controllo per gli accessi non riusciti e aggiunge un gruppo di azioni di controllo per l'accesso agli oggetti di Database per un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] audit denominato `HIPPA_Audit`.  
  
```  
ALTER SERVER AUDIT SPECIFICATION HIPPA_Audit_Specification  
FOR SERVER AUDIT HIPPA_Audit  
    DROP (FAILED_LOGIN_GROUP)  
    ADD (DATABASE_OBJECT_ACCESS_GROUP);  
GO  
```  
  
 Per un esempio completo su come creare un controllo, vedere [SQL Server Audit &#40; motore di Database &#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  
  

## <a name="see-also"></a>Vedere anche  
 [CREATE SERVER AUDIT &#40; Transact-SQL &#41;](../../t-sql/statements/create-server-audit-transact-sql.md)   
 [ALTER SERVER AUDIT &#40; Transact-SQL &#41;](../../t-sql/statements/alter-server-audit-transact-sql.md)   
 [DROP SERVER AUDIT &#40; Transact-SQL &#41;](../../t-sql/statements/drop-server-audit-transact-sql.md)   
 [CREATE SERVER AUDIT SPECIFICATION &#40; Transact-SQL &#41;](../../t-sql/statements/create-server-audit-specification-transact-sql.md)   
 [DROP SERVER AUDIT SPECIFICATION &#40; Transact-SQL &#41;](../../t-sql/statements/drop-server-audit-specification-transact-sql.md)   
 [CREARE DATABASE AUDIT SPECIFICATION &#40; Transact-SQL &#41;](../../t-sql/statements/create-database-audit-specification-transact-sql.md)   
 [ALTER DATABASE AUDIT SPECIFICATION &#40; Transact-SQL &#41;](../../t-sql/statements/alter-database-audit-specification-transact-sql.md)   
 [DROP DATABASE AUDIT SPECIFICATION &#40; Transact-SQL &#41;](../../t-sql/statements/drop-database-audit-specification-transact-sql.md)   
 [AUTORIZZAZIONE ALTER &#40; Transact-SQL &#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [Sys. fn_get_audit_file &#40; Transact-SQL &#41;](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)   
 [Sys. server_audits &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-server-audits-transact-sql.md)   
 [Sys. server_file_audits &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)   
 [server_audit_specifications &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)   
 [Sys. server_audit_specification_details – &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)   
 [Sys. database_audit_specifications &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)   
 [database_audit_specification_details &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)   
 [Sys.dm server_audit_status &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [Sys.dm audit_actions &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)   
 [Creazione di un controllo del server e di una specifica del controllo del server](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
