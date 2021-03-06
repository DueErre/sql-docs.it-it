---
title: sp_addapprole (Transact-SQL) | Documenti Microsoft
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
- sp_addapprole_TSQL
- sp_addapprole
dev_langs: TSQL
helpviewer_keywords: sp_addapprole
ms.assetid: 24200295-9a54-4cab-9922-fb2e88632721
caps.latest.revision: "31"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7556f2f78890a0e52efde7758077fbf124ed3bac
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2017
---
# <a name="spaddapprole-transact-sql"></a>sp_addapprole (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aggiunge un ruolo applicazione al database corrente.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Utilizzare [CREATE APPLICATION ROLE](../../t-sql/statements/create-application-role-transact-sql.md) invece.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_addapprole [ @rolename = ] 'role' , [ @password = ] 'password'  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@rolename =** ] **'***ruolo***'**  
 Nome del nuovo ruolo applicazione. *ruolo* è **sysname**, non prevede alcun valore predefinito. *ruolo* deve essere un identificatore valido e non può già esistere nel database corrente.  
  
 I nomi dei ruoli applicazione possono includere da 1 a 128 caratteri, compresi lettere, simboli e numeri. I nomi dei ruoli non può contenere una barra rovesciata (\\) né essere NULL o una stringa vuota (").  
  
 [  **@password =** ] **'***password***'**  
 Password richiesta per attivare il ruolo applicazione. *password* è **sysname**, non prevede alcun valore predefinito. *password* non può essere NULL.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="remarks"></a>Osservazioni  
 Nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gli utenti (e i ruoli) non si diversificano completamente dagli schemi. A partire da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], gli schemi sono completamente distinti dai ruoli. Questa nuova architettura si riflette nel funzionamento dell'istruzione CREATE APPLICATION ROLE. Questa istruzione sostituisce **sp_addapprole**.  
  
 Per mantenere la compatibilità con le versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], **sp_addapprole** verranno eseguite le operazioni seguenti:  
  
-   Se uno schema con lo stesso nome del ruolo applicazione non esiste, tale schema verrà creato. Il nuovo schema sarà di proprietà del ruolo applicazione e sarà lo schema predefinito del ruolo applicazione.  
  
-   Se invece uno schema con lo stesso nome del ruolo applicazione esiste già, la procedura verrà interrotta.  
  
-   La complessità delle password non viene verificato **sp_addapprole**. ma viene controllata dall'istruzione CREATE APPLICATION ROLE.  
  
 Il parametro *password* viene archiviato come hash unidirezionale.  
  
 Il **sp_addapprole** stored procedure non può essere eseguita all'interno di una transazione definita dall'utente.  
  
> [!IMPORTANT]  
>  Microsoft ODBC **crittografare** opzione non è supportata da **SqlClient**. Se possibile, richiedere all'utente di immettere le credenziali del ruolo applicazione in fase di esecuzione. Evitare di archiviare le credenziali in un file. Se è necessario disporre di credenziali persistenti, crittografarle tramite le funzioni CryptoAPI.  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione ALTER ANY APPLICATION ROLE nel database. Se uno schema con lo stesso nome e lo stesso proprietario del nuovo ruolo non esiste, è richiesta anche l'autorizzazione CREATE SCHEMA nel database.  
  
## <a name="examples"></a>Esempi  
 L'esempio seguente aggiunge il nuovo ruolo applicazione `SalesApp` con la password `x97898jLJfcooFUYLKm387gf3` al database corrente.  
  
```  
EXEC sp_addapprole 'SalesApp', 'x97898jLJfcooFUYLKm387gf3' ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE APPLICATION ROLE &#40; Transact-SQL &#41;](../../t-sql/statements/create-application-role-transact-sql.md)  
  
  
