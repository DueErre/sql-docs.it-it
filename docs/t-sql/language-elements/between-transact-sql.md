---
title: BETWEEN (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/28/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- BETWEEN
- BETWEEN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- inclusive ranges
- testing range
- exclusive ranges
- NOT BETWEEN operator
- BETWEEN operator
- range to test [SQL Server]
ms.assetid: a5d5b050-203e-4355-ac85-e08ef5ca7823
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: b2e5f028fdc431ebd52302cc0b62dcf456d1d79f
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2018
---
# <a name="between-transact-sql"></a>BETWEEN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Specifica un intervallo da testare.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
test_expression [ NOT ] BETWEEN begin_expression AND end_expression  
```  
  
## <a name="arguments"></a>Argomenti  
 *test_expression*  
 È il [espressione](../../t-sql/language-elements/expressions-transact-sql.md) da testare nell'intervallo definito da *begin_expression*e *end_expression*. *test_expression* deve essere dello stesso tipo di dati sia *begin_expression* e *end_expression*.  
  
 NOT  
 Specifica che il risultato del predicato viene negato.  
  
 *begin_expression*  
 Qualsiasi espressione valida. *begin_expression* deve essere dello stesso tipo di dati sia *test_expression* e *end_expression*.  
  
 *end_expression*  
 Qualsiasi espressione valida. *end_expression* deve essere dello stesso tipo di dati sia *test_expression*e *begin_expression*.  
  
 AND  
 Funge da segnaposto che indica *test_expression* deve essere compreso nell'intervallo indicato da *begin_expression* e *end_expression*.  
  
## <a name="result-types"></a>Tipi restituiti  
 **Boolean**  
  
## <a name="result-value"></a>Valore restituito  
 BETWEEN restituisce **TRUE** se il valore di *test_expression* è maggiore o uguale al valore di *begin_expression* e minore o uguale al valore di *end_expression*.  
  
 NOT BETWEEN restituisce **TRUE** se il valore di *test_expression* è minore del valore di *begin_expression* o maggiore del valore di *end_expression* .  
  
## <a name="remarks"></a>Osservazioni  
 Per specificare un intervallo esclusivo, utilizzare gli operatori maggiore di (>) e minore di (<). Se l'input per il predicato BETWEEN o NOT BETWEEN è NULL, il risultato è UNKNOWN.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-using-between"></a>A. Utilizzo di BETWEEN  
 L'esempio seguente restituisce informazioni sui ruoli del database in un database. La prima query restituisce tutti i ruoli. Il secondo esempio viene utilizzato il `BETWEEN` clausola per limitare i ruoli per l'oggetto specificato `database_id` valori.  
  
```sql  
SELECT principal_id, name 
FROM sys.database_principals
WHERE type = 'R';

SELECT principal_id, name 
FROM sys.database_principals
WHERE type = 'R'
AND principal_id BETWEEN 16385 AND 16390;
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]   
```  
principal_id    name
------------  ---- 
0               public
16384           db_owner
16385           db_accessadmin
16386           db_securityadmin
16387           db_ddladmin
16389           db_backupoperator
16390           db_datareader
16391           db_datawriter
16392           db_denydatareader
16393           db_denydatawriter
```  
```  
principal_id    name
------------  ---- 
16385           db_accessadmin
16386           db_securityadmin
16387           db_ddladmin
16389           db_backupoperator
16390           db_datareader
```  
  
### <a name="b-using--and--instead-of-between"></a>B. Utilizzo di > e < al posto di BETWEEN  
 Nell'esempio seguente vengono utilizzati gli operatori maggiore di (`>`) e minore di (`<`) e, poiché non sono operatori inclusivi, vengono restituite nove righe anziché le dieci restituite nell'esempio precedente.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT e.FirstName, e.LastName, ep.Rate  
FROM HumanResources.vEmployee e   
JOIN HumanResources.EmployeePayHistory ep   
    ON e.BusinessEntityID = ep.BusinessEntityID  
WHERE ep.Rate > 27 AND ep.Rate < 30  
ORDER BY ep.Rate;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 FirstName   LastName             Rate  
 ---------   -------------------  ---------  
 Paula       Barreto de Mattos    27.1394  
 Janaina     Bueno                27.4038  
 Dan         Bacon                27.4038  
 Ramesh      Meyyappan            27.4038  
 Karen       Berg                 27.4038  
 David       Bradley              28.7500  
 Hazem       Abolrous             28.8462  
 Ovidiu      Cracium              28.8462  
 Rob         Walters              29.8462  
 ```    
  
### <a name="c-using-not-between"></a>C. Utilizzo di NOT BETWEEN  
 Nell'esempio seguente vengono trovate tutte le righe che non rientrano nell'intervallo da `27` a `30`.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT e.FirstName, e.LastName, ep.Rate  
FROM HumanResources.vEmployee e   
JOIN HumanResources.EmployeePayHistory ep   
    ON e.BusinessEntityID = ep.BusinessEntityID  
WHERE ep.Rate NOT BETWEEN 27 AND 30  
ORDER BY ep.Rate;  
GO  
```  
  
### <a name="d-using-between-with-datetime-values"></a>D. Utilizzo di BETWEEN tra valori datetime  
 Nell'esempio seguente recupera le righe in cui **datetime** valori sono compresi tra `'20011212'` e `'20020105'`, inclusivo.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT BusinessEntityID, RateChangeDate  
FROM HumanResources.EmployeePayHistory  
WHERE RateChangeDate BETWEEN '20011212' AND '20020105';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 BusinessEntityID RateChangeDate  
 ----------- -----------------------  
 3           2001-12-12 00:00:00.000  
 4           2002-01-05 00:00:00.000  
 ```  
 
 La query recupera le righe previste poiché i valori di data nella query e **datetime** valori archiviati nel `RateChangeDate` colonna sono stati specificati senza la parte dell'ora della data. Quando la frazione di ora non è specificata, il valore predefinito viene impostato su 00.00. Si noti che una riga contenente una frazione dell'ora successiva all'ora 0.00 del 5 gennaio 2002 non verrà restituita dalla query, poiché non inclusa nell'intervallo.  
  
  
## <a name="see-also"></a>Vedere anche  
 [&#62; &#40;Greater Than&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/greater-than-transact-sql.md)   
 [&#60; &#40;Less Than&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/less-than-transact-sql.md)   
 [Expressions &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Funzioni predefinite &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [Operators &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)  
  
  


