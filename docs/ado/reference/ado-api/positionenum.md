---
title: PositionEnum | Documenti Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- PositionEnum
helpviewer_keywords:
- PositionEnum enumeration
ms.assetid: e69af0a5-3405-4b72-9c6e-6b188ff746fd
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c3f317b92d138f020a43f26d71cbadd0f0cd412e
ms.contentlocale: it-it
ms.lasthandoff: 09/09/2017

---
# <a name="positionenum"></a>PositionEnum
Specifica la posizione corrente del puntatore del record all'interno di un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
|Costante|Valore|Description|  
|--------------|-----------|-----------------|  
|**adPosBOF**|-2|Indica che il puntatore del record corrente è a inizio file (vale a dire il [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) proprietà **True**).|  
|**adPosEOF**|-3|Indica che il puntatore del record corrente è alla fine del file (vale a dire il [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) proprietà **True**).|  
|**adPosUnknown**|-1|Indica che il **Recordset** è vuoto, la posizione corrente è sconosciuta, o il provider non supporta il [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) o [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md) proprietà.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC equivalente  
 Pacchetto: **com.ms. wfc.**  
  
|Costante|  
|--------------|  
|AdoEnums.Position.BOF|  
|AdoEnums.Position.EOF|  
|AdoEnums.Position.UNKNOWN|  
  
## <a name="applies-to"></a>Si applica a  
  
|||  
|-|-|  
|[Proprietà AbsolutePage (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)|[Proprietà AbsolutePosition (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)|

