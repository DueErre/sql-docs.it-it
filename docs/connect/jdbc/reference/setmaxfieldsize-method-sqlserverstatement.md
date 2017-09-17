---
title: Metodo (SQLServerStatement) setMaxFieldSize | Documenti Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerStatement.setMaxFieldSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 38f7fc1d-acad-4d10-9fc8-3c0669d93b07
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 79a7cd17e2d28fde42bfad8c82fdc4bcde3ef00f
ms.contentlocale: it-it
ms.lasthandoff: 09/09/2017

---
# <a name="setmaxfieldsize-method-sqlserverstatement"></a>setMaxFieldSize (metodo) (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Imposta il limite per il numero massimo di byte in un [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) colonna archivia i valori binari al numero specificato di byte o carattere.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public final void setMaxFieldSize(int max)  
```  
  
#### <a name="parameters"></a>Parametri  
 *Max*  
  
 Un **int** che indica il numero massimo di byte.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo setMaxFieldSize viene specificato dal metodo setMaxFieldSize nell'interfaccia Java.SQL. Statement.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
