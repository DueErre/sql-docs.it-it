---
title: sp_help_publication_access (Transact-SQL) | Documenti Microsoft
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
- sp_help_publication_access
- sp_help_publication_access_TSQL
helpviewer_keywords: sp_help_publication_access
ms.assetid: 9408fa13-54a0-4cb1-8fb0-845e5536ef50
caps.latest.revision: "26"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1568ded984bcb38c6633fdf5ceddfb2b960df41b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="sphelppublicationaccess-transact-sql"></a>sp_help_publication_access (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce un elenco di tutti gli account di accesso a cui sono state concesse autorizzazioni per una pubblicazione. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_help_publication_access [ @publication = ] 'publication'  
    [ , [ @return_granted = ] 'return_granted' ]   
    [ , [ @login = ] 'login' ]  
    [ , [ @initial_list = ] initial_list ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@publication=**] **'***pubblicazione***'**  
 Nome della pubblicazione a cui si desidera accedere. *pubblicazione* è **sysname**, non prevede alcun valore predefinito.  
  
 [  **@return_granted=**] **'***return_granted***'**  
 ID di accesso. *return_granted* è **bit**, con un valore predefinito è 1. Se **0** specificato e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene utilizzata l'autenticazione, vengono restituiti gli account di accesso disponibili visualizzati nel server di pubblicazione, ma non nel server di distribuzione. Se **0** specificato e viene utilizzata l'autenticazione di Windows, gli account di accesso non sia stata esplicitamente negato l'accesso a livello server di pubblicazione o server di distribuzione vengono restituiti.  
  
 [  **@login=**] **'***accesso***'**  
 ID dell'account di accesso di sicurezza standard. *account di accesso* è **sysname**, il valore predefinito è  **%** .  
  
 [  **@initial_list =**] *initial_list*  
 Specifica se devono essere restituiti tutti i membri con accesso alla pubblicazione oppure solo i membri che avevano accesso prima che venissero aggiunti nuovi membri all'elenco. *initial_list* è di tipo bit, il valore predefinito è **0**.  
  
 **1** restituisce informazioni per tutti i membri del **sysadmin** ruolo predefinito del server con un account di accesso validi nel server di distribuzione esistente al momento della creazione della pubblicazione, nonché l'account di accesso corrente.  
  
 **0** restituisce informazioni per tutti i membri del **sysadmin** ruolo predefinito del server con l'account di accesso validi nel server di distribuzione esistente al momento della creazione della pubblicazione anche come tutti gli utenti nell'elenco di accesso alla pubblicazione che non far parte di **sysadmin** ruolo predefinito del server.  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|**LoginName**|**nvarchar(256)**|Nome effettivo dell'account di accesso.|  
|**Isntname**|**int**|**0** = account di accesso non è un utente di Windows.<br /><br /> **1** = account di accesso è un utente di Windows.|  
|**Isntgroup**|**int**|**0** = account di accesso non è un gruppo di Windows.<br /><br /> **1** = account di accesso è un gruppo di Windows.|  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_help_publication_access** viene utilizzata in tutti i tipi di replica.  
  
 Quando entrambi **Isntname** e **Isntgroup** nel risultato sono set **0**, si presuppone che l'account di accesso sia un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] account di accesso.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server o **db_owner** ruolo predefinito del database possono eseguire **sp_help_publication_access**.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_grant_publication_access &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-grant-publication-access-transact-sql.md)   
 [sp_revoke_publication_access &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-revoke-publication-access-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
