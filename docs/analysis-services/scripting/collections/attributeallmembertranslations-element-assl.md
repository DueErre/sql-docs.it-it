---
title: Elemento AttributeAllMemberTranslations (ASSL) | Documenti Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- AttributeAllMemberTranslations Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- AttributeAllMemberTranslations
helpviewer_keywords:
- AttributeAllMemberTranslations element
ms.assetid: 1a0d86ea-d95d-4d93-b321-acd35ed4ac26
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d3e9208e7b4568a751b3a3a65ab9f17c0919093f
ms.contentlocale: it-it
ms.lasthandoff: 09/01/2017

---
# <a name="attributeallmembertranslations-element-assl"></a>Elemento AttributeAllMemberTranslations (ASSL)
  Contiene la raccolta di traduzioni per la didascalia del membro Totale della dimensione.  
  
## <a name="syntax"></a>Sintassi  
  
```xml  
  
<Dimension>  
   ...  
   <AttributeAllMemberTranslations>  
      <AttributeAllMemberTranslation xsi:type="Translation">...</AttributeAllMemberTranslation>  
   </AttributeAllMemberTranslations>  
      ...  
</Dimension>  
```  
  
## <a name="element-characteristics"></a>Caratteristiche elemento  
  
|Caratteristica|Descrizione|  
|--------------------|-----------------|  
|Tipo di dati e lunghezza|Nessuno|  
|Valore predefinito|Nessuno|  
|Cardinalità|0-1: elemento facoltativo che può ricorrere una sola volta.|  
  
## <a name="element-relationships"></a>Relazioni elemento  
  
|Relazione|Elemento|  
|------------------|-------------|  
|Elementi padre|[Dimension](../../../analysis-services/scripting/objects/dimension-element-assl.md)|  
|Elementi figlio|[AttributeAllMemberTranslation](../../../analysis-services/scripting/objects/attributeallmembertranslation-element-assl.md)|  
  
## <a name="remarks"></a>Osservazioni  
 L'elemento che corrisponde all'elemento padre **AttributeAllMemberTranslations** nell'oggetto oggetti AMO (Analysis Management) è modello <xref:Microsoft.AnalysisServices.Dimension>.  
  
## <a name="see-also"></a>Vedere anche  
 [Elemento Translation &#40; ASSL &#41;](../../../analysis-services/scripting/objects/translation-element-assl.md)   
 [Raccolte &#40; ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  

