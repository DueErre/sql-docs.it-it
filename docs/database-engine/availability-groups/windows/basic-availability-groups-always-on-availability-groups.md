---
title: "Gruppi di disponibilità di base (gruppi di disponibilità AlwaysOn) | Microsoft Docs"
ms.custom: 
ms.date: 02/01/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: availability-groups
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 285adbc7-ac9b-40f6-b4a9-3f1591d3b632
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ba38095f11a5f40ec6b9a9398217a98f390d146d
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/03/2018
---
# <a name="basic-availability-groups-always-on-availability-groups"></a>Gruppi di disponibilità di base (gruppi di disponibilità AlwaysOn)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  I gruppi di disponibilità di base AlwaysOn sono una soluzione a disponibilità elevata per SQL Server 2016 e SQL Server 2017 Standard Edition. Un gruppo di disponibilità di base supporta un ambiente di failover per un singolo database e viene creato e gestito in modo molto simile ai tradizionali [gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md) (avanzati) con Enterprise Edition. In questo documento sono riepilogate differenze e limitazioni dei gruppi di disponibilità di base.  
  
## <a name="features"></a>Funzionalità  
 I gruppi di disponibilità di base AlwaysOn sono la funzionalità deprecata di mirroring del database e garantiscono un livello simile di supporto della funzionalità. I gruppi di disponibilità di base consentono a un database primario di mantenere una singola replica. Questa replica può usare la modalità commit asincrono o la modalità commit sincrono. Per altre informazioni sulle modalità di disponibilità, vedere [Modalità di disponibilità&#40; (gruppi di disponibilità AlwaysOn)&#41;](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md). La replica secondaria rimane inattiva a meno che non sia necessario eseguire il failover. Questo failover inverte le assegnazioni di ruolo primario e secondario, pertanto la replica secondaria diventerà il database attivo primario. Per altre informazioni sul failover, vedere [Failover e modalità di failover&#40;(gruppi di disponibilità AlwaysOn)&#41;](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md). I gruppi di disponibilità di base possono operare in un ambiente ibrido che si estende in locale e su Microsoft Azure.  
  
## <a name="limitations"></a>Limitazioni  
 I gruppi di disponibilità di base usano un sottoinsieme di funzionalità rispetto ai gruppi di disponibilità avanzati in SQL Server 2016 Enterprise Edition. I gruppi di disponibilità di base includono le limitazioni seguenti:  
  
- Limite di due repliche (primaria e secondaria).  
  
- Nessun accesso in lettura sulla replica secondaria.  
  
- Nessun backup sulla replica secondaria.  

- Nessun controllo di integrità sulle repliche secondarie. 

- Nessun supporto per le repliche ospitate nei server che eseguono una versione di SQL Server precedente a SQL Server 2016 Community Technology Preview 3 (CTP3).  

- Supporto per un database di disponibilità.  
  
- I gruppi di disponibilità di base non possono essere aggiornati a gruppi di disponibilità avanzati. Il gruppo deve essere eliminato e aggiunto nuovamente a un gruppo contenente server che eseguono solo SQL Server 2016 Enterprise Edition.  
  
- I gruppi di disponibilità di base sono supportati solo per i server Standard Edition. 

- I gruppi di disponibilità di base non possono far parte di un gruppo di disponibilità distribuito. 
  
## <a name="configuration"></a>Configurazione  
 I gruppi di disponibilità di base AlwaysOn possono essere creati in due server SQL Server 2016 Standard Edition qualsiasi. Durante la creazione di un gruppo di disponibilità di base, è necessario specificare entrambe le repliche.  
  
 Per creare un gruppo di disponibilità di base, usare il comando transact-SQL **CREATE AVAILABILITY GROUP** e specificare l'opzione **WITH BASIC**. Il valore predefinito è **ADVANCED**. Per altre informazioni, vedere [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/create-availability-group-transact-sql.md). Attualmente non è disponibile supporto dell'interfaccia utente per creare gruppi di disponibilità di base in SQL Server Management Studio.  
  
> [!NOTE]  
>  Quando si specifica **WITH BASIC** , si applicano al comando **CREATE AVAILABILITY GROUP** le limitazioni dei gruppi di disponibilità di base. Si verificherà un errore se ad esempio si tenta di creare un gruppo di disponibilità di base che consente l'accesso in lettura. Le altre limitazioni si applicano allo stesso modo. Per informazioni dettagliate, vedere la sezione Limitazioni di questo argomento.  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
