---
title: "DENY-autorizzazioni per entità Server (Transact-SQL) | Documenti Microsoft"
ms.custom: 
ms.date: 06/09/2017
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
dev_langs:
- TSQL
helpviewer_keywords:
- DENY statement, impersonate
- permissions [SQL Server], impersonate
- impersonate [SQL Server], denying
- DENY statement, logins
- permissions [SQL Server], logins
- denying permissions [SQL Server], logins
- servers [SQL Server], permissions
- logins [SQL Server], denying access
ms.assetid: 859affa7-0567-47d1-9490-57c1abbd619b
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 795c7dcc946966859e5d81382df75a4bb646e38d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="deny-server-principal-permissions-transact-sql"></a>Autorizzazioni per entità server DENY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Nega le autorizzazioni concesse per un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
DENY permission [ ,...n ] }   
    ON   
    { [ LOGIN :: SQL_Server_login ]  
      | [ SERVER ROLE :: server_role ] }   
    TO <server_principal> [ ,...n ]  
    [ CASCADE ]  
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
 Specifica un'autorizzazione che può essere negata per un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per un elenco delle autorizzazioni, vedere la sezione Osservazioni di seguito in questo argomento.  
  
 Account di accesso **::** *SQL_Server_login*  
 Specifica l'account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per cui viene negata l'autorizzazione. Il qualificatore di ambito (**::**) è obbligatorio.  
  
 RUOLO del SERVER **::** *server_role*  
 Specifica il ruolo del server a cui viene negata l'autorizzazione. Il qualificatore di ambito (**::**) è obbligatorio.  
  
 PER \<server_principal >  
 Specifica il ruolo del server o l'account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a cui viene concessa l'autorizzazione.  
  
 PER *SQL_Server_login*  
 Specifica l'account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a cui viene negata l'autorizzazione.  
  
 *SQL_Server_login*  
 Specifica il nome di un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 *SQL_Server_login_from_Windows_login*  
 Specifica il nome di un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] creato da un account di accesso di Windows.  
  
 *SQL_Server_login_from_certificate*  
 Specifica il nome di un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sul quale viene eseguito il mapping a un certificato.  
  
 *SQL_Server_login_from_AsymKey*  
 Specifica il nome di un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sul quale viene eseguito il mapping a una chiave asimmetrica.  
  
 *server_role*  
 Specifica il nome di un ruolo del server.  
  
 CASCADE  
 Indica che l'autorizzazione negata viene negata anche ad altre entità alle quali è stata concessa da questa entità.  
  
 AS *SQL_Server_login*  
 Specifica l'account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dal quale l'entità che esegue la query ottiene il diritto di negare l'autorizzazione.  
  
## <a name="remarks"></a>Osservazioni  
 È possibile negare autorizzazioni nell'ambito del server solo se il database corrente è il database master.  
  
 Informazioni sulle autorizzazioni del server sono disponibile nel [server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) vista del catalogo. Informazioni sulle entità server sono disponibile nel [Sys. server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) vista del catalogo.  
  
 L'istruzione DENY ha esito negativo se non si specifica CASCADE la negazione di un'autorizzazione a un'entità che è stato concesso tale autorizzazione con GRANT OPTION.  
  
 I ruoli del server e gli account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono entità a protezione diretta a livello di server. Nella tabella seguente sono elencate le autorizzazioni più specifiche e limitate che è possibile negare per un ruolo del server o account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], insieme alle autorizzazioni più generali che le includono in modo implicito.  
  
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
  
### <a name="a-denying-impersonate-permission-on-a-login"></a>A. Negazione dell'autorizzazione IMPERSONATE per un account di accesso  
 Nell'esempio seguente viene negata il `IMPERSONATE` l'autorizzazione per la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] accesso `WanidaBenshoof` per un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] account di accesso creato dall'utente di Windows `AdvWorks\YoonM`.  
  
```  
USE master;  
DENY IMPERSONATE ON LOGIN::WanidaBenshoof TO [AdvWorks\YoonM];  
GO  
```  
  
### <a name="b-denying-view-definition-permission-with-cascade"></a>B. Negazione dell'autorizzazione VIEW DEFINITION con CASCADE  
 Nell'esempio seguente viene negata l'autorizzazione `VIEW DEFINITION` per l'account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `EricKurjan` all'account accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `RMeyyappan`. L'opzione `CASCADE` indica che l'autorizzazione `VIEW DEFINITION` per `EricKurjan` verrà negata anche alle entità a cui `RMeyyappan` ha concesso tale autorizzazione.  
  
```  
USE master;  
DENY VIEW DEFINITION ON LOGIN::EricKurjan TO RMeyyappan   
    CASCADE;  
GO   
```  
  
### <a name="c-denying-view-definition-permission-on-a-server-role"></a>C. Negazione dell'autorizzazione VIEW DEFINITION per un ruolo del server  
 Nell'esempio seguente viene negata l'autorizzazione `VIEW DEFINITION` nel ruolo del server `Sales` per il ruolo del server `Auditors`.  
  
```  
USE master;  
DENY VIEW DEFINITION ON SERVER ROLE::Sales TO Auditors ;  
GO   
```  
  
## <a name="see-also"></a>Vedere anche  
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.server_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)   
 [Autorizzazioni per entità server GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-server-principal-permissions-transact-sql.md)   
 [Autorizzazioni per entità server REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-server-principal-permissions-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [Entità &#40;motore di database&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Autorizzazioni &#40;motore di database&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Funzioni di sicurezza &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)   
 [Stored procedure di sicurezza &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)  
  
  
