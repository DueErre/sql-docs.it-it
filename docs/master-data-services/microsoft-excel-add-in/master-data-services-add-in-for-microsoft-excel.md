---
title: Componente aggiuntivo Master Data Services per Microsoft Excel | Microsoft Docs
ms.custom: 
ms.date: 07/25/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: microsoft-excel-add-in
ms.reviewer: 
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 33d9c8fc-9602-494d-b9ab-8f0f42785974
caps.latest.revision: 
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 8f1e34eb5bb7992661f79e2c524b660442a6df35
ms.sourcegitcommit: 6ac1956307d8255dc544e1063922493b30907b80
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/05/2018
---
# <a name="master-data-services-add-in-for-microsoft-excel"></a>Componente aggiuntivo Master Data Services per Microsoft Excel
  Con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]è possibile caricare elenchi filtrati di dati da MDS in Excel, dove è possibile usare i dati come si farebbe con qualsiasi altro tipo di dati. Una volta completata l'operazione, è possibile pubblicare di nuovo i dati in MDS, dove vengono archiviati centralmente. La sicurezza determina quali dati è possibile visualizzare e aggiornare.  
  
 Se si è un amministratore, è possibile usare [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] per creare entità e attributi e caricarli con i dati. In questo modo viene eliminata la necessità di usare altri strumenti per caricare i dati nei modelli.  
  
 In [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]è possibile utilizzare Data Quality Services (DQS) per la corrispondenza dei dati prima del caricamento in MDS. In tal modo si impedisce la duplicazione dei dati in MDS.  

