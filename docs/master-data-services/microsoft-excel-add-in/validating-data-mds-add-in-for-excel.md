---
title: Convalida dei dati (componente aggiuntivo MDS per Excel) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
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
ms.assetid: 71eda98f-01a4-4fff-8246-be3133782523
caps.latest.revision: 
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6900e6cd61c5ea332c515fff99a802a63ccaf655
ms.sourcegitcommit: 6ac1956307d8255dc544e1063922493b30907b80
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/05/2018
---
# <a name="validating-data-mds-add-in-for-excel"></a>Convalida dei dati (componente aggiuntivo MDS per Excel)
  Nel [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]quando si pubblicano i dati, vengono eseguiti due tipi di convalida:  
  
-   Tutte le regole business definite sono applicate ai dati.  
  
-   I dati vengono controllati in base ai valori di attributo consentiti (ad esempio il numero di caratteri o il tipo di dati).  
  
 In ogni caso, i dati validi vengono pubblicati nel repository MDS. I dati non validi vengono evidenziati e i dettagli dell'errore possono essere visualizzati nelle colonne di stato.  
  
## <a name="when-validation-occurs"></a>Esecuzione della convalida  
 In [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]la convalida viene eseguita quando si pubblicano dati nuovi o modificati oppure quando si applicano manualmente regole business.  
  
 Quando le regole business hanno esito negativo, i dati vengono comunque pubblicati nel repository MDS. Quando la convalida dell'input ha esito negativo, i dati non vengono pubblicati nel repository.  
  
## <a name="validation-statuses"></a>Stati di convalida  
 Nel [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]sono possibili gli stati di convalida seguenti.  
  
 Per informazioni su ulteriori stati, vedere [Stati di convalida &#40;Master Data Services&#41;](../../master-data-services/validation-statuses-master-data-services.md)  
  
|Stato|Description|  
|------------|-----------------|  
|Convalida non riuscita|Si è verificato un errore di convalida di uno o più valori nella riga in base alle regole business definite da un amministratore di MDS.|  
|Convalida completata|Tutti i valori nella riga sono stati convalidati in base alle regole business.|  
  
## <a name="input-statuses"></a>Stati di input  
 Nel [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]sono possibili gli stati di input seguenti  
  
|Stato|Description|  
|------------|-----------------|  
|Errore|Uno o più valori nella riga non soddisfano i requisiti di sistema, come la lunghezza o il tipo di dati. Il valore non è aggiornato nel repository MDS.|  
|Nuova riga|I valori nella riga non sono ancora stati pubblicati nel repository MDS.|  
|Read Only|L'utente che ha eseguito l'accesso dispone di autorizzazioni di sola lettura per uno o più valori nella riga e non è possibile aggiornare il valore o i valori.|  
|Non modificato|Nessun valore nella riga è stato modificato nel foglio di lavoro. Ciò non significa che i valori nel repository non sono stati modificati. Per ottenere i dati più recenti nel foglio, fare clic su **Carica o aggiorna** nel gruppo **Connetti e carica**.<br /><br /> Questa è l'impostazione predefinita per ogni riga.|  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descrizione dell'attività|Argomento|  
|----------------------|-----------|  
|Determinare quali valori non passano le regole business definite.|[Applicare le regole di business &#40;componente aggiuntivo MDS per Excel&#41;](../../master-data-services/microsoft-excel-add-in/apply-business-rules-mds-add-in-for-excel.md)|  
|Per correggere gli errori di convalida, visualizzare tutte le transazioni eseguite per un membro.|[Visualizzare tutte le annotazioni o transazioni per un membro &#40;componente aggiuntivo MDS per Excel&#41;](../../master-data-services/microsoft-excel-add-in/view-all-annotations-or-transactions-for-a-member-mds-add-in-for-excel.md)|  
  
## <a name="related-content"></a>Contenuto correlato  
  
-   [Panoramica: Importazione di dati da Excel &#40;componente aggiuntivo MDS per Excel&#41;](../../master-data-services/microsoft-excel-add-in/overview-importing-data-from-excel-mds-add-in-for-excel.md)  
  
  
