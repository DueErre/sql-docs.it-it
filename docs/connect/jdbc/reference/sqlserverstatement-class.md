---
title: Classe SQLServerStatement | Documenti Microsoft
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
ms.assetid: ec24963c-8b51-4838-91e9-1fbfa2347451
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5ef6ef57bda9fe69685c042b564306655c67f516
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/18/2017
---
# <a name="sqlserverstatement-class"></a>Classe SQLServerStatement
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Rappresenta l'implementazione di base della funzionalità dell'istruzione JDBC.  
  
 **Pacchetto:** com.microsoft.sqlserver.jdbc  
  
 **Implementa:** [ISQLServerStatement](../../../connect/jdbc/reference/isqlserverstatement-interface.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public class SQLServerStatement  
```  
  
## <a name="remarks"></a>Osservazioni  
 La classe SQLServerStatement fornisce anche un numero di metodi di implementazione della classe base per JDBC preparata l'istruzione e le istruzioni disponibili. Il ruolo di base della classe SQLServerStatement consiste nell'eseguire istruzioni SQL e quindi restituzione dei conteggi aggiornamenti e il risultato di imposta per l'applicazione dell'utente.  
  
 Questa classe supporta l'annullamento del wrapping nella classe SQLServerStatement, l'interfaccia ISQLServerStatement e l'interfaccia Java.SQL. Statement. Per ulteriori informazioni, vedere [wrapper e interfacce](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Riferimento all'API del Driver JDBC](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
