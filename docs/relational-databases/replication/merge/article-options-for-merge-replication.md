---
title: Opzioni degli articoli per la replica di tipo merge | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- merge replication [SQL Server replication], article options
- articles [SQL Server replication], merge replication options
ms.assetid: 670abd41-d204-4cd7-a371-7664e603a0ce
caps.latest.revision: "37"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2ddef0bdc5d08fadc7d232417ffc7579671e8c2c
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/18/2018
---
# <a name="article-options-for-merge-replication"></a>Opzioni degli articoli per la replica di tipo merge
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Sono disponibili diverse opzioni per gli articoli di tabella di merge che consentono di adattare il comportamento della replica alle esigenze delle applicazioni. La replica di tipo merge consente di eseguire le operazioni seguenti:  
  
-   Utilizzare filtri di riga, join e di colonna. L'applicazione di filtri agli articoli di una tabella consente di creare partizioni di dati da pubblicare. Per altre informazioni, vedere [Filtrare i dati pubblicati](../../../relational-databases/replication/publish/filter-published-data.md).  
  
-   Specificare se le modifiche del Sottoscrittore vengono caricate nel server di Pubblicazione. Per le applicazioni in cui è necessario che alcuni o tutti i dati siano di sola lettura nel Sottoscrittore, gli articoli di solo download sono vantaggiosi in termini di prestazioni. Per altre informazioni, vedere [Ottimizzare le prestazioni della replica di tipo merge con gli articoli di solo download](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md).  
  
-   Specificare che le eliminazioni di uno o più articoli non devono essere rilevate dai trigger di replica e dalle tabelle di sistema. Questa opzione può essere utile in molti scenari applicativi, inclusi quelli in cui vengono utilizzate eliminazioni batch che non richiedono una replica. Per altre informazioni, vedere [Ottimizzare le prestazioni della replica di tipo merge con il rilevamento condizionale delle eliminazioni](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-conditional-delete-tracking.md).  
  
-   Specificare l'ordine di elaborazione degli articoli per garantire che corrisponda a quello richiesto dall'applicazione. Per altre informazioni, vedere [Specificare l'ordine di elaborazione degli articoli di merge](../../../relational-databases/replication/merge/specify-the-processing-order-of-merge-articles.md).  
  
-   Specificare che i set di record correlati devono essere elaborati come unità. Per impostazione predefinita, la replica di tipo merge elabora le modifiche nelle tabelle procedendo riga per riga. Per altre informazioni, vedere [Raggruppare modifiche alle righe correlate con record logici](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).  
  
-   Utilizzare il rilevamento e la risoluzione dei conflitti per i casi in cui è possibile che gli stessi dati vengano modificati in più nodi di una topologia. Per altre informazioni, vedere [Detect and Resolve Merge Replication Conflicts](../../../relational-databases/replication/merge/advanced-merge-replication-resolve-merge-replication-conflicts.md).  
  
-   Specificare le opzioni di schema, ad esempio se i vincoli e i trigger vengono copiati nel Sottoscrittore. Per altre informazioni, vedere [Specificare le opzioni dello schema](../../../relational-databases/replication/publish/specify-schema-options.md).  
  
-   Utilizzare un gestore della logica di business in grado di rispondere a molte condizioni durante la sincronizzazione, ad esempio modifiche dei dati, conflitti ed errori. Per altre informazioni, vedere [Eseguire logiche di business durante la sincronizzazione di tipo merge](../../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Pubblicare dati e oggetti di database](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
