---
title: Sviluppo di tipi specifici di componenti del flusso di dati | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-custom-objects-data-flow-types
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data flow task [Integration Services], components
- components [Integration Services], data flow
- data flow [Integration Services], components
ms.assetid: 348e219a-b8ff-425e-b9c6-811880101c54
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 31c2dafb94bc5f3755d607a3686637b6f8baa205
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2018
---
# <a name="developing-specific-types-of-data-flow-components"></a>Sviluppo di tipi specifici di componenti del flusso di dati
  In questa sezione vengono descritte le specifiche dello sviluppo di componenti di origine, componenti di trasformazione con output sincroni, componenti di trasformazione con output asincroni e componenti di destinazione.  
  
 Per informazioni sullo sviluppo di componenti flusso dati in generale, vedere [Sviluppo di un componente flusso di dati personalizzato](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md).  
  
## <a name="in-this-section"></a>Argomenti della sezione  
 [Sviluppo di un componente di origine personalizzato](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-source-component.md)  
 Contiene informazioni sullo sviluppo di un componente che accede ai dati da un'origine dati esterna e li fornisce ai componenti a valle nel flusso di dati.  
  
 [Sviluppo di un componente di trasformazione personalizzato con output sincroni](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md)  
 Contiene informazioni sullo sviluppo di un componente di trasformazione i cui output sono sincroni con gli input. Questi componenti non aggiungono dati al flusso di dati, ma li elaborano mentre passano.  
  
 [Sviluppo di un componente di trasformazione personalizzato con output asincroni](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md)  
 Contiene informazioni sullo sviluppo di un componente di trasformazione i cui output non sono sincroni con gli input. Questi componenti ricevono dati dai componenti a monte, ma aggiungono anche dati al flusso di dati.  
  
 [Sviluppo di un componente di destinazione personalizzato](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-destination-component.md)  
 Contiene informazioni sullo sviluppo di un componente che riceve righe dai componenti a monte nel flusso di dati e li scrive in un'origine dati esterna.  
  
## <a name="reference"></a>Riferimento  
 <xref:Microsoft.SqlServer.Dts.Pipeline>  
 Contiene le classi e le interfacce utilizzate per creare componenti del flusso di dati personalizzati.  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper>  
 Contiene le classi e le interfacce non gestite dell'attività Flusso di dati. Lo sviluppatore utilizza questi oggetti e lo spazio dei nomi <xref:Microsoft.SqlServer.Dts.Pipeline> gestito quando compila un flusso di dati a livello di programmazione o crea componenti del flusso di dati personalizzati.  
  
## <a name="see-also"></a>Vedere anche  
 [Confronto tra soluzioni di scripting e oggetti personalizzati](../../integration-services/extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)   
 [Sviluppo di tipi specifici di componenti script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md)  
  
  
