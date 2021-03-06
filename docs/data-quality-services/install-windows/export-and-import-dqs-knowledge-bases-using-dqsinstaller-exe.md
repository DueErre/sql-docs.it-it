---
title: Esportare e importare le Knowledge Base di DQS con DQSInstaller.exe | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: data-quality-services
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: sql
ms.technology: data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8234c63b-a018-4e55-8184-9a6bdf03274d
caps.latest.revision: "9"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0fd097f81d5139e7775a8418c5f20c0aeefacb9d
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/19/2018
---
# <a name="export-and-import-dqs-knowledge-bases-using-dqsinstallerexe"></a>Esportare e importare le Knowledge Base di DQS con DQSInstaller.exe
  Per un'installazione esistente di DQS, è possibile esportare contemporaneamente tutte le Knowledge Base presenti in [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] in un file di backup DQS (con estensione dqsb) e quindi utilizzare successivamente il file con estensione dqsb per importare contemporaneamente tutte le Knowledge Base presenti in un'istanza diversa di [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] eseguendo il file DQSInstaller.exe dal prompt dei comandi. Per ulteriori informazioni sull'esecuzione di DQSInstaller.exe dal prompt dei comandi, vedere [Run DQSInstaller.exe from Command Prompt](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md#CommandPrompt) in [Run DQSInstaller.exe to Complete Data Quality Server Installation](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md).  
  
 Questa funzionalità consente di eseguire un backup di *tutte* le Knowledge Base in [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] contemporaneamente senza dovere esportare singolarmente ogni Knowledge Base in un file con estensione dqs tramite [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]. Allo stesso modo, è possibile importare contemporaneamente *tutte* le Knowledge Base dal file di backup in un altro [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] senza dovere importare singolarmente ogni Knowledge Base da un file con estensione dqs tramite [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]. Tale operazione è particolarmente utile per eseguire il backup e il ripristino delle Knowledge Base quando si disinstalla [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] su un computer e quindi per reinstallarlo su un computer diverso. È possibile esportare facilmente tutte le Knowledge Base presenti in un'installazione esistente di [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] in un file di backup (con estensione dqsb) DQS, quindi importare tutte le Knowledge Base dal file di backup dopo avere installato [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] su un computer diverso.  
  
##  <a name="export"></a> Esportazione delle Knowledge Base nel file con estensione dqsb  
 È possibile esportare in qualsiasi momento tutte le Knowledge Base nel [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] esistente o durante la disinstallazione di [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)].  
  
-   Per esportare tutte le Knowledge Base presenti in un [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] in un file di backup (con estensione dqsb) DQS, eseguire DQSInstaller.exe con il parametro `exportkbs` dal prompt dei comandi, insieme al percorso completo e al nome file dove si desidera esportare le Knowledge Base. Ad esempio, per esportare tutte le Knowledge Base nel file DQSBackup.dqsb nell'unità C:  
  
    ```  
    dqsinstaller.exe –exportkbs c:\DQSBackup.dqsb  
    ```  
  
    > [!NOTE]  
    >  Se il nome file fornito già esiste nel percorso specificato, il programma di installazione richiederà se ricoprire il file.  
  
-   Per esportare tutte le Knowledge Base presenti in un file di backup DQS durante la disinstallazione di [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)], eseguire DQSInstaller.exe con il parametro `uninstall` dal prompt dei comandi, insieme al percorso completo e al nome file dove si desidera esportare le Knowledge Base. Ad esempio, per esportare tutte le Knowledge Base nel file DQSBackup.dqsb nell'unità C: e quindi disinstallare [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]:  
  
    ```  
    dqsinstaller.exe –uninstall c:\DQSBackup.dqsb  
    ```  
  
    > [!NOTE]  
    >  Se non si specificano il percorso completo e il nome file del file di backup DQS durante la disinstallazione di [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] dal prompt dei comandi utilizzando il parametro `uninstall` , viene visualizzato un messaggio in cui viene segnalato che tutte le Knowledge Base verranno eliminate e che consente di scegliere se proseguire il processo di disinstallazione.  
  
##  <a name="import"></a> Importazione delle Knowledge Base dal file con estensione dqsb  
 È possibile importare tutte le Knowledge Base da un file di backup DQS (con estensione dqsb) dopo aver completato l'installazione di [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] . Per importare le Knowledge Base, è necessario disporre di un file di backup DQS valido (con estensione dqsb).  
  
 Eseguire il file DQSInstaller.exe con il parametro `importkbs` dal prompt dei comandi, insieme al percorso completo e al nome file da cui si desidera importare le Knowledge Base. Ad esempio, per importare tutte le Knowledge Base dal file DQSBackup.dqsb nell'unità C:  
  
```  
dqsinstaller.exe –importkbs c:\DQSBackup.dqsb  
```  
  
 Se vi sono Knowledge Base in [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] con lo stesso nome di quelle che si stanno importando, i nomi delle Knowledge Base importate saranno accodati con un carattere di sottolineatura (_) seguito da un valore intero che inizia con 1. Ad esempio, se il dominio "CompanyName" è duplicato, il nome di dominio importato sarà "CompanyName_1."  
  
## <a name="see-also"></a>Vedere anche  
 [Eseguire DQSInstaller.exe per completare l'installazione del server DQS](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md)   
 [Installare Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)   
 [Esportare una Knowledge Base in un file DQS](../../data-quality-services/export-a-knowledge-base-to-a-dqs-file.md)   
 [Importare una Knowledge Base da un file DQS](../../data-quality-services/import-a-knowledge-base-from-a-dqs-file.md)  
  
  
