---
title: moveToInsertRow (metodo) (SQLServerResultSet) | Documenti Microsoft
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
apiname: SQLServerResultSet.moveToInsertRow
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: f3c54bfe-d5b7-4f6e-ae6c-3e8954e5b1c9
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a430421535e5037771256b43353148ae12c35d18
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/18/2017
---
# <a name="movetoinsertrow-method-sqlserverresultset"></a>moveToInsertRow (metodo) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Sposta il cursore nella riga di inserimento.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void moveToInsertRow()  
```  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo moveToInsertRow viene specificato dal metodo moveToInsertRow nell'interfaccia Java.SQL. ResultSet.  
  
 La posizione corrente del cursore viene memorizzata mentre il cursore viene posizionato sulla riga di inserimento. La riga di inserimento è una riga speciale associata a un set di risultati aggiornabile. Si tratta essenzialmente di un buffer in cui è possibile costruire una nuova riga chiamando i metodi di aggiornamento prima di aggiungere la riga al set di risultati.  
  
 Solo l'aggiornamento, richiamo e [insertRow](../../../connect/jdbc/reference/insertrow-method-sqlserverresultset.md) metodi possono essere chiamati quando il cursore si trova sulla riga di inserimento. Tutte le colonne in un set di risultati devono essere specificato un valore ogni volta che questo metodo viene chiamato e prima di chiamare insertRow. Un metodo di aggiornamento deve essere chiamato prima che uno di richiamo possa essere chiamato su un valore della colonna.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
