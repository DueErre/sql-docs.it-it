---
title: Metodo setAsciiStream (int, Java.IO. InputStream, long) | Documenti Microsoft
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
ms.assetid: 9dfa7781-d72f-407a-a8d4-1c78c9446d09
caps.latest.revision: "22"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c87f1df8edce144e50e030f35640e95f09c8e5f6
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/18/2017
---
# <a name="setasciistream-method-int-javaioinputstream-long"></a>Metodo setAsciiStream (int, java.io.InputStream, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Imposta il numero del parametro designato sull'oggetto java.IO. InputStream specificato con il numero specificato di byte.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public final void setAsciiStream(int parameterIndex,  
                                 java.io.InputStream x,  
                                    long length)  
```  
  
#### <a name="parameters"></a>Parametri  
 *parameterIndex*  
  
 Un **int** che indica il numero di parametro.  
  
 *x*  
  
 Un oggetto java.IO. InputStream.  
  
 *length*  
  
 Oggetto **lungo** che indica il numero di byte.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo setAsciiStream viene specificato dal metodo setAsciiStream nell'interfaccia Java.SQL. PreparedStatement.  
  
 Se la lunghezza del flusso è diversa rispetto a quello specificato nel *lunghezza* parametro, il driver JDBC genera un'eccezione quando viene inserita o aggiornata la riga.  
  
 Se la lunghezza del flusso è sconosciuta, il *lunghezza* parametro può essere impostato su -1 per indicare che il driver deve accettare il flusso indipendentemente dalla lunghezza. Con sqljdbc4.jar, si consiglia di utilizzare il metodo di JDBC 4.0 [setAsciiStream metodo &#40; int, Java.IO. InputStream &#41;](../../../connect/jdbc/reference/setasciistream-method-int-java-io-inputstream.md) quando l'applicazione deve aggiornare la colonna da un flusso la cui lunghezza è sconosciuta.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo setAsciiStream &#40; SQLServerPreparedStatement &#41;](../../../connect/jdbc/reference/setasciistream-method-sqlserverpreparedstatement.md)   
 [Membri di SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  
