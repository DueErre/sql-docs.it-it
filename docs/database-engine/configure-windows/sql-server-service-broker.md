---
title: SQL Server Service Broker | Microsoft Docs
ms.custom: 
ms.date: 08/01/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL13.SWB.SSBMSGTYPEPROPERTIES.GENERAL.F1
- SQL13.SWB.SSBCONTRACTPROPERTIES.GENERAL.F1
- SQL13.SWB.SSBQUEUEPROPERTIES.GENERAL.F1
- SQL13.SWB.SSBREMSVCBINDPROPERTIES.GENERAL.F1
- SQL13.SWB.SSBROUTEPROPERTIES.GENERAL.F1
- SQL13.SWB.SSBPRIORITYPROPERTIES.GENERAL.F1
- SQL13.SWB.SSBSERVICEPROPERTIES.GENERAL.F1
helpviewer_keywords:
- Broker See Service Broker
- SQL Server Service Broker
- Service Broker
ms.assetid: 8b8b3b57-fd46-44de-9a4e-e3a8e3999c1e
caps.latest.revision: "22"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Active
ms.openlocfilehash: 20407c3b614ed6e977e2ba69ba687b75f7d18fdf
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/18/2018
---
# <a name="sql-server-service-broker"></a>SQL Server Service Broker
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSB](../../includes/sssb-md.md)] include il supporto nativo per le applicazioni di messaggistica e accodamento nel [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Questa caratteristica semplifica il lavoro degli sviluppatori per creare applicazioni complesse che utilizzano i componenti di [!INCLUDE[ssDE](../../includes/ssde-md.md)] per comunicare tra database diversi. Gli sviluppatori possono utilizzare [!INCLUDE[ssSB](../../includes/sssb-md.md)] per compilare con facilità applicazioni distribuite e affidabili.  
  
 Gli sviluppatori di applicazioni che utilizzano [!INCLUDE[ssSB](../../includes/sssb-md.md)] possono distribuire il carico di lavoro su più database senza programmare interni di comunicazione e messaggistica complessi. In questo modo, è possibile ottenere una riduzione delle attività di sviluppo e test, in quanto [!INCLUDE[ssSB](../../includes/sssb-md.md)] gestisce i percorsi di comunicazione nel contesto di una conversazione, con conseguente miglioramento delle prestazioni. Ad esempio, i database front-end che supportano i siti Web possono registrare le informazioni e mettere in coda le attività con molti processi nei database back-end. [!INCLUDE[ssSB](../../includes/sssb-md.md)] si assicura che tutte le attività vengano gestite nel contesto delle transazioni per garantire affidabilità e coerenza tecnica.  
  
## <a name="where-is-the-documentation-for-service-broker"></a>Dove si trova la documentazione per Service Broker?  
 La documentazione di riferimento per [!INCLUDE[ssSB](../../includes/sssb-md.md)] è inclusa nella documentazione di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Nella documentazione di riferimento sono incluse le sezioni seguenti:  
  
-   [Istruzioni Data Definition Language &#40;DDL&#41; &#40;Transact-SQL&#41;](~/mdx/mdx-data-definition-statements-mdx.md) per istruzioni CREATE, ALTER e DROP  
  
-   [Istruzioni di Service Broker](../../t-sql/statements/service-broker-statements.md)  
  
-   [Viste del catalogo di Service Broker &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/service-broker-catalog-views-transact-sql.md)  
  
-   [Viste a gestione dinamica relative a Service Broker &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/service-broker-related-dynamic-management-views-transact-sql.md)  
  
-   [Utilità ssbdiagnose &#40;Service Broker&#41;](../../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md)  
  
 Vedere la [documentazione pubblicata in precedenza](http://go.microsoft.com/fwlink/?LinkId=231312) per i concetti relativi a [!INCLUDE[ssSB](../../includes/sssb-md.md)] e per le attività di gestione e sviluppo. Questa documentazione non è riprodotta nella documentazione di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] a causa del numero esiguo di modifiche in [!INCLUDE[ssSB](../../includes/sssb-md.md)] in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
## <a name="whats-new-in-service-broker"></a>Novità di Service Broker  
 Non è stata introdotta alcuna modifica significativa in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  In [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]sono state introdotte le modifiche riportate di seguito.  
  
### <a name="messages-can-be-sent-to-multiple-target-services-multicast"></a>È possibile inviare messaggi a più servizi di destinazione (multicast)  
 La sintassi dell'istruzione [SEND &#40;Transact-SQL&#41;](../../t-sql/statements/send-transact-sql.md) è stata estesa per abilitare il multicast supportando più handle di conversazione.  
  
### <a name="queues-expose-the-message-enqueued-time"></a>Le code espongono il tempo di accodamento del messaggio  
 Le code dispongono di una nuova colonna, **message_enqueue_time**in cui è indicato il tempo di accodamento di un messaggio.  
  
### <a name="poison-message-handling-can-be-disabled"></a>La gestione dei messaggi non elaborabili può essere disabilitata  
 Tramite le istruzioni [CREATE QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/create-queue-transact-sql.md) e [ALTER QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-queue-transact-sql.md) è possibile abilitare o disabilitare la gestione dei messaggi non elaborabili aggiungendo la clausola, `POISON_MESSAGE_HANDLING (STATUS = ON | OFF)`. La vista del catalogo **sys.service_queues** contiene ora la colonna **is_poison_message_handling_enabled** per indicare se il messaggio non elaborabile è abilitato o disabilitato.  
  
### <a name="always-on-support-in-service-broker"></a>Supporto Always On in Service Broker  
 Per altre informazioni, vedere [Service Broker con i gruppi di disponibilità Always On (SQL Server)](../../database-engine/availability-groups/windows/service-broker-with-always-on-availability-groups-sql-server.md).  
  
  

