---
title: Database di distribuzione | Microsoft Docs
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
f1_keywords: sql13.rep.replicationutilities.selectdistributor.f1
ms.assetid: 787f0e9c-09dd-438a-bc04-5b8f99c127b8
caps.latest.revision: "22"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: eda1d3fc60baeea0f657561febb9f188ea78b16a
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/18/2018
---
# <a name="distributor"></a>Database di distribuzione
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] La pagina **Database di distribuzione** viene visualizzata nella Configurazione guidata distribuzione e nella Creazione guidata nuova pubblicazione. Il server di distribuzione è il server che contiene il database di distribuzione e che gestisce l'archiviazione dei metadati e dei dati di cronologia per tutti i tipi di replica. Il server di distribuzione gestisce inoltre l'archiviazione delle transazioni per la replica transazionale. Il server di distribuzione può corrispondere al server di pubblicazione (server di distribuzione locale) o essere un server distinto (server di distribuzione remoto). Il ruolo del server di distribuzione varia in base al tipo di replica implementato. In generale, il ruolo del server di distribuzione è più rilevante per la replica transazionale rispetto a quanto non lo sia per la replica di tipo merge e snapshot. La replica di tipo merge e la replica snapshot utilizzano normalmente un server di distribuzione locale, mentre la replica transazionale in sistemi sottoposti a un utilizzo particolarmente intensivo possono trarre vantaggio dall'utilizzo di un server di distribuzione remoto.  
  
 Il server di distribuzione utilizza le risorse aggiuntive seguenti nel server in cui è installato:  
  
-   Maggiore spazio su disco se i file di snapshot per la pubblicazione sono archiviati al suo interno, così come avviene normalmente.  
  
-   Maggiore spazio su disco per l'archiviazione del database di distribuzione.  
  
-   Maggior utilizzo del processore da parte degli agenti di replica per le sottoscrizioni push in esecuzione nel server di distribuzione.  
  
 Nel server selezionato come server di distribuzione devono essere disponibili spazio su disco e capacità del processore sufficienti per il supporto delle attività di replica e di altre eventuali operazioni basate su tale server.  
  
## <a name="options"></a>Opzioni  
 **'\<NomeServer>' fungerà da database di distribuzione per se stesso. Verranno creati un database di distribuzione e un log**  
 Selezionare questa opzione per configurare il server a cui si è connessi come server di distribuzione.  
  
 **Usa il server seguente come server di distribuzione (nota: il server selezionato deve essere già stato configurato come server di distribuzione)**  
 Selezionare questa opzione e quindi fare clic sul nome di un server elencato per configurare un altro server come server di distribuzione.  
  
 **Aggiungi**  
 Se il server che si desidera utilizzare non è elencato come server di distribuzione, fare clic su **Aggiungi** per identificare il server e aggiungerlo all'elenco.  
  
> [!NOTE]  
>  Per utilizzare un server remoto come server di distribuzione è necessario che il server remoto sia già stato configurato come server di distribuzione. Il server sul quale è in esecuzione la procedura guidata deve essere stato abilitato come server di pubblicazione nel server di distribuzione specifico.  
  
## <a name="see-also"></a>Vedere anche  
 [Configura distribuzione](../../relational-databases/replication/configure-distribution.md)   
 [Configurare la pubblicazione e la distribuzione](../../relational-databases/replication/configure-publishing-and-distribution.md)  
  
  
