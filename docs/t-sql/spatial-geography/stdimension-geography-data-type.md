---
title: STDimension (tipo di dati geography) | Documenti Microsoft
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
- STDimension (geography Data Type)
- STDimension_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STDimension method
ms.assetid: 4368b0f6-0678-4ade-87dc-b43d8b2e8d92
caps.latest.revision: 19
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0026ae44feb99e398a4502488d52594dac3b6bd4
ms.contentlocale: it-it
ms.lasthandoff: 09/01/2017

---
# <a name="stdimension-geography-data-type"></a>STDimension (tipo di dati geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Restituisce le dimensioni massime di un **geography** istanza.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
.STDimension ( )  
```  
  
## <a name="return-types"></a>Tipi restituiti  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo restituito: **int**  
  
 Tipo CLR restituito: **SqlInt32**  
  
## <a name="remarks"></a>Osservazioni  
 STDimension() restituisce -1 se il **geography** istanza è vuota.  
  
## <a name="examples"></a>Esempi  
 L'esempio seguente usa `STDimension()` per creare una variabile di tabella per contenere `geography` le istanze e inserisce un `Point`, `LineString`e un `Polygon`.  
  
```  
DECLARE @temp table ([name] varchar(10), [geom] geography);  
  
INSERT INTO @temp values ('Point', geography::STGeomFromText('POINT(-122.34900 47.65100)', 4326));  
INSERT INTO @temp values ('LineString', geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326));  
INSERT INTO @temp values ('Polygon', geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326));  
  
SELECT [name], [geom].STDimension() as [dim]  
FROM @temp;  
```  
  
 Nell'esempio vengono restituite le dimensioni di ogni `geography`istanza.  
  
|name|dim|  
|----------|---------|  
|Punto|0|  
|LineString|1|  
|Poligono|2|  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi OGC sulle istanze di geografia](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  

