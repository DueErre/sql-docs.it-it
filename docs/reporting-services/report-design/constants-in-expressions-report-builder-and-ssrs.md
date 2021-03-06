---
title: Costanti nelle espressioni (Generatore report e SSRS) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b8ae650b-0f46-4848-b62b-15f8a40751b8
caps.latest.revision: "8"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 816a3f835ee8f3d903a22844450d557fb4b8086c
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2018
---
# <a name="constants-in-expressions-report-builder-and-ssrs"></a>Costanti nelle espressioni (Generatore report e SSRS)
  Una costante è costituita da testo letterale o da testo predefinito. Il componente di elaborazione del report ha accesso alle costanti predefinite in modo che quando queste vengono incluse in un'espressione, i valori che rappresentano vengono sostituiti prima di essere valutati.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="literal-text"></a>Testo letterale  
 In un'espressione il testo letterale corrisponde a testo racchiuso tra virgolette doppie. È anche possibile digitare il testo direttamente in una casella di testo senza virgolette doppie, se non fa parte di un'espressione. Se il valore della casella di testo non inizia con un segno di uguale (=), il testo viene trattato come testo letterale. Nella tabella seguente sono illustrati diversi esempi di testo letterale in un'espressione.  
  
|Costante|Testo visualizzato|Testo dell'espressione|  
|--------------|------------------|---------------------|  
|Report eseguito alle:|<\<Expr>>|`="Report run at: " & Globals!ExecutionTime`|  
|Adventure Works Cycles|Adventure Works Cycles|Adventure Works Cycles|  
|[Testo visualizzato tra parentesi quadre]|\\[Testo visualizzato tra parentesi quadre\\]|[Testo visualizzato tra parentesi quadre]|  
  
## <a name="rdl-constants"></a>Costanti RDL  
 È possibile utilizzare le costanti definite in Report Definition Language (RDL) in un'espressione. Nella finestra di dialogo **Espressione** le costanti vengono visualizzate quando si crea un'espressione per una proprietà del report che accetta solo determinati valori validi, noti anche come tipi enumerati. Nella tabella seguente sono illustrati due esempi.  
  
|Proprietà|Description|Valori|  
|--------------|-----------------|------------|  
|TextAlign|Valori validi per l'allineamento del testo in una casella di testo.|Standard, A sinistra, Al centro, A destra|  
|BorderStyle|Valori validi per una linea aggiunta a un report.|Predefinito, Nessuno, Punteggiato, Tratteggiato, Continuo, Doppio, TrattoPunto, TrattoPuntoPunto|  
  
## <a name="visual-basic-constants"></a>Costanti di Visual Basic  
 In un'espressione è possibile usare costanti definite nella libreria run-time di [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] . È possibile, ad esempio, utilizzare la costante **DateInterval.Day**. L'espressione seguente per la data 10 gennaio 2008 restituisce il numero 10:  
  
 `=DatePart("d",Globals!ExecutionTime)`  
  
## <a name="clr-constants"></a>Costanti CLR  
 È possibile utilizzare le costanti definite nelle classi CLR (Common Language Run-time) di [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] in un'espressione. Nella tabella seguente è illustrato un esempio di un colore definito dal sistema.  
  
|Costante|Description|  
|--------------|-----------------|  
|MistyRose|Quando si crea un'espressione per una proprietà del report basata su un colore di sfondo, è possibile specificare un colore per nome. I nomi validi sono elencati nella finestra di dialogo **Espressione** .|  
  
## <a name="see-also"></a>Vedere anche  
 [Finestra di dialogo Espressione](http://msdn.microsoft.com/library/e6c74ccb-4594-4d4f-b958-618d710e34eb)   
 [Espressioni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [Esempi di espressioni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Tipi di dati nelle espressioni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Finestra di dialogo dell'espressione &#40;Generatore report&#41;](http://msdn.microsoft.com/library/e89c4d97-5d41-4b55-8695-79329edac15d)  
  
  
