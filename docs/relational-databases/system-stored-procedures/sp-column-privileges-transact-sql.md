---
title: sp_column_privileges (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_column_privileges_TSQL
- sp_column_privileges
dev_langs: TSQL
helpviewer_keywords: sp_column_privileges
ms.assetid: a3784301-2517-4b1d-bbd9-47404483fad0
caps.latest.revision: "36"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f930dc96633f526259dccf89f7fb592a4f9caf10
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2017
---
# <a name="spcolumnprivileges-transact-sql"></a>sp_column_privileges (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Restituisce informazioni sui privilegi delle colonne di una tabella dell'ambiente corrente.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_column_privileges [ @table_name = ] 'table_name'   
     [ , [ @table_owner = ] 'table_owner' ]   
     [ , [ @table_qualifier = ] 'table_qualifier' ]   
     [ , [ @column_name = ] 'column' ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [ @table_name=] '*table_name*'  
 Tabella utilizzata per restituire informazioni del catalogo. *TABLE_NAME* è **sysname**, non prevede alcun valore predefinito. I criteri di ricerca con caratteri jolly non sono supportati.  
  
 [ @table_owner=] '*table_owner*'  
 Proprietario della tabella utilizzata per restituire informazioni sul catalogo. *TABLE_OWNER* è **sysname**, con un valore predefinito è NULL. I criteri di ricerca con caratteri jolly non sono supportati. Se *table_owner* viene omesso, si applicano le regole di visibilità della tabella predefinite del sistema di gestione di database (DBMS) sottostante.  
  
 Se l'utente corrente è il proprietario di una tabella avente il nome specificato, vengono restituite le colonne di tale tabella. Se *table_owner* viene omesso e l'utente corrente non dispone di una tabella con l'oggetto specificato *table_name*, sp_column privilegi Cerca una tabella con l'oggetto specificato *table_name* il proprietario del database. Se viene individuata, vengono restituite le colonne di tale tabella.  
  
 [ @table_qualifier=] '*table_qualifier*'  
 Nome del qualificatore di tabella. *TABLE_QUALIFIER* è *sysname*, con un valore predefinito è NULL. Vari prodotti DBMS supportano nomi in tre parti per le tabelle (*qualificatore***.** *proprietario***.** *nome*). In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] questa colonna rappresenta il nome del database. In altri prodotti rappresenta il nome del server dell'ambiente di database della tabella.  
  
 [ @column_name=] '*colonna*'  
 Colonna utilizzata quando si desidera ottenere una sola colonna di informazioni del catalogo. *colonna* è **nvarchar (**384**)**, con un valore predefinito è NULL. Se *colonna* viene omesso, vengono restituite tutte le colonne. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], *colonna* rappresenta il nome di colonna elencato nella tabella sys. Columns. *colonna* possono includere caratteri jolly criteri di corrispondenza del sistema DBMS sottostante. Per ottenere la massima interoperabilità, è consigliabile che nel client del gateway vengano utilizzati solo i caratteri jolly dello standard ISO, ovvero i caratteri % e _.  
  
## <a name="result-sets"></a>Set di risultati  
 sp_datatype_privileges corrisponde a SQLColumnPrivileges in ODBC. I risultati restituiti sono ordinati per TABLE_QUALIFIER, TABLE_OWNER, TABLE_NAME, COLUMN_NAME e PRIVILEGE.  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|TABLE_QUALIFIER|**sysname**|Nome del qualificatore della tabella. Questo campo può essere NULL.|  
|TABLE_OWNER|**sysname**|Nome del proprietario della tabella. Questo campo restituisce sempre un valore.|  
|TABLE_NAME|**sysname**|Nome della tabella. Questo campo restituisce sempre un valore.|  
|COLUMN_NAME|**sysname**|Nome di ogni colonna della tabella TABLE_NAME restituita. Questo campo restituisce sempre un valore.|  
|GRANTOR|**sysname**|Nome dell'utente del database che ha concesso le autorizzazioni per la colonna COLUMN_NAME all'utente GRANTEE specificato. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] questa colonna corrisponde sempre a TABLE_OWNER. Questo campo restituisce sempre un valore.<br /><br /> La colonna GRANTOR può rappresentare il proprietario del database (TABLE_OWNER) o un utente a cui il proprietario del database ha concesso le autorizzazioni tramite la clausola WITH GRANT OPTION dell'istruzione GRANT.|  
|GRANTEE|**sysname**|Nome dell'utente del database a cui l'utente GRANTOR specificato ha concesso le autorizzazioni per la colonna COLUMN_NAME. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] questa colonna include sempre un utente di database della tabella sysusers. Questo campo restituisce sempre un valore.|  
|PRIVILEGE|**varchar (**32**)**|Una delle autorizzazioni di colonna disponibili. Le autorizzazioni di colonna possono essere rappresentate da uno dei valori riportati di seguito o da altri valori supportati dall'origine dei dati in fase di definizione dell'implementazione:<br /><br /> SELECT = l'utente GRANTEE può recuperare dati per le colonne.<br /><br /> INSERT = l'utente GRANTEE può fornire dati per la colonna specificata quando inserisce nuove righe nella tabella.<br /><br /> UPDATE = l'utente GRANTEE può modificare i dati della colonna.<br /><br /> REFERENCES = l'utente GRANTEE può fare riferimento a una colonna di una tabella esterna in una relazione chiave primaria/chiave esterna. Questo tipo di relazione viene definito tramite vincoli di tabella.|  
|IS_GRANTABLE|**varchar (**3**)**|Indica se l'utente GRANTEE può concedere autorizzazioni ad altri utenti (autorizzazione per la concessione di autorizzazioni). I possibili valori sono YES, NO e NULL. Un valore sconosciuto, o NULL, fa riferimento a un'origine dei dati per la quale questo tipo di assegnazione indiretta delle autorizzazioni non è consentito.|  
  
## <a name="remarks"></a>Osservazioni  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] le autorizzazioni vengono concesse tramite l'istruzione GRANT e rimosse tramite l'istruzione REVOKE.  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione SELECT per lo schema.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono restituite informazioni sui privilegi di una colonna specifica.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_column_privileges @table_name = 'Employee'   
    ,@table_owner = 'HumanResources'  
    ,@table_qualifier = 'AdventureWorks2012'  
    ,@column_name = 'SalariedFlag';  
```  
  
## <a name="see-also"></a>Vedere anche  
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
