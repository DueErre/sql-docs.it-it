---
title: "Livelli di conformità SQL, il Driver ODBC per Oracle | Documenti Microsoft"
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
- conformance levels [ODBC], SQL
- SQL conformance levels [ODBC]
- ODBC driver for Oracle [ODBC], conformance levels
ms.assetid: 077a6c6a-2c57-42c9-a4fd-4cf0e65cf7e2
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d57a126459d250a13a2ddd5ef1bb90732d1b4a45
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/21/2017
---
# <a name="sql-conformance-levels-odbc-driver-for-oracle"></a>Livelli di conformità SQL (Driver ODBC per Oracle)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. In alternativa, utilizzare il driver ODBC fornito da Oracle.  
  
 Il Driver ODBC per Oracle supporta la grammatica SQL minima e la grammatica SQL principale e supporta inoltre le seguenti estensioni ODBC per SQL:  
  
-   Dati di data, ora e timestamp  
  
-   Left e right outer join  
  
-   Funzioni numeriche:  
  
    |||||  
    |-|-|-|-|  
    |Abs|File di log|round|Tan|  
    |Limite massimo|LOG10|second|truncate|  
    |Cos|Mod|Accesso||  
    |Exp|PI|sin||  
    |floor|Power|sqrt||  
  
-   Funzioni di data:  
  
    |||||  
    |-|-|-|-|  
    |CURDATE|DayOfWeek|MonthName|second|  
    |Curtime|Dayofyear|minute|week|  
    |Dayname|Ora|a questo punto|year|  
    |DayOfMonth|Month|trimestre||  
  
-   Funzioni stringa:  
  
    |||||  
    |-|-|-|-|  
    |ASCII|Left|Ok|funzione UCase|  
    |Char|Length|RTrim||  
    |Concat|Ltrim|SOUNDEX||  
    |Lcase|Sostituisci|substring||  
  
-   Funzione di conversione del tipo:  
  
    ||  
    |-|  
    |Converti|  
  
-   Funzioni di sistema:  
  
    ||  
    |-|  
    |Ifnull|  
    |Utente|
