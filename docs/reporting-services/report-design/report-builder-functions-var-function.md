---
title: Funzione Var (Generatore report e SSRS) | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7b2018ce-c5f9-4f8b-bd44-4201379a584b
caps.latest.revision: "7"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 2b47bf33f96a48df19e3fad06c1db2abaf925441
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2018
---
# <a name="report-builder-functions---var-function"></a>Funzioni di Generatore report - Funzione Var
  Restituisce la varianza di tutti i valori numerici non Null specificati dall'espressione, valutata nell'ambito specificato.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Var(expression, scope, recursive)  
```  
  
#### <a name="parameters"></a>Parametri  
 *expression*  
 (**Integer** o **Float**) Espressione su cui eseguire l'aggregazione.  
  
 *ambito*  
 (**String**) Facoltativo. Constante che corrisponde al nome di un set di dati, gruppo o area dati che contiene gli elementi del report a cui applicare la funzione di aggregazione. Se si omette *scope* , viene usato l'ambito corrente.  
  
 *ricorsivi*  
 (**Enumerated Type**) Facoltativo. **Simple** (impostazione predefinita) o **RdlRecursive**. Specifica se eseguire l'aggregazione in modo ricorsivo.  
  
## <a name="return-type"></a>Tipo restituito  
 Restituisce un valore **Decimal** per le espressioni decimali e un valore **Double** per tutte le altre espressioni.  
  
## <a name="remarks"></a>Remarks  
 Il set di dati specificato nell'espressione deve essere dello stesso tipo di dati. Per convertire dati con più tipi di dati numerici nello stesso tipo di dati, usare funzioni di conversione come **CInt**, **CDbl** o **CDec**. Per altre informazioni, vedere [Funzioni di conversione del tipo](http://go.microsoft.com/fwlink/?LinkId=96142).  
  
 Il valore di *scope* deve essere una costante di tipo stringa e non può essere un'espressione. Per aggregazioni o aggregazioni esterne che non specificano altre aggregazioni, *scope* deve fare riferimento all'ambito corrente o a un ambito contenitore. Per le aggregazioni di aggregazioni, le aggregazioni nidificate possono specificare un ambito figlio.  
  
 *Expression* può contenere chiamate alle funzioni di aggregazione nidificate con le eccezioni e le condizioni seguenti:  
  
-   *Scope* per le aggregazioni nidificate deve corrispondere o essere contenuto nell'ambito dell'aggregazione esterna. Per tutti gli ambiti distinti nell'espressione, un ambito deve essere in una relazione figlio con tutti gli altri ambiti.  
  
-   *Scope* per le aggregazioni nidificate non può essere il nome di un set di dati.  
  
-   *Expression* non deve contenere funzioni **First**, **Last**, **Previous**o **RunningValue** .  
  
-   *Expression* non deve contenere aggregazioni nidificate che specificano *recursive*.  
  
 Per altre informazioni, vedere [Riferimento a funzioni di aggregazione &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md) e [Ambito di espressioni per totali, aggregazioni e raccolte predefinite &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
 Per altre informazioni sulle aggregazioni ricorsive, vedere [Creazione di gruppi di gerarchie ricorsive &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md).  
  
## <a name="example"></a>Esempio  
 L'esempio di codice seguente consente di ottenere la varianza dei totali degli elementi nel gruppo o nell'area dati `Order` :  
  
```  
=Var(Fields!LineTotal.Value, "Order")  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo delle espressioni nei report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Esempi di espressioni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Tipi di dati nelle espressioni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Ambito di espressioni per totali, aggregazioni e raccolte predefinite &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
