---
title: Metodo (Java.IO. InputStream, long) updateBinaryStream | Documenti Microsoft
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
ms.assetid: d3c0fb5d-ca05-43f7-9f38-fba6cf3705c6
caps.latest.revision: "18"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0abd8f96e0c289520433f1c8d15a5b64ba73b66c
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/18/2017
---
# <a name="updatebinarystream-method-javalangstring-javaioinputstream-long"></a>Metodo updateBinaryStream (java.lang.String, java.io.InputStream, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Aggiorna la colonna designata con un valore del flusso binario, che conterrà il numero specificato di byte.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void updateBinaryStream(java.lang.String columnLabel,  
                               java.io.InputStream x,  
                               long length)  
```  
  
#### <a name="parameters"></a>Parametri  
 *columnLabel*  
  
 AStringthat contiene l'etichetta di colonna.  
  
 *x*  
  
 Un oggetto InputStream.  
  
 *length*  
  
 Oggetto **lungo** che indica la lunghezza del flusso.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo updateBinaryStream viene specificato dal metodo updateBinaryStream nell'interfaccia Java.SQL. ResultSet.  
  
 Questo metodo passa byte da un oggetto InputStream selezionare [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] colonne binarie quali binary, varbinary, varbinary (max), image, xml e udt. L'aggiornamento delle colonne di tipo carattere non è supportato con questo metodo. Per aggiornare colonne di tipo carattere con un InputStream, utilizzare il [updateAsciiStream](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md) metodo.  
  
 Se la lunghezza del flusso è diversa rispetto a quello specificato nel *lunghezza* parametro, il driver JDBC genera un'eccezione quando viene inserita o aggiornata la riga.  
  
 Se la lunghezza del flusso è sconosciuta, il *lunghezza* parametro può essere impostato su -1 per indicare che il driver deve accettare il flusso indipendentemente dalla lunghezza. Con sqljdbc4.jar, si consiglia di utilizzare il metodo di JDBC 4.0 [updateBinaryStream metodo &#40;java.lang.String, Java.IO. InputStream &#41;](../../../connect/jdbc/reference/updatebinarystream-method-java-lang-string-java-io-inputstream.md) quando l'applicazione deve aggiornare la colonna da un flusso la cui lunghezza è sconosciuto.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo updateBinaryStream &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/updatebinarystream-method-sqlserverresultset.md)   
 [Membri di SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
