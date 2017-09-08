---
title: InstanceOf (tipo di dati geography) | Documenti Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- InstanceOf
- InstanceOf_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- InstanceOf method
ms.assetid: 1eaed0e4-1c72-45a9-9926-5b513335cf33
caps.latest.revision: 28
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0edbebbb6754fd09ff834e4ffe8d453853b6f240
ms.contentlocale: it-it
ms.lasthandoff: 09/01/2017

---
# <a name="instanceof-geography-data-type"></a>InstanceOf (tipo di dati geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Verifica se il **geography** istanza corrisponde al tipo specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
.InstanceOf ( 'geography_type')  
```  
  
## <a name="arguments"></a>Argomenti  
 *geography_type*  
 È un **nvarchar (4000)** specificando una delle 16 tipi esposti nella stringa di **geography** gerarchia dei tipi.  
  
## <a name="return-types"></a>Tipi restituiti  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo restituito: **bit**  
  
 Tipo CLR restituito: **SqlBoolean**  
  
## <a name="remarks"></a>Osservazioni  
 Restituisce 1 se il tipo di un **geography** istanza corrisponde al tipo specificato, o se il tipo specificato è un predecessore del tipo di istanza; in caso contrario, restituisce 0.  
  
 Questo **geography** metodo supportata dal tipo di dati **FullGlobe** istanze o le istanze spaziali con dimensioni maggiori di un emisfero.  
  
 L'input per il metodo deve essere uno dei seguenti: Geometry, punto, Curve, LineString, CircularString, area, Polygon, CurvePolygon, **GeometryCollection**, **MultiSurface**,  **MultiLineString, multiPolygon, MultiCurve**, **MultiPoint**, o **FullGlobe**.  
  
 Questo metodo genera un'eccezione `ArgumentException` se per l'input viene utilizzata una qualsiasi altra stringa.  
  
 Il metodo non è preciso.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene creata un'istanza `MultiPoint` e viene utilizzato `InstanceOf()` per verificare se l'istanza è di tipo `GeometryCollection`.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('MULTIPOINT(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.InstanceOf('GEOMETRYCOLLECTION');  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi estesi sulle istanze di geografia](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  