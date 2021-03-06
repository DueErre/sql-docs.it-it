---
title: Ottimizzazione delle prestazioni per i server di pubblicazione Oracle | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Oracle publishing [SQL Server replication], performance tuning
ms.assetid: 32c0b4ec-c166-45a3-b41e-38a30fd56813
caps.latest.revision: "34"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 48afc3f5b4123b4a08b4be4ffe248a01dbd10461
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/18/2018
---
# <a name="performance-tuning-for-oracle-publishers"></a>Ottimizzazione delle prestazioni per i server di pubblicazione Oracle
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] L'architettura di pubblicazione Oracle è simile all'architettura di pubblicazione di [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], pertanto per ottimizzare le prestazioni della replica è necessario innanzitutto seguire le indicazioni generali disponibili in [Migliorare le prestazioni generali della replica](../../../relational-databases/replication/administration/enhance-general-replication-performance.md).  
  
 Sono inoltre disponibili due opzioni per i server di pubblicazione Oracle relative alle prestazioni:  
  
-   Impostazione dell'opzione di pubblicazione appropriata: Oracle o Oracle Gateway.  
  
-   Configurazione del processo del set di transazioni in modo che le modifiche vengano elaborate sul server di pubblicazione a intervalli appropriati.  
  
## <a name="specifying-the-appropriate-publishing-option"></a>Impostazione dell'opzione di pubblicazione appropriata  
 L'opzione Oracle Gateway offre prestazioni migliori rispetto all'opzione Oracle Complete, ma non è possibile utilizzarla per pubblicare la stessa tabella in più pubblicazioni transazionali. Una tabella può essere visualizzata al massimo in una pubblicazione transazionale e in qualsiasi numero di pubblicazioni snapshot. Se è necessario pubblicare la stessa tabella in più pubblicazioni transazionali, scegliere l'opzione Oracle Complete. Specificare questa opzione quando si identifica il server di pubblicazione Oracle nel server di distribuzione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Per altre informazioni, vedere [Create a Publication from an Oracle Database](../../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md).  
  
## <a name="configuring-the-transaction-set-job"></a>Configurazione del processo del set di transazioni  
 Le modifiche apportate alle tabelle Oracle pubblicate vengono elaborate in gruppi definiti set di transazioni. Per garantire la consistenza transazionale, viene eseguito il commit di ogni set di transazioni come una singola transazione nel database di distribuzione. Se le dimensioni del set di transazioni diventano eccessive, non sarà possibile elaborarlo in modo efficiente come una singola transazione.  
  
 Per impostazione predefinita, i set di transazioni vengono creati solo dall'agente di lettura log. Se durante i periodi di elevata attività di modifica l'agente di lettura log non viene eseguito o non è in grado di stabilire una connessione dal server di distribuzione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] al server di pubblicazione Oracle, i set di transazioni possono raggiungere dimensioni ingestibili. Per evitare questo problema, verificare che i set di transazioni vengano creati a intervalli regolari, anche se l'agente di lettura log non viene eseguito o non è in grado di stabilire una connessione dal server di pubblicazione Oracle.  
  
 I set di transazioni possono essere creati tramite il processo Xactset, un processo del database Oracle installato dalla replica, che utilizza lo stesso meccanismo adottato dall'agente di lettura log per creare i set. Ogni volta che il processo viene eseguito, viene creata una nuova transazione. Alla successiva esecuzione dell'agente di lettura log vengono elaborati tutti i set creati. Se dopo l'elaborazione di tutti i set di transazioni esistenti risultano ancora modifiche in sospeso, l'agente di lettura log crea ed elabora uno o più set di transazioni aggiuntivi.  
  
 Per configurare il processo del set di transazioni, vedere [Configurare il processo del set di transazioni per un server di pubblicazione Oracle &#40;programmazione Transact-SQL della replica&#41;](../../../relational-databases/replication/administration/configure-the-transaction-set-job-for-an-oracle-publisher.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare un server di pubblicazione Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Oracle Publishing Overview](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  
