---
title: Utilizzo di un'istruzione SQL per modificare dati | Documenti Microsoft
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
ms.assetid: 4704199b-c0ae-4c77-8a2e-6963715b4ffb
caps.latest.revision: "17"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 27923be2ebcb56c79dc08ecec1fc1b27de7c04a3
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/18/2017
---
# <a name="using-an-sql-statement-to-modify-data"></a>Utilizzo di un'istruzione SQL per modificare i dati
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Per modificare i dati contenuti in un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] database utilizzando un'istruzione SQL, è possibile utilizzare il [executeUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md) metodo il [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) classe. Il metodo executeUpdate verrà passerà l'istruzione SQL al database per l'elaborazione e quindi restituire un valore che indica il numero di righe interessate.  
  
 A tale scopo, è innanzitutto necessario creare un oggetto SQLServerStatement utilizzando il [createStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md) metodo il [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) classe.  
  
 Nell'esempio seguente, una connessione aperta per la [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] database di esempio viene passato alla funzione, viene costruita un'istruzione SQL che consente di aggiungere nuovi dati alla tabella, quindi viene eseguita l'istruzione e viene visualizzato il valore restituito.  
  
 [!code[JDBC#UsingSQLToModifyData1](../../connect/jdbc/codesnippet/Java/using-an-sql-statement-t_1_1.java)]  
  
> [!NOTE]  
>  Se è necessario utilizzare un'istruzione SQL che contiene i parametri per modificare i dati in un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] database, è consigliabile utilizzare il [executeUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverpreparedstatement.md) metodo il [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) classe.  
>   
>  Se nella colonna in cui si desidera inserire i dati sono presenti caratteri speciali, quali, ad esempio, gli spazi, è necessario fornire i valori da inserire, anche se si tratta dei valori predefiniti. In caso contrario, l'operazione di inserimento non verrà eseguita correttamente.  
>   
>  Se si desidera che il driver JDBC restituisca tutti i conteggi degli aggiornamenti, inclusi i conteggi degli aggiornamenti restituiti dai trigger eventualmente attivati, impostare la proprietà della stringa di connessione lastUpdateCount su "false". Per ulteriori informazioni sulla proprietà lastUpdateCount, vedere [impostando le proprietà di connessione](../../connect/jdbc/setting-the-connection-properties.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Uso di istruzioni con SQL](../../connect/jdbc/using-statements-with-sql.md)  
  
  
