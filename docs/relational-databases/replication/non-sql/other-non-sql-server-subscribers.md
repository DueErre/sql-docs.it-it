---
title: Altri Sottoscrittori non SQL Server | Microsoft Docs
ms.custom: 
ms.date: 03/08/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: non-SQL Server Subscribers, other types
ms.assetid: 96b8beb9-38e8-4ce4-97ca-c0f8656b73b4
caps.latest.revision: "31"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 035bddbc96126c98d48ac599db9307f565f1d38a
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/18/2018
---
# <a name="other-non-sql-server-subscribers"></a>Altri Sottoscrittori non SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Per un elenco di Sottoscrittori non [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] supportati da [!INCLUDE[msCoName](../../../includes/msconame-md.md)], vedere [Sottoscrittori non SQL Server](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md). In questo argomento vengono fornite informazioni sui requisiti per i driver ODBC e i provider OLE DB.  
  
## <a name="odbc-driver-requirements"></a>Requisiti per i driver ODBC  
 Il driver ODBC deve soddisfare i requisiti seguenti:  
  
-   Deve essere conforme a ODBC di livello 1.  
  
-   Deve essere un ambiente di distribuzione thread-safe.  
  
-   Deve essere in grado di eseguire transazioni.  
  
-   Deve supportare il linguaggio DDL (Data Definition Language).  
  
-   Non può essere di sola lettura.  
  
-   Deve supportare nomi di tabella lunghi, ad esempio **MSreplication_subscriptions**.  
  
## <a name="replicating-using-ole-db-interfaces"></a>Esecuzione della replica tramite interfacce OLE DB  
 Per la replica transazionale i provider OLE DB devono supportare gli oggetti seguenti:  
  
-   **DataSource**  
  
-   **Session**  
  
-   **Command**  
  
-   **Rowset**  
  
-   **Error**  
  
### <a name="datasource-object-interfaces"></a>Interfacce per oggetti DataSource  
 Per la connessione a un'origine dei dati sono necessarie le interfacce seguenti:  
  
-   **IDBInitialize**  
  
-   **IDBCreateSession**  
  
-   **IDBProperties**  
  
 Se il provider supporta l'interfaccia **IDBInfo** , tale interfaccia viene utilizzata in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per il recupero di informazioni quali l'identificatore tra virgolette, la lunghezza massima delle istruzioni SQL e il numero massimo di caratteri nei nomi delle colonne e delle tabelle.  
  
### <a name="session-object-interfaces"></a>Interfacce per oggetti Session  
 Sono necessarie le interfacce seguenti:  
  
-   **IDBCreateCommand**  
  
-   **ITransaction**  
  
-   **ITransactionLocal**  
  
-   **IDBSchemaRowset**  
  
### <a name="command-object-interfaces"></a>Interfacce per oggetti Command  
 Sono necessarie le interfacce seguenti:  
  
-   **ICommand**  
  
-   **ICommandProperties**  
  
-   **ICommandText**  
  
-   **ICommandPrepare**  
  
-   **IColumnsInfo**  
  
-   **IAccessor**  
  
-   **ICommandWithParameters**  
  
 L'interfaccia**IAccessor** è necessaria per la creazione di funzioni di accesso ai parametri. Se il provider supporta l'interfaccia **IColumnRowset**, tale interfaccia viene utilizzata in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per determinare se una colonna è di tipo Identity.  
  
### <a name="rowset-object-interfaces"></a>Interfacce per oggetti Rowset  
 Sono necessarie le interfacce seguenti:  
  
-   **IRowset**  
  
-   **IAccessor**  
  
-   **IColumnsInfo**  
  
 In un'applicazione può essere necessario aprire un set di righe di una tabella replicata creata nel database di sottoscrizione. Le interfacce**IColumnsInfo** e **IAccessor** consentono di accedere ai dati del set di righe.  
  
### <a name="error-object-interfaces"></a>Interfacce per oggetti Error  
 Per la gestione degli errori, utilizzare le interfacce seguenti:  
  
-   **IErrorRecords**  
  
-   **IErrorInfo**  
  
 Utilizzare l'interfaccia **ISQLErrorInfo** se è supportata dal provider OLE DB.  
  
 Per ulteriori informazioni sul provider OLE DB, vedere la relativa documentazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Non-SQL Server Subscribers](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)  
  
  
