---
title: Specifica delle impostazioni di configurazione di distribuzione di soluzioni | Documenti Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Analysis Services Deployment Wizard, configuration settings
- input files [Analysis Services]
- configuration options [Analysis Services]
- Analysis Services deployments, configuration settings
- deploying [Analysis Services], configuration settings
ms.assetid: 953814a3-85ef-40cc-b46a-d532aa7a6569
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e778ee4c1962ac51eb145174dd424b9c3868512d
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/15/2018
---
# <a name="deployment-script-files---solution-deployment-config-settings"></a>File di Script di distribuzione - impostazioni di configurazione di distribuzione di soluzioni
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
Il [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] distribuzione guidata di legge ruoli e delle partizioni le opzioni di distribuzione nello script di distribuzione da cui si utilizzano il \< *nome progetto*>. configsettings file. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]tale file viene creato quando si compila il [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] progetto. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] Usa le impostazioni di configurazione del progetto corrente per creare il \< *nome progetto*>. configsettings file.  
  
## <a name="reviewing-the-configuration-settings-for-deployment"></a>Esame delle opzioni di configurazione per la distribuzione  
 Di seguito sono le impostazioni di configurazione archiviate nel \< *nome progetto*>. configsettings file:  
  
-   **Stringhe di connessione origine dati** Stringhe di connessione per ciascuna origine dati basate sui valori specificati nel progetto [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. L'ID utente e la password vengono sempre rimossi dalla stringa di connessione prima che il resto della stringa venga archiviato nel file. Se invece viene eseguita la distribuzione direttamente in un'istanza di Analysis Services, è possibile aggiungere le informazioni appropriate relative a ID utente e password all'interno della Distribuzione guidata per garantire l'elaborazione corretta del database di distribuzione. Queste informazioni di connessione non vengono archiviate nello script di distribuzione eventualmente salvato dalla Distribuzione guidata.  
  
-   **Impostazioni di rappresentazione** Questa impostazione definisce il nome utente usato da [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per eseguire istruzioni in ciascuna origine dati. Se non è stato specificato alcun account di rappresentazione, in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] verrà utilizzato l'account di accesso per eseguire le istruzioni. Se all'account di accesso [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] viene concesso l'accesso diretto all'origine dati, tutti gli amministratori del database di tutti i database dell'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] avranno accesso all'origine dati attraverso l'account di accesso. Se vengono specificati un account utente e una password, tali informazioni vengono sempre rimosse prima che le impostazioni di rappresentazione vengano archiviate nel file. Se invece viene eseguita la distribuzione direttamente in un'istanza di Analysis Services, è possibile aggiungere le informazioni appropriate relative a ID utente e password all'interno della Distribuzione guidata per garantire l'elaborazione corretta del database di distribuzione. Queste impostazioni di rappresentazione non vengono archiviate nello script di distribuzione eventualmente salvato dalla Distribuzione guidata.  
  
-   **File di log degli errori di chiave** Questa impostazione definisce il nome e il percorso del file di log degli errori di chiave di ciascun cubo, gruppo di misure, partizione e dimensione del database.  
  
-   **Percorsi di archiviazione** Questa impostazione definisce la posizione di archiviazione di ciascun cubo, gruppo di misure e partizione del database. Se non è stato specificato alcun valore per un oggetto, Distribuzione guidata di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utilizza la posizione predefinita per tale oggetto. Le partizioni utilizzano ad esempio la posizione del gruppo di misure, i gruppi di misure utilizzano la posizione del cubo e i cubi utilizzano la posizione predefinita degli oggetti dell'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . La posizione di archiviazione può essere un percorso locale o un percorso UNC (Universal Naming Convention).  
  
-   **Server di report** Questa impostazione definisce il server di report e la posizione della cartella per ciascuna azione report definita in ciascun cubo del database.  
  
## <a name="modifying-the-configuration-settings-for-deployment"></a>Modifica delle impostazioni di configurazione per la distribuzione  
 In alcuni casi, potrebbe essere necessario distribuire il [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] progetto che utilizza le impostazioni di configurazione diverse da quelle archiviate nel \< *nome progetto*>. configsettings file. Potrebbe ad esempio essere preferibile modificare la stringa di connessione per una o più origini dati o specificare posizioni di archiviazione per particolari partizioni o gruppi di misure.  
  
 Per modificare la distribuzione di partizioni e ruoli in un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] progetto, è necessario modificare queste informazioni all'interno di \< *nome progetto*>. configsettings file, come descritto nella procedura seguente. È possibile modificare le impostazioni di partizioni e dei ruoli all'interno del progetto poiché il  *\<nome progetto >* **pagine delle proprietà** nella finestra di dialogo [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] queste opzioni non sono visualizzate.  
  
> [!NOTE]  
>  Le impostazioni di configurazione possono essere applicate a tutti gli oggetti o solo ai nuovi oggetti creati. Le impostazioni di configurazione possono essere applicate solo ai nuovi oggetti creati quando si distribuiscono oggetti aggiuntivi a un database [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] distribuito precedentemente e non si desidera sovrascrivere gli oggetti esistenti. Per specificare se le impostazioni di configurazione si applicano a tutti gli oggetti o solo a appena creati, impostare questa opzione \< *nome progetto*>. deploymentoptions. Per altre informazioni, vedere [Impostazione delle opzioni di distribuzione dei ruoli e delle partizioni](../../analysis-services/multidimensional-models/deployment-script-files-partition-and-role-deployment-options.md).  
  
#### <a name="to-change-configuration-settings-after-the-input-files-have-been-generated"></a>Per modificare le opzioni di configurazione dopo la generazione dei file di input  
  
-   Eseguire Distribuzione guidata di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in modo interattivo e specificare le impostazioni di configurazione per gli oggetti da distribuire nella pagina **Impostazione proprietà di configurazione** .  
  
     -oppure-  
  
-   Eseguire Distribuzione guidata di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] attraverso il prompt dei comandi e impostarla in modo che venga eseguita in modalità file di risposte. Per altre informazioni sulla modalità file di risposte, vedere [Esecuzione della Distribuzione guidata Analysis Services](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md).  
  
     -oppure-  
  
-   Modificare il \< *nome progetto*>. configsettings file utilizzando un editor di testo.  
  
## <a name="see-also"></a>Vedere anche  
 [Specifica la destinazione di installazione](../../analysis-services/multidimensional-models/deployment-script-files-specifying-the-installation-target.md)   
 [Specifica opzioni di distribuzione di ruoli e partizioni](../../analysis-services/multidimensional-models/deployment-script-files-partition-and-role-deployment-options.md)   
 [Specifica le opzioni di elaborazione](../../analysis-services/multidimensional-models/deployment-script-files-specifying-processing-options.md)  
  
  
