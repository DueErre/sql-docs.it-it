---
title: SQLGetConnectAttr | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-api
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apitype: DLLExport
helpviewer_keywords: SQLGetConnectAttr function
ms.assetid: 26e4e69a-44fd-45e3-b47a-ae39184f041b
caps.latest.revision: "60"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4a075d06b4425a5f07e3e805fdefe73b1c5eabba
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/24/2018
---
# <a name="sqlgetconnectattr"></a>SQLGetConnectAttr
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Il driver ODBC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client definisce gli attributi di connessione specifici del driver. Alcuni degli attributi sono disponibili per **SQLGetConnectAttr**, e la funzione viene utilizzata per segnalare le relative impostazioni correnti. I valori segnalati per questi attributi sono garantiti solo dopo che è stata stabilita una connessione o l'attributo è stato impostato utilizzando [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md).  
  
 In questo argomento sono elencati gli attributi di sola lettura. Per informazioni sulle altre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gli attributi di connessione specifici del driver ODBC di Native Client, vedere [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md).  
  
## <a name="sqlcoptssconnectiondead"></a>SQL_COPT_SS_CONNECTION_DEAD  
 L'attributo SQL_COPT_SS_CONNECTION_DEAD consente di segnalare lo stato di una connessione a un server. Il driver esegue query sulla rete al fine di individuare lo stato corrente della connessione.  
  
> [!NOTE]  
>  L'attributo di connessione ODBC standard SQL_COPT_SS_CONNECTION_DEAD restituisce lo stato più recente della connessione. Tale stato potrebbe non essere quello corrente.  
  
|Valore|Description|  
|-----------|-----------------|  
|SQL_CD_TRUE|La connessione al server è stata persa.|  
|SQL_CD_FALSE|La connessione è aperta e disponibile per l'elaborazione di istruzioni.|  
  
## <a name="sqlcoptssclientconnectionid"></a>SQL_COPT_SS_CLIENT_CONNECTION_ID  
 L'attributo SQL_COPT_SS_CLIENT_CONNECTION_ID consente di recuperare l'ID di connessione client che può essere utilizzato per individuare:  
  
-   Informazioni di diagnostica nel registro XEvents, se abilitato.  
  
-   Informazioni sull'errore di connessione nel buffer circolare della connessione.  
  
-   Informazioni di diagnostica nei registri di traccia di accesso ai dati, se abilitati.  
  
 Per ulteriori informazioni, vedere [l'accesso a informazioni di diagnostica nel Log degli eventi estesi](../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md).  
  
|Valore|Description|  
|-----------|-----------------|  
|SQL_ERROR|Connessione non riuscita.|  
|SQL_SUCCESS|Connessione attivata. L'ID di connessione client verrà trovato nel buffer di output.|  
  
## <a name="sqlcoptssperfdata"></a>SQL_COPT_SS_PERF_DATA  
 Tramite l'attributo SQL_COPT_SS_PERF_DATA viene restituito un puntatore a una struttura SQLPERF contenente le statistiche correnti sulle prestazioni del driver. **SQLGetConnectAttr** restituirà NULL se non è abilitata la registrazione delle prestazioni. Le statistiche nella struttura SQLPERF non vengono aggiornate in modo dinamico dal driver. Chiamare **SQLGetConnectAttr** ogni volta che devono essere aggiornate le statistiche sulle prestazioni.  
  
|Valore|Description|  
|-----------|-----------------|  
|NULL|La registrazione delle prestazioni non è abilitata.|  
|Qualsiasi altro valore|Puntatore a una struttura SQLPERF.|  
  
## <a name="sqlcoptssperfquery"></a>SQL_COPT_SS_PERF_QUERY  
 L'attributo SQL_COPT_SS_PERF_QUERY restituisce TRUE se è abilitata la registrazione di query con esecuzione prolungata. La richiesta restituisce FALSE se la registrazione delle query non è attiva.  
  
## <a name="sqlcoptssuserdata"></a>SQL_COPT_SS_USER_DATA  
 L'attributo SQL_COPT_SS_USER_DATA recupera il puntatore ai dati utente. I dati utente vengono archiviati nella memoria del client e registrati per singola connessione. Se il puntatore ai dati utente SQL_UD_NOTSET non è stato impostato, viene restituito un puntatore NULL.  
  
|Valore|Description|  
|-----------|-----------------|  
|SQL_UD_NOTSET|Non è impostato alcun puntatore ai dati utente.|  
|Qualsiasi altro valore|Puntatore ai dati utente.|  
  
## <a name="sqlgetconnectattr-support-for-service-principal-names-spns"></a>Supporto di SQLSetConnectAttr per i nomi SPN (Service Principal Names)  
 SQLGetConnectAttr utilizzabile per interrogare il valore dei nuovi attributi di connessione SQL_COPT_SS_SERVER_SPN, SQL_COPT_SS_FAILOVER_PARTNER_SPN, SQL_COPT_SS_MUTUALLY_AUTHENTICATED e SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD. (SQLGetConnectOption anche utilizzabile per eseguire una query questi valori.)  
  
 SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD è disponibile solo per connessioni aperte che utilizzano l'autenticazione di Windows.  
  
 Se non è stato impostato SQL_COPT_SS_SERVER_SPN o SQL_COPT_SS_FAILOVER_PARTNER, viene restituito il valore predefinito (una stringa vuota).  
  
 Per ulteriori informazioni sui nomi SPN, vedere [nomi dell'entità servizio &#40; I nomi SPN &#41; le connessioni Client &#40; ODBC &#41; ](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Funzione SQLGetConnectAttr](http://go.microsoft.com/fwlink/?LinkId=59347)   
 [Dettagli di implementazione di API ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)   
 [SET QUOTED_IDENTIFIER &#40; Transact-SQL &#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)   
 [SET ANSI_NULLS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md)   
 [SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)   
 [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md)  
  
  
