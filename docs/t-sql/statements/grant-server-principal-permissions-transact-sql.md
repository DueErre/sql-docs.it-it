---
title: "Autorizzazioni per entità Server GRANT (Transact-SQL) | Documenti Microsoft"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- impersonate [SQL Server], granting
- granting permissions [SQL Server], logins
- permissions [SQL Server], impersonate
- permissions [SQL Server], logins
- GRANT statement, impersonation
- GRANT statement, logins
- logins [SQL Server], granting access
- granting permissions [SQL Server], impersonation
ms.assetid: 4cbed281-5e1e-4d8b-b410-4c18a6cd0205
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ee77fb0aa9ddcb274b1ac3ff88690d9675d2d192
ms.contentlocale: it-it
ms.lasthandoff: 09/01/2017

---
# <a name="grant-server-principal-permissions-transact-sql"></a>Autorizzazioni per entità server GRANT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Concede le autorizzazioni per un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
GRANT permission [ ,...n ] }   
    ON   
    { [ LOGIN :: SQL_Server_login ]  
      | [ SERVER ROLE :: server_role ] }   
    TO <server_principal> [ ,...n ]  
    [ WITH GRANT OPTION ]  
    [ AS SQL_Server_login ]   
  
<server_principal> ::=   
    SQL_Server_login  
    | SQL_Server_login_from_Windows_login   
    | SQL_Server_login_from_certificate   
    | SQL_Server_login_from_AsymKey   
    | server_role  
```  
  
## <a name="arguments"></a>Argomenti  
 *autorizzazione*  
 Specifica un'autorizzazione che può essere concessa per un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per un elenco delle autorizzazioni, vedere la sezione Osservazioni di seguito in questo argomento.  
  
 Account di accesso **::** *SQL_Server_login*  
 Specifica l'account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per cui viene concessa l'autorizzazione. Il qualificatore di ambito (**::**) è obbligatorio.  
  
 RUOLO del SERVER **::** *server_role*  
 Specifica il ruolo del server definito dall'utente per cui viene concessa l'autorizzazione. Il qualificatore di ambito (**::**) è obbligatorio.  
  
 PER \<server_principal > specifica il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] account di accesso o ruolo server a cui viene concessa l'autorizzazione.  
  
 *SQL_Server_login*  
 Specifica il nome di un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 *SQL_Server_login_from_Windows_login*  
 Specifica il nome di un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] creato da un account di accesso di Windows.  
  
 *SQL_Server_login_from_certificate*  
 Specifica il nome di un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sul quale viene eseguito il mapping a un certificato.  
  
 *SQL_Server_login_from_AsymKey*  
 Specifica il nome di un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sul quale viene eseguito il mapping a una chiave asimmetrica.  
  
 *server_role*  
 Specifica il nome di un ruolo del server definito dall'utente.  
  
 WITH GRANT OPTION  
 Indica che l'entità potrà inoltre concedere l'autorizzazione specificata ad altre entità.  
  
 AS *SQL_Server_login*  
 Specifica l'account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dal quale l'entità che esegue la query ottiene il diritto di concedere l'autorizzazione.  
  
## <a name="remarks"></a>Osservazioni  
 È possibile concedere autorizzazioni nell'ambito del server solo se il database corrente è il database master.  
  
 Informazioni sulle autorizzazioni del server sono visibili nella [server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) vista del catalogo. Informazioni sulle entità server sono visibili nella [Sys. server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) vista del catalogo.  
  
 I ruoli del server e gli account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono entità a protezione diretta a livello di server. Nella tabella seguente sono elencate le autorizzazioni più specifiche e limitate che è possibile concedere per un ruolo del server o account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], insieme alle autorizzazioni più generali che le includono in modo implicito.  
  
|Autorizzazione del ruolo del server o dell'account di accesso di SQL Server|Autorizzazione del ruolo del server o dell'account di accesso di SQL Server in cui è inclusa|Autorizzazione del server in cui è inclusa|  
|------------------------------------------------|-----------------------------------------------------------|----------------------------------|  
|CONTROL|CONTROL|CONTROL SERVER|  
|IMPERSONATE|CONTROL|CONTROL SERVER|  
|VIEW DEFINITION|CONTROL|VIEW ANY DEFINITION|  
|ALTER|CONTROL|ALTER ANY LOGIN<br /><br /> ALTER ANY SERVER ROLE|  
  
## <a name="permissions"></a>Permissions  
 Per gli account di accesso, è richiesta l'autorizzazione CONTROL per l'account di accesso o l'autorizzazione ALTER ANY LOGIN per il server.  
  
 Per i ruoli del server, è richiesta l'autorizzazione CONTROL per il ruolo del server o l'autorizzazione ALTER ANY SERVER ROLE per il server.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-granting-impersonate-permission-on-a-login"></a>A. Concessione dell'autorizzazione IMPERSONATE per un account di accesso  
 Nell'esempio seguente viene concessa l'autorizzazione `IMPERSONATE` per l'account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `WanidaBenshoof` a un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] creato dall'utente di Windows `AdvWorks\YoonM`.  
  
```  
USE master;  
GRANT IMPERSONATE ON LOGIN::WanidaBenshoof to [AdvWorks\YoonM];  
GO  
```  
  
### <a name="b-granting-view-definition-permission-with-grant-option"></a>B. Concessione dell'autorizzazione VIEW DEFINITION con GRANT OPTION  
 Nell'esempio seguente viene concessa l'autorizzazione `VIEW DEFINITION` per l'account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `EricKurjan` all'account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `RMeyyappan` con `GRANT OPTION`.  
  
```  
USE master;  
GRANT VIEW DEFINITION ON LOGIN::EricKurjan TO RMeyyappan   
    WITH GRANT OPTION;  
GO   
```  
  
### <a name="c-granting-view-definition-permission-on-a-server-role"></a>C. Concessione dell'autorizzazione VIEW DEFINITION per un ruolo del server  
 Nell'esempio seguente viene concessa l'autorizzazione `VIEW DEFINITION` nel ruolo del server `Sales` per il ruolo del server `Auditors`.  
  
```  
USE master;  
GRANT VIEW DEFINITION ON SERVER ROLE::Sales TO Auditors ;  
GO   
```  
  
## <a name="see-also"></a>Vedere anche  
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.server_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [Entità &#40;motore di database&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Autorizzazioni &#40;motore di database&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Funzioni di sicurezza &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)   
 [Stored procedure di sicurezza &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)  
  
  

