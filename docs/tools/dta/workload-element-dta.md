---
title: Elemento Workload (DTA) | Documenti Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: dta
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: XML
helpviewer_keywords: Workload element
ms.assetid: 68ffd473-6546-4015-98d0-3763165de65c
caps.latest.revision: "16"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0f39cc50aa258df595bd7c010d992740a0a68976
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/17/2018
---
# <a name="workload-element-dta"></a>Elemento Workload (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Specifica il carico di lavoro da utilizzare per una sessione di ottimizzazione.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
<DTAInput>  
    <Server>  
...code removed...  
    <Workload>...</Workload>  
```  
  
## <a name="element-characteristics"></a>Caratteristiche elemento  
  
|Caratteristica|Descrizione|  
|--------------------|-----------------|  
|**Tipo di dati e lunghezza**|Nessuno|  
|**Valore predefinito**|Nessuno|  
|**Occorrenza**|Obbligatorio una sola volta per ogni elemento **DTAInput** .|  
  
## <a name="element-relationships"></a>Relazioni elemento  
  
|Relazione|Elementi|  
|------------------|--------------|  
|**Elemento padre**|[Avvio e utilizzo di Ottimizzazione guidata motore di database](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)|  
|**Elementi figlio**|[Elemento file &#40; DTA &#41;](../../tools/dta/file-element-dta.md)<br /><br /> [Elemento database per Workload &#40; DTA &#41;](../../tools/dta/database-element-for-workload-dta.md)<br /><br /> [Elemento EventString &#40; DTA &#41;](../../tools/dta/eventstring-element-dta.md)|  
  
## <a name="remarks"></a>Osservazioni  
 Un carico di lavoro è un set di istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] eseguite sui database che si desidera ottimizzare. Ottimizzazione guidata motore di database può utilizzare come carichi di lavoro script [!INCLUDE[tsql](../../includes/tsql-md.md)] , file di traccia e tabelle di traccia.  
  
 Se viene specificato un carico di lavoro in un file di input XML e un carico di lavoro nella riga di comando con lo strumento **dta** , per l'ottimizzazione verrà utilizzato il carico di lavoro specificato nella riga di comando. Tutte le opzioni di ottimizzazione specificate nella riga di comando prevalgono su quelle specificate in un file di input XML. L'unica eccezione è rappresentata dal caso in cui una configurazione definita dall'utente venga specificata in modalità di valutazione nel file di input XML. Se, ad esempio, viene immessa una configurazione nell'elemento **Configuration** del file di input XML e anche l'elemento **EvaluateConfiguration** viene specificato come una delle opzioni di ottimizzazione, le opzioni di ottimizzazione specificate nel file di input XML prevarranno su qualsiasi opzione di ottimizzazione immessa dalla riga di comando.  
  
 È necessario specificare un carico di lavoro per ogni sessione di ottimizzazione.  
  
## <a name="example"></a>Esempio  
 Nell'esempio di codice seguente viene specificata la tabella di traccia **MyDatabase.MyDBOwner.TuningTable001** per l'elemento **Workload** . La tabella **TuningTable001** è stata creata con il modello Tuning di SQL Server Profiler e salvando l'output della traccia come tabella.  
  
```  
<DTAXML ...>  
  <DTAInput>  
    <Server>  
...code removed here...  
    </Server>  
    <Workload>  
      <Database>  
        <Name>MyDatabase</Name>  
        <Schema>  
          <Name>MyDBOwner</Name>  
            <Table>  
              <Name>TuningTable001</Name>  
            </Table>  
        </Schema>  
      </Database>  
    </Workload>  
...code removed here...  
  </DTAInput>  
</DTAXML>  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai file di input XML &#40;Ottimizzazione guidata motore di database&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
