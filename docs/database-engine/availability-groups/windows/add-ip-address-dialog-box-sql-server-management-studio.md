---
title: Finestra di dialogo Aggiungi indirizzo IP (SQL Server Management Studio) | Microsoft Docs
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: availability-groups
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.availabilitygrouplistener.addipaddress.f1
ms.assetid: 98c9ad3b-ff3c-4c1d-b344-59a72fca137c
caps.latest.revision: "10"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0aa89a5d92d7a20bbc7e4daf732f8f5ce2b09f47
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/18/2018
---
# <a name="add-ip-address-dialog-box-sql-server-management-studio"></a>Finestra di dialogo Aggiungi indirizzo IP (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Questo argomento della Guida sensibile al contesto descrive le opzioni della finestra di dialogo **Aggiungi indirizzo IP**. Questa finestra di dialogo a cui si accede dalla finestra di dialogo **Nuovo listener gruppo di disponibilità** e dalla scheda **Listener** della pagina **Specifica repliche** della [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)] o della [!INCLUDE[ssAoAddRepWiz](../../../includes/ssaoaddrepwiz-md.md)] di [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
## <a name="prerequisites"></a>Prerequisites  
 Prima di iniziare ad aggiungere subnet a un listener del gruppo di disponibilità, assicurarsi di conoscere l'indirizzo IP per ogni subnet e, per un indirizzo IPv4, la subnet mask.  
  
##  <a name="PageOptions"></a> Opzioni di aggiunta dell'indirizzo IP  
 **Subnet**  
 Utilizzare l'elenco a discesa per selezionare un indirizzo per la subnet da aggiungere al listener del gruppo di disponibilità. Per impostazione predefinita, una subnet ha sia un indirizzo IPv4 sia un indirizzo IPv6. Al primo utilizzo della finestra di dialogo **Aggiungi indirizzo IP** , nell'elenco a discesa **Subnet** sono visualizzati entrambi gli indirizzi per ogni subnet che ospita una replica per il gruppo di disponibilità. Per aggiungere una determinata subnet al listener, selezionare uno dei relativi indirizzi subnet.  
  
 Dopo avere completato la finestra di dialogo **Aggiungi indirizzo IP** e scelto **OK** per aggiungere un indirizzo di subnet selezionato al listener, nell'elenco a discesa **Subnet** tale indirizzo di subnet sarà filtrato. Tutti gli indirizzi della subnet deselezionati rimangono nell'elenco a discesa. Verificare di aggiungere un solo indirizzo per subnet al listener, in caso contrario la creazione del listener avrà esito negativo.  
  
 **Indirizzi**  
 Utilizzare questo campo per immettere un indirizzo IP statico per l'indirizzo di subnet selezionato. Contattare l'amministratore della rete per questo indirizzo IP. Assicurarsi di immettere un indirizzo valido per l'indirizzo di subnet selezionato, in caso contrario la creazione del listener avrà esito negativo.  
  
 **Indirizzo IPv4**  
 Se è stato selezionato l'indirizzo IPv4 di una subnet, immettere un indirizzo statico IPv4 valido.  
  
 **Subnet mask**  
 Per un indirizzo IPv4, in questo campo di sola lettura viene visualizzata la subnet mask della subnet selezionata.  
  
 **Indirizzo IPv6**  
 Se è stato selezionato l'indirizzo IPv6 di una subnet, immettere un indirizzo statico IPv6 valido.  
  
 **OK**  
 Fare clic per creare o aggiungere la subnet di cui è stato selezionato l'indirizzo con l'indirizzo IP statico specificato. Verrà aggiunta una riga con tali valori nella griglia della subnet della finestra di dialogo **Nuovo listener gruppo di disponibilità** o **Specifica repliche** .  
  
> [!IMPORTANT]  
>  L'indirizzo IP non viene verificato nella finestra di dialogo **Aggiungi indirizzo IP** . Inoltre, la finestra di dialogo non impedisce che venga aggiunto il secondo indirizzo per una subnet già aggiunta al listener del gruppo di disponibilità.  
  
 **Annulla**  
 Fare clic per annullare le selezioni e tornare alla finestra di dialogo **Nuovo listener gruppo di disponibilità** o alla scheda **Listener** senza aggiungere un indirizzo IP statico per qualsiasi subnet.  
  
##  <a name="RelatedTasks"></a> Attività correlate  
  
-   [Creare o configurare un listener del gruppo di disponibilità &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [Utilizzare la finestra di dialogo Nuovo gruppo di disponibilità &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Usare la procedura guidata Aggiungi replica a gruppo di disponibilità &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Listener del gruppo di disponibilità, connettività client e failover dell'applicazione &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)   
 [Connettività client Always On &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-client-connectivity-sql-server.md)  
  
  
