---
title: sp_pkeys (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_pkeys
- sp_pkeys_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_pkeys
ms.assetid: e614c75d-847b-4726-8f6f-cd18de688eda
caps.latest.revision: "27"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bbf8a10a560bcf058f30281ceebe34a47689e3b1
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="sppkeys-transact-sql"></a>sp_pkeys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Restituisce informazioni sulle chiavi primarie di una tabella dell'ambiente corrente.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
sp_pkeys [ @table_name = ] 'name'       
    [ , [ @table_owner = ] 'owner' ]   
    [ , [ @table_qualifier = ] 'qualifier' ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [ @table_name=] '*nome*'  
 È la tabella per cui restituire informazioni. *nome* è **sysname**, non prevede alcun valore predefinito. I criteri di ricerca con caratteri jolly non sono supportati.  
  
 [ @table_owner=] '*proprietario*'  
 Viene indicato il proprietario della tabella specificata. *proprietario* è **sysname**, con un valore predefinito è NULL. I criteri di ricerca con caratteri jolly non sono supportati. Se *proprietario* viene omesso, si applicano le regole di visibilità della tabella predefinite del sistema DBMS sottostante.  
  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se l'utente corrente è il proprietario di una tabella con il nome specificato, vengono restituite le colonne di tale tabella. Se il *proprietario* non è specificato e l'utente corrente non dispone di una tabella con l'oggetto specificato *nome*, viene eseguita la ricerca per una tabella con l'oggetto specificato *nome* di proprietà di proprietario del database. Se viene individuata, vengono restituite le colonne di tale tabella.  
  
 [ @table_qualifier=] '*qualificatore*'  
 Qualificatore di tabella. *qualificatore* è **sysname**, con un valore predefinito è NULL. Vari prodotti DBMS supportano nomi in tre parti per le tabelle (*qualificatore***.** *proprietario***.** *nome*). In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] questa colonna rappresenta il nome del database. In alcuni prodotti rappresenta il nome del server dell'ambiente di database della tabella.  
  
## <a name="return-code-values"></a>Valori restituiti  
 Nessuno  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|TABLE_QUALIFIER|**sysname**|Nome del qualificatore della tabella. Questo campo può essere NULL.|  
|TABLE_OWNER|**sysname**|Nome del proprietario della tabella. Questo campo restituisce sempre un valore.|  
|TABLE_NAME|**sysname**|Nome della tabella. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] questa colonna rappresenta il nome della tabella specificato in sysobjects. Questo campo restituisce sempre un valore.|  
|COLUMN_NAME|**sysname**|Nome di ogni colonna restituita per la tabella specificata in TABLE_NAME. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] questa colonna rappresenta il nome della colonna specificato in sys.columns. Questo campo restituisce sempre un valore.|  
|KEY_SEQ|**smallint**|Numero sequenziale della colonna in una chiave primaria a più colonne.|  
|PK_NAME|**sysname**|Identificatore della chiave primaria. Se non è applicabile all'origine dei dati, restituisce NULL.|  
  
## <a name="remarks"></a>Osservazioni  
 La stored procedure sp_pkeys restituisce informazioni sulle colonne definite in modo esplicito con un vincolo PRIMARY KEY. Dato che le chiavi primarie denominate in modo esplicito non sono supportate in tutti i sistemi, lo strumento di implementazione che regola gli scambi tra i sistemi determina l'elemento che corrisponde a una chiave primaria. Il termine "chiave primaria" fa riferimento a una chiave primaria logica di una tabella. Si presume che su tutte le chiavi considerate chiavi primarie logiche sia definito un indice univoco. Tale indice viene inoltre restituito in sp_statistics.  
  
 La stored procedure sp_pkeys è equivalente alla SQLPrimaryKeys in ODBC. I risultati restituiti sono ordinati per TABLE_QUALIFIER, TABLE_OWNER, TABLE_NAME e KEY_SEQ.  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione SELECT per lo schema.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene recuperata la chiave primaria della tabella `HumanResources.Department` nel database `AdventureWorks2012`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_pkeys @table_name = N'Department'  
    ,@table_owner = N'HumanResources';  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Esempi: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 Nell'esempio seguente viene recuperata la chiave primaria della tabella `DimAccount` nel database `AdventureWorksPDW2012`. Restituisce zero righe, che indica che la tabella non contiene una chiave primaria.  
  
```  
-- Uses AdventureWorks  
  
EXEC sp_pkeys @table_name = N'DimAccount;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Catalogo Stored procedure &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

