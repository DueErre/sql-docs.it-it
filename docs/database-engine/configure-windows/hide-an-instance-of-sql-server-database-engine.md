---
title: Nascondere un'istanza del motore di database di SQL Server | Microsoft Docs
ms.custom: 
ms.date: 08/19/2015
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
- Database Engine [SQL Server], hiding instances
- hiding instances of Database Engine
ms.assetid: 392de21a-57fa-4a69-8237-ced8ca86ed1d
caps.latest.revision: "22"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c82fb16bf871164502317768070d18b339120bd0
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/18/2018
---
# <a name="hide-an-instance-of-sql-server-database-engine"></a>Nascondere un'istanza del Motore di database di SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Questo argomento illustra come nascondere un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando Gestione configurazione SQL Server. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser per enumerare le istanze del [!INCLUDE[ssDE](../../includes/ssde-md.md)] installate nel computer. Ciò consente alle applicazioni client di cercare un server e ai client di distinguere tra più istanze del [!INCLUDE[ssDE](../../includes/ssde-md.md)] presenti nello stesso computer. È possibile usare la seguente procedura per evitare che il servizio SQL Server Browser esponga un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] ai computer client che tentano di individuarla tramite il pulsante **Sfoglia** .  
  
##  <a name="SSMSProcedure"></a> Utilizzo di Gestione configurazione SQL Server  
  
#### <a name="to-hide-an-instance-of-the-sql-server-database-engine"></a>Per nascondere un'istanza del Motore di database di SQL Server  
  
1.  In **Gestione configurazione SQL Server** espandere **Configurazione di rete SQL Server**, fare clic con il pulsante destro del mouse su **Protocolli per** *\<istanza del server>* e quindi selezionare **Proprietà**.  
  
2.  Nella casella **HideInstance** della scheda **Flag** selezionare **Sì**e quindi fare clic su **OK** per chiudere la finestra di dialogo. La modifica diventa effettiva immediatamente per le nuove connessioni.  
  
## <a name="remarks"></a>Remarks  
 Se si nasconde un'istanza denominata, per connettersi all'istanza nascosta è necessario specificare il numero di porta nella stringa di connessione anche se il servizio browser è in esecuzione. Per l'istanza denominata nascosta è consigliabile usare una porta statica invece di una porta dinamica.  
  Per altre informazioni, vedere [Configurazione di un server per l'attesa su una porta TCP specifica &#40;Gestione configurazione SQL Server&#41;](../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md).  
  
### <a name="clustering"></a>Clustering  
 Se si nasconde un'istanza denominata cluster, è possibile che il servizio cluster non riesca a connettersi a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il controllo **IsAlive** dell'istanza del cluster avrà quindi esito negativo e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] passerà alla modalità offline. È consigliabile creare in tutti i nodi dell'istanza del cluster un alias che rispecchi la porta statica configurata per l'istanza.  
 Per altre informazioni, vedere [Creazione o eliminazione di un alias server per l'utilizzo da parte di un client &#40;Gestione configurazione SQL Server&#41;](../../database-engine/configure-windows/create-or-delete-a-server-alias-for-use-by-a-client.md).  
  
 Se si nasconde un'istanza denominata cluster, il servizio cluster potrebbe non connettersi a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se nella chiave del Registro di sistema **LastConnect** (**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SNI11.0\LastConnect**) è indicata una porta diversa da quella su cui [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è in ascolto. Se il servizio cluster non riesce a stabilire una connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], potrebbe essere visualizzato un errore simile al seguente:  
**ID evento: 1001: Nome evento: Deadlock delle risorse Clustering di failover.**  
  
## <a name="see-also"></a>Vedere anche  
 [Configurazione di rete del server](../../database-engine/configure-windows/server-network-configuration.md)   
 [Descrizione delle connessioni client SQL Server virtuale](https://support.microsoft.com/kb/273673)   
 [Come assegnare una porta statica a un'istanza denominata di SQL Server ed evitare un errore comune](http://blogs.msdn.com/b/arvindsh/archive/2012/09/08/how-to-assign-a-static-port-to-a-sql-server-named-instance-and-avoid-a-common-pitfall.aspx)  
  
  
