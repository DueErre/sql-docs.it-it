---
title: REVOKE-autorizzazioni per Assembly (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 07/26/2017
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
- REVOKE statement, assemblies
- assemblies [CLR integration], permissions
ms.assetid: f88e9da1-2c0b-4bdd-9ec5-44467707cb46
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fd735936ae0e1ffc03b98e93ff1edf0dd5bf2e08
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="revoke-assembly-permissions-transact-sql"></a>REVOKE - autorizzazioni per assembly (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Revoca le autorizzazioni per un assembly.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
REVOKE [ GRANT OPTION FOR ] permission [ ,...n ]   
    ON ASSEMBLY :: assembly_name   
    { TO | FROM } database_principal [ ,...n ]  
    [ CASCADE ]  
    [ AS revoking_principal ]  
```  
  
## <a name="arguments"></a>Argomenti  
 GRANT OPTION FOR  
 Indica che verrà revocata la capacità di concedere o negare l'autorizzazione specificata. L'autorizzazione stessa non verrà revocata.  
  
> [!IMPORTANT]  
>  Se l'autorizzazione specificata è stata concessa all'entità senza l'opzione GRANT, l'autorizzazione stessa verrà revocata.  
  
 *autorizzazione*  
 Specifica un'autorizzazione che può essere revocata in un assembly. Vedere l'elenco riportato di seguito.  
  
 ASSEMBLY **::***nome_assembly*  
 Specifica l'assembly per cui vengono revocate le autorizzazioni. Il qualificatore di ambito **::** è obbligatorio.  
  
 *database_principal*  
 Specifica l'entità da cui viene revocata l'autorizzazione. I tipi validi sono:  
  
-   utente del database  
  
-   ruolo del database  
  
-   ruolo dell'applicazione  
  
-   utente del database sul quale viene eseguito il mapping a un account di accesso di Windows  
  
-   utente del database sul quale viene eseguito il mapping a un gruppo di Windows  
  
-   utente del database sul quale viene eseguito il mapping a un certificato  
  
-   utente del database mappato a una chiave asimmetrica  
  
-   utente del database non mappato ad alcuna entità server.  
  
 CASCADE  
 Indica che l'autorizzazione che viene revocata anche ad altre entità a cui è stata concessa o negata da questa entità.  
  
> [!CAUTION]  
>  La revoca propagata di un'autorizzazione concessa con WITH GRANT OPTION comporterà la revoca sia delle autorizzazioni GRANT che delle autorizzazioni DENY per tale autorizzazione.  
  
 AS *revoking_principal*  
 Specifica un'entità dalla quale l'entità che esegue la query ottiene il diritto di revocare l'autorizzazione. I tipi validi sono:  
  
-   utente del database  
  
-   ruolo del database  
  
-   ruolo dell'applicazione  
  
-   utente del database sul quale viene eseguito il mapping a un account di accesso di Windows  
  
-   utente del database sul quale viene eseguito il mapping a un gruppo di Windows  
  
-   utente del database sul quale viene eseguito il mapping a un certificato  
  
-   utente del database mappato a una chiave asimmetrica  
  
-   utente del database non mappato ad alcuna entità server.  
  
## <a name="remarks"></a>Osservazioni  
 Un assembly è un'entità a protezione diretta a livello di database contenuta nel database padre nella gerarchia delle autorizzazioni. Di seguito sono elencate le autorizzazioni più specifiche e limitate che è possibile revocare per un assembly, insieme alle autorizzazioni più generali che le includono in modo implicito.  
  
|Autorizzazione dell'assembly|Autorizzazione dell'assembly in cui è inclusa|Autorizzazione del database in cui è inclusa|  
|-------------------------|------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY ASSEMBLY|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione CONTROL per l'assembly.  
  
## <a name="see-also"></a>Vedere anche  
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [Autorizzazioni &#40;motore di database&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Entità &#40;motore di database&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [CREAZIONE di ASSEMBLY &#40; Transact-SQL &#41;](../../t-sql/statements/create-assembly-transact-sql.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [CREATE APPLICATION ROLE &#40; Transact-SQL &#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [Gerarchia di crittografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
