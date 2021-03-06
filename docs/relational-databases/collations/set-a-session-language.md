---
title: Impostare una lingua di sessione | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: collations
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- errors [SQL Server], international considerations
- globalization [SQL Server], sessions
- time [SQL Server]
- sessions [SQL Server], languages
- international considerations [SQL Server], sessions
- dates [SQL Server], session languages
- global considerations [SQL Server], sessions
- client-side session language
- time [SQL Server], session languages
- messages [SQL Server], international considerations
- server-side session language
ms.assetid: de7f2c90-8f4f-4cfc-94cc-4933a7fd2bde
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f6846c5fc1e63465c1327f8304ca512b23a580c6
ms.sourcegitcommit: 9d0467265e052b925547aafaca51e5a5e93b7e38
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/02/2018
---
# <a name="set-a-session-language"></a>Impostazione di una lingua di sessione
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
È possibile utilizzare la lingua di sessione per impostare la modalità di visualizzazione degli elementi seguenti nel server, in base a preferenze linguistiche e impostazioni locali:  
  
-   Lingua che verrà utilizzata per messaggi di errore e altri messaggi di sistema. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta più copie di tutte le stringhe di errore e dei messaggi del sistema in tutte le lingue in cui è disponibile [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Questi messaggi possono essere visualizzati nella vista del catalogo [sys.messages](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md) . Quando si installa una versione localizzata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], questi messaggi di sistema vengono tradotti nella lingua della versione installata. Per impostazione predefinita, è disponibile anche il set dei messaggi in inglese (Stati Uniti). È inoltre possibile aggiungere messaggi definiti dall'utente in una lingua specifica usando [sp_addmessage](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md).  
  
-   Il formato di data e ora.  
  
-   I nomi dei giorni e dei mesi, incluse le abbreviazioni.  
  
-   Il primo giorno della settimana.  
  
-   Le informazioni di valuta.  
  
 Sono disponibili 33 lingue per le impostazioni di sessione. Per un elenco completo, vedere [sys.syslanguages](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md).  
  
## <a name="setting-the-session-language-from-the-server"></a>Impostazione della lingua di sessione dal server  
 Per impostare la lingua di sessione dal lato server, utilizzare l'istruzione [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md).  
  
## <a name="setting-the-session-language-from-the-client"></a>Impostazione della lingua di sessione dal client  
 È possibile impostare la lingua di sessione dal client utilizzando OLE DB, ODBC o ADO.NET. Per OLE DB, utilizzare la proprietà SSPROP_INIT_CURRENTLANGUAGE. Per altre informazioni, vedere [Proprietà di inizializzazione e di autorizzazione](../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md).  
  
 Per ODBC, utilizzare la parola chiave Language. Per altre informazioni, vedere [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md).  
  
 Per ADO.NET, usare il parametro **Current Language** dell'oggetto **ConnectionString** . Per ulteriori informazioni, vedere la documentazione relativa al Software Development Kit (SDK) di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Data Access Components (MDAC).  
  
  
