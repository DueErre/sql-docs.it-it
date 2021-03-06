---
title: sp_table_privileges (Transact-SQL) | Documenti Microsoft
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
- sp_table_privileges
- sp_table_privileges_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_table_privileges
ms.assetid: 0512e688-4fc0-4557-8dc8-016672c1e3fe
caps.latest.revision: "36"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 3f71b84e9f2aa0f732178a302f3d131f0a448dc0
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2017
---
# <a name="sptableprivileges-transact-sql"></a>sp_table_privileges (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce un elenco delle autorizzazioni di tabella, ad esempio INSERT, DELETE, UPDATE, SELECT o REFERENCES, per la tabella o le tabelle specificate.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_table_privileges [ @table_name = ] 'table_name'     
     [ , [ @table_owner = ] 'table_owner' ]   
     [ , [ @table_qualifier = ] 'table_qualifier' ]   
     [ , [ @fUsePattern = ] 'fUsePattern' ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [ @table_name=] '*table_name*'  
 Tabella utilizzata per restituire informazioni del catalogo. *TABLE_NAME* è **nvarchar (**384**)**, non prevede alcun valore predefinito. La ricerca con caratteri jolly è supportata.  
  
 [ @table_owner=] '*table_owner*'  
 Proprietario della tabella utilizzata per restituire informazioni sul catalogo. *TABLE_OWNER*è **nvarchar (**384**)**, con un valore predefinito è NULL. La ricerca con caratteri jolly è supportata. Se owner viene omesso, vengono applicate le regole di visibilità della tabella predefinite nel sistema DBMS sottostante.  
  
 Se l'utente corrente è il proprietario di una tabella con il nome specificato, vengono restituite le colonne di tale tabella. Se *proprietario* viene omesso e l'utente corrente non dispone di una tabella con l'oggetto specificato *nome*, viene eseguita la ricerca per una tabella con l'oggetto specificato *table_name* di proprietà di proprietario del database. Se viene individuata, vengono restituite le colonne di tale tabella.  
  
 [ @table_qualifier=] '*table_qualifier*'  
 Nome del qualificatore di tabella. *TABLE_QUALIFIER* è **sysname**, con un valore predefinito è NULL. Vari prodotti DBMS supportano nomi in tre parti per le tabelle (*composti*). In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] questa colonna rappresenta il nome del database. In altri prodotti rappresenta il nome del server dell'ambiente di database della tabella.  
  
 [ @fUsePattern=] '*fUsePattern*'  
 Determina se il carattere di sottolineatura (_), simbolo di percentuale (%) e tra parentesi quadre ([o]) caratteri vengono interpretate come caratteri jolly. I valori validi sono 0 (utilizzo dei criteri di ricerca disattivato) e 1 (utilizzo dei criteri di ricerca attivato). *fUsePattern* è **bit**, con un valore predefinito è 1.  
  
## <a name="return-code-values"></a>Valori restituiti  
 Nessuno  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|TABLE_QUALIFIER|**sysname**|Nome del qualificatore della tabella. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] questa colonna rappresenta il nome del database. Questo campo può essere NULL.|  
|TABLE_OWNER|**sysname**|Nome del proprietario della tabella. Questo campo restituisce sempre un valore.|  
|TABLE_NAME|**sysname**|Nome della tabella. Questo campo restituisce sempre un valore.|  
|GRANTOR|**sysname**|Nome dell'utente del database che ha concesso autorizzazioni all'utente specificato in GRANTEE per la tabella specificata in TABLE_NAME. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] questa colonna corrisponde sempre a TABLE_OWNER. Questo campo restituisce sempre un valore. Inoltre, il valore della colonna GRANTOR può essere il proprietario del database (TABLE_OWNER) o un utente a cui il proprietario del database ha concesso autorizzazioni tramite la clausola WITH GRANT OPTION dell'istruzione GRANT.|  
|GRANTEE|**sysname**|Nome dell'utente di database a cui l'utente GRANTOR specificato ha concesso autorizzazioni per la tabella TABLE_NAME. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], questa colonna include sempre un utente del database dalla vista sys.database_principalssystem. Questo campo restituisce sempre un valore.|  
|PRIVILEGE|**sysname**|Una delle autorizzazioni di tabella disponibili. I possibili valori delle autorizzazioni possono essere quelli seguenti o altri valori supportati dall'origine dati al momento della definizione dell'implementazione:<br /><br /> SELECT = l'utente GRANTEE può recuperare i dati di una o più colonne.<br /><br /> INSERT = L'utente GRANTEE può inserire dati in nuove righe di una o più colonne.<br /><br /> UPDATE = L'utente GRANTEE può modificare i dati esistenti di una o più colonne.<br /><br /> DELETE = L'utente GRANTEE può rimuovere righe dalla tabella.<br /><br /> REFERENCES = l'utente GRANTEE può fare riferimento a una colonna di una tabella esterna in una relazione chiave primaria/chiave esterna. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] questo tipo di relazione viene definito tramite vincoli di tabella.<br /><br /> L'ambito di azione ottenuto dall'utente GRANTEE tramite un privilegio di tabella specifico dipende dall'origine dati. Il privilegio UPDATE, ad esempio, può permettere all'utente GRANTEE di aggiornare tutte le colonne di una tabella in una certa origine dei dati e solo le colonne per le quali l'utente GRANTOR dispone del privilegio UPDATE in un'origine dei dati diversa.|  
|IS_GRANTABLE|**sysname**|Indica se all'utente GRANTEE è consentito o meno concedere autorizzazioni ad altri utenti (autorizzazione per la concessione di autorizzazioni). I possibili valori sono YES, NO e NULL. Un valore sconosciuto, o NULL, fa riferimento a un'origine dati per le quali l'autorizzazione per la concessione di autorizzazioni non è applicabile.|  
  
## <a name="remarks"></a>Osservazioni  
 La stored procedure sp_table_privileges corrisponde a sp_table_privileges in ODBC. I risultati restituiti vengono ordinati in base alle colonne TABLE_QUALIFIER, TABLE_OWNER, TABLE_NAME e PRIVILEGE.  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione SELECT per lo schema.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono restituite informazioni sui privilegi per tutte le tabelle con nome che inizia con la parola `Contact`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_table_privileges   
   @table_name = 'Contact%';  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Catalogo Stored procedure &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
