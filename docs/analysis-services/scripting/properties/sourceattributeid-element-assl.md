---
title: Elemento SourceAttributeID (ASSL) | Documenti Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: SourceAttributeID Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: SourceAttributeID
helpviewer_keywords: SourceAttributeID element
ms.assetid: 8973eb62-6142-4ce2-ad42-c8be2b43c04f
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 2f40e4559613c38be86e5239440626cb6a55f931
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/08/2017
---
# <a name="sourceattributeid-element-assl"></a>Elemento SourceAttributeID (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Contiene l'identificatore (ID) dell'attributo di origine in cui il [livello](../../../analysis-services/scripting/objects/level-element-assl.md) si basa l'elemento.  
  
## <a name="syntax"></a>Sintassi  
  
```xml  
  
<Level>  
   ...  
   <SourceAttributeID>...</SourceAttributeID>  
   ...  
</Level>  
```  
  
## <a name="element-characteristics"></a>Caratteristiche elemento  
  
|Caratteristica|Descrizione|  
|--------------------|-----------------|  
|Tipo di dati e lunghezza|String|  
|Valore predefinito|Nessuno|  
|Cardinalità|0-1: elemento facoltativo che può ricorrere una sola volta.|  
  
## <a name="element-relationships"></a>Relazioni elemento  
  
|Relazione|Elemento|  
|------------------|-------------|  
|Elemento padre|[Level](../../../analysis-services/scripting/objects/level-element-assl.md)|  
|Elementi figlio|Nessuno|  
  
## <a name="remarks"></a>Osservazioni  
 L'elemento corrispondente dell'elemento padre del **SourceAttributeID** nell'oggetto oggetti AMO (Analysis Management) è modello <xref:Microsoft.AnalysisServices.Level>.  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