## <a name="downloads"></a>Download 
>*  Scaricare il componente aggiuntivo Master Data Services di Master Data Services per Excel per SQL Server 2016 SP1 da [questa pagina dell'Area download Microsoft](https://go.microsoft.com/fwlink/?linkid=836866). 
>* Scaricare [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] per SQL Server 2017 CTP1 da [questa pagina dell'Area download Microsoft](https://go.microsoft.com/fwlink/?linkid=836867). Questo componente aggiuntivo funziona anche per SQL Server 2017 RC1.

 
  
## <a name="terms"></a>Termini  
 Quando si utilizza il componente aggiuntivo, è possibile incontrare i termini seguenti. Per altre informazioni, vedere [Panoramica di Master Data Services &#40;MDS&#41;](../../master-data-services/master-data-services-overview-mds.md).  
  
-   Il *MDS repository* in cui vengono memorizzati tutti i dati master. È un database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] configurato per archiviare dati MDS. Per usare dati provenienti dal repository, caricarli in Excel. Dopo averli usati, pubblicare di nuovo le modifiche nel repository. Gli amministratori possono aggiungere nuove entità e attributi al repository.  
  
-   I*dati gestiti tramite MDS* sono dati archiviati nel repository MDS che vengono caricati in Excel, dove vengono visualizzati come righe evidenziate. È possibile aggiungere dati che non sono gestiti da MDS al foglio di lavoro, senza che quest'ultimo venga modificato quando si aggiornano i dati gestiti da MDS.  
  
-   Un *model* è un contenitore di dati. È possibile creare versioni di questi contenitori e generalmente l'ultima versione è la più recente. Per altre informazioni, vedere [Modelli &#40;Master Data Services&#41;](../../master-data-services/models-master-data-services.md).  
  
-   Un oggetto *entity* è un elenco di dati. Un'entità può essere considerata come una tabella in un database. È possibile, ad esempio, che un'entità **Color** contenga un elenco di colori. Per altre informazioni, vedere [Entità &#40;Master Data Services&#41;](../../master-data-services/entities-master-data-services.md).  
  
-   Un *membro* è una riga di dati (un record). Ogni entità contiene membri. Un esempio di un membro è **Blu**. Per altre informazioni, vedere [Membri &#40;Master Data Services&#41;](../../master-data-services/members-master-data-services.md).  
  
-   Un *attribute* è una colonna di dati. Ogni membro dispone di attributi. Ad esempio, l'attributo **Code** per il membro **Blue** è **B**. Per altre informazioni sugli attributi, vedere [Attributi &#40;Master Data Services&#41;](../../master-data-services/attributes-master-data-services.md).  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descrizione dell'attività|Argomento|  
|----------------------|-----------|  
|Creare una connessione a un repository [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] .|[Connettersi a un repository MDS &#40;componente aggiuntivo MDS per Excel&#41;](../../master-data-services/microsoft-excel-add-in/connect-to-an-mds-repository-mds-add-in-for-excel.md)|  
|Caricare dati gestiti da MDS in Excel.|[Esportare dati in Excel da Master Data Services](../../master-data-services/microsoft-excel-add-in/export-data-to-excel-from-master-data-services.md)|  
|Salvare una query di collegamento che è possibile usare per aprire i dati gestiti da MDS attualmente visualizzati in seguito.|[Salvare un file di query collegamento &#40;componente aggiuntivo MDS per Excel&#41;](../../master-data-services/microsoft-excel-add-in/save-a-shortcut-query-file-mds-add-in-for-excel.md)|  
|Condividere collegamenti con gli altri.|[Inviare tramite posta elettronica un file di query collegamento &#40;componente aggiuntivo MDS per Excel&#41;](../../master-data-services/microsoft-excel-add-in/email-a-shortcut-query-file-mds-add-in-for-excel.md)|  
|Visualizzare tutte le modifiche apportate a un membro.|[Visualizzare tutte le annotazioni o transazioni per un membro &#40;componente aggiuntivo MDS per Excel&#41;](../../master-data-services/microsoft-excel-add-in/view-all-annotations-or-transactions-for-a-member-mds-add-in-for-excel.md)|  
|Prima di pubblicare nuovi dati, verificare se esistono duplicati.|[Cercare la corrispondenza tra dati simili &#40;componente aggiuntivo MDS per Excel&#41;](../../master-data-services/microsoft-excel-add-in/match-similar-data-mds-add-in-for-excel.md)|  
|Pubblicare dati da un foglio di lavoro nel repository MDS.|[Importare dati da Excel in Master Data Services &#40;componente aggiuntivo MDS per Excel&#41;](../../master-data-services/microsoft-excel-add-in/import-data-from-excel-to-master-data-services-mds-add-in-for-excel.md)|  
|Creare una nuova entità con i dati nel foglio di lavoro. (Solo amministratori).|[Creare un'entità &#40;componente aggiuntivo MDS per Excel&#41;](../../master-data-services/microsoft-excel-add-in/create-an-entity-mds-add-in-for-excel.md)|  
|Creare un attributo basato sul dominio, anche noto come un elenco vincolato. (Solo amministratori).|[Creare un attributo basato su dominio &#40;componente aggiuntivo MDS per Excel&#41;](../../master-data-services/microsoft-excel-add-in/create-a-domain-based-attribute-mds-add-in-for-excel.md)|  
|Impostare le proprietà per il caricamento e la pubblicazione di dati nel componente aggiuntivo Master Data Services per Excel. (Solo amministratori).|[Impostazione delle proprietà per il componente aggiuntivo Master Data Services per Excel](../../master-data-services/microsoft-excel-add-in/setting-properties-for-master-data-services-add-in-for-excel.md)|  
  
## <a name="related-content"></a>Contenuto correlato  
  
-   [Connessioni &#40;componente aggiuntivo MDS per Excel&#41;](../../master-data-services/microsoft-excel-add-in/connections-mds-add-in-for-excel.md)  
  
-   [Panoramica: Esportazione dei dati in Excel &#40;componente aggiuntivo MDS per Excel&#41;](../../master-data-services/microsoft-excel-add-in/overview-exporting-data-to-excel-mds-add-in-for-excel.md)  
  
-   [File di query collegamento &#40;componente aggiuntivo MDS per Excel&#41;](../../master-data-services/microsoft-excel-add-in/shortcut-query-files-mds-add-in-for-excel.md)  
  
-   [Aggiornamento dei dati &#40;Componente aggiuntivo MDS per Excel&#41;](../../master-data-services/microsoft-excel-add-in/refreshing-data-mds-add-in-for-excel.md)  
  
-   [Panoramica: Importazione di dati da Excel &#40;componente aggiuntivo MDS per Excel&#41;](../../master-data-services/microsoft-excel-add-in/overview-importing-data-from-excel-mds-add-in-for-excel.md)  
  
-   [Convalida dei dati &#40;componente aggiuntivo MDS per Excel&#41;](../../master-data-services/microsoft-excel-add-in/validating-data-mds-add-in-for-excel.md)  
  
-   [Corrispondenza Data Quality nel componente aggiuntivo MDS per Excel](../../master-data-services/microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md)  
  
-   [Compilazione di un modello &#40;componente aggiuntivo MDS per Excel&#41;](../../master-data-services/microsoft-excel-add-in/building-a-model-mds-add-in-for-excel.md)  
  
-   [Impostazione delle proprietà per il componente aggiuntivo Master Data Services per Excel](../../master-data-services/microsoft-excel-add-in/setting-properties-for-master-data-services-add-in-for-excel.md)  
  
-   [Sicurezza &#40;Master Data Services&#41;](../../master-data-services/security-master-data-services.md)  
  
  
