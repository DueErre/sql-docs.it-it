---
title: Metodo getTime (lang, java.util.Calendar) | Documenti Microsoft
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
apiname: SQLServerCallableStatement.getTime (java.lang.String, java.util.Calendar)
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 3d4c67c2-a3c8-4a26-a159-89c5d63fda0b
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f24f1bcc53cb6675d12cfceb206514dadc7c9f9b
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/18/2017
---
# <a name="gettime-method-javalangstring-javautilcalendar"></a>Metodo getTime (java.lang.String, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera il valore del parametro designato come oggetto java.SQL. Time nel linguaggio di programmazione Java, dato il nome del parametro, utilizzando l'oggetto di calendario specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public java.sql.Time getTime(java.lang.String sCol,  
                             java.util.Calendar cal)  
```  
  
#### <a name="parameters"></a>Parametri  
 *sCol*  
  
 Oggetto **stringa** che contiene il nome del parametro.  
  
 *licenza CAL*  
  
 Un oggetto di calendario.  
  
## <a name="return-value"></a>Valore restituito  
 Un oggetto di tempo.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo getTime viene specificato dal metodo getTime nell'interfaccia Java.SQL. CallableStatement.  
  
 Vedere il grafico denominato "Conversioni dei metodi di richiamo" in [informazioni sulle conversioni di tipi di dati](../../../connect/jdbc/understanding-data-type-conversions.md) per vedere quali [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] tipi di dati possono essere recuperati con questo metodo.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo getTime &#40; SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/gettime-method-sqlservercallablestatement.md)   
 [Membri di SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
