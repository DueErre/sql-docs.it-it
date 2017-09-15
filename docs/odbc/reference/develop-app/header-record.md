---
title: Record di intestazione | Documenti Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic records
- header records [ODBC]
- diagnostic records [ODBC]
ms.assetid: d0fff1ed-5616-422a-a394-7ea1d2486f89
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0e4b73bf94c2d90f34c1d06240cbcceb07702c7a
ms.contentlocale: it-it
ms.lasthandoff: 09/09/2017

---
# <a name="header-record"></a>Record di intestazione
I campi nel record di intestazione contengono informazioni generali sull'esecuzione di una funzione, incluso il codice restituito, conteggio delle righe, numero di record di stato e tipo di istruzione eseguita. Il record di intestazione viene sempre creato, a meno che la funzione non restituisca SQL_INVALID_HANDLE. Per un elenco completo dei campi nel record di intestazione, vedere il [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) descrizione della funzione.
