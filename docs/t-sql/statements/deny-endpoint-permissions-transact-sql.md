---
title: DENY-autorizzazioni per Endpoint (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 05/15/2017
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
- endpoints [SQL Server], permissions
- DENY statement, endpoints
- denying permissions [SQL Server], endpoints
- permissions [SQL Server], endpoints
ms.assetid: 3ac40457-7529-4eda-95a4-5247345cc8cf
caps.latest.revision: 28
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a263d6a5a576b4f4e06bb44a6c6fb40c99e64660
ms.contentlocale: it-it
ms.lasthandoff: 09/01/2017

---
# <a name="deny-endpoint-permissions-transact-sql"></a>DENY - autorizzazioni per endpoint (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Nega le autorizzazioni per un endpoint.  

  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
DENY permission  [ ,...n ] ON ENDPOINT :: endpoint_name  
    TO < server_principal >  [ ,...n ]  
    [ CASCADE ]  
    [ AS SQL_Server_login ]   
  
<server_principal> ::=   
        SQL_Server_login  
    | SQL_Server_login_from_Windows_login   
    | SQL_Server_login_from_certificate   
    | SQL_Server_login_from_AsymKey  
```  
  
## <a name="arguments"></a>Argomenti  
 *autorizzazione*  
 Specifica un'autorizzazione che può essere negata per un endpoint. Per un elenco delle autorizzazioni, vedere la sezione Osservazioni di seguito in questo argomento.  
  
 ENDPOINT **::***endpoint_name*  
 Specifica l'endpoint per cui viene negata l'autorizzazione. Il qualificatore di ambito (**::**) è obbligatorio.  
  
 PER \<server_principal >  
 Specifica l'account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a cui viene negata l'autorizzazione.  
  
 *SQL_Server_login*  
 Specifica il nome di un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 *SQL_Server_login_from_Windows_login*  
 Specifica il nome di un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] creato da un account di accesso di Windows.  
  
 *SQL_Server_login_from_certificate*  
 Specifica il nome di un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sul quale viene eseguito il mapping a un certificato.  
  
 *SQL_Server_login_from_AsymKey*  
 Specifica il nome di un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sul quale viene eseguito il mapping a una chiave asimmetrica.  
  
 CASCADE  
 Indica che l'autorizzazione negata viene negata anche ad altre entità alle quali è stata concessa da questa entità.  
  
 AS *SQL_Server_login*  
 Specifica l'account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dal quale l'entità che esegue la query ottiene il diritto di negare l'autorizzazione.  
  
## <a name="remarks"></a>Osservazioni  
 Possibile negare autorizzazioni nell'ambito del server solo quando il database corrente è **master**.  
  
 Informazioni sugli endpoint sono visibili nella [Endpoints](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md) vista del catalogo. Informazioni sulle autorizzazioni del server sono visibili nella [server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) è visibile nella vista del catalogo e le informazioni sulle entità server il [Sys. server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) vista del catalogo.  
  
 Un endpoint è un'entità a protezione diretta a livello del server. Nella tabella seguente sono elencate le autorizzazioni più specifiche e limitate che è possibile negare per un endpoint, insieme alle autorizzazioni più generali che le includono in modo implicito.  
  
|Autorizzazione dell'endpoint|Autorizzazione dell'endpoint in cui è inclusa|Autorizzazione del server in cui è inclusa|  
|-------------------------|------------------------------------|----------------------------------|  
|ALTER|CONTROL|ALTER ANY ENDPOINT|  
|CONNECT|CONTROL|CONTROL SERVER|  
|CONTROL|CONTROL|CONTROL SERVER|  
|TAKE OWNERSHIP|CONTROL|CONTROL SERVER|  
|VIEW DEFINITION|CONTROL|VIEW ANY DEFINITION|  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione CONTROL per l'endpoint o l'autorizzazione ALTER ANY ENDPOINT per il server.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-denying-view-definition-permission-on-an-endpoint"></a>A. Negazione dell'autorizzazione VIEW DEFINITION per un endpoint  
 Nell'esempio seguente viene negata il `VIEW DEFINITION` autorizzazione per l'endpoint `Mirror7` per il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] accesso `ZArifin`.  
  
```  
USE master;  
DENY VIEW DEFINITION ON ENDPOINT::Mirror7 TO ZArifin;  
GO  
```  
  
### <a name="b-denying-take-ownership-permission-with-cascade-option"></a>B. Negazione dell'autorizzazione TAKE OWNERSHIP con l'opzione CASCADE  
 Nell'esempio seguente viene negata l'autorizzazione `TAKE OWNERSHIP` per l'endpoint `Shipping83` all'utente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `PKomosinski` e alle entità a cui l'utente `PKomosinski` ha concesso l'autorizzazione `TAKE OWNERSHIP`.  
  
```  
USE master;  
DENY TAKE OWNERSHIP ON ENDPOINT::Shipping83 TO PKomosinski   
    CASCADE;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [GRANT Endpoint Permissions &#40;Transact-SQL&#41;](../../t-sql/statements/grant-endpoint-permissions-transact-sql.md)   
 [REVOKE-autorizzazioni per Endpoint &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-endpoint-permissions-transact-sql.md)   
 [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)   
 [Viste del catalogo degli endpoint &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)   
 [Sys. Endpoints &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md)   
 [Autorizzazioni &#40;motore di database&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Entità &#40;motore di database&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
