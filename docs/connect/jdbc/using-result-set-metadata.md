---
title: Utilizzo Set di risultati metadati | Documenti Microsoft
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
ms.assetid: 5e37529a-30db-48c8-b90a-ae9657d0f6b0
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d0753963363939c4ae5447d57859bc1d96fcb367
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/18/2017
---
# <a name="using-result-set-metadata"></a>Utilizzo dei metadati del set di risultati
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Eseguire una query di un set di risultati per informazioni sulle colonne in esso contenuti, il [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] implementa il [SQLServerResultSetMetaData](../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md) classe. Questa classe contiene vari metodi che restituiscono informazioni sotto forma di singolo valore.  
  
 Per creare un oggetto SQLServerResultSetMetaData, è possibile utilizzare il [getMetaData](../../connect/jdbc/reference/getmetadata-method-sqlserverresultset.md) metodo il [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) classe.  
  
 Nell'esempio seguente, una connessione aperta per la [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] database di esempio viene passato alla funzione, il metodo getMetaData della classe SQLServerResultSet viene utilizzato per restituire un oggetto SQLServerResultSetMetaData e quindi vari metodi del Oggetto SQLServerResultSetMetaData consentono di visualizzare informazioni sul tipo di nome e i dati delle colonne contenute nel set di risultati.  
  
 [!code[JDBC#UsingResultSetMetaData1](../../connect/jdbc/codesnippet/Java/using-result-set-metadata_1.java)]  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione dei metadati con il driver JDBC](../../connect/jdbc/handling-metadata-with-the-jdbc-driver.md)  
  
  
