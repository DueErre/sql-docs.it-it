---
title: Eseguire l'applicazione Data Quality Client | Microsoft Docs
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
f1_keywords:
- sql13.dqs.browseforservers.f1
- sql13.dqs.connecttoserver.f1
ms.assetid: 0b2aa202-7ab2-4c9d-b0f1-802588053a1e
caps.latest.revision: "13"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 470523ae689891e12b119b03941ceb2f17f2d3ae
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/19/2018
---
# <a name="run-the-data-quality-client-application"></a>Eseguire l'applicazione client Data Quality
  Eseguire il [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]e accedere a un [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)].  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Prerequisites"></a> Prerequisiti  
 È necessario aver completato l'installazione di [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] tramite l'esecuzione del file DQSInstaller.exe. Per altre informazioni, vedere [Eseguire DQSInstaller.exe per completare l'installazione del server DQS](../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md).  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Permissions  
 Per potere accedere al [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)], è necessario disporre di uno dei tre ruoli DQS (dqs_adminstrator, dqs_kb_editor o dqs_kb_operator) concessi per il database DQS_MAIN.  
  
##  <a name="Run"></a> Eseguire il client Data Quality  
 Per eseguire il [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] nel computer in cui è stato installato:  
  
1.  Fare clic su **Start**, puntare **Tutti i programmi**, fare clic su **[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]**, su **Data Quality Services**, quindi su **Client Data Quality**.  
  
2.  Nella finestra di dialogo **Connetti al server** :  
  
    1.  Specificare il server a cui si desidera connettere l'applicazione [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] . Selezionare **(LOCAL)** per connettersi al [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] nel computer locale. È anche possibile fare clic sulla freccia in giù e selezionare **\<Cerca altri server nella rete>** per connettersi a un server diverso, o al server locale in base al nome. Verrà visualizzata la finestra di dialogo **Cerca server** . È possibile selezionare un server nella scheda **Server locali** o nella scheda **Server di rete** .  
  
    2.  Per crittografare il trasferimento dei dati tra [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] e [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)], fare clic su **Opzioni**e quindi selezionare la casella di controllo **Crittografa connessione** .  
  
3.  Fare clic su **Connetti**.  
  
 Verrà visualizzata la schermata iniziale del [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]. Per altre informazioni, vedere [Schermata iniziale del client Data Quality](../data-quality-services/data-quality-client-home-screen.md).  
  
  
