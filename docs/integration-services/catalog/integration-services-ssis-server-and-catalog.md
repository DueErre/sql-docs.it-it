---
title: Server e catalogo di Integration Services (SSIS) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: service
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- packages [Integration Services], managing
- managing packages [Integration Services]
ms.assetid: 6d667bba-7c25-492a-8f4d-70ebaca28f40
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: b6451f3d322ff92ee928e6a9ed98759df0bcc2e6
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/09/2018
---
# <a name="integration-services-ssis-server-and-catalog"></a>Server e catalogo di Integration Services (SSIS)
  Dopo aver progettato e testato i pacchetti in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], è possibile distribuire i progetti contenenti i pacchetti nel server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Il server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] è un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] in cui viene ospitato il database di **SSISDB** . Nel database vengono archiviati gli oggetti seguenti: pacchetti, progetti, parametri, autorizzazioni, proprietà del server e cronologia operativa.  
  
 Tramite il database **SSISDB** vengono esposte le informazioni sull'oggetto nelle viste pubbliche su cui è possibile eseguire query. Nel database sono inoltre disponibili stored procedure che è possibile chiamare per gestire gli oggetti.  
  
 Prima di poter distribuire i progetti nel server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , è necessario creare il catalogo **SSISDB** .  
  
 Per una panoramica della funzionalità del catalogo SSISDB, vedere [Catalogo SSISDB](../../integration-services/catalog/ssis-catalog.md).  
  
## <a name="high-availability"></a>Disponibilità elevata  
 Analogamente ad altri database utente, il database **SSISDB** supporta il mirroring del database e la replica. Per altre informazioni sul mirroring e la replica, vedere [Mirroring del database &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md).  
  
 È anche possibile fornire la disponibilità elevata di SSISDB e i relativi contenuti usando i gruppi di disponibilità SSIS e AlwaysOn. Per altre informazioni, vedere [Always On per il catalogo SSIS (SSISDB)](ssis-catalog.md#always-on-for-ssis-catalog-ssisdb). Vedere anche il post di blog di Matt Masson relativo a [SSIS with AlwaysOn](http://go.microsoft.com/fwlink/?LinkId=255873) (SSIS con AlwaysOn) nel sito Web blogs.msdn.com.  
  
##  <a name="ssms"></a> Server Integration Services in SQL Server Management Studio  
 Quando si stabilisce la connessione a un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] in cui viene ospitato il database di **SSISDB** , gli oggetti seguenti sono visibili in Esplora oggetti:  
  
-   **Database SSISDB**  
  
     Il database **SSISDB** viene visualizzato nel nodo **Database** in Esplora oggetti. È possibile eseguire una query sulle viste e chiamare le stored procedure tramite cui vengono gestiti il server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e gli oggetti archiviati nel server.  
  
-   **Cataloghi di Integration Services**  
  
     Nel nodo **Cataloghi di Integration Services** sono presenti cartelle per i progetti e gli ambienti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Visualizzare l'elenco di pacchetti nel server Integration Services](../../integration-services/catalog/view-the-list-of-packages-on-the-integration-services-server.md)  
  
-   [Distribuire progetti e pacchetti di Integration Services (SSIS)](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)  
  
-   [Eseguire pacchetti di Integration Services (SSIS)](../../integration-services/packages/run-integration-services-ssis-packages.md)  
  
## <a name="related-content"></a>Contenuto correlato  
 Intervento sul blog relativo a [SSIS con AlwaysOn](http://go.microsoft.com/fwlink/?LinkId=255873) nel sito Web blogs.msdn.com.  
  
  
