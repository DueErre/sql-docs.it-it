---
title: setPoolable (metodo) (SQLServerStatement) | Documenti Microsoft
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
ms.assetid: f0f798c8-cafb-4acc-b85d-2e0059c91d92
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3cb4fd96733a36f6f9f0743fede135327c7d8b5e
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/18/2017
---
# <a name="setpoolable-method-sqlserverstatement"></a>setPoolable (metodo) (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Richiede che un'istruzione sia o meno inserita in un pool.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void setPoolable(boolean poolable) throws SQLException  
```  
  
#### <a name="parameters"></a>Parametri  
 *inserito*  
  
 Se **true**, richiede che l'istruzione inserire in un pool. Se **false**, richiede che l'istruzione non essere in pool.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Il valore specificato nella *inserito* parametro è un hint per l'implementazione di pool di istruzione che indica se l'applicazione desidera che l'istruzione per essere in pool. L'utilizzo dell'hint sarà deciso tramite la gestione del pool di istruzioni.  
  
 Un valore del pool di istruzioni viene applicato sia alle cache interne dell'istruzione implementate dal driver sia a quelle esterne implementate dai server applicazioni e da altre applicazioni.  
  
 Per impostazione predefinita, un oggetto SQLServerStatement non è inserito quando creato. Oggetti SQLServerPreparedStatement e SQLServerCallableStatement sono inseriti quando creato.  
  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) viene generata se questo metodo viene chiamato su un'istruzione chiusa.  
  
 [isPoolable](../../../connect/jdbc/reference/ispoolable-method-sqlserverstatement.md) restituisce un valore che indica se l'oggetto inserito.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
