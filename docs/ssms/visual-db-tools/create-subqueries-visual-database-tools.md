---
title: Creare sottoquery (Visual Database Tools) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- search criteria [SQL Server], subqueries
- nested queries
- subqueries [SQL Server], SQL pane
ms.assetid: 34f6b9b4-ca3a-4a4f-9594-36e513f1c547
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 2eb9fd6d0a542c4b9636edb1b65b146b0c043e2d
ms.lasthandoff: 04/11/2017

---
# <a name="create-subqueries-visual-database-tools"></a>Creazione di sottoquery (Visual Database Tools)
È possibile utilizzare i risultati di una query come input per un'altra. I risultati di una sottoquery possono essere usati come istruzione che usa la funzione IN( ), l'operatore EXISTS o la clausola FROM.  
  
Per creare una sottoquery, immetterla direttamente nel riquadro SQL oppure copiare una query e incollarla in un'altra query.  
  
### <a name="to-define-a-subquery-in-the-sql-pane"></a>Per definire una sottoquery nel riquadro SQL  
  
1.  Creare la query primaria.  
  
2.  Selezionare l'istruzione SQL nel riquadro SQL e usare il comando **Copia** per copiare la query negli Appunti.  
  
3.  Iniziare la nuova query e usare il comando **Incolla** per spostare la prima query nella clausola WHERE o FROM della nuova query.  
  
    Si supponga ad esempio di disporre di due tabelle, `products` e `suppliers`, e di creare una query che mostri tutti i prodotti dei fornitori in Svezia. Creare la prima query sulla tabella `suppliers` per individuare tutti i fornitori svedesi:  
  
    ```  
    SELECT supplier_id  
    FROM supplier  
    WHERE (country = 'Sweden')  
    ```  
  
    Utilizzare il comando Copia per copiare la query negli Appunti. Creare la seconda query utilizzando la tabella `products` , in cui sono elencate tutte le informazioni necessarie sui prodotti:  
  
    ```  
    SELECT product_id, supplier_id, product_name  
    FROM products  
    ```  
  
    Nel riquadro SQL aggiungere una clausola WHERE alla seconda query, quindi incollare la prima query dagli Appunti. Racchiudere fra parentesi la prima query, in modo da ottenere un risultato analogo al seguente:  
  
    ```  
    SELECT product_id, supplier_id, product_name  
    FROM products  
    WHERE supplier_id IN  
       (SELECT supplier_id  
      FROM supplier  
      WHERE (country = 'Sweden'))  
    ```  
  
## <a name="see-also"></a>Vedere anche  
[Tipi di query supportati &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/supported-query-types-visual-database-tools.md)  
[Specifica di criteri di ricerca &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  
