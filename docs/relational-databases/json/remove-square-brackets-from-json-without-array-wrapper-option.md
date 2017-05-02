---
title: Rimuovere le parentesi quadre dall&quot;output JSON con l&quot;opzione WITHOUT_ARRAY_WRAPPER | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 06/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- WITHOUT_ARRAY_WRAPPER
ms.assetid: aa86c2d1-458e-465f-abfa-75470137d054
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ea60d5a74c680e9c2aba571a76815f77913da471
ms.lasthandoff: 04/11/2017

---
# <a name="remove-square-brackets-from-json---withoutarraywrapper-option"></a>Rimuovere le parentesi quadre dall'output JSON con l'opzione WITHOUT_ARRAY_WRAPPER
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Per rimuovere le parentesi quadre che racchiudono l'output JSON della clausola **FOR JSON** per impostazione predefinita, specificare l'opzione **WITHOUT_ARRAY_WRAPPER** . Usare questa opzione per generare un singolo oggetto JSON come output anziché una matrice.  
  
 Se non si specifica questa opzione, l'output JSON è racchiuso tra parentesi quadre.  
  
## <a name="examples"></a>Esempi  
 L'esempio seguente mostra l'output della clausola **FOR JSON** con e senza l'opzione **WITHOUT_ARRAY_WRAPPER** .  
  
 **Query**  
  
```tsql  
SELECT 2015 as year, 12 as month, 15 as day  
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER 
```  

 **Risultato**  con l'opzione **WITHOUT_ARRAY_WRAPPER**  
  
```json  
{
    "year": 2015,
    "month": 12,
    "day": 15
} 
```  
  
 **Risultato**  senza l'opzione **WITHOUT_ARRAY_WRAPPER**  
  
```json  
[{
    "year": 2015,
    "month": 12,
    "day": 15
}]
```  
  
 Ecco un altro esempio di clausola **FOR JSON** con e senza l'opzione **WITHOUT_ARRAY_WRAPPER** .  
  
 **Query**  
  
```tsql  
SELECT TOP 1 SalesOrderNumber, OrderDate, Status  
FROM Sales.SalesOrderHeader  
ORDER BY ModifiedDate  
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER 
```  
  
 **Risultato**  con l'opzione **WITHOUT_ARRAY_WRAPPER**  
  
```json  
{
    "SalesOrderNumber": "SO43660",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
} 
```  
  
 **Risultato**  senza l'opzione **WITHOUT_ARRAY_WRAPPER**  
  
```json  
[{
    "SalesOrderNumber": "SO43660",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
}]
```  
  
## <a name="see-also"></a>Vedere anche  
 [Clausola FOR &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)  
  
  

