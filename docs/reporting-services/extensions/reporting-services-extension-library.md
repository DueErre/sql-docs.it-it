---
title: Reporting Services estensione libreria | Documenti Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- namespaces [Reporting Services]
- Reporting Services, extending
- extensions [Reporting Services], library
- library [Reporting Services]
ms.assetid: e8eff470-64d6-41c3-b98b-5ec916c121c3
caps.latest.revision: 33
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: b9a1ce1e388575d6d5b9b46a00dbc85ae8cde84b
ms.contentlocale: it-it
ms.lasthandoff: 06/13/2017

---
# <a name="reporting-services-extension-library"></a>Libreria di estensioni di Reporting Services
  La libreria di estensioni di Reporting Services è un set di classi, interfacce e tipi di valori inclusi in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Questa libreria fornisce accesso alle funzionalità di sistema ed è progettata per essere la base [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] applicazioni possono essere utilizzate per estendere [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] componenti.  
  
## <a name="namespaces"></a>Spazi dei nomi  
 La libreria di estensioni [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornisce gli spazi dei nomi seguenti.  
  
 <xref:Microsoft.ReportingServices.DataProcessing>  
 Contiene classi e interfacce che consentono di compilare componenti che estendono le funzionalità di elaborazione dati di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 <xref:Microsoft.ReportingServices.Interfaces>  
 Contiene classi e interfacce che consentono di costruire notifiche personalizzate e di inviarle agli utenti tramite estensioni per il recapito personalizzate, nonché di compilare estensioni di sicurezza personalizzate per [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 **Microsoft.ReportingServices.ReportRendering**  
 Contiene classi e interfacce che consentono di estendere le funzionalità di rendering di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Utilizzando i membri di questo spazio dei nomi con i membri dello spazio dei nomi <xref:Microsoft.ReportingServices.Interfaces>, è possibile compilare estensioni per il rendering personalizzate per [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Estensioni di Reporting Services](../../reporting-services/extensions/reporting-services-extensions.md)  
  
  