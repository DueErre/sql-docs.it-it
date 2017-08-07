---
title: YTD (MDX) | Documenti Microsoft
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
- YTD
dev_langs:
- kbMDX
helpviewer_keywords:
- Ytd function
ms.assetid: b77fdba2-d4a9-4271-8c21-c1f12eba526d
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 99600f9684215a1147b5372c3e912040fb9f122f
ms.contentlocale: it-it
ms.lasthandoff: 08/02/2017

---
# <a name="ytd-mdx"></a>Ytd (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce i membri di un set di pari livello dallo stesso livello di un membro dato, iniziando con il primo elemento di pari livello e terminando con il membro specificato, come vincolo imposto dal *anno* livello nella dimensione temporale.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Ytd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>Argomenti  
 *Member_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un membro.  
  
## <a name="remarks"></a>Osservazioni  
 Se un'espressione di membro non è specificata, il valore predefinito è il membro corrente della prima gerarchia con un livello di tipo *anni* nella prima dimensione di tipo *ora* nel gruppo di misure.  
  
 Il **Ytd** è una funzione di scelta rapida per il [PeriodsToDate](../mdx/periodstodate-mdx.md) in cui la proprietà Type della gerarchia dell'attributo in cui si basa il livello è impostato su *anni*. In altre parole, `Ytd(Member_Expression)` equivale a `PeriodsToDate(Year_Level_Expression,Member_Expression)`. Si noti che questa funzione non funziona quando la proprietà Type è impostata su *FiscalYears*.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente restituisce la somma del `Measures.[Order Quantity]` membro, aggregato sui primi otto mesi dell'anno di calendario 2003 contenuti nel `Date` dimensione, dal **Adventure Works** cubo.  
  
```  
WITH MEMBER [Date].[Calendar].[First8MonthsCY2003] AS  
    Aggregate(  
        YTD([Date].[Calendar].[Month].[August 2003])  
    )  
SELECT   
    [Date].[Calendar].[First8MonthsCY2003] ON COLUMNS,  
    [Product].[Category].Children ON ROWS  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Order Quantity]  
```  
  
 **YTD** spesso viene utilizzata in combinazione con nessun parametro specificato, il che significa che il [CurrentMember &#40; MDX &#41; ](../mdx/currentmember-mdx.md) funzione visualizzerà un totale cumulativo di year-to-date in un report, come illustrato nella query seguente:  
  
 `WITH MEMBER MEASURES.YTDDEMO AS`  
  
 `AGGREGATE(YTD(), [Measures].[Internet Sales Amount])`  
  
 `SELECT {[Measures].[Internet Sales Amount], MEASURES.YTDDEMO} ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento alla funzione MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
