---
title: Aggiungere parametri a un report per dispositivi mobili | Reporting Services | Microsoft Docs
ms.custom: 
ms.date: 11/01/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: mobile-reports
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 113cb057-deec-40eb-abc8-f35d3900eaa6
caps.latest.revision: "12"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d531c2f0b5d9b1e01d3d40a61f6f05ce50fe3c29
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2018
---
# <a name="add-parameters-to-a-mobile-report--reporting-services"></a>Aggiungere parametri a un report per dispositivi mobili | Reporting Services
È possibile creare report per dispositivi mobili di [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] con parametri in modo che l'autore e i lettori dei report possano filtrare i report stessi. I report con parametri possono essere anche la destinazione di un [drill-through da un report di origine](../../reporting-services/mobile-reports/add-drillthrough-from-a-mobile-report-to-other-mobile-reports-or-urls.md). 

Per creare un report per dispositivi mobili con parametri, iniziare con un set di dati condiviso con almeno un parametro. Per altre informazioni, vedere [Creare un set di dati condiviso o un set di dati incorporato (Generatore report e SSRS)](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md).  

Dopo aver aggiunto i parametri a un report per dispositivi mobili, creare un URL per [aprire il report con parametri della stringa di query](../../reporting-services/mobile-reports/open-a-mobile-report-with-specific-query-string-parameters-reporting-services.md).

1. Nella barra superiore del portale Web di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion.md)] selezionare **Nuovo** > **Report per dispositivi mobili**.  
  
   ![PBI_SSMRP_NewMenu](../../reporting-services/mobile-reports/media/pbi-ssmrp-newmenu.png)  
     
2. Selezionare la scheda **Dati** nell'angolo in alto a sinistra di [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)].   
  
3. Selezionare **Aggiungi dati**nell'angolo in alto a destra.  
  
4. Selezionare **Server di report**e quindi selezionare un server.  
  
5. Passare ai set di dati condivisi sul server e selezionarne uno dotato di parametri.  
  
   I dati del set di dati vengono visualizzati nella griglia. Il cerchio verde con parentesi graffe **{ }** contrassegna un set di dati con un parametro.  
     
   ![SSMRP_PforParam](../../reporting-services/mobile-reports/media/ssmrp-pforparam.png)  
  
6. Fare clic sulla ruota visualizzata sulla scheda e quindi selezionare **Param {}**.  
  
   ![SSMRP_ParamWheel](../../reporting-services/mobile-reports/media/ssmrp-paramwheel.png)  
  
7. Selezionare l'elemento di report che passerà i valori al parametro.  
  
   ![SSMRP_SetParam](../../reporting-services/mobile-reports/media/ssmrp-setparam.png)  
     
8. Selezionare **Anteprima** per visualizzare l'aspetto del report. In questo report l'elenco di selezione usa il parametro di categoria.

   ![sql-server-mobile-report-publisher-Selection-List-View-No-Selection](../../reporting-services/mobile-reports/media/sql-server-mobile-report-publisher-selection-list-view-no-selection.png) 
   
9. Quando si seleziona un valore nell'elenco di selezione, il report viene filtrato per tale valore. In questo caso, Accessori.

   ![sql-server-mobile-report-publisher-Selection-List-Category-Selected](../../reporting-services/mobile-reports/media/sql-server-mobile-report-publisher-selection-list-category-selected.png)   
  
### <a name="see-also"></a>Vedere anche  
-  [Aprire un report per dispositivi mobili con parametri della stringa di query specifici](../../reporting-services/mobile-reports/open-a-mobile-report-with-specific-query-string-parameters-reporting-services.md)
-  [Aggiungere il drill-through da un report per dispositivi mobili ad altri report per dispositivi mobili o URL](../../reporting-services/mobile-reports/add-drillthrough-from-a-mobile-report-to-other-mobile-reports-or-urls.md)
-  [Creare un set di dati condiviso o un set di dati incorporato](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)
- [Creare e pubblicare report per dispositivi mobili con SQL Server Mobile Report Publisher](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
  
  

