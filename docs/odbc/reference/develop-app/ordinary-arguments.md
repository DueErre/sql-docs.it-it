---
title: Argomenti normali | Documenti Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- arguments in catalog functions [ODBC], ordinary
- catalog functions [ODBC], arguments
- ordinary arguments [ODBC]
ms.assetid: a18cdae1-6b85-41cb-875c-b5a01ec90aeb
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: db56df9bfd37b4395268250e6b921a3f98a2f6ee
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/21/2017
---
# <a name="ordinary-arguments"></a>Argomenti normali
Quando l'argomento di stringa di una funzione di catalogo è un argomento normale, viene considerato come una stringa letterale. Un argomento normale accetta un criterio di ricerca stringa né un elenco di valori. Nel caso di un argomento normale è significativo e considerati virgolette nella stringa. Questi argomenti vengono trattati come argomenti normali, se l'attributo di istruzione SQL_ATTR_METADATA_ID è impostato su SQL_FALSE; vengono considerate come argomenti identificatore invece se questo attributo è impostato su SQL_TRUE.  
  
 Se un argomento normale è impostato su un puntatore null e l'argomento è un argomento obbligatorio, la funzione restituisce SQL_ERROR e SQLSTATE HY009 (utilizzo non valido del puntatore null). Se un argomento normale è impostato su un puntatore null e l'argomento non è un argomento obbligatorio, il comportamento dell'argomento è dipendente dal driver. Gli argomenti obbligatori sono elencati nella tabella seguente.  
  
|Funzione|Argomenti obbligatori|  
|--------------|------------------------|  
|**SQLColumnPrivileges**|*TableName*|  
|**SQLForeignKeys**|*PKTableName*, *FKTableName*|  
|**SQLPrimaryKeys**|*TableName*|  
|**SQLSpecialColumns**|*TableName*|  
|**SQLStatistics**|*TableName*|
