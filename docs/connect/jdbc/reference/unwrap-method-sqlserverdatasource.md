---
title: Metodo Unwrap (SQLServerDataSource) | Documenti Microsoft
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
ms.assetid: eb8abe29-f3ec-4752-a590-1d5dc3e48f08
caps.latest.revision: "19"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2d3519e11a7fb461e444525ea827908e0929dab1
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/18/2017
---
# <a name="unwrap-method-sqlserverdatasource"></a>Metodo unwrap (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Restituisce un oggetto che implementa l'interfaccia specificata per consentire l'accesso per il [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]-metodi specifici.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public <T> T unwrap(Class<T> iface)  
```  
  
#### <a name="parameters"></a>Parametri  
 *iface*  
  
 Classe di tipo T che definisce un'interfaccia.  
  
## <a name="return-value"></a>Valore restituito  
 Oggetto che implementa l'interfaccia specificata.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Il [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverdatasource.md) metodo è definito dall'interfaccia Java.SQL, introdotta nella specifica JDBC 4.0.  
  
 Potrebbe essere necessario accedere alle estensioni dell'API JDBC siano per le applicazioni di [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]. Il metodo unwrap supporta l'annullamento del wrapping classi pubbliche che consente di estendere l'oggetto se le classi espongono estensioni del fornitore.  
  
 Quando questo metodo viene chiamato, l'oggetto Annulla il wrapping di [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) classe.  
  
 Per ulteriori informazioni, vedere [wrapper e interfacce](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo isWrapperFor &#40; SQLServerDataSource &#41;](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverdatasource.md)   
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
