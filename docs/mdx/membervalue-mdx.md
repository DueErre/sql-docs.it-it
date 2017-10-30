---
title: MemberValue (MDX) | Documenti Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- MEMBERVALUE
dev_langs:
- kbMDX
helpviewer_keywords:
- MemberValue function
ms.assetid: f9b2af16-2b81-48e4-ae81-99f64e4bbc98
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 2ede5ef1aa5903095bc990ed6871682ce341e77b
ms.contentlocale: it-it
ms.lasthandoff: 08/02/2017

---
# <a name="membervalue-mdx"></a>MemberValue (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce il valore di un membro.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Member_Expression.MemberValue  
```  
  
## <a name="arguments"></a>Argomenti  
 *Member_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un membro.  
  
## <a name="return-value"></a>Valore restituito  
 Il valore del membro restituito contiene le informazioni seguenti, elencate in base all'ordine in cui appaiono nel valore restituito:  
  
-   Associazione del valore, se definita.  
  
-   Chiave con il tipo di dati originale se non esiste un'associazione del nome oppure se la chiave e la didascalia sono associate alla stessa colonna.  
  
-   Didascalia del membro.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente vengono restituiti l'associazione del valore, la chiave del membro e la didascalia della prima data nella dimensione Date del cubo Adventure Works.  
  
```  
WITH MEMBER Measures.ValueColumn as [Date].[Calendar].[July 1, 2001].MemberValue  
MEMBER Measures.KeyColumn as [Date].[Calendar].[July 1, 2001].Member_Key  
MEMBER Measures.NameColumn as [Date].[Calendar].[July 1, 2001].Member_Name  
  
SELECT {Measures.ValueColumn, Measures.KeyColumn, Measures.NameColumn}  ON 0  
from [Adventure Works]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento alla funzione MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

