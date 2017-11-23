---
title: Libreria di cursori ODBC | Documenti Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-cursors
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- cursors [ODBC], library
- SQL_CUR_USE_DRIVER option
- ODBC applications, cursors
- ODBC cursors, library
- SQL_CUR_USE_IF_NEEDED option
- SQLSetConnectAttr function
- SQL_CUR_USE_ODBC option
ms.assetid: 3c610d3d-6e06-49cf-9a40-05b6a1c83a32
caps.latest.revision: "30"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e9d1540cab27708bfb01cb210a2f82c771de1d57
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/17/2017
---
# <a name="odbc-cursor-library"></a>Libreria di cursori ODBC
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Alcuni driver ODBC supportano solo le impostazioni di cursore predefinito. Questi driver inoltre non supportano operazioni del cursore posizionate, ad esempio **SQLSetPos**. La libreria di cursori ODBC è un componente di Microsoft Data Access Components (MDAC) utilizzato per implementare cursori a blocchi o statici in un driver che generalmente non li supporta. La libreria di cursori implementa anche le istruzioni UPDATE e DELETE posizionate e **SQLSetPos** per i cursori che crea.  
  
 La libreria di cursori ODBC viene implementata come livello tra Gestione driver ODBC e il driver ODBC. Se la libreria viene caricata, a questa, e non al driver, vengono indirizzati tutti i comandi correlati al cursore. La libreria di cursori implementa un cursore mediante il recupero dell'intero set di risultati dal driver sottostante e la memorizzazione nella cache del client del set di risultati. Quando si utilizza la libreria di cursori ODBC, nell'applicazione sono disponibili solo le funzionalità di cursore della libreria di cursori e non funzionalità di cursore aggiuntive del driver sottostante.  
  
 Con il driver ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client non esiste l'esigenza di utilizzare la libreria di cursori ODBC, in quanto il driver supporta un numero maggiore di funzionalità di cursore rispetto alla libreria. L'unico motivo per utilizzare la libreria di cursori ODBC con il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client è perché il driver implementa il supporto dei cursori tramite i cursori del server e i cursori del server non supportano tutte le istruzioni SQL. È pertanto consigliabile utilizzare la libreria di cursori ODBC ogni volta che si richiede un cursore statico con stored procedure, batch o istruzioni SQL contenenti COMPUTE, COMPUTE BY, FOR BROWSE o INTO. È tuttavia necessario prestare attenzione nell'utilizzo della libreria in quanto memorizza nella cache del client l'intero set di risultati con conseguente impiego di grandi quantità di memoria e rallentamento delle prestazioni.  
  
 Un'applicazione richiama la libreria di cursori in modo da connessioni utilizzando [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) per impostare l'attributo di connessione SQL_ATTR_ODBC_CURSORS prima della connessione a un'origine dati. L'attributo SQL_ATTR_ODBC_CURSORS può essere impostato su uno di tre valori seguenti:  
  
 SQL_CUR_USE_ODBC  
 Quando questa opzione è impostata con la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client, la libreria di cursori ODBC sostituisce il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] supporto nativo dei cursori del driver ODBC di Native Client. Solo i tipi di cursore supportati dalla libreria di cursori possono essere utilizzati per la connessione. Non è invece possibile utilizzare i cursori server a questo scopo.  
  
 SQL_CUR_USE_DRIVER  
 Quando questa opzione è impostata, tutto il cursore supporto nativo per il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC di Native Client può essere utilizzato per la connessione. Non è possibile utilizzare la libreria di cursori ODBC. Tutti i cursori vengono implementati come cursori server.  
  
 SQL_CUR_USE_IF_NEEDED  
 Quando questa opzione è impostata, l'effetto è identico SQL_CUR_USE_DRIVER se usato con il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client. In fase di connessione, gestione Driver ODBC esegue i test per verificare se il driver ODBC cui si è connessi supporta l'opzione SQL_FETCH_PRIOR di [SQLFetchScroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md). Se il driver non supporta l'opzione, Gestione driver ODBC carica la libreria di cursori ODBC. In caso contrario, Gestione driver ODBC non carica la libreria in questione e l'applicazione utilizza il supporto nativo del driver. Poiché il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client supporta SQL_FETCH_PRIOR, gestione Driver ODBC non carica la libreria di cursori ODBC.  
  
 La libreria di cursori consente alle applicazioni di utilizzare più istruzioni attive in una connessione, nonché cursori scorrevoli aggiornabili. Per il supporto di tale funzionalità è necessario caricare la libreria di cursori. Utilizzare [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) per specificare come deve essere utilizzata la libreria di cursori e [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) per specificare la dimensione di tipo, concorrenza e set di righe del cursore.  
  
## <a name="see-also"></a>Vedere anche  
 [Modalità di implementazione dei cursori](../../../relational-databases/native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)  
  
  