---
title: REVOCARE autorizzazioni per chiavi asimmetriche (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 06/10/2016
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
- permissions [SQL Server], asymmetric keys
- asymmetric keys [SQL Server], permissions
- REVOKE statement, asymmetric keys
ms.assetid: 1a1063e8-ffc7-4775-a40d-e155740ad7b2
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d4f9f08fda905261e188bb90f8d85fd0a48b2f2c
ms.contentlocale: it-it
ms.lasthandoff: 09/01/2017

---
# <a name="revoke-asymmetric-key-permissions-transact-sql"></a>REVOKE (autorizzazioni per chiavi asimmetriche) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Revoca le autorizzazioni per una chiave asimmetrica.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
REVOKE [ GRANT OPTION FOR ] { permission  [ ,...n ] }   
    ON ASYMMETRIC KEY :: asymmetric_key_name   
    { TO | FROM } database_principal [ ,...n ]  
    [ CASCADE ]  
    [ AS revoking_principal ]  
```  
  
## <a name="arguments"></a>Argomenti  
 GRANT OPTION FOR  
 Indica che verrà revocata la capacità di concedere l'autorizzazione specificata.  
  
> [!IMPORTANT]  
>  Se l'autorizzazione specificata è stata concessa all'entità senza l'opzione GRANT, l'autorizzazione stessa verrà revocata.  
  
 *autorizzazione*  
 Specifica un'autorizzazione che può essere revocata in un assembly. Vedere l'elenco riportato di seguito.  
  
 CHIAVE asimmetrica **::***asymmetric_key_name*  
 Specifica la chiave asimmetrica per cui viene revocata l'autorizzazione. Il qualificatore di ambito **::** è obbligatorio.  
  
 *database_principal*  
 Specifica l'entità da cui viene revocata l'autorizzazione. I tipi validi sono:  
  
-   Utente del database  
  
-   Ruolo del database  
  
-   Ruolo applicazione  
  
-   Utente del database di cui è stato eseguito il mapping a un account di accesso di Windows  
  
-   Utente del database di cui è stato eseguito il mapping a un gruppo di Windows  
  
-   Utente del database di cui è stato eseguito il mapping a un certificato  
  
-   Utente del database di cui è stato eseguito il mapping a una chiave asimmetrica  
  
-   Utente del database sul quale non viene eseguito il mapping ad alcuna entità server.  
  
 CASCADE  
 Indica che l'autorizzazione che viene revocata anche ad altre entità a cui è stata concessa o negata da questa entità. L'autorizzazione stessa non verrà revocata.  
  
> [!CAUTION]  
>  La revoca propagata di un'autorizzazione concessa con WITH GRANT OPTION comporterà la revoca sia delle autorizzazioni GRANT che delle autorizzazioni DENY per tale autorizzazione.  
  
 AS *revoking_principal*  
 Specifica un'entità dalla quale l'entità che esegue la query ottiene il diritto di revocare l'autorizzazione. I tipi validi sono:  
  
-   Utente del database  
  
-   Ruolo del database  
  
-   Ruolo applicazione  
  
-   Utente del database di cui è stato eseguito il mapping a un account di accesso di Windows  
  
-   Utente del database di cui è stato eseguito il mapping a un gruppo di Windows  
  
-   Utente del database di cui è stato eseguito il mapping a un certificato  
  
-   Utente del database di cui è stato eseguito il mapping a una chiave asimmetrica  
  
-   Utente del database sul quale non viene eseguito il mapping ad alcuna entità server.  
  
## <a name="remarks"></a>Osservazioni  
 Una chiave asimmetrica è un'entità a protezione diretta a livello di database contenuta nel database padre nella gerarchia delle autorizzazioni. Di seguito sono indicate le autorizzazioni più specifiche e limitate che è possibile revocare per una chiave asimmetrica, insieme alle autorizzazioni più generali che le includono in modo implicito.  
  
|Autorizzazione della chiave asimmetrica|Autorizzazione della chiave asimmetrica in cui è inclusa.|Autorizzazione del database in cui è inclusa|  
|-------------------------------|------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY ASYMMETRIC KEY|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione CONTROL per la chiave asimmetrica.  
  
## <a name="see-also"></a>Vedere anche  
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [Autorizzazioni &#40;motore di database&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Entità &#40;motore di database&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [CREATE APPLICATION ROLE &#40; Transact-SQL &#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [Gerarchia di crittografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
