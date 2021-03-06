---
title: CREAZIONE dello SCHEMA (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 12/01/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE_SCHEMA_TSQL
- SCHEMA
- CREATE SCHEMA
- SCHEMA_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- owners [SQL Server], schemas
- table creation [SQL Server], CREATE SCHEMA statement
- permissions [SQL Server], schemas
- schemas [SQL Server], creating
- CREATE SCHEMA statement
ms.assetid: df74fc36-20da-4efa-b412-c4e191786695
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 3185725a8b5db647d047830f4b87248b839ad230
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="create-schema-transact-sql"></a>CREATE SCHEMA (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Crea uno schema nel database corrente. La transazione CREATE SCHEMA può anche creare tabelle e viste all'interno del nuovo schema e impostare le autorizzazioni GRANT, DENY o REVOKE per tali oggetti.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
CREATE SCHEMA schema_name_clause [ <schema_element> [ ...n ] ]  
  
<schema_name_clause> ::=  
    {  
    schema_name  
    | AUTHORIZATION owner_name  
    | schema_name AUTHORIZATION owner_name  
    }  
  
<schema_element> ::=   
    {   
        table_definition | view_definition | grant_statement |   
        revoke_statement | deny_statement   
    }  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
CREATE SCHEMA schema_name [ AUTHORIZATION owner_name ] [;]  
```  
  
## <a name="arguments"></a>Argomenti  
 *schema_name*  
 Nome con il quale viene identificato lo schema all'interno del database.  
  
 AUTORIZZAZIONE *owner_name*  
 Specifica il nome dell'entità a livello di database che sarà proprietaria dello schema. L'entità può essere proprietaria di altri schemi e non può utilizzare lo schema corrente come schema predefinito.  
  
 *Table_Definition*  
 Specifica un'istruzione CREATE TABLE che crea una tabella all'interno dello schema. L'entità che esegue l'istruzione deve disporre dell'autorizzazione CREATE TABLE per il database corrente.  
  
 *VIEW_DEFINITION*  
 Specifica un'istruzione CREATE VIEW che crea una vista all'interno dello schema. L'entità che esegue l'istruzione deve disporre dell'autorizzazione CREATE VIEW per il database corrente.  
  
 *istruzione_GRANT*  
 Specifica un'istruzione GRANT che concede le autorizzazioni per ogni entità a protezione diretta ad eccezione del nuovo schema.  
  
 *revoke_statement*  
 Specifica un'istruzione REVOKE che revoca le autorizzazioni per ogni entità a protezione diretta ad eccezione del nuovo schema.  
  
 *deny_statement*  
 Specifica un'istruzione DENY che nega le autorizzazioni per ogni entità a protezione diretta ad eccezione del nuovo schema.  
  
## <a name="remarks"></a>Osservazioni  
  
> [!NOTE]  
>  Le istruzioni che contengono CREATE SCHEMA AUTHORIZATION ma non specificano un nome sono supportate unicamente per compatibilità con le versioni precedenti. L'istruzione non causa un errore ma non crea uno schema.  
  
 CREATE SCHEMA consente di creare uno schema, le tabelle e le viste in esso contenute e concedere, revocare o negare le autorizzazioni per ogni entità a protezione diretta in una singola istruzione. Questa istruzione deve essere eseguita come batch separato. Gli oggetti creati tramite l'istruzione CREATE SCHEMA vengono creati all'interno dello schema di cui è in corso la creazione.  
  
 Le transazioni CREATE SCHEMA sono atomiche. In caso di errori durante l'esecuzione di un'istruzione CREATE SCHEMA, non verrà creata alcuna entità a protezione diretta e non verranno concesse autorizzazioni.  
  
 Le entità a protezione diretta da creare tramite CREATE SCHEMA possono essere elencate in qualsiasi ordine, ad eccezione delle viste che fanno riferimento ad altre viste. In questo caso, la vista a cui viene fatto riferimento deve essere creata prima della vista che vi fa riferimento.  
  
 Un'istruzione GRANT può pertanto concedere l'autorizzazione per un oggetto prima che l'oggetto stesso venga creato, mentre un'istruzione CREATE VIEW può essere visualizzata prima delle istruzioni CREATE TABLE che creano le tabelle a cui fa riferimento la vista. Le istruzioni CREATE TABLE, inoltre, possono dichiarare chiavi esterne per le tabelle definite successivamente nell'istruzione CREATE SCHEMA.  
  
> [!NOTE]  
>  Le clausole DENY e REVOKE sono supportate nelle istruzioni CREATE SCHEMA. Le clausole DENY e REVOKE vengono eseguite nell'ordine in cui compaiono nell'istruzione CREATE SCHEMA.  
  
 L'entità che esegue CREATE SCHEMA può specificare un'altra entità di database come proprietario dello schema di cui è in corso la creazione. A tale scopo, sono richieste ulteriori autorizzazioni, come illustrato nella sezione "Autorizzazioni" più avanti in questo argomento.  
  
 Il nuovo schema è di proprietà di una delle seguenti entità a livello di database: utente di database, ruolo di database o ruolo applicazione. Gli oggetti creati all'interno di uno schema appartengono al proprietario dello schema e hanno un valore NULL per **principal_id** in **sys.objects**. La proprietà degli oggetti contenuti in uno schema può essere trasferita a qualsiasi entità a livello di database, ma il proprietario dello schema mantiene sempre l'autorizzazione CONTROL per gli oggetti all'interno dello schema.  
  
> [!CAUTION]  
>  [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]  
  
 **Schema implicito e creazione di utenti**  
  
 In alcuni casi un utente può usare un database senza disporre di un account utente di database, ovvero un'entità database nel database. Usare i vincoli nelle situazioni seguenti:  
  
-   È un account di accesso **CONTROL SERVER** privilegi.  
  
-   Un utente di Windows non dispone di un account utente di database individuale (un'entità database nel database), ma accede a un database come membro di un gruppo di Windows che dispone di un account utente di database (un'entità database per il gruppo di Windows).  
  
 Quando un utente privo di account utente di database crea un oggetto senza specificare uno schema esistente, nel database saranno creati automaticamente un'entità database e uno schema predefinito per tale utente. L'entità database e lo schema creati avranno lo stesso nome usato dall'utente per la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (il nome di accesso per l'autenticazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o il nome utente di Windows).  
  
 Questo comportamento è necessario per permettere agli utenti che usano gruppi di Windows di creare e possedere oggetti. Può tuttavia comportare la creazione accidentale di schemi e utenti. Per evitare di creare implicitamente utenti e schema, creare sempre, quando possibile, in modo esplicito le entità database e assegnare uno schema predefinito. In alternativa, dichiarare in modo esplicito uno schema esistente quando si creano oggetti in un database, usando nomi oggetto costituiti da due o tre parti.  

>  [!NOTE]
>  La creazione implicita di un utente di Azure Active Directory non è possibile utilizzare in [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]. Poiché la creazione di un utente AD Azure da provider esterni deve controllare lo stato di utenti in Azure ad, l'utente non sarà possibile creare con errore 2760: **il nome dello schema specificato "\<user_name@domain>" non esiste o non si dispone autorizzazioni necessarie per utilizzarlo.** E quindi l'errore 2759: **CREATE SCHEMA non riuscita a causa di errori precedenti.** Per risolvere questi errori, creare l'utente di Azure AD da provider esterni prima e quindi eseguire nuovamente l'istruzione di creazione dell'oggetto.
 
  
## <a name="deprecation-notice"></a>Informativa sulle funzionalità deprecate  
 Le istruzioni CREATE SCHEMA che non specificano un nome di schema sono attualmente supportate per compatibilità con le versioni precedenti. Tali istruzioni in realtà non creano uno schema all'interno del database, ma creano tabelle e viste e concedono autorizzazioni. Le entità non necessitano dell'autorizzazione CREATE SCHEMA per eseguire questa versione meno recente di CREATE SCHEMA, perché non viene creato alcuno schema. Questa funzionalità verrà rimossa a partire da una delle prossime versioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione CREATE SCHEMA per il database.  
  
 Per creare un oggetto specificato all'interno dell'istruzione CREATE SCHEMA, l'utente deve disporre dell'autorizzazione CREATE corrispondente.  
  
 Per specificare un altro utente come proprietario dello schema che viene creato, l'utente deve disporre dell'autorizzazione IMPERSONATE per quell'utente. Se si specifica un ruolo di database come proprietario, il chiamante deve disporre dell'appartenenza al ruolo oppure dell'autorizzazione ALTER per il ruolo.  
  
> [!NOTE]  
>  Per motivi di compatibilità con la sintassi precedente, non vengono controllate le autorizzazioni per CREATE SCHEMA perché non viene creato alcuno schema.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-creating-a-schema-and-granting-permissions"></a>A. Creazione di uno schema e la concessione di autorizzazioni  
 Nell'esempio seguente viene creato lo schema `Sprockets`, di proprietà di `Annik`, contenente la tabella `NineProngs`. L'istruzione concede `SELECT` a `Mandar` e nega `SELECT` a `Prasanna`. Si noti che `Sprockets` e `NineProngs` vengono creati in una singola istruzione.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE SCHEMA Sprockets AUTHORIZATION Annik  
    CREATE TABLE NineProngs (source int, cost int, partnumber int)  
    GRANT SELECT ON SCHEMA::Sprockets TO Mandar  
    DENY SELECT ON SCHEMA::Sprockets TO Prasanna;  
GO   
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Esempi: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-creating-a-schema-and-a-table-in-the-schema"></a>B. Creazione di uno schema e una tabella nello schema  
 L'esempio seguente crea schema `Sales` e quindi crea una tabella `Sales.Region` in tale schema.  
  
```  
CREATE SCHEMA Sales;  
GO;  
  
CREATE TABLE Sales.Region   
(Region_id int NOT NULL,  
Region_Name char(5) NOT NULL)  
WITH (DISTRIBUTION = REPLICATE);  
GO  
```  
  
### <a name="c-setting-the-owner-of-a-schema"></a>C. Impostando il proprietario di uno schema  
 Nell'esempio seguente viene creato uno schema `Production` proprietà `Mary`.  
  
```  
CREATE SCHEMA Production AUTHORIZATION [Contoso\Mary];  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [L'autorizzazione ALTER SCHEMA &#40; Transact-SQL &#41;](../../t-sql/statements/alter-schema-transact-sql.md)   
 [DROP SCHEMA &#40; Transact-SQL &#41;](../../t-sql/statements/drop-schema-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [Schemas &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/schemas-catalog-views-sys-schemas.md)   
 [Creazione di uno schema di database](../../relational-databases/security/authentication-access/create-a-database-schema.md)  
  
  


