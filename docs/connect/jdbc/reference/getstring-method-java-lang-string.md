---
title: getString (metodo) (lang) | Documenti Microsoft
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
apiname: SQLServerCallableStatement.getString (java.lang.String)
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: f67371e0-e879-4188-85fc-ecb85f0be2a9
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e6d9437a7fbba96fc92908fdd875dae964ee3bbb
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/18/2017
---
# <a name="getstring-method-javalangstring"></a>Metodo getString (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera il valore del parametro designato come un **stringa** nel linguaggio di programmazione Java specificato il nome del parametro.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public java.lang.String getString(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>Parametri  
 *sCol*  
  
 Oggetto **stringa** che contiene il nome del parametro.  
  
## <a name="return-value"></a>Valore restituito  
 Oggetto **stringa** valore.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo getString viene specificato dal metodo getString nell'interfaccia Java.SQL. CallableStatement.  
  
 Tutte le colonne [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] può essere restituito come stringa. Pertanto, possono essere restituite una rappresentazione di stringa di tutti i tipi numerici e basati su caratteri e una rappresentazione in stringa esadecimale di colonne binarie quali binary, varbinary, varbinary(max), image, timestamp e uniqueidentifier.  
  
 I tipi dipendenti dai percorsi quali money, smallmoney, datetime, smalldatetime, float, real, decimal e numeric restituiranno il formato canonico toString() per il valore sottostante del tipo.  
  
 I tipi definiti dall'utente vengono restituiti come valori di stringa esadecimali.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo getString &#40; SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/getstring-method-sqlservercallablestatement.md)   
 [Membri di SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
