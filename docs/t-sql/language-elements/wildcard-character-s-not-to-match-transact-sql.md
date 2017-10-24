---
title: Mancata corrispondenza dei caratteri (jolly) (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 12/06/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server (starting with 2008)
f1_keywords:
- wildcard
- '[^]_TSQL'
- '[^]'
- Not Match
dev_langs:
- TSQL
helpviewer_keywords:
- wildcard characters [SQL Server]
- '[^] (wildcard - character(s) not to match)'
ms.assetid: b970038f-f4e7-4a5d-96f6-51e3248c6aef
caps.latest.revision: 36
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 96749cb88e4d98b112de2ce1eb9bff4c7e156e42
ms.contentlocale: it-it
ms.lasthandoff: 09/01/2017

---
# <a name="wildcard---characters-not-to-match-transact-sql"></a>Mancata corrispondenza dei caratteri (jolly) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Corrisponde a un qualsiasi singolo carattere non compreso nell'intervallo o nel set specificato tra le parentesi quadre.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene utilizzato l'operatore [^] per individuare tutte le persone nella tabella `Contact` il cui nome inizia con `Al` e non contiene la lettera `a` come terzo carattere.  
  
```  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName  
FROM Person.Person  
WHERE FirstName LIKE 'Al[^a]%'  
ORDER BY FirstName;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Ad esempio &#40; Transact-SQL &#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [PATINDEX &#40; Transact-SQL &#41;](../../t-sql/functions/patindex-transact-sql.md)   
 [% &#40; Carattere jolly - carattere &#40; s &#41; in corrispondenza &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/percent-character-wildcard-character-s-to-match-transact-sql.md)   
  [&#91; &#93; (Carattere jolly alla corrispondenza)](../../t-sql/language-elements/wildcard-character-s-to-match-transact-sql.md)   
 [_ (Carattere jolly per corrispondenze di singoli caratteri)](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)  
  
  

