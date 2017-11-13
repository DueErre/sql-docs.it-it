---
title: La chiamata di funzione SQLGetDiagField | Documenti Microsoft
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
- application upgrades [ODBC], SQLGetDiagField
- backward compatibility [ODBC], SqlGetDiagField
- upgrading applications [ODBC], SQLGetDiagField
- SQLGetDiagField function [ODBC], calling
- compatibility [ODBC], SQLGetDiagField
ms.assetid: 3c4fb606-b81c-4f11-9820-f0a54e3bc401
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2d19805c12075a9d8961e161070b8c95ae08be89
ms.contentlocale: it-it
ms.lasthandoff: 09/09/2017

---
# <a name="calling-sqlgetdiagfield"></a>La chiamata di funzione SQLGetDiagField
Quando un'applicazione ODBC 3. *x* applicazione chiama **SQLGetDiagField** un 2 di ODBC*x* driver, il driver restituisce SQL_SUCCESS e le informazioni appropriate nella  *\*DiagInfoPtr* se il *DiagIdentifier* argomento è SQL_DIAG_CLASS_ORIGIN, SQL_DIAG_CLASS_SUBCLASS_ORIGIN, SQL_DIAG_CONNECTION_NAME, SQL_DIAG_MESSAGE_TEXT, SQL_DIAG_NATIVE, SQL_DIAG_ NUMERO, SQL_DIAG_RETURNCODE, SQL_DIAG_SERVER_NAME o SQL_DIAG_SQLSTATE. Tutti gli altri campi di diagnostica restituirà SQL_ERROR.

