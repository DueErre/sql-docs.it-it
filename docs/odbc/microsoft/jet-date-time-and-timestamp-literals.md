---
title: 'Jet: Date, Time e Timestamp letterali | Documenti Microsoft'
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
- literals [ODBC], SQL grammar
- SQL grammar [ODBC], literals
- date literals [ODBC]
- timestamp literals [ODBC]
- time literals [ODBC]
ms.assetid: 37db1ae1-ca4e-4cd8-9b47-7f1a38e7fcad
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 819b40dd4cc3e8481ed5e0795debca13c0779fd6
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/21/2017
---
# <a name="jet-date-time-and-timestamp-literals"></a>Jet: Date, Time e Timestamp letterali
Per garantire la massima interoperabilità, le applicazioni devono passare valori letterali di data nel formato canonico ODBC utilizzando la sintassi della clausola di escape:  
  
-   Per i valori letterali data, {d '*valore*'}, dove *valore*e è nel formato "aaaa-mm-gg"  
  
-   Per i valori letterali ora, {t '*valore*'}, dove *valore*e è nel formato "hh"  
  
 Per i valori letterali timestamp {ts'*valore*'}, dove *valore*e è nel formato "aaaa-mm-gg hh: mm: [. f....]".
