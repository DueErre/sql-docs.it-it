---
title: Definire l'ordinamento di una dimensione | Documenti Microsoft
ms.custom: 
ms.date: 03/01/2017
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
- OrderBy property
- dimensions [Analysis Services], ordering
- Business Intelligence enhancements [Analysis Services], ordering
- dimensions [Analysis Services], Business Intelligence enhancements
- ordering dimensions [Analysis Services]
- OrderByAttributeID property
ms.assetid: c42fbd58-244d-4e0a-b715-6f919cbc3ad9
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 128efeccdeb3b99a580bd4e2f2ba360df874c222
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/15/2018
---
# <a name="bi-wizard---define-the-ordering-for-a-dimension"></a>Creazione guidata BI - definire l'ordinamento di una dimensione
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
L'aggiunta della funzionalità avanzata di ordinamento degli attributi a un cubo o una dimensione consente di specificare come verranno ordinati i membri di un attributo. I membri possono essere ordinati in base al nome o alla chiave dell'attributo oppure in base al nome o alla chiave di un altro attributo (tramite una relazione tra attributi). Per impostazione predefinita, i membri vengono ordinati in base al nome. Questa funzionalità avanzata modifica l'impostazione delle proprietà **OrderBy** e **OrderByAttributeID** degli attributi in una dimensione.  
  
 Per aggiungere la funzionalità di ordinamento degli attributi, usare Configurazione guidata funzionalità di Business Intelligence e quindi selezionare l'opzione **Impostazione ordinamento attributi** nella pagina **Scelta funzionalità avanzata** . Questa procedura guidata consente di eseguire in modo semplificato i passaggi relativi alla selezione di una dimensione alla quale si desidera applicare l'ordinamento degli attributi e all'impostazione della modalità di ordinamento degli attributi per la dimensione selezionata.  
  
## <a name="selecting-a-dimension"></a>Selezione di una dimensione  
 Nella prima pagina **Impostazione ordinamento attributi** della procedura guidata specificare la dimensione alla quale si desidera applicare l'ordinamento degli attributi. L'aggiunta della funzionalità avanzata dell'ordinamento degli attributi alla dimensione selezionata implica modifiche alla dimensione. Tali modifiche verranno ereditate da tutti i cubi che includono la dimensione selezionata.  
  
## <a name="specifying-ordering"></a>Impostazione dell'ordinamento  
 Nella seconda pagina **Impostazione ordinamento attributi** della procedura guidata specificare la modalità di ordinamento di tutti gli attributi nella dimensione.  
  
 Nella colonna **Attributo di ordinamento** è possibile modificare l'attributo usato per l'ordinamento. Se l'attributo che si desidera utilizzare per ordinare i membri non è presente nell'elenco, scorrere verso il basso nell'elenco e quindi selezionare  **\<nuovo attributo... >** per aprire la **selezionare una colonna** nella finestra di dialogo in cui è possibile Selezionare una colonna nella tabella della dimensione. La selezione di una colonna tramite la finestra di dialogo **Seleziona colonna** consente di creare un attributo aggiuntivo in base al quale ordinare i membri di un attributo.  
  
 Nella colonna **Criteri** è quindi possibile selezionare se ordinare i membri dell'attributo in base alla **chiave** oppure al **nome**.  
  
  
