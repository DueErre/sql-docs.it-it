---
title: Si esegue l'override di scala e precisione predefinita per i tipi di dati numerici | Documenti Microsoft
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
- numeric data type [ODBC], precision and scale
- precision [ODBC], numeric data types
- data types [ODBC], numeric data types
- numeric data type [ODBC]
- numeric literals [ODBC]
ms.assetid: 84292334-0e33-4a1b-84de-8c018dd787f3
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e2be244dd3ad258ab3fa6b5679e5989d8a08778e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/21/2017
---
# <a name="overriding-default-precision-and-scale-for-numeric-data-types"></a>Si esegue l'override di scala e precisione predefinita per i tipi di dati numerici
Quando il campo SQL_DESC_TYPE in un ARD è SQL_C_NUMERIC, con una chiamata a **SQLBindCol** o **SQLSetDescField**, il campo SQL_DESC_SCALE nel ARD è impostato su 0 e il campo SQL_DESC_PRECISION è impostato a una precisione predefiniti definiti dal driver. Ciò vale anche quando il campo SQL_DESC_TYPE in un APD è impostato su SQL_C_NUMERIC, con una chiamata a **SQLBindParameter** o **SQLSetDescField**. Questo vale per l'input, input/output o i parametri di output.  
  
 Se uno dei valori predefiniti descritti in precedenza non sono consentito per un'applicazione, l'applicazione deve impostare il campo SQL_DESC_SCALE o SQL_DESC_PRECISION chiamando **SQLSetDescField** o **SQLSetDescRec**.  
  
 Se l'applicazione chiama **SQLGetData** per restituire i dati in una struttura SQL_C_NUMERIC, vengono utilizzati i campi predefiniti, SQL_DESC_SCALE e SQL_DESC_PRECISION. Se le impostazioni predefinite non sono consentite, l'applicazione deve chiamare **SQLSetDescRec** o **SQLSetDescField** per impostare i campi e quindi chiamare **SQLGetData** con un *TargetType* di SQL_ARD_TYPE per utilizzare i valori nei campi del descrittore.  
  
 Quando **SQLPutData** viene chiamato, la chiamata utilizza i campi SQL_DESC_SCALE e SQL_DESC_PRECISION di record del descrittore che corrisponde al parametro data-at-execution o colonna, che sono i campi per le chiamate a APD  **SQLExecute** o **SQLExecDirect**, o campi ARD per le chiamate a **SQLBulkOperations** o **SQLSetPos**.
