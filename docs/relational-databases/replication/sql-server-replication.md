---
title: Replica di SQL Server | Microsoft Docs
ms.custom: 
ms.date: 03/30/2017
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
- replication [SQL Server], about
- replication [SQL Server]
ms.assetid: 3a5f4592-3c61-4b4d-9ceb-39716aeeba41
caps.latest.revision: "58"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Active
ms.openlocfilehash: e117185264245dc5c3ed2db3a679f60d73cfa994
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/18/2018
---
# <a name="sql-server-replication"></a>Replica di SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] La replica è costituita da un set di tecnologie per la copia e la distribuzione di oggetti di database e dati da un database a un altro e dalla successiva sincronizzazione dei database allo scopo di garantirne la coerenza. Usare la replica per distribuire dati a diverse posizioni e a utenti remoti o mobili tramite reti locali e WAN, connessioni remote, connessioni wireless e Internet.  
  
 La replica transazionale viene in genere utilizzata negli scenari server-server con esigenze di elevata velocità effettiva, inclusi il miglioramento delle caratteristiche di scalabilità e disponibilità, funzionalità di data warehouse e di creazione di report, integrazione di dati da più siti, integrazione di dati eterogenei e ripartizione del carico di lavoro dell'elaborazione batch. La replica di tipo merge è principalmente progettata per le applicazioni mobili o server distribuite con possibili conflitti di dati. Tra gli scenari comuni sono inclusi lo scambio di dati con utenti mobili, applicazioni POS e integrazione di dati da più siti. La replica snapshot viene utilizzata per fornire il set di dati iniziale per la replica di tipo merge o transazionale, nonché nel caso sia necessario un aggiornamento completo dei dati. Con questi tre tipi di replica, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] costituisce un sistema potente e flessibile per la sincronizzazione dei dati aziendali. La replica in SQLCE 3.5 e SQLCE 4.0 è supportata sia in [!INCLUDE[win8srv](../../includes/win8srv-md.md)] sia in [!INCLUDE[win8](../../includes/win8-md.md)].  
  
 In alternativa alla replica, è possibile sincronizzare i database utilizzando Microsoft Sync Framework. Sync Framework include componenti e una API intuitiva e flessibile che facilitano la sincronizzazione fra i database di SQL Server, SQL Server Express, SQL Server Compact e SQL Azure. Sync Framework include anche classi che possono essere adattate per la sincronizzazione tra un database di SQL Server e un qualsiasi altro database compatibile con ADO.NET. Per la documentazione dettagliata dei componenti per la sincronizzazione di Sync Framework, vedere [Sincronizzazione di database](http://go.microsoft.com/fwlink/?LinkId=209079). Per una panoramica su Sync Framework, vedere la pagina relativa al [centro per sviluppatori di Microsoft Sync Framework](http://go.microsoft.com/fwlink/?LinkId=209078). Per un confronto tra Sync Framework e la replica di tipo merge, vedere [Panoramica sulla sincronizzazione di database](http://msdn.microsoft.com/library/bb902818\(SQL.110\).aspx)  
  
 **Esplorare per area**  
 - [Novità](../../relational-databases/replication/what-s-new-replication.md)  
 - [Compatibilità con le versioni precedenti](../../relational-databases/replication/replication-backward-compatibility.md)  
 - [Funzionalità e attività di replica](../../relational-databases/replication/replication-features-and-tasks.md)  
 - [Riferimento tecnico](../../relational-databases/replication/technical-reference-replication.md)  
  
  
