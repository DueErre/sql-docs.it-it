---
title: SIGN (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SIGN_TSQL
- SIGN
dev_langs:
- TSQL
helpviewer_keywords:
- '- (negative)'
- + (positive sign)
- zero (0)
- SIGN function
- positive values [SQL Server]
- 0 (zero)
- negative values
ms.assetid: c3a98b52-6fbe-4127-a5c9-8a4922e83e28
caps.latest.revision: 33
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5ec7a98db7e5fa31bebed31ba02758ebc4ec02a1
ms.contentlocale: it-it
ms.lasthandoff: 09/01/2017

---
# <a name="sign-transact-sql"></a>SIGN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Restituisce il segno positivo (+1), zero (0) o il segno negativo (-1) dell'espressione specificata.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
SIGN ( numeric_expression )  
```  
  

## <a name="arguments"></a>Argomenti  
 *numeric_expression*  
 È un [espressione](../../t-sql/language-elements/expressions-transact-sql.md) di uno, categoria del tipo di dati numerici o numerici approssimativi, ad eccezione del **bit** tipo di dati.  
  
## <a name="return-types"></a>Tipi restituiti  
  
|Espressione specificata|Tipo restituito|  
|--------------------------|-----------------|  
|**bigint**|**bigint**|  
|**int o smallint/tinyint**|**int**|  
|**Money/smallmoney**|**money**|  
|**numerici o decimali**|**numerici o decimali**|  
|**Altri tipi**|**float**|  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono restituiti i valori SIGN dei numeri compresi tra -1 e 1.  
  
```  
DECLARE @value real  
SET @value = -1  
WHILE @value < 2  
   BEGIN  
      SELECT SIGN(@value)  
      SET NOCOUNT ON  
      SELECT @value = @value + 1  
      SET NOCOUNT OFF  
   END  
SET NOCOUNT OFF  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
(1 row(s) affected)  
  
------------------------   
-1.0                       
  
(1 row(s) affected)  
  
------------------------   
0.0                        
  
(1 row(s) affected)  
  
------------------------   
1.0                        
  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Esempi: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 L'esempio seguente restituisce i valori SIGN dei tre numeri.  
  
```  
SELECT SIGN(-125), SIGN(0), SIGN(564);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `-----  -----  -----`  
  
 `-1     0      1`  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni matematiche &#40; Transact-SQL &#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  
  
  


