---
title: "Chiusura degli oggetti quando non è In uso | Documenti Microsoft"
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
ms.assetid: ce8f9b35-c761-4b0c-9a46-985eef2c2e0b
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1c7f6a0421355676909de0edb1b6d1349c84e785
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/18/2017
---
# <a name="closing-objects-when-not-in-use"></a>Chiusura degli oggetti quando non vengono utilizzati
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Quando si utilizzano gli oggetti di [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], in particolare [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) o uno dell'istruzione, ad esempio oggetti [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md), [SQLServerPreparedStatement ](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) o [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md), è consigliabile chiuderli in modo esplicito tramite i relativi metodi Chiudi quando non sono più necessari. In questo modo, è possibile migliorare le prestazioni liberando le risorse del driver e del server appena possibile, anziché attendere che questa operazione venga eseguita dal Garbage Collector di Java Virtual Machine.  
  
 La chiusura degli oggetti è particolarmente importante per garantire una buona concorrenza nel server quando si utilizzano blocchi di scorrimento. I blocchi di scorrimento nel buffer di recupero in cui è stato effettuato l'ultimo accesso vengono mantenuti attivi fino a quando non viene chiuso il set di risultati. Analogamente, gli handle di istruzione preparati vengono mantenuti fino a quando l'istruzione non viene chiusa. Se si sta riutilizzando una connessione per più istruzioni, chiudendo le istruzioni prima che escano dall'ambito si consente al server di eseguire prima la pulizia degli handle preparati.  
  
## <a name="see-also"></a>Vedere anche  
 [Uso del driver JDBC per il miglioramento di prestazioni e affidabilità](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
