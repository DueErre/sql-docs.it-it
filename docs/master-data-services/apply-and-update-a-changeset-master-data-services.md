---
title: Applicare e aggiornare un insieme di modifiche (Master Data Services) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3a6a3cf2-1e77-43d3-a64a-855ae51258e7
caps.latest.revision: 
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3e6f059a5ac85fce47256ae2b75f170017186e14
ms.sourcegitcommit: 6ac1956307d8255dc544e1063922493b30907b80
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/05/2018
---
# <a name="apply-and-update-a-changeset-master-data-services"></a>Applicare e aggiornare un insieme di modifiche (Master Data Services)
  Un insieme di modifiche è una raccolta delle modifiche in sospeso relative ai dati master. È possibile applicare l'insieme di modifiche localmente per visualizzare, aggiungere, aggiornare ed eliminare le modifiche in sospeso nell'insieme di modifiche.  
  
## <a name="prerequisites"></a>Prerequisites  
  
-   È necessario disporre dell'autorizzazione per accedere all'area funzionale **Esplora** . Per altre informazioni, vedere [Autorizzazioni per aree funzionali &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
-   È necessario almeno l'accesso con diritti di aggiornamento all'entità o a uno dei relativi attributi.  
  
-   È possibile visualizzare solo l'insieme di modifiche di cui si è proprietari o l'insieme di modifiche sottoposto ad approvazione se si è l'amministratore dell'entità.  
  
-   È possibile modificare solo l'insieme di modifiche di cui si è proprietari e solo quando lo stato dell'insieme di modifiche è aperto o rifiutato.  
  
## <a name="to-apply-and-update-a-changeset"></a>Per applicare e aggiornare un insieme di modifiche  
  
1.  Nella home page di [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] selezionare un modello e una versione, quindi fare clic su **Visualizzatore**.  
  
2.  Scegliere un'entità nel menu **Entità** .  
  
3.  Nel riquadro destro selezionare **Insiemi di modifiche** e fare doppio clic sull'insieme di modifiche da visualizzare e modificare.  
  
4.  Fare clic su **Applica**.  
  
     Le modifiche in sospeso vengono applicate al membro dell'entità nella griglia. Le modifiche in sospeso vengono evidenziate.  
  
     La creazione, l'eliminazione e l'aggiornamento dei membri modificano l'insieme di modifiche.  
  
5.  Per ripristinare le modifiche in sospeso, nel riquadro **Insiemi di modifiche** fare clic con il pulsante destro del mouse sulla griglia e quindi fare clic su **Ripristino**.  
  
## <a name="next-steps"></a>Next Steps  
 [Eseguire il commit o inviare un insieme di modifiche &#40;Master Data Services&#41;](../master-data-services/commit-or-submit-a-changeset-master-data-services.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Creare un insieme di modifiche &#40;Master Data Services&#41;](../master-data-services/create-a-changeset-master-data-services.md)   
 [Applicare e rifiutare un insieme di modifiche &#40;Master Data Services&#41;](../master-data-services/approve-or-reject-a-changeset-master-data-services.md)  
  
  
