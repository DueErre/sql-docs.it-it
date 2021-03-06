---
title: Sottoscrizioni aggiornabili | Microsoft Docs
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
f1_keywords: sql13.rep.newsubwizard.updatablesubscriptions.f1
ms.assetid: 8e9a13a0-6b24-47c6-9d83-3cbaf08f673d
caps.latest.revision: "22"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bc0506ee6e924be3d3587855e5b57d4e743a2a26
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/18/2018
---
# <a name="updatable-subscriptions"></a>Sottoscrizioni aggiornabili
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Con la replica transazionale, è consigliabile usare i dati replicati in sola lettura. È tuttavia possibile modificare i dati replicati nel Sottoscrittore [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando le sottoscrizioni aggiornabili. Se è necessario modificare i dati nel Sottoscrittore, scegliere una delle opzioni seguenti in base ai requisiti specifici.  
  
|Tipo di sottoscrizione aggiornabile|Requisiti|  
|---------------------------------|------------------|  
|Aggiornamento immediato|Per aggiornare i dati nel Sottoscrittore è necessario che il server di pubblicazione e il Sottoscrittore siano connessi.|  
|Aggiornamento in coda|Per aggiornare i dati nel Sottoscrittore non è necessario che il server di pubblicazione e il Sottoscrittore siano connessi. È possibile eseguire gli aggiornamenti in modalità offline ed eseguire in seguito la sincronizzazione tra il server di pubblicazione e il Sottoscrittore.|  
  
## <a name="options"></a>Opzioni  
 **Replica modifiche del Sottoscrittore**  
 Selezionare questa casella di controllo nella colonna **Replica** per ogni Sottoscrittore che deve essere in grado di eseguire aggiornamenti. Per i Sottoscrittori che possono eseguire aggiornamenti, selezionare l'opzione appropriata nell'elenco a discesa della colonna **Commit nel server di pubblicazione** :  
  
-   Selezionare **Commit delle modifiche simultaneo** per una sottoscrizione ad aggiornamento immediato.  
  
-   Selezionare **Accoda le modifiche ed esegui il commit appena possibile** per una sottoscrizione ad aggiornamento in coda.  
  
## <a name="see-also"></a>Vedere anche  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Subscribe to Publications](../../relational-databases/replication/subscribe-to-publications.md)   
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)  
  
  
