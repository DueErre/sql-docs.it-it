---
title: Riferimento tecnico di Microsoft Naive Bayes algoritmo | Documenti Microsoft
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
- MINIMUM_DEPENDENCY_PROBABILITY parameter
- MAXIMUM_INPUT_ATTRIBUTES parameter
- naive bayes model [Analysis Services]
- Bayesian classifiers
- naive bayes algorithms [Analysis Services]
- MAXIMUM_OUTPUT_ATTRIBUTES parameter
- MAXIMUM_STATES parameter
ms.assetid: a4cd47fe-2127-4930-b18f-3edd17ee9a65
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 93884e29674fa1a96402d23e397cddb3a1fe0bef
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/15/2018
---
# <a name="microsoft-naive-bayes-algorithm-technical-reference"></a>Riferimento tecnico per l'algoritmo Microsoft Naive Bayes
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes è un algoritmo di classificazione per la modellazione predittiva incluso in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. L'algoritmo calcola la probabilità condizionale tra colonne di input e stimabili e presuppone che le colonne siano indipendenti. Il nome Naive Bayes deriva da questo presupposto di indipendenza.  
  
## <a name="implementation-of-the-microsoft-naive-bayes-algorithm"></a>Implementazione dell'algoritmo Microsoft Naive Bayes  
 Questo algoritmo include funzionalità di calcolo più semplici di quelle di altri algoritmi [!INCLUDE[msCoName](../../includes/msconame-md.md)] ed è utile pertanto per generare rapidamente i modelli di data mining al fine di individuare le relazioni tra colonne di input e colonne stimabili. L'algoritmo considera ogni coppia di valori di attributi di input e di output.  
  
 Una descrizione delle proprietà matematiche del teorema di Bayes esula dagli scopi di questa documentazione. Per altre informazioni, vedere il documento di Microsoft Research [Learning Bayesian Networks: The Combination of Knowledge and Statistical Data](http://go.microsoft.com/fwlink/?LinkId=207029) (Informazioni sulle reti bayesiane: combinazione di conoscenza e dati statistici).  
  
 Per una descrizione della modifica delle probabilità in tutti i modelli in modo da tenere conto dei potenziali valori mancanti, vedere [Valori mancanti &#40;Analysis Services - Data mining &#41;](../../analysis-services/data-mining/missing-values-analysis-services-data-mining.md).  
  
### <a name="feature-selection"></a>Selezione funzionalità  
 L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes esegue la selezione automatica delle caratteristiche per limitare il numero di valori considerati quando si compila il modello. Per altre informazioni, vedere [Selezione delle caratteristiche &#40;Data mining&#41;](../../analysis-services/data-mining/feature-selection-data-mining.md).  
  
|Algoritmo|Metodo di analisi|Commenti|  
|---------------|------------------------|--------------|  
|Naive Bayes|entropia di Shannon<br /><br /> Bayes con probabilità a priori K2<br /><br /> Equivalente Bayes Dirichlet con probabilità a priori a distribuzione uniforme (impostazione predefinita)|Naive Bayes accetta solo attributi discreti o discretizzati e non può pertanto utilizzare il punteggio di interesse.|  
  
 L'algoritmo è progettato per ridurre il tempo di elaborazione e selezionare in modo efficiente gli attributi di massima importanza; è tuttavia possibile controllare i dati utilizzati dall'algoritmo impostando i parametri nel modo seguente:  
  
-   Per limitare i valori utilizzati come input, ridurre il valore di MAXIMUM_INPUT_ATTRIBUTES.  
  
-   Per limitare il numero di attributi analizzati dal modello, ridurre il valore di MAXIMUM_OUTPUT_ATTRIBUTES.  
  
-   Per limitare il numero di valori che possono essere presi in considerazione per qualsiasi attributo, ridurre il valore di MINIMUM_STATES.  
  
## <a name="customizing-the-naive-bayes-algorithm"></a>Personalizzazione dell'algoritmo Microsoft Naive Bayes  
 L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes supporta vari parametri che influiscono sul comportamento, sulle prestazioni e sull'accuratezza del modello di data mining risultante. È anche possibile impostare flag di modellazione nelle colonne del modello per controllare la modalità di elaborazione dei dati o impostare flag nella struttura di data mining per specificare la modalità di gestione dei valori mancanti o Null.  
  
### <a name="setting-algorithm-parameters"></a>Impostazione dei parametri dell'algoritmo  
 L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes supporta vari parametri che influiscono sulle prestazioni e sull'accuratezza del modello di data mining risultante. Nella tabella seguente viene descritto ogni parametro.  
  
 *MAXIMUM_INPUT_ATTRIBUTES*  
 Specifica il numero massimo di attributi di input che l'algoritmo è in grado di gestire prima di richiamare la caratteristica di selezione degli attributi. Se si imposta il valore su 0, la caratteristica di selezione degli attributi viene disabilitata per gli attributi di input.  
  
 Il valore predefinito è 255.  
  
 *MAXIMUM_OUTPUT_ATTRIBUTES*  
 Specifica il numero massimo di attributi di output che l'algoritmo è in grado di gestire prima di richiamare la caratteristica di selezione degli attributi. Se si imposta il valore su 0, la caratteristica di selezione degli attributi viene disabilitata per gli attributi di output.  
  
 Il valore predefinito è 255.  
  
 *MINIMUM_DEPENDENCY_PROBABILITY*  
 Specifica la probabilità di dipendenza minima tra gli attributi di input e di output. Questo valore viene utilizzato per limitare le dimensioni del contenuto generato dall'algoritmo. Il valore di questa proprietà è compreso tra 0 e 1. Valori maggiori riducono il numero di attributi nel contenuto del modello.  
  
 Il valore predefinito è 0.5.  
  
 *MAXIMUM_STATES*  
 Specifica il numero massimo di stati degli attributi supportati dall'algoritmo. Se il numero di stati di un attributo è maggiore del numero massimo, l'algoritmo utilizza gli stati più frequenti e considera gli stati rimanenti come mancanti.  
  
 Il valore predefinito è 100.  
  
### <a name="modeling-flags"></a>Flag di modellazione  
 L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Decision Trees supporta i flag di modellazione seguenti. Quando si crea la struttura o il modello di data mining, i flag di modellazione vengono definiti per specificare la modalità di gestione dei valori presenti in ogni colonna durante l'analisi. Per altre informazioni, vedere [Flag di modellazione &#40;data mining&#41;](../../analysis-services/data-mining/modeling-flags-data-mining.md).  
  
|Flag di modellazione|Description|  
|-------------------|-----------------|  
|MODEL_EXISTENCE_ONLY|Indica che la colonna verrà considerata come se presentasse due stati possibili, ovvero Missing ed Existing. Un valore Null è un valore mancante.<br /><br /> Si applica alla colonna del modello di data mining.|  
|NOT NULL|Indica che la colonna non può contenere un valore Null. Se Analysis Services rileva un valore Null durante il training del modello, viene generato un errore.<br /><br /> Si applica alla colonna della struttura di data mining.|  
  
## <a name="requirements"></a>Requisiti  
 Un modello di albero Naive Bayes deve contenere una colonna chiave e almeno un attributo stimabile e un attributo di input. Nessun attributo può essere continuo. Se i dati contengono elementi numerici continui, vengono ignorati o discretizzati.  
  
### <a name="input-and-predictable-columns"></a>Colonne di input e stimabili  
 L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes supporta le colonne di input e le colonne stimabili specifiche riportate nella tabella seguente. Per altre informazioni sul significato dei tipi di contenuto usati in un modello di data mining, vedere [Tipi di contenuto &#40;Data mining&#41;](../../analysis-services/data-mining/content-types-data-mining.md).  
  
|Colonna|Tipi di contenuto|  
|------------|-------------------|  
|Attributo di input|Cyclical, Discrete, Discretized, Key, Table e Ordered|  
|Attributo stimabile|Cyclical, Discrete, Discretized, Table e Ordered|  
  
> [!NOTE]  
>  Sono supportati i tipi di contenuto Cyclical e Ordered ma l'algoritmo li considera come valori discreti e non esegue un'elaborazione speciale.  
  
## <a name="see-also"></a>Vedere anche  
 [Algoritmo Microsoft Naive Bayes](../../analysis-services/data-mining/microsoft-naive-bayes-algorithm.md)   
 [Esempi di Query modello Naive Bayes](../../analysis-services/data-mining/naive-bayes-model-query-examples.md)   
 [Contenuto del modello di data mining per i modelli Naive Bayes &#40; Analysis Services - Data Mining &#41;](../../analysis-services/data-mining/mining-model-content-for-naive-bayes-models-analysis-services-data-mining.md)  
  
  
