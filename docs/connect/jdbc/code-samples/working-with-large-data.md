---
title: Utilizzo di dati di grandi dimensioni | Documenti Microsoft
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
ms.assetid: 5b93569f-eceb-4f05-b49c-067564cd3c85
caps.latest.revision: "24"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.openlocfilehash: c8195decee231a628599e42d2f44109ff0452ed8
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/18/2017
---
# <a name="working-with-large-data"></a>Utilizzo di dati di grandi dimensioni
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Il driver JDBC fornisce supporto per la memorizzazione nel buffer adattiva, che consente di recuperare qualsiasi tipo di dati con valori di grandi dimensioni senza l'overhead dei cursori server. Con il buffer adattivo il [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] recupera i risultati dell'esecuzione di istruzioni dal [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] come questi sono necessari per l'applicazione, anziché tutti contemporaneamente. Quando l'applicazione non necessita più di accedere ai dati, questi vengono inoltre eliminati dal driver.  
  
 Nel [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005_md.md)] JDBC Driver versione 1.2, la modalità di buffer è "**completo**" per impostazione predefinita. Se l'applicazione non imposta la proprietà di connessione "responseBuffering" "**adattivo**" nelle proprietà di connessione o utilizzando il [setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) metodo il [ SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) oggetto, il driver supportata la lettura dell'intero risultato dal server in una sola volta. Per ottenere il comportamento di memorizzazione nel buffer adattivo, l'applicazione era necessario impostare la proprietà di connessione "responseBuffering" su "**adattivo**" in modo esplicito.  
  
 Il **adattivo** è il valore predefinito modalità di buffering e il driver JDBC memorizza nel buffer di dati minima possibile quando necessario. Per ulteriori informazioni sull'utilizzo del buffer adattivo, vedere [utilizzando il buffer adattivo](../../../connect/jdbc/using-adaptive-buffering.md).  
  
 Negli argomenti di questa sezione vengono descritti diversi modi in cui è possibile utilizzare per recuperare i dati di valori di grandi dimensioni da un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] database.  
  
## <a name="in-this-section"></a>Argomenti della sezione  
  
|Argomento|Description|  
|-----------|-----------------|  
|[Esempio di lettura di dati di grandi dimensioni](../../../connect/jdbc/reading-large-data-sample.md)|Descrive come utilizzare un'istruzione SQL per recuperare dati per valori di grandi dimensioni.|  
|[Esempio di lettura di dati di grandi dimensioni con una stored procedure](../../../connect/jdbc/reading-large-data-with-stored-procedures-sample.md)|Descrive come recuperare un valore del parametro OUT CallableStatement di grandi dimensioni.|  
|[Esempio di aggiornamento di dati di grandi dimensioni](../../../connect/jdbc/updating-large-data-sample.md)|Descrive come aggiornare dati per valori di grandi dimensioni in un database.|  
  
## <a name="see-also"></a>Vedere anche  
 [Applicazioni di esempio del driver JDBC](../../../connect/jdbc/sample-jdbc-driver-applications.md)  
  
  
