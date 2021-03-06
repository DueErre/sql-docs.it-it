---
title: Supporto delle traduzioni in Analysis Services | Documenti Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Business Intelligence Development Studio, translations [Analysis Services]
- translations [Analysis Services], about translations
- object translations [Analysis Services]
- language identifiers [Analysis Services]
- attribute translations [Analysis Services]
- translations [Analysis Services]
ms.assetid: 018471e0-3c82-49ec-aa16-467fb58a6d5f
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: fc97336300fef2dd621f1f151ff39a04cc3fbfe6
ms.sourcegitcommit: 82c9868b5bf95e5b0c68137ba434ddd37fc61072
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/22/2018
---
# <a name="translation-support-in-analysis-services"></a>Supporto delle traduzioni in Analysis Services
[!INCLUDE[ssas-appliesto-sqlas-aas](../includes/ssas-appliesto-sqlas-aas.md)]

  In un modello di dati di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] è possibile incorporare più traduzioni di una didascalia o di una descrizione per fornire stringhe specifiche delle impostazioni cultura in base all'identificatore LCID. Per i modelli multidimensionali, è possibile aggiungere traduzioni per il nome del database, gli oggetti cubo e gli oggetti dimensione del database. Per i modelli tabulari, è possibile tradurre le descrizioni e le didascalie di tabella e colonna.  
  
 La definizione di una traduzione crea i metadati e la didascalia tradotta all'interno del modello, ma per eseguire il rendering delle stringhe localizzate in un'applicazione client, è necessario impostare la proprietà **Language** per l'oggetto o passare un parametro **Culture** o **Locale Identifier** nella stringa di connessione, ad esempio impostando `LocaleIdentifier=1036` per restituire le stringhe in francese.  
  
 Pensare di usare **Locale Identifier** se si vuole supportare più traduzioni simultanee dello stesso oggetto in lingue diverse. L'impostazione della proprietà **Language** funziona, ma influisce anche sull'elaborazione e l'esecuzione di query comportando conseguenze impreviste. È preferibile scegliere di impostare il parametro **Locale Identifier** in quanto viene usato solo per restituire le stringhe tradotte.  
  
 Una traduzione è costituita da un identificatore delle impostazioni locali (LCID), una didascalia tradotta per l'oggetto (ad esempio, il nome di una dimensione o di un attributo), e facoltativamente un'associazione a una colonna che fornisce i valori dei dati nella lingua di destinazione. È possibile avere più traduzioni, ma è possibile usarne solo una per ogni connessione specifica. In teoria, non vi sono limiti al numero di traduzioni che è possibile incorporare nel modello, ma ogni traduzione aggiunge complessità al test e tutte le traduzioni devono condividere le stesse regole di confronto, pertanto quando si progetta la soluzione tenere presenti questi vincoli normali.  
  
> [!TIP]  
>  È possibile usare le applicazioni client quali Excel, Management Studio e SQL Server Profiler per restituire le stringhe tradotte. Per informazioni dettagliate, vedere [Suggerimenti e procedure consigliate per la globalizzazione &#40;Analysis Services&#41;](../analysis-services/globalization-tips-and-best-practices-analysis-services.md).  
  
## <a name="how-to-add-translated-metadata-to-model-in-analysis-services"></a>Come aggiungere metadati tradotti al modello in Analysis Services  
 Per istruzioni dettagliate, usare questi collegamenti:  
  
-   [Traduzioni in modelli tabulari &#40;Analysis Services&#41;](../analysis-services/tabular-models/translations-in-tabular-models-analysis-services.md)  
  
-   [Traduzioni nei modelli multidimensionali &#40;Analysis Services&#41;](../analysis-services/multidimensional-models/translations-in-multidimensional-models-analysis-services.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Scenari di globalizzazione per Analysis Services](../analysis-services/globalization-scenarios-for-analysis-services.md)   
 [Lingue e regole di confronto &#40; Analysis Services &#41;](../analysis-services/languages-and-collations-analysis-services.md)   
 [Impostare o modificare le regole di confronto delle colonne](../relational-databases/collations/set-or-change-the-column-collation.md)   
 [Suggerimenti per la globalizzazione e procedure consigliate &#40; Analysis Services &#41;](../analysis-services/globalization-tips-and-best-practices-analysis-services.md)  
  
  
