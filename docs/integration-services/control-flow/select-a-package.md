---
title: Seleziona pacchetto | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: control-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.selectapackage.f1
helpviewer_keywords:
- Select a Package dialog box
ms.assetid: 92b47a2b-21b5-460a-885d-6cc4bb567249
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fab572c14d87acd3776a94675063ffe372525a5a
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2018
---
# <a name="select-a-package"></a>Seleziona pacchetto
  Utilizzare la finestra di dialogo **Seleziona pacchetto** per specificare il pacchetto da cui l'attività Message Queue può ricevere messaggi.  
  
## <a name="static-options"></a>Opzioni statiche  
 **Percorso**  
 Consente di specificare il percorso del pacchetto. Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente.  
  
|valore|Description|  
|-----------|-----------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Impostare il percorso su un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se si seleziona questo valore vengono visualizzate le opzioni dinamiche **Server**, **Usa autenticazione di Windows**, **Usa autenticazione di SQL Server**, **Nome utente**e **Password**.|  
|File DTSX|Consente di impostare il percorso su un file DTSX. Se si seleziona questo valore viene visualizzata l'opzione dinamica **Nome file**.|  
  
## <a name="location-dynamic-options"></a>Opzioni dinamiche relative al percorso  
  
### <a name="location--sql-server"></a>Percorso = SQL Server  
 **Nome pacchetto**  
 Consente di selezionare un pacchetto archiviato nel server specificato.  
  
 **Server**  
 Consente di specificare il nome del server o di selezionarlo nell'elenco.  
  
 **Usa autenticazione di Windows**  
 Fare clic su questa opzione per utilizzare l'autenticazione di Windows.  
  
 **Usa autenticazione di SQL Server**  
 Fare clic su questa opzione per usare l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **User name**  
 Se si usa l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , specificare il nome utente da usare per l'accesso al server.  
  
 **Password**  
 Se si usa l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , specificare una password.  
  
### <a name="location--dtsx-file"></a>Percorso = File DTSX  
 **Nome file**  
 Specificare il percorso di un pacchetto oppure fare clic sul pulsante Sfoglia **(…)** per individuare il pacchetto.  
  
## <a name="see-also"></a>Vedere anche  
 [Attività Message Queue](../../integration-services/control-flow/message-queue-task.md)  
  
  
