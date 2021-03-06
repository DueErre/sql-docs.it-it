---
title: Metodo Unwrap (SQLServerStatement) | Documenti Microsoft
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
ms.assetid: ce680176-ef04-4e44-bb6c-ec50bd06e7e6
caps.latest.revision: "22"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 26a0e6fd3cec7cde459dc72416e35bc98275e3f1
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/18/2017
---
# <a name="unwrap-method-sqlserverstatement"></a>Metodo unwrap (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Restituisce un oggetto che implementa l'interfaccia specificata per consentire l'accesso per il [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]-metodi specifici.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public <T> T unwrap(Class<T> iface)  
```  
  
#### <a name="parameters"></a>Parametri  
 *iface*  
  
 Una classe di tipo **T** che definisce un'interfaccia.  
  
## <a name="return-value"></a>Valore restituito  
 Oggetto che implementa l'interfaccia specificata.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Il [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md) metodo è definito dall'interfaccia Java.SQL, introdotta nella specifica JDBC 4.0.  
  
 Potrebbe essere necessario accedere alle estensioni dell'API JDBC siano per le applicazioni di [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]. Il metodo unwrap supporta l'annullamento del wrapping classi pubbliche che estende l'oggetto, se le classi espongono estensioni del fornitore.  
  
 Quando questo metodo viene chiamato, l'oggetto Annulla il wrapping di [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) classe.  
  
 Ad esempio di codice, vedere [l'aggiornamento di grandi dimensioni campione di dati](../../../connect/jdbc/updating-large-data-sample.md), o [unwrap (metodo) &#40; SQLServerCallableStatement &#41; ](../../../connect/jdbc/reference/unwrap-method-sqlservercallablestatement.md).  
  
 Per ulteriori informazioni, vedere [wrapper e interfacce](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo isWrapperFor &#40; SQLServerStatement &#41;](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md)   
 [Membri di SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
