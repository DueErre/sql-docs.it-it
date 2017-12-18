---
title: "Modificare l'account proxy per il set di raccolta utilità in un'istanza gestita di SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: maintenance-plans
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ff37ba8b-a08c-4109-b6e2-5748c995a52c
caps.latest.revision: "8"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 26a275b6a0ac87b06c8866988910b4d33e608fa6
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/17/2017
---
# <a name="change-proxy-account-for-utility-collection-on--managed-sql-server"></a>Modificare l'account proxy per il set di raccolta utilità in un'istanza gestita di SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Questo argomento descrive come modificare l'account proxy per il set di raccolta utilità in un'istanza gestita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-change-the-proxy-account-for-the-utility-collection-set-on-a-managed-instance-of-sql-server"></a>Per modificare l'account proxy per il set di raccolta dell'utilità in un'istanza gestita di SQL Server  
  
1.  Rimuovere l'istanza gestita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
    -   In **Esplora utilità** in SSMS fare clic sul nodo **Istanze gestite** .  
  
    -   Nella visualizzazione elenco di **Esplora utilità** , fare clic con il pulsante destro del mouse sul nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e scegliere **Rimuovi istanza gestita**. Per altre informazioni, vedere [Rimuovere un'istanza di SQL Server da Utilità SQL Server](../../relational-databases/manage/remove-an-instance-of-sql-server-from-the-sql-server-utility.md).  
  
2.  Registrare nuovamente l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
    -   In **Esplora utilità** in SSMS fare clic con il pulsante destro del mouse sul nodo **Istanze gestite** e scegliere **Aggiungi istanza gestita**.  
  
    -   Seguire le istruzioni nelle finestre visualizzate per completare la procedura guidata, specificando il nuovo account proxy.  
  
## <a name="see-also"></a>Vedere anche  
 [Attività e funzionalità di Utilità SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [Risoluzione dei problemi relativi a Utilità SQL Server](http://msdn.microsoft.com/library/f5f47c2a-38ea-40f8-9767-9bc138d14453)  
  
  
