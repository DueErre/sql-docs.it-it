---
title: Metodo setURL (SQLServerDataSource) | Documenti Microsoft
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
apiname: SQLServerDataSource.setURL
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: bea70100-ac98-4625-8748-ef7cc0b111ea
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 222948f40537e84e0c294f05fd8d953b61f53f65
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/18/2017
---
# <a name="seturl-method-sqlserverdatasource"></a>Metodo setURL (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Imposta l'URL utilizzato per la connessione all'origine dati.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void setURL(java.lang.String url)  
```  
  
#### <a name="parameters"></a>Parametri  
 *URL*  
  
 Oggetto **stringa** contenente l'URL.  
  
## <a name="remarks"></a>Osservazioni  
 Per motivi di sicurezza, si deve includere la password nell'URL fornito al metodo setURL. poiché nei server applicazioni Java di terze parti sarà molto spesso visualizzato il set di valori per la proprietà URL nella relativa interfaccia utente di configurazione dell'origine dati. Utilizzare invece il [setPassword](../../../connect/jdbc/reference/setpassword-method-sqlserverdatasource.md) per impostare il valore della password. Nei server applicazioni Java non sarà visualizzata una password che viene impostata nella relativa origine dati nell'interfaccia utente di configurazione.  
  
> [!NOTE]  
>  Se il metodo setURL non viene chiamato prima di chiamare il [getURL](../../../connect/jdbc/reference/geturl-method-sqlserverdatasource.md) metodo getURL restituisce il valore predefinito "JDBC: / /".  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
