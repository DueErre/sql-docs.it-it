---
title: parametro del metodo (lang) getDate | Documenti Microsoft
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
- SQLServerCallableStatement.getDate (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a605bca6-d960-4756-ad14-0f42b313e60a
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 34845dae4eae7d80d8c210cd605e7b5e4655b61a
ms.contentlocale: it-it
ms.lasthandoff: 09/09/2017

---
# <a name="getdate-method-javalangstring"></a>Metodo getDate (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera il valore del parametro designato come oggetto java.sql.Date nel linguaggio di programmazione Java in base al nome del parametro.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public java.sql.Date getDate(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>Parametri  
 *sCol*  
  
 Oggetto **stringa** che contiene il nome del parametro.  
  
## <a name="return-value"></a>Valore restituito  
 Oggetto Date.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo getDate è specificato dal metodo getDate nell'interfaccia Java.SQL. CallableStatement.  
  
 Questo metodo restituisce una parte della data valida di un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] **datetime** o **smalldatetime** il tipo di dati, con la parte dell'ora impostata sull'ora di base Java di 00:00 (mezzanotte).  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo getDate &#40; SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/getdate-method-sqlservercallablestatement.md)   
 [Membri di SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  