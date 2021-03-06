---
title: Esecuzione del debug del codice dell'estensione per il recapito | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: extensions
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- delivery extensions [Reporting Services], debugging
- debugging delivery extensions [Reporting Services]
- troubleshooting [Reporting Services], delivery extensions
ms.assetid: a7d959da-5005-4a50-aca7-2cef36aa9947
caps.latest.revision: "35"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 2b959a6917313abc2913412d756e483f9e9e6807
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2018
---
# <a name="debugging-delivery-extension-code"></a>Esecuzione del debug del codice dell'estensione per il recapito
  In [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] sono disponibili diversi strumenti di debug che consentono di analizzare il codice dell'estensione per il recapito e di individuare gli errori. Gli strumenti più appropriati da utilizzare variano in base alla finalità desiderata. In questo esempio viene utilizzato [!INCLUDE[vsOrcas](../../../includes/vsorcas-md.md)].  
  
#### <a name="to-debug-your-delivery-extension-code"></a>Per eseguire il debug del codice dell'estensione per il recapito  
  
1.  Avviare [!INCLUDE[vsOrcas](../../../includes/vsorcas-md.md)] e aprire il progetto di estensione per il recapito.  
  
2.  Compilare il progetto e distribuire l'assembly di estensioni per il recapito e il file con estensione pdb associato nel server di report e in Gestione report. Per altre informazioni sulla distribuzione, vedere [Distribuzione di un'estensione per il recapito](../../../reporting-services/extensions/delivery-extension/deploying-a-delivery-extension.md).  
  
3.  Se è stata scritta un'interfaccia utente di sottoscrizione per estendere Gestione report, aprire Internet Explorer e passare a Gestione report lasciando aperto il codice dell'estensione per il recapito in [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]. Se per Gestione report non è stata distribuita un'interfaccia utente di sottoscrizione, aprire semplicemente l'applicazione client dalla quale si chiama l'estensione per il recapito utilizzando l'API SOAP.  
  
4.  Passare a [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] e al progetto di estensione per il recapito e impostare alcuni punti di interruzione nel codice.  
  
5.  Con il progetto di estensione per il recapito ancora nella finestra attiva, scegliere **Connetti a processo** dal menu **Debug**.  
  
     Verrà visualizzata la finestra di dialogo **Connetti a processo**.  
  
6.  Nell'elenco di processi selezionare il processo aspnet_wp.exe o w3wp.exe, se l'applicazione è distribuita in IIS 6.0, e fare clic su **Connetti**.  
  
7.  Definire una nuova sottoscrizione utilizzando l'estensione per il recapito. In genere, a tale scopo è possibile utilizzare Gestione report o l'API SOAP. In questo modo, è possibile richiamare il debugger ed eseguire il codice in corrispondenza dei punti di interruzione.  
  
8.  Esaminare il codice istruzione per istruzione premendo **F11**. Per ulteriori informazioni sull'utilizzo di [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] per eseguire il debug, vedere la documentazione di [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Implementazione di un'estensione per il recapito](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Libreria di estensioni di Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
