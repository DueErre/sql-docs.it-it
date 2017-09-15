---
title: Metodo (SQLServerStatement) getFetchSize | Documenti Microsoft
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
- SQLServerStatement.getFetchSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8115ca58-8ae9-46ce-8515-7905d7bb25fe
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: efb6e1aca84c36afbfb761813ae8ab0efdfd2501
ms.contentlocale: it-it
ms.lasthandoff: 09/09/2017

---
# <a name="getfetchsize-method-sqlserverstatement"></a>getFetchSize (metodo) (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera il numero di risultati dei set di righe che rappresenta la dimensione di recupero predefinita per gli oggetti generati da questo set di risultati [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) oggetto.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public final int getFetchSize()  
```  
  
## <a name="return-value"></a>Valore restituito  
 Un **int** che indica la dimensione di recupero specificato mediante il [setFetchSize](../../../connect/jdbc/reference/setfetchsize-method-sqlserverstatement.md) metodo.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo getFetchSize viene specificato dal metodo getFetchSize nell'interfaccia Java.SQL. Statement.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
