---
title: "Supporto della disponibilità elevata per i database OLTP in memoria | Microsoft Docs"
ms.custom: 
ms.date: 08/31/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: in-memory-oltp
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2113a916-3b1e-496c-8650-7f495e492510
caps.latest.revision: 
author: JennieHubbard
ms.author: jhubbard
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 299c2e0d7306fb1cca33eac4a26c1d3b04dca83c
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2018
---
# <a name="high-availability-support-for-in-memory-oltp-databases"></a>Supporto della disponibilità elevata per i database OLTP in memoria
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
I database che contengono tabelle ottimizzate per la memoria, con o senza stored procedure compilate native, sono completamente supportati con i gruppi di disponibilità AlwaysOn.  Non c'è alcuna differenza di configurazione e supporto per i database contenenti oggetti [!INCLUDE[hek_2](../../includes/hek-2-md.md)] rispetto a quelli che non li contengono.  
  
 Quando un database OLTP in memoria viene distribuito in una configurazione del gruppo di disponibilità AlwaysOn, le modifiche alle tabelle ottimizzate per la memoria nella replica primaria vengono applicate in memoria alle tabelle nelle repliche secondarie, quando è applicato ROLLFORWARD. Ciò significa che il failover su una replica secondaria può essere molto rapido, perché i dati sono già in memoria. Inoltre, le tabelle sono disponibili per le query nelle repliche secondarie che sono state configurate per l'accesso in lettura.  
  
## <a name="always-on-availability-groups-and-in-memory-oltp-databases"></a>Gruppi di disponibilità AlwaysOn e database OLTP in memoria  
 La configurazione dei database con componenti [!INCLUDE[hek_2](../../includes/hek-2-md.md)] offre quanto segue:  
  
-   **Un'esperienza completamente integrata**   
    È possibile configurare i database contenenti tabelle ottimizzate per la memoria usando la stessa procedura guidata con lo stesso livello di supporto sia per le repliche secondarie asincrone sia per quelle sincrone. Inoltre, il monitoraggio dello stato viene fornito tramite il noto dashboard AlwaysOn in SQL Server Management Studio.  
  
-   **Tempo di failover confrontabile**   
    Le repliche secondarie mantengono lo stato in memoria delle tabelle durevoli ottimizzate per la memoria. In caso di failover automatico o forzato, il tempo di failover al nuovo database primario è paragonabile a quello del failover a tabelle basate su disco, in quanto non è necessario il ripristino. Le tabelle con ottimizzazione per la memoria create come SCHEMA_ONLY sono supportate in questa configurazione. Tuttavia, le modifiche a queste tabelle non vengono registrate e pertanto non saranno presenti dati in queste tabelle nella replica secondaria.  
  
-   **Secondario leggibile**   
    È possibile accedere ed eseguire query su tabelle ottimizzate per la memoria nella replica secondaria se questa è stata configurata per l'accesso in lettura. In [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]la sincronizzazione del timestamp di lettura sulla replica secondaria con il timestamp di lettura sulla replica primaria è molto veloce, il che significa che le modifiche apportate alla replica primaria diventano visibili molto rapidamente nella replica secondaria. Questo comportamento di sincronizzazione rapida è diverso rispetto a OLTP in memoria di [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] .  
  
## <a name="failover-clustering-instance-fci-and-in-memory-oltp-databases"></a>Istanza di clustering di failover e database OLTP in memoria  
 Per ottenere la disponibilità elevata in una configurazione di archiviazione condivisa, è possibile impostare il clustering di failover nelle istanze con uno o più database con tabelle ottimizzate per la memoria. Per l'impostazione di un'istanza di clustering di failover, è necessario considerare i fattori seguenti.  
  
-   **Obiettivo tempo di ripristino**   
    Il tempo di failover sarà probabilmente maggiore perché le tabelle ottimizzate per la memoria devono essere caricate in memoria prima che il database venga reso disponibile.  
  
-   **Tabelle SCHEMA_ONLY**   
    Tenere presente che le tabelle SCHEMA_ONLY saranno vuote e senza righe dopo il failover. Si tratta di un comportamento previsto definito dall'applicazione. Questo comportamento corrisponde esattamente a ciò che succede quando si riavvia un database [!INCLUDE[hek_2](../../includes/hek-2-md.md)] con una o più tabelle SCHEMA_ONLY.  
  
## <a name="support-for-transaction-replication-in-in-memory-oltp"></a>Supporto per la replica transazionale in OLTP In memoria  
 Le tabelle con funzione di sottoscrittori di replica transazionale, esclusa la replica transazionale peer-to-peer, possono essere configurate come tabelle ottimizzate per la memoria. Le altre configurazioni di replica non sono compatibili con le tabelle ottimizzate per la memoria.  Per altre informazioni, vedere [Replica in sottoscrittori di tabelle con ottimizzazione per la memoria](../../relational-databases/replication/replication-to-memory-optimized-table-subscribers.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Gruppi di disponibilità Always On (SQL Server)](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Panoramica di gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Repliche secondarie attive: Repliche secondarie leggibili (gruppi di disponibilità Always On)](../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)   
 [Replica in sottoscrittori di tabelle con ottimizzazione per la memoria](../../relational-databases/replication/replication-to-memory-optimized-table-subscribers.md)  
  
  
