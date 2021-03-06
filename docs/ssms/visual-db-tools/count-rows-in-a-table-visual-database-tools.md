---
title: Contare le righe di una tabella (Visual Database Tools) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-visual-db
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- totals [SQL Server], row counts
- row counts [SQL Server]
- column values [SQL Server]
- number of rows
- number of values
- counting rows
ms.assetid: dda4296a-1d16-4e77-8d6f-e295f6dd4e87
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c2174809cafd6fd8b1b7bfad5ee8861d2d91cc09
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/17/2018
---
# <a name="count-rows-in-a-table-visual-database-tools"></a>Conteggio delle righe di una tabella (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Il conteggio delle righe di una tabella consente di determinare:  
  
-   Il numero totale delle righe di una tabella, ad esempio il numero di tutti i libri nella tabella `titles` .  
  
-   Il numero totale delle righe di una tabella che soddisfano una determinata condizione, ad esempio il numero di libri di uno specifico editore nella tabella `titles` .  
  
-   Il numero di valori di una determinata colonna.  
  
Dal conteggio dei valori in una colonna sono esclusi i valori Null. È ad esempio possibile contare il numero di libri nella tabella `titles` che contengono valori nella colonna `advance` . In base all'impostazione predefinita, nel conteggio vengono inclusi tutti i valori, non solo i valori univoci.  
  
Per tutti i tre tipi di conteggio è utilizzata una procedura analoga.  
  
### <a name="to-count-all-the-rows-in-a-table"></a>Per contare tutte le righe di una tabella  
  
1.  Assicurarsi che la tabella che si desidera riepilogare sia già presente nel riquadro Diagramma.  
  
2.  Fare clic con il pulsante destro del mouse sullo sfondo del riquadro Diagramma e scegliere **Aggiungi raggruppamento** dal menu di scelta rapida. In [Progettazione query e Progettazione viste](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) verrà aggiunta una colonna **Group By** alla griglia nel riquadro Criteri.  
  
3.  Selezionare **\&#42; (Tutte le colonne)** nel rettangolo che rappresenta la tabella o l'oggetto con valori di tabella.  
  
    In Progettazione query e Progettazione viste verrà inserito automaticamente il termine **Count** nella colonna **Group By** nel riquadro Criteri e verrà assegnato un alias alla colonna di cui si sta eseguendo il riepilogo. Tale alias generato automaticamente può essere sostituito con un alias più significativo. Per altre informazioni dettagliate, vedere [Creazione di alias di colonna &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-column-aliases-visual-database-tools.md).  
  
4.  Consente di eseguire la query.  
  
### <a name="to-count-all-the-rows-that-meet-a-condition"></a>Per contare tutte le righe che soddisfano una condizione  
  
1.  Assicurarsi che la tabella che si desidera riepilogare sia già presente nel riquadro Diagramma.  
  
2.  Fare clic con il pulsante destro del mouse sullo sfondo del riquadro Diagramma e scegliere **Aggiungi raggruppamento** dal menu di scelta rapida. In Progettazione query e Progettazione viste verrà aggiunta una colonna **Group By** alla griglia nel riquadro Criteri.  
  
3.  Selezionare **\&#42;(Tutte le colonne)** nel rettangolo che rappresenta la tabella o l'oggetto con struttura di tabella.  
  
    In Progettazione query e Progettazione viste verrà inserito automaticamente il termine **Count** nella colonna **Group By** nel riquadro Criteri e verrà assegnato un alias alla colonna di cui si sta eseguendo il riepilogo. Per creare un'intestazione di colonna più utile nell'output della query, vedere [Creazione di alias di colonna &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-column-aliases-visual-database-tools.md).  
  
4.  Aggiungere la colonna di dati da includere nella ricerca e deselezionare la casella di controllo nella colonna **Output**.  
  
    In Progettazione query e Progettazione viste il termine **Group By** verrà inserito automaticamente nella colonna **Group By** della griglia.  
  
5.  Sostituire **Group By** nella colonna **Group By** con **Where**.  
  
6.  Nella colonna **Filtro** per la colonna di dati da includere nella ricerca, specificare la condizione di ricerca.  
  
7.  Consente di eseguire la query.  
  
### <a name="to-count-the-values-in-a-column"></a>Per contare i valori di una colonna  
  
1.  Assicurarsi che la tabella che si desidera riepilogare sia già presente nel riquadro Diagramma.  
  
2.  Fare clic con il pulsante destro del mouse sullo sfondo del riquadro Diagramma e scegliere **Aggiungi raggruppamento** dal menu di scelta rapida. In Progettazione query e Progettazione viste verrà aggiunta una colonna **Group By** alla griglia nel riquadro Criteri.  
  
3.  Aggiungere al riquadro Criteri la colonna su cui si desidera eseguire il conteggio.  
  
    In Progettazione query e Progettazione viste il termine **Group By** verrà inserito automaticamente nella colonna **Group By** della griglia.  
  
4.  Sostituire **Group By** nella colonna **Group By** con **Count**.  
  
    > [!NOTE]  
    > Per contare solo i valori univoci, scegliere **Count Distinct**.  
  
5.  Consente di eseguire la query.  
  
## <a name="see-also"></a>Vedere anche  
[Ordinare e raggruppare i risultati delle query &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[Creare un riepilogo dei risultati di query &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
  
