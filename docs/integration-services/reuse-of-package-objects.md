---
title: Riutilizzo di oggetti di pacchetto | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- GUID regenerating [Integration Services]
- reusing packages
- templates [Integration Services]
- copying packages
- regenerating package GUID
ms.assetid: 08f723bf-15b5-44bd-9a46-04e8781bfbfb
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a3a926890e084e254acf3b6694bc4f43e7b17eff
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2018
---
# <a name="reuse-of-package-objects"></a>Riutilizzo di oggetti di pacchetto
  Viene compressa frequentemente la funzionalità che si desidera riutilizzare. Se, ad esempio, è stato creato un set di attività, potrebbe essere necessario riutilizzare questi elementi insieme, come gruppo, oppure riutilizzare singoli elementi quali una gestione connessione creata in un altro progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
## <a name="copy-and-paste"></a>Copiare e incollare  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] e Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] Designer support copying e Progettazione pasting package objects, which can include control flow items, data flow items, e Progettazione connection managers. È possibile copiare e incollare elementi sia tra progetti che tra pacchetti. Se la soluzione contiene più progetti, è possibile copiare elementi tra i vari progetti, che possono anche essere di tipi diversi.  
  
 Se una soluzione contiene più pacchetti, sarà possibile copiare e incollare elementi tra i vari pacchetti, che possono appartenere a uno stesso progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] o a progetti diversi. Gli oggetti di pacchetto possono tuttavia avere dipendenze da altri oggetti, in assenza dei quali non sono validi. Se ad esempio un'attività Esegui SQL utilizza una gestione connessione, per consentire l'esecuzione dell'attività sarà necessario copiare anche la gestione connessione. Esistono inoltre oggetti di pacchetto per cui è necessario che il pacchetto di destinazione contenga già un determinato oggetto, senza il quale non è possibile incollare gli oggetti copiati. Non è ad esempio possibile incollare un flusso di dati in un pacchetto che non include almeno un'attività Flusso di dati.  
  
 Se si nota che alcuni pacchetti vengono copiati di frequente, sarà possibile impostarli come modelli da utilizzare per la creazione di nuovi pacchetti, evitando così di copiarli ogni volta.  
  
 Quando si copia un oggetto di pacchetto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] provvede automaticamente ad assegnare un nuovo GUID alla proprietà **ID** del nuovo oggetto e ad aggiornare la proprietà **Name** .  
  
 Non è possibile copiare variabili. Se si copia un oggetto che utilizza variabili, ad esempio un'attività, sarà necessario ricreare le variabili nel pacchetto di destinazione. Se invece si copia l'intero pacchetto, verranno copiate anche le variabili presenti nel pacchetto.  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Copia di oggetti di pacchetto](../integration-services/copy-package-objects.md)  
  
-   [Copia di elementi di progetto](http://msdn.microsoft.com/library/1606c54d-20f9-49f3-a4ef-caad83a772aa)  
  
-   [Salvataggio di un pacchetto come modello di pacchetto](http://msdn.microsoft.com/library/efe66cec-3933-4f6e-8d35-fe3d300de66c)  
  
  
