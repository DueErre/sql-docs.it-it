---
title: Gestire eventi | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- event forwarding servers [SQL Server]
- events [SQL Server], forwarding
- event-triggered jobs [SQL Server]
- forwarding events [SQL Server]
- alerts [SQL Server], forwarded events
- alerts [SQL Server], management servers
- SQL Server Agent alerts, management servers
ms.assetid: 8f4ee7f5-80df-49fd-b2b8-d020e04b6e1b
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: aaa831f2f09c12a02fa997a912bd9d0b97ec6cba
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/17/2018
---
# <a name="manage-events"></a>Gestione di eventi
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] È possibile inoltrare a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tutti i messaggi di evento con livello di gravità dell'errore corrispondente o superiore a un determinato valore. Questa caratteristica è nota come *inoltro degli eventi*. Il server di inoltro è un server dedicato che può essere anche un server master. L'inoltro degli eventi consente di gestire in modo centralizzato gli avvisi per un gruppo di server, riducendo in tal modo il carico di lavoro per i server utilizzati molto frequentemente.  
  
Un singolo server che riceve gli eventi per un gruppo di altri server è denominato *server di gestione avvisi*. In un ambiente multiserver come server di gestione degli avvisi viene scelto il server master.  
  
## <a name="advantages-of-using-an-alerts-management-server"></a>Vantaggi derivanti dall'utilizzo di un server di gestione degli avvisi  
I vantaggi derivanti dall'impostazione di un server di gestione degli avvisi sono:  
  
-   **Centralizzazione**. Da un unico server è possibile controllare in modo centralizzato e visualizzare globalmente gli eventi di più istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] .  
  
-   **Scalabilità**. È possibile amministrare molti server fisici come un unico server logico, nonché aggiungere o rimuovere server da questo gruppo di server fisici a seconda delle necessità.  
  
-   **Efficienza**. Il tempo necessario per la configurazione risulta ridotto, in quanto è sufficiente definire avvisi e operatori una sola volta.  
  
## <a name="disadvantages-of-using-an-alerts-management-server"></a>Svantaggi derivanti dall'utilizzo di un server di gestione degli avvisi  
Gli svantaggi derivanti dall'impostazione di un server di gestione degli avvisi sono:  
  
-   **Aumento del traffico**. L'inoltro di eventi a un server di gestione degli avvisi può determinare un aumento del traffico di rete. È possibile ridurre il traffico limitando l'inoltro ai soli eventi con livello di gravità superiore a un determinato valore.  
  
-   **Singolo punto di errore**. Se il server di gestione degli avvisi viene portato offline, non verrà generato nessun avviso per qualsiasi evento del gruppo di server gestito.  
  
-   **Carico server**. La gestione degli avvisi per gli eventi inoltrati determina un aumento del carico di elaborazione nel server di gestione degli avvisi.  
  
## <a name="guidelines-for-using-an-alerts-management-server"></a>Linee guida per l'utilizzo di un server di gestione degli avvisi  
Per la configurazione di un server di gestione degli avvisi attenersi alle linee guida riportate di seguito.  
  
-   Per ricevere eventi inoltrati, il server di gestione degli avvisi deve essere un'istanza predefinita di SQL Server.  
  
-   Nel server di gestione degli avvisi evitare di eseguire applicazioni di primaria importanza o utilizzate molto frequentemente.  
  
-   Pianificare con attenzione il traffico di rete associato alla configurazione di molti server per la condivisione dello stesso server di gestione degli avvisi. In caso di congestione, ridurre il numero di server che utilizzano lo stesso server di gestione degli avvisi.  
  
    I server registrati in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] sono quelli selezionabili come server di inoltro degli avvisi.  
  
-   Definire nell'istanza locale di [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] avvisi che richiedono una risposta specifica del server, anziché inoltrare gli avvisi al server di gestione degli avvisi.  
  
    Il server di gestione degli avvisi visualizza tutti i server che inoltrano avvisi come un insieme logico. Un server di gestione degli avvisi risponde ad esempio in modo identico a un evento 605 inoltrato dal server A e a un evento 605 inoltrato dal server B.  
  
-   Dopo aver configurato il sistema degli avvisi, controllare periodicamente se nel registro applicazioni di Microsoft Windows sono presenti eventi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent.  
  
    Le condizioni di errore rilevate dal motore degli avvisi vengono registrate nel registro applicazioni locale di Windows con il nome di origine "SQL Server Agent". Se ad esempio [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent non è in grado di inviare notifiche tramite posta elettronica in base alle impostazioni definite, nel registro applicazioni verrà registrato un evento.  
  
Se un avviso definito localmente è disattivato e viene generato un evento che avrebbe causato l'attivazione di tale avviso, l'evento verrà inoltrato al server di gestione degli avvisi purché soddisfi la condizione di inoltro degli avvisi. In tal modo, a seconda dei casi, gli utenti del sito locale potranno attivare o disattivare gli avvisi definiti sia localmente che nel server di gestione degli avvisi. È inoltre possibile richiedere che gli eventi siano sempre inoltrati, anche quando sono gestiti da avvisi locali.  
  
Di seguito sono riportate le attività comuni per la gestione degli eventi in un ambiente multiserver:  
  
**Per impostare un server di gestione degli avvisi**  
  
-   [SQL Server Management Studio](../../ssms/agent/designate-an-events-forwarding-server-sql-server-management-studio.md)  
  
**Per definire la risposta a un avviso**  
  
-   [SQL Server Management Studio](../../ssms/agent/define-the-response-to-an-alert-sql-server-management-studio.md)  
  
-   [Transact-SQL](http://msdn.microsoft.com/en-us/0525e0a2-ed0b-4e69-8a4c-a9e3e3622fbd)  
  
## <a name="running-event-triggered-jobs"></a>Esecuzione di processi attivati da eventi  
È possibile definire l'esecuzione di un processo in risposta a un avviso, ad esempio eseguendo un processo che corregga il problema segnalato dall'avviso o ne esegua un'analisi aggiuntiva.  
  
> [!NOTE]  
> Poiché un processo può generare un evento, assicurarsi che non venga creato un ciclo ricorsivo avviso-processo.  
  
## <a name="see-also"></a>Vedere anche  
[sp_add_notification (Transact-SQL)](http://msdn.microsoft.com/en-us/44bee7d9-7517-4071-99be-8b36f979c7cc)  
  
