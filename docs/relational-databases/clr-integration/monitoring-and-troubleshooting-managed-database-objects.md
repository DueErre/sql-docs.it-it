---
title: Monitoraggio e risoluzione dei problemi di oggetti di Database gestiti | Documenti Microsoft
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], performance
- monitoring [CLR integration]
- performance [CLR integration]
ms.assetid: a7b589ac-104d-4b68-b4aa-9f5fc192b13d
caps.latest.revision: "18"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 488b1caaab31a06f2bff4f611e0bc1e6affada68
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/17/2017
---
# <a name="monitoring-and-troubleshooting-managed-database-objects"></a>Monitoraggio e risoluzione dei problemi relativi agli oggetti di database gestiti
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]In questo argomento vengono fornite informazioni sugli strumenti che consentono di monitorare e risolvere i problemi relativi a oggetti di database gestiti e assembly in esecuzione in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="profiler-trace-events"></a>Eventi di traccia del profiler  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] offre Traccia SQL e notifiche di eventi per monitorare gli eventi che si verificano nel Motore di database. Tramite la registrazione di eventi specificati, Traccia SQL consente di risolvere problemi relativi alle prestazioni, controllare l'attività dei database, raccogliere dati esempio per un ambiente di prova, eseguire il debug delle istruzioni e delle stored procedure di [!INCLUDE[tsql](../../includes/tsql-md.md)], nonché raccogliere dati per gli strumenti di analisi delle prestazioni. Per ulteriori informazioni, vedere [traccia SQL](../../relational-databases/sql-trace/sql-trace.md) e [degli eventi estesi](../../relational-databases/extended-events/extended-events.md).  
  
