---
title: Elemento ExecuteResponse (XMLA) | Documenti Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: ExecuteResponse Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#ExecuteResponse
- http://schemas.microsoft.com/analysisservices/2003/engine#ExecuteResponse
- microsoft.xml.analysis.executeresponse
helpviewer_keywords: ExecuteResponse element
ms.assetid: 6edb1b82-da4c-4cd9-9385-bea04032f0eb
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 1ce67e186ba1de23fda714359f4fcdc7a78b51fa
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/17/2017
---
# <a name="xml-elements---objects---executeresponse"></a>ExecuteResponse - oggetti - elementi XML
  Contiene le informazioni restituite da un'istanza di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in risposta a un [Execute](../../analysis-services/xmla/xml-elements-methods-execute.md) chiamata al metodo.  
  
 **Namespace** urn:schemas-microsoft-com:xml-analysis  
  
## <a name="syntax"></a>Sintassi  
  
```xml  
  
<ExecuteResponse>  
   <return>  
</ExecuteResponse>  
```  
  
## <a name="element-characteristics"></a>Caratteristiche elemento  
  
|Caratteristica|Descrizione|  
|--------------------|-----------------|  
|Tipo di dati e lunghezza|Nessuno|  
|Valore predefinito|Nessuno|  
|Cardinalità|1-1: elemento obbligatorio che può ricorrere una sola volta.|  
  
## <a name="element-relationships"></a>Relazioni elemento  
  
|Relazione|Elemento|  
|------------------|-------------|  
|Elementi padre|Nessuno|  
|Elementi figlio|[restituire](../../analysis-services/xmla/xml-elements-properties/return-element-xmla.md)|  
  
## <a name="remarks"></a>Osservazioni  
 Il **ExecuteResponse** è l'elemento in primo piano all'interno del corpo di una risposta SOAP per il **Execute** metodo.  
  
## <a name="see-also"></a>Vedere anche  
 [Elemento DiscoverResponse &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-objects-discoverresponse.md)   
 [Oggetti &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-objects.md)  
  
  
