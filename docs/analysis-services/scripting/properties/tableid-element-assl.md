---
title: Elemento TableID (ASSL) | Documenti Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- TableID Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- TableID
helpviewer_keywords:
- TableID element
ms.assetid: 45fe7e23-b274-4bc2-be63-1a5bb6680f51
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 89a10083cd42179ad72af682e337c67691dff491
ms.contentlocale: it-it
ms.lasthandoff: 09/01/2017

---
# <a name="tableid-element-assl"></a>Elemento TableID (ASSL)
  Contiene l'identificatore (ID) della tabella (dal [DataSourceView](../../../analysis-services/scripting/objects/datasourceview-element-assl.md) elemento) associato all'elemento padre.  
  
## <a name="syntax"></a>Sintassi  
  
```xml  
  
<ColumnBinding> <!-- or DSVTableBinding, RowBinding, IncrementalProcessingNotification -->  
   ...  
   <TableID>...</TableID>  
   ...  
</ColumnBinding>  
```  
  
## <a name="element-characteristics"></a>Caratteristiche elemento  
  
|Caratteristica|Descrizione|  
|--------------------|-----------------|  
|Tipo di dati e lunghezza|String|  
|Valore predefinito|Nessuno|  
|Cardinalità|1-1: elemento obbligatorio visualizzato una sola volta.|  
  
## <a name="element-relationships"></a>Relazioni elemento  
  
|Relazione|Elemento|  
|------------------|-------------|  
|Elementi padre|[ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md), [DSVTableBinding](../../../analysis-services/scripting/data-type/dsvtablebinding-data-type-assl.md), [IncrementalProcessingNotification](../../../analysis-services/scripting/objects/incrementalprocessingnotification-element-assl.md), [RowBinding](../../../analysis-services/scripting/data-type/rowbinding-data-type-assl.md)|  
|Elementi figlio|Nessuno|  
  
## <a name="remarks"></a>Osservazioni  
 La tabella identificata da **TableID** deve essere all'interno dell'origine dati a cui è associato l'oggetto proprietario (dimensione o cubo).  
  
 Gli elementi che corrispondono ai padri di **TableID** nel modello a oggetti oggetti AMO (Analysis Management) sono <xref:Microsoft.AnalysisServices.ColumnBinding>, <xref:Microsoft.AnalysisServices.DSVTableBinding>, <xref:Microsoft.AnalysisServices.IncrementalProcessingNotification>, e <xref:Microsoft.AnalysisServices.RowBinding>.  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

