---
title: Opzione di configurazione del server blocked process threshold | Microsoft Docs
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- thresholds [SQL Server]
- blocked process threshold option
ms.assetid: 3d46d143-bc6a-4220-8b55-6baa37547c25
caps.latest.revision: "20"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a3f979eab8c73ebdf80fffe277a47f35d4c8ab02
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/18/2018
---
# <a name="blocked-process-threshold-server-configuration-option"></a>Opzione di configurazione del server blocked process threshold
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  L'opzione **blocked process threshold** consente di specificare la soglia, in secondi, superata la quale vengono generati i report relativi ai processi bloccati. La soglia può essere compresa tra 0 e 86.400. Per impostazione predefinita, non vengono generati report relativi ai processi bloccati. L'evento non viene generato per le attività di sistema o le attività in attesa nelle risorse che non comportano la generazione di deadlock rilevabili.  
  
 È possibile definire l'invio di un [avviso](http://msdn.microsoft.com/library/3f57d0f0-4781-46ec-82cd-b751dc5affef) quando viene generato questo evento. È possibile, ad esempio, scegliere di inviare un avviso nel cercapersone dell'amministratore affinché questi esegua l'azione appropriata per gestire la situazione di blocco.  
  
 La soglia per i processi bloccati utilizza il thread in background di monitoraggio dei deadlock per eseguire l'elenco di attività in attesa per un periodo di tempo maggiore o multiplo della soglia configurata. L'evento viene generato una volta per ogni intervallo di creazione del report per ogni attività bloccata.  
  
 Il report relativo ai processi bloccati viene creato in base ad approssimazioni ottimali. Non vi è alcuna garanzia di report in tempo reale o quasi in tempo reale.  
  
 L'impostazione diventa effettiva immediatamente e non richiede l'arresto e il riavvio del server.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente l'opzione `blocked process threshold` viene impostata su `20` secondi, comportando la generazione di report per ogni attività bloccata.  
  
```  
sp_configure 'show advanced options', 1 ;  
GO  
RECONFIGURE ;  
GO  
sp_configure 'blocked process threshold', 20 ;  
GO  
RECONFIGURE ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [Classe di evento Blocked Process Report](../../relational-databases/event-classes/blocked-process-report-event-class.md)  
  
  
