---
title: Importare una Knowledge Base da un file DQS | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: data-quality-services
ms.service: 
ms.component: data-quality-services
ms.reviewer: 
ms.suite: sql
ms.technology: data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9b9786fe-9e80-429a-afcb-dc3b3dd6f0b0
caps.latest.revision: "17"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 375cd4bf583935ce4ddbc058a653b8a39093e323
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/19/2018
---
# <a name="import-a-knowledge-base-from-a-dqs-file"></a>Importazione di una Knowledge Base da un file DQS
  In questo argomento viene descritto come importare un'intera Knowledge Base da un file di dati con estensione DQS in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Il file di dati viene creato esportando una Knowledge Base esistente dall'interno dell'applicazione [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] (vedere [Esportare una Knowledge Base in un File DQS](../data-quality-services/export-a-knowledge-base-to-a-dqs-file.md)).  
  
 L'utilizzo di un file di dati DQS per l'esportazione del contenuto di una Knowledge Base e la successiva reimportazione del contenuto in un'altra Knowledge Base nello stesso [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] , o su un [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] diverso, semplifica il processo di generazione delle informazioni e consente di risparmiare tempo e impegno. La procedura permette di condividere una Knowledge Base e le relative informazioni con altri utenti, consentendo in tal modo anche ad essi un notevole risparmio di tempo. Il file DQS conterrà tutte le informazioni della Knowledge Base, compresi domini e i criteri di corrispondenza, tranne le informazioni sui dati di riferimento collegati. Verranno importati sia i dati pubblicati che quelli non pubblicati.  
  
 I file di dati DQS sono crittografati, pertanto non è possibile visualizzarne il contenuto.  
  
 Quando si importa una Knowledge Base, è possibile utilizzare lo stesso nome, a meno che il nome della Knowledge Base già esista nell'applicazione client, nel qual caso sarà necessario modificarlo.  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Prerequisites"></a> Prerequisiti  
 Per importare una Knowledge Base da un file DQS, è necessario avere già esportato la Knowledge Base nel file DQS.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Permissions  
 Per importare una Knowledge Base da un file DQS è necessario disporre del ruolo dqs_kb_editor o dqs_administrator nel database DQS_MAIN.  
  
##  <a name="Import"></a> Import a knowledge base from a .dqs file  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Eseguire l'applicazione Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Nella schermata iniziale del [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] fare clic su **Nuova Knowledge Base**.  
  
3.  Immettere un nome per la Knowledge Base.  
  
4.  Fare clic sulla freccia in giù per **Crea Knowledge Base da**, quindi selezionare **Importa da file DQS**.  
  
5.  Per **Seleziona il file di dati**, fare clic su **Sfoglia**.  
  
6.  Nella finestra di dialogo **Importa da file di dati** spostarsi nella cartella contenente il file DQS da importare, quindi fare clic sul nome del file. Fare clic su **Apri**.  
  
7.  Verificare che la Knowledge Base e i domini corretti vengano visualizzati nell'elenco dei **Domini** .  
  
8.  Selezionare l'attività che si desidera eseguire, quindi fare clic su **Crea**.  
  
9. Nella finestra di dialogo **Importa Knowledge Base** verificare che la riga dello stato indichi che l'importazione è stata completata. Fare clic su **OK**.  
  
10. Completare l'individuazione delle informazioni, la gestione del dominio o l'attività dei criteri di corrispondenza richieste, quindi fare clic su **Fine**.  
  
11. Fare clic su **Pubblica** per pubblicare le informazioni nella Knowledge Base o **No** per non pubblicarle.  
  
12. Se si è scelto di pubblicare la Knowledge Base, fare clic su **OK**.  
  
13. Nella pagina iniziale di Data Quality Services, verificare che la Knowledge Base sia elencata in **Knowledge Base recenti**.  
  
##  <a name="FollowUp"></a> Completamento: Dopo avere importato una Knowledge Base da un file DQS  
 Dopo avere importato una Knowledge Base da un file DQS, è possibile aggiungervi informazioni o utilizzarla per progetti di pulizia o di individuazione delle corrispondenze, a seconda del suo contenuto. Per altre informazioni, vedere [Eseguire l'individuazione di informazioni](../data-quality-services/perform-knowledge-discovery.md), [Gestione di un dominio](../data-quality-services/managing-a-domain.md), [Gestione di un dominio composito](../data-quality-services/managing-a-composite-domain.md), [Creare criteri di corrispondenza](../data-quality-services/create-a-matching-policy.md), [Pulizia dei dati](../data-quality-services/data-cleansing.md), o [Corrispondenza di dati](../data-quality-services/data-matching.md).  
  
  
