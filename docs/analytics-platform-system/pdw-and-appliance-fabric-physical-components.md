---
title: PDW e dell'infrastruttura dello strumento componenti fisici (Analitica piattaforma sistema)
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7748d3da-0b7c-4ec6-9c22-4897758ba573
caps.latest.revision: "17"
ms.openlocfilehash: 95e80aaa641b04391d96b55f7491e21f1a30b6d1
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/21/2017
---
# <a name="pdw-and-appliance-fabric-physical-components"></a>Componenti fisici PDW e dell'infrastruttura di dispositivo
I nomi e descrizioni per i componenti fisici dell'infrastruttura PDW e il dispositivo. L'area PDW contiene tutti questi componenti.  
  
<!-- MISSING LINKS See also [HDInsight Physical Components &#40;Analytics Platform System&#41;](hdinsight-physical-components.md).  -->  
  
## <a name="diagrams"></a>Diagrammi componente  
Mostra i nomi dei componenti fisici e in cui si trovano nel primo rack del dispositivo nodo di calcolo di 6.  
  
![Nomi dei componenti area PDW - HP](./media/pdw-and-appliance-fabric-physical-components/APS_HW_ComponentNames-HP.png "APS_HW_ComponentNames HP")  
  
Il nome effettivo per i componenti PDW è il nome dell'area PDW, seguito da un trattino, seguito dal nome del componente. Ad esempio, se il nome dell'area PDW è PDW123, i nomi effettivi sono **PDW123 CTL01**, **PDW123-CMP01**e così via.  
  
Analogamente, il nome effettivo per i componenti dell'infrastruttura di dispositivo è il dominio applicazione, seguito da un trattino, seguito dal nome del componente. Ad esempio, se il dominio applicazione è FSW123, l'infrastruttura accessorio macchine virtuali sono **FSW123 WDS**, **FSW123 AD01**, **FSW123 VMM**e così via.  
  
Ecco una visualizzazione consolidata di un'area PDW con 6 nodi di calcolo.  
  
![Nomi dei componenti PDW](./media/pdw-and-appliance-fabric-physical-components/APS_HW_Names.png "APS_HW_Names")  
  
## <a name="pdw"></a>Componenti PDW  
Le macchine virtuali PDW fanno parte dell'area PDW.  
  
*PDW_region*-CTL01  
Una macchina virtuale che esegue il nodo di controllo. Questo viene eseguito su HST01 ed eseguire il failover a HST02.  
  
> [!WARNING]  
> SQL Server PDW non supporta la creazione di uno snapshot della macchina virtuale CTL01 tramite Hyper-V Manager. Gli snapshot si basano su archiviazione locale, che genera errori se la macchina virtuale tenta di failover per le operazioni di backup. Creazione di uno snapshot può provocare problemi di affidabilità con altre VM che il failover su server passivo.  
  
*PDW_region*-CMP01 tramite *PDW_Region*-CMP06  
Una macchina virtuale che esegue il nodo di calcolo. In questo diagramma del nodo di calcolo di 6, gli host HSA01 tramite HSA06 esecuzione nodo di calcolo CMP01 macchine virtuali tramite CMP06 rispettivamente.  
  
## <a name="fabric"></a>Componenti dell'infrastruttura di dispositivo  
Questi componenti fanno parte dell'infrastruttura dello strumento.  
  
### <a name="virtual-machines"></a>Macchine virtuali  
*appliance_domain*- servizi di distribuzione Windows  
L'host di macchine virtuali servizi di distribuzione Windows (WDS), che utilizza il sistema di piattaforma Analitica distribuire sistemi operativi Windows in rete accessorio. Include anche il servizio DHCP, che consente agli host di dispositivo per connettersi alla rete dispositivo senza un indirizzo IP configurato in precedenza.  
  
Il *appliance_domain*macchina virtuale - WDS viene eseguito su HST01 ed eseguire il failover a HST02. La macchina virtuale di servizi di distribuzione Windows e la macchina virtuale VMM, distribuire Windows in host fisici durante l'installazione dello strumento. Durante il ciclo di vita dello strumento, WDS e VMM eseguire operazioni quali la sostituzione di un host.  
  
*appliance_domain*- VMM  
Virtual Machine Manager (VMM) viene eseguito in una macchina virtuale e può eseguire il failover a HST02. System Center per distribuire il sistema operativo negli host fisici ospitati da VMM. VMM offre anche Windows Server Update Services (WSUS) per applicare o rimuovere gli aggiornamenti di Windows in tutti gli host e macchine virtuali.  
  
*appliance_domain*-AD01, *appliance_domain*-AD02  
Servizi di dominio, che contiene il sistema DNS (Domain Name), viene eseguito in una macchina virtuale in HST01 sia HST02. Per la disponibilità elevata del dispositivo, AD01 e AD02 sono controller di dominio replicati ed eseguono il failover. Se uno ha esito negativo, l'altro è già disponibile con i dati corretti.  
  
*appliance_domain*-ISCSI01  
Una macchina virtuale ISCSI viene eseguito su ciascuno degli host con spazio di archiviazione collegato (HSA01 HSA06). Questa macchina virtuale esegue il failover.  
  
### <a name="hosts"></a>Host  
*appliance_domain*-HST01 tramite *appliance_domain*-HST06  
Gli host per il controllo PDW nodo e il dispositivo dell'infrastruttura le macchine virtuali. HST03 è un host passivo facoltativo.  
  
*appliance_domain*-HSA01 tramite *appliance_domain*-HSA08  
Gli host con spazio di archiviazione collegato (HSA). Ogni ha host viene eseguito un nodo di calcolo VM e una VM ISCSI.  
  
### <a name="cluster-for-pdw"></a>Cluster per PDW  
*appliance_domain*-WFOHST01  
Il cluster PDW è denominato WFOHST01. Gestisce tutti gli host fisici e macchine virtuali che appartengono a PDW.  
  
### <a name="direct-attached-storage"></a>Direct Attached Storage  
*appliance_domain*-DAS01 tramite *appliance_domain*-DAS03  
Questo è l'archiviazione collegata direttamente connessa ai nodi di calcolo. HP ha uno DAS per ogni due nodi di calcolo. Dell e quantum hanno uno DAS per ogni tre nodi di calcolo.  
  
## <a name="see-also"></a>Vedere anche  
<!-- MISSING LINKS [Hardware Configurations &#40;Analytics Platform System&#41;](../architecture/hardware-configurations.md)  -->  
[Configurazione del dispositivo &#40; Sistema della piattaforma Analitica &#41;](appliance-configuration.md)  
[Attività di gestione dispositivo &#40; Sistema della piattaforma Analitica &#41;](appliance-management-tasks.md)  
  
