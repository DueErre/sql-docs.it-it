---
title: Forzare un server di destinazione a eseguire il polling del server master | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- forcing master server polling
- polling master servers [SQL Server]
- master servers [SQL Server], polling
- target servers [SQL Server], polling the master server
ms.assetid: f1189a47-5ac3-45e2-9c5f-847810672279
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 57fe0392adfb1e290491815acd216fd356e20f3e
ms.contentlocale: it-it
ms.lasthandoff: 04/11/2017

---
# <a name="force-a-target-server-to-poll-the-master-server"></a>Force a Target Server to Poll the Master Server
In questo argomento viene descritta la procedura per il polling forzato del server di destinazione al server master. Il server di destinazione deve essere registrato nel server master.  
  
Un processo è una serie specificata di azioni eseguite da [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent. Un processo multiserver è un processo eseguito da un server master in uno o più server di destinazione. Ogni server di destinazione può eseguire contemporaneamente una sola istanza dello stesso processo. Ogni server di destinazione esegue periodicamente il polling del server master, scarica una copia dei nuovi processi assegnati al server di destinazione, quindi si disconnette. Il server di destinazione esegue il processo in locale, quindi si riconnette al server master per caricare lo stato del risultato del processo una volta terminato.  
  
> [!NOTE]  
> Se il server master non è accessibile quando il server di destinazione tenta di caricare lo stato del processo, per tale stato viene eseguito lo spooling fino a quando non è possibile accedere al server master.  
  
-   **Prima di iniziare:**  [Limitazioni e restrizioni](#Restrictions), [Sicurezza](#Security)  
  
-   **Per forzare un server di destinazione a eseguire il polling del server master con:** [SQL Server Management Studio](#SSMS)  
  
## <a name="BeforeYouBegin"></a>Prima di iniziare  
  
### <a name="Restrictions"></a>Limitazioni e restrizioni  
Il server di destinazione deve essere registrato nel server master. È necessario eseguire le istruzioni fornite in questo argomento dal server master.  
  
### <a name="Security"></a>Sicurezza  
Per informazioni dettagliate, vedere [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md) e [Scegliere l'account di servizio SQL Server Agent adatto ad ambienti multiserver](../../ssms/agent/choose-the-right-sql-server-agent-service-account-for-multiserver-environments.md).  
  
## <a name="SSMS"></a>Utilizzo di SQL Server Management Studio  
**Per forzare un server di destinazione a eseguire il polling del server master**  
  
1.  In **Esplora oggetti**espandere il server master.  
  
2.  Fare clic con il pulsante destro del mouse su **SQL Server Agent**, scegliere **Amministrazione multiserver**e fare clic su **Gestione server di destinazione**.  
  
3.  Selezionare un server di destinazione e fare clic su **Forza polling**.  
  
