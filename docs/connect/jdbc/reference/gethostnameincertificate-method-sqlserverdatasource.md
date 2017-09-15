---
title: Metodo getHostNameInCertificate (SQLServerDataSource) | Documenti Microsoft
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
- getHostNameInCertificate Method (SQLServerDataSource)
apilocation:
- getHostNameInCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 45ea04e2-9ea5-4171-9136-d09f8a95e128
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d74305f9c389da375a26bf0516f577939b50f7e9
ms.contentlocale: it-it
ms.lasthandoff: 09/09/2017

---
# <a name="gethostnameincertificate-method-sqlserverdatasource"></a>Metodo getHostNameInCertificate (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Restituisce il nome host utilizzato per la convalida del certificato SSL (Secure Sockets Layer) di SQL Server.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public java.lang.String getHostNameInCertificate()  
```  
  
## <a name="return-value"></a>Valore restituito  
 Oggetto **stringa** che contiene l'host del nome, o null se è impostato alcun valore.  
  
## <a name="remarks"></a>Osservazioni  
 Il nome host viene utilizzato per la convalida del valore del certificato SSL di SQL Server quando il livello di comunicazione è crittografato tramite SSL.  
  
 Se il nome host non è impostato, il [getHostNameInCertificate](../../../connect/jdbc/reference/gethostnameincertificate-method-sqlserverdatasource.md) metodo restituisce null.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
