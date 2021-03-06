---
title: sp_adduser (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_adduser
- sp_adduser_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_adduser
ms.assetid: 61a40eb4-573f-460c-9164-bd1bbfaf8b25
caps.latest.revision: "27"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d1a5e8a9041d32823a44f2f0329562741c2e253a
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2017
---
# <a name="spadduser-transact-sql"></a>sp_adduser (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aggiunge un nuovo utente al database corrente.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Utilizzare [CREATE USER](../../t-sql/statements/create-user-transact-sql.md) invece.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_adduser [ @loginame = ] 'login'   
    [ , [ @name_in_db = ] 'user' ]   
    [ , [ @grpname = ] 'role' ]   
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@loginame =** ] **'***accesso***'**  
 Nome dell'account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o dell'account di accesso di Windows. *account di accesso* è un **sysname**, non prevede alcun valore predefinito. *account di accesso* deve essere un oggetto esistente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] account di accesso o account di accesso di Windows.  
  
 [  **@name_in_db =** ] **'***utente***'**  
 Nome del nuovo utente del database. *utente* è un **sysname**, con un valore predefinito è NULL. Se *utente* non viene specificato, il nome del nuovo utente del database predefinito per il *accesso* nome. Specifica di *utente* assegna il nuovo utente, un nome del database diverso dal nome dell'account di accesso a livello di server.  
  
 [  **@grpname =** ] **'***ruolo***'**  
 Ruolo del database di cui è membro il nuovo utente. *ruolo* è **sysname**, con un valore predefinito è NULL. *ruolo* deve essere un ruolo di database valido nel database corrente.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_adduser** verrà creato anche uno schema con il nome dell'utente.  
  
 Dopo avere aggiunto un utente, utilizzare le istruzioni GRANT, DENY e REVOKE per definire le autorizzazioni per controllare le attività che l'utente può svolgere.  
  
 Utilizzare **Sys. server_principals** per visualizzare un elenco di nomi di account di accesso valido.  
  
 Utilizzare **sp_helprole** per visualizzare un elenco di nomi di ruolo validi. Se si specifica un ruolo, l'utente ottiene automaticamente le autorizzazioni definite per tale ruolo. Se non viene specificato un ruolo, l'utente ottiene le autorizzazioni concesse per impostazione predefinita **pubblica** ruolo. Per aggiungere un utente a un ruolo, un valore per il *nome utente* devono essere specificati. (*username* può essere identico *login_id*.)  
  
 Utente **guest** esiste già in ogni database. Aggiunta dell'utente **guest** abiliterà questo utente, se era disabilitata. Per impostazione predefinita, utente **guest** è disabilitato nei nuovi database.  
  
 **sp_adduser** non può essere eseguita all'interno di una transazione definita dall'utente.  
  
 Non è possibile aggiungere un **guest** utente perché un **guest** utente esiste già all'interno di ogni database. Per abilitare il **guest** utente, concedere **guest** dell'autorizzazione CONNECT, come illustrato:  
  
```  
GRANT CONNECT TO guest;  
GO  
```  
  
## <a name="permissions"></a>Permissions  
 È necessario essere il proprietario del database.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-adding-a-database-user"></a>A. Aggiunta di un utente del database  
 Nell'esempio seguente l'utente del database `Vidur` viene aggiunto al ruolo esistente `Recruiting` nel database corrente utilizzando l'account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esistente `Vidur`.  
  
```  
EXEC sp_adduser 'Vidur', 'Vidur', 'Recruiting';  
```  
  
### <a name="b-adding-a-database-user-with-the-same-login-id"></a>B. Aggiunta di un utente del database con lo stesso ID di accesso  
 Nell'esempio seguente l'utente `Arvind` viene aggiunto al database corrente per l'account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `Arvind`. Il valore predefinito di cui appartiene l'utente **pubblica** ruolo.  
  
```  
EXEC sp_adduser 'Arvind';  
```  
  
### <a name="c-adding-a-database-user-with-a-different-name-than-its-server-level-login"></a>C. Aggiunta di un utente del database con un nome diverso dall'account di accesso a livello di server  
 Nell'esempio seguente l'account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `BjornR` viene aggiunto al database corrente che include il nome utente `Bjorn`, quindi l'utente del database `Bjorn` viene aggiunto al ruolo del database `Production`.  
  
```  
EXEC sp_adduser 'BjornR', 'Bjorn', 'Production';  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Sicurezza Stored procedure &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sp_addrole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md)   
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [sp_dropuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropuser-transact-sql.md)   
 [sp_grantdbaccess &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantdbaccess-transact-sql.md)   
 [sp_grantlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