|Evento|Description|  
|-----------|-----------------|  
|[Classe di evento Assembly Load](http://msdn.microsoft.com/library/cfb0b69d-4ce0-4067-a3df-d82775e57886)|Utilizzato per monitorare le richieste di caricamento degli assembly (esito positivo ed errori).|  
|[Classe di evento SQL: BatchStarting](../../relational-databases/event-classes/sql-batchstarting-event-class.md), [la classe di evento SQL: BatchCompleted](../../relational-databases/event-classes/sql-batchcompleted-event-class.md)|Fornisce informazioni sui batch [!INCLUDE[tsql](../../includes/tsql-md.md)] avviati o completati.|  
|[SP: Starting-classe di evento](../../relational-databases/event-classes/sp-starting-event-class.md), [SP: Completed-classe di evento](../../relational-databases/event-classes/sp-completed-event-class.md)|Utilizzato per monitorare l'esecuzione di stored procedure [!INCLUDE[tsql](../../includes/tsql-md.md)].|  
|[Classe di evento SQL: StmtStarting](../../relational-databases/event-classes/sql-stmtstarting-event-class.md), [la classe di evento SQL: StmtCompleted](../../relational-databases/event-classes/sql-stmtcompleted-event-class.md)|Utilizzato per monitorare l'esecuzione di routine CLR e [!INCLUDE[tsql](../../includes/tsql-md.md)].|  
  
## <a name="performance-counters"></a>Contatori delle prestazioni  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] include oggetti e contatori utilizzabili da Monitor di sistema per il monitoraggio dell'attività in computer che eseguono un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per oggetto si intende qualsiasi risorsa di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ad esempio un blocco di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o un processo di Windows. Ogni oggetto contiene uno o più contatori che determinano diversi aspetti degli oggetti da monitorare. Per altre informazioni, vedere [Usare oggetti di SQL Server](../../relational-databases/performance-monitor/use-sql-server-objects.md).  
  
|Oggetto|Description|  
|------------|-----------------|  
|[Oggetto CLR di SQL Server](../../relational-databases/performance-monitor/sql-server-clr-object.md)|Tempo totale di esecuzione in CLR.|  
  
## <a name="windows-system-monitor-perfmonexe-counters"></a>Contatori di Monitor di sistema di Windows (PERFMON.EXE)  
 Lo strumento Monitor di sistema di Windows (PERFMON.EXE) include diversi contatori delle prestazioni che è possibile utilizzare per monitorare le applicazioni di integrazione CLR. I contatori delle prestazioni CLR .NET possono essere filtrati tramite il nome di processo "sqlservr" per tenere traccia delle applicazioni di integrazione CLR attualmente in esecuzione.  
  
|Oggetto prestazione|Description|  
|------------------------|-----------------|  
|SqlServer:CLR|Fornisce statistiche sulla CPU per il server.|  
|Eccezioni CLR .NET|Tiene traccia del numero di eccezioni generate al secondo.|  
|Caricamento CLR .NET|Fornisce informazioni su AppDomain e assembly caricati nel server.|  
|Memoria CLR .NET|Offre informazioni relative all'utilizzo della memoria in CLR. Questo oggetto può essere utilizzato per contrassegnare gli avvisi in caso di un utilizzo eccessivo di memoria.|  
|Provider di dati .NET per SQL Server|Tiene traccia del numero di connessioni e disconnessioni eseguite al secondo. Questo oggetto può essere utilizzato per monitorare il livello di attività del database.|  
  
## <a name="catalog-views"></a>Viste del catalogo  
 Le viste del catalogo restituiscono informazioni utilizzate dal Motore di database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. È consigliabile utilizzare tali viste perché rappresentano l'interfaccia più immediata per l'accesso ai metadati del catalogo e sono inoltre lo strumento più efficiente per ottenere, trasformare e presentare tali informazioni in forme personalizzate. Tutti i metadati del catalogo disponibili per gli utenti vengono esposti tramite le viste del catalogo. Per altre informazioni, vedere [Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md).  
  
|Vista del catalogo|Description|  
|------------------|-----------------|  
|[Assemblies &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)|Restituisce informazioni sugli assembly registrati in un database.|  
|[Sys.assembly_references &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-assembly-references-transact-sql.md)|Identifica gli assembly che fanno riferimento ad altri assembly.|  
|[sys.assembly_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)|Restituisce informazioni su ogni funzione, stored procedure e trigger definito in un assembly.|  
|[assembly_files &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-assembly-files-transact-sql.md)|Restituisce informazioni sui file di assembly registrati nel database.|  
|[Sys.assembly_types &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-assembly-types-transact-sql.md)|Identifica i tipi definiti dall'utente specificati da un assembly.|  
|[Sys.module_assembly_usages &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-module-assembly-usages-transact-sql.md)|Identifica gli assembly in cui sono definiti moduli CLR.|  
|[parameter_type_usages &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-parameter-type-usages-transact-sql.md)|Restituisce informazioni sui parametri che sono tipi definiti dall'utente.|  
|[sys.server_assembly_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-assembly-modules-transact-sql.md)|Identifica l'assembly in cui è definito un trigger CLR.|  
|[sys.server_triggers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-triggers-transact-sql.md)|Identifica i trigger DLL a livello di server, inclusi i trigger CLR.|  
|[Sys.type_assembly_usages &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-type-assembly-usages-transact-sql.md)|Identifica gli assembly in cui sono specificati tipi definiti dagli utenti.|  
|[Sys. Types &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)|Restituisce i tipi di sistema e definiti dall'utente registrati nel database.|  
  
## <a name="dynamic-management-views"></a>DMV  
 Le funzioni e le viste a gestione dinamica restituiscono informazioni sullo stato del server che possono essere utilizzate per monitorare l'integrità di un'istanza del server, diagnosticare i problemi e ottimizzare le prestazioni. Per ulteriori informazioni, vedere [funzioni e viste a gestione dinamica &#40; Transact-SQL &#41; ](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md).  
  
|Vista a gestione dinamica|Description|  
|---------|-----------------|  
|[Sys.dm clr_appdomains &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-clr-appdomains-transact-sql.md)|Fornisce informazioni su ogni dominio applicazione nel server.|  
|[Sys.dm clr_loaded_assemblies &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql.md)|Identifica ogni assembly gestito registrato nel server.|  
|[Sys.dm clr_properties &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-clr-properties-transact-sql.md)|Restituisce informazioni relative al CLR hosted.|  
|[Sys.dm clr_tasks &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-clr-tasks-transact-sql.md)|Identifica tutte le attività CLR attualmente in esecuzione.|  
|[Sys.dm exec_cached_plans &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)|Restituisce informazioni sui piani di esecuzione di query memorizzati nella cache da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per accelerare l'esecuzione di query.|  
|[sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)|Restituisce dati statistici aggregati sulle prestazioni dei piani di query memorizzati nella cache.|  
|[Sys.dm exec_requests &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)|Restituisce informazioni su ciascuna richiesta in esecuzione all'interno di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Sys.dm os_memory_clerks &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)|Restituisce tutti i clerk di memoria attivi nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], inclusi i clerk di memoria CLR.|  
  
## <a name="see-also"></a>Vedere anche  
 [Concetti relativi alla programmazione dell'integrazione con CLR &#40;Common Language Runtime&#41;](../../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md)  
  
  