---
title: Metodo ownDeletesAreVisible (SQLServerDatabaseMetaData) | Documenti Microsoft
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
apiname: SQLServerDatabaseMetaData.ownDeletesAreVisible
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 2dd6d976-9f8f-4a24-9354-ff239cfd4364
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 61644a52ba7e7c6e9b0eb15ac97295ec681e234e
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/18/2017
---
# <a name="owndeletesarevisible-method-sqlserverdatabasemetadata"></a>Metodo ownDeletesAreVisible (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera un valore che indica se sono visibili le operazioni di eliminazione di un set di risultati eseguite dall'utente corrente.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public boolean ownDeletesAreVisible(int type)  
```  
  
#### <a name="parameters"></a>Parametri  
 *type*  
  
 Un **int** che indica il set di risultati tipo, che può essere uno dei valori seguenti come definito in Java.SQL. ResultSet o SQLServerResultSet:  
  
## <a name="javasqlresultset-types"></a>Tipi java.sql.ResultSet  
 TYPE_FORWARD_ONLY  
  
 TYPE_SCROLL_SENSITIVE  
  
 TYPE_SCROLL_INSENSITIVE  
  
## <a name="sqlserverresultset-types"></a>Tipi SQLServerResultSet  
 TYPE_SS_SCROLL_STATIC  
  
 TYPE_SS_SCROLL_KEYSET  
  
 TYPE_SS_DIRECT_FORWARD_ONLY  
  
 TYPE_SS_SERVER_CURSOR_FORWARD_ONLY  
  
 TYPE_SS_SCROLL_DYNAMIC  
  
## <a name="return-value"></a>Valore restituito  
 **true** se le eliminazioni sono visibili. In caso contrario, **false**.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo ownDeletesAreVisible viene specificato dal metodo ownDeletesAreVisible nell'interfaccia DatabaseMetaData.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membri di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
