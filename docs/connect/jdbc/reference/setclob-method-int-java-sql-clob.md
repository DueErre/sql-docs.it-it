---
title: Metodo setClob (int, Java.SQL. Clob) | Documenti Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerPreparedStatement.setClob
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 68d49f2c-fd8d-4abb-bfdc-e7b0fbd9a9da
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 89056fc3a5c61211b7a3c542d31e68161a2fcc80
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/18/2017
---
# <a name="setclob-method-int-javasqlclob"></a>Metodo setClob (int, java.sql.Clob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Imposta il parametro designato sull'oggetto Clob specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public final void setClob(int parameterIndex,  
                          java.sql.Clob clobValue)  
```  
  
#### <a name="parameters"></a>Parametri  
 *parameterIndex*  
  
 Un **int** che indica il numero di parametro.  
  
 *clobValue*  
  
 Un oggetto Clob.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo setClob viene specificato dal metodo setClob nell'interfaccia Java.SQL. PreparedStatement.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-methods.md)   
 [Classe SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
