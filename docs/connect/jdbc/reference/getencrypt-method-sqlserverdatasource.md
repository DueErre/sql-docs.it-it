---
title: Metodo getEncrypt (SQLServerDataSource) | Documenti Microsoft
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
apiname: getEncrypt Method (SQLServerDataSource)
apilocation: getEncrypt Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 1cdb12dd-6e6f-4bbd-8f5f-9e630f3ee2c9
caps.latest.revision: "19"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cb76a00e1fdf8b2999675bc1949e8cc06ff25d9b
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/18/2017
---
# <a name="getencrypt-method-sqlserverdatasource"></a>Metodo getEncrypt (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Restituisce un **booleano** valore che indica se la proprietà di crittografia è abilitata.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public boolean getEncypt()  
```  
  
## <a name="return-value"></a>Valore restituito  
 **true** se la crittografia è abilitata. In caso contrario, **false**.  
  
## <a name="remarks"></a>Osservazioni  
 Se la proprietà encrypt è impostata su **true**, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] assicura che [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] utilizza la crittografia SSL per tutti i dati inviati tra il client e il server se il server è installato un certificato.  
  
 Se la proprietà di crittografia non viene specificata o impostata su **false**, il driver non imporrà la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] per supportare la crittografia SSL. Se il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] istanza non è configurata per forzare la crittografia SSL, viene stabilita una connessione senza crittografia. Se il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] istanza è configurata per forzare la crittografia SSL, il [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] verrà automaticamente abilita la crittografia SSL quando eseguono correttamente configurato Java Virtual Machine (JVM), altrimenti la connessione viene terminata e il driver genera un errore. Se la proprietà di crittografia non è impostata, il [getEncrypt](../../../connect/jdbc/reference/getencrypt-method-sqlserverdatasource.md) il metodo restituisce il valore predefinito di **false**.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
