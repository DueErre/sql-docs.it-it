---
title: Metodo setDate al valore di data - int | Documenti Microsoft
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
- SQLServerPreparedStatement.setDate (int, java.sql.Date)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 12e5a4cc-45a2-4779-bbfc-e4da66829588
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2b1ebded8c928a6d86da5a6ee58a345e1f67270b
ms.contentlocale: it-it
ms.lasthandoff: 09/09/2017

---
# <a name="setdate-method-int-javasqldate"></a>Metodo setDate (int, java.sql.Date)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Imposta il parametro designato sul valore di data specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public final void setDate(int n,  
                          java.sql.Date x)  
```  
  
#### <a name="parameters"></a>Parametri  
 *n*  
  
 Un **int** che indica il numero di parametro.  
  
 *x*  
  
 Oggetto Date.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo setDate viene specificato dal metodo setDate nell'interfaccia Java.SQL. PreparedStatement.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo setDate &#40; SQLServerPreparedStatement &#41;](../../../connect/jdbc/reference/setdate-method-sqlserverpreparedstatement.md)   
 [Membri di SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Classe SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
