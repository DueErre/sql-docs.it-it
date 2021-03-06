---
title: Riconciliare un diagramma di database con un database modificato (Visual Database Tools) | Microsoft Docs
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
- updating diagram to match database
- reconciling database diagrams
- diagrams [SQL Server], reconciling changes
- updating database to match diagram
- database diagrams [SQL Server], reconciling changes
ms.assetid: eda8dea2-eedd-43a7-85aa-92bd97783b5f
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f9943baa610ab167d3421b7f4d68ac81f04dcece
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/17/2018
---
# <a name="reconcile-a-database-diagram-with-a-modified-database-visual-database-tools"></a>Riconciliazione di un diagramma di database con un database modificato (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Il diagramma di database viene salvato per aggiornare il database in modo che corrisponda al diagramma. Tuttavia, se il database è stato aggiornato da altri utenti dopo l'apertura del diagramma, le modifiche apportate potranno avere effetto sul diagramma e viceversa.  
  
Salvando il diagramma, le differenze tra il database e il diagramma verranno riconciliate sovrascrivendo le modifiche apportate da altri utenti, al fine di garantire la corrispondenza tra il database e il diagramma.  
  
### <a name="to-update-a-database-to-match-your-diagram"></a>Per aggiornare un database in modo che corrisponda al diagramma  
  
1.  Salvare il diagramma del database.  
  
    Se si salva il diagramma per la prima volta, specificare un nome per il diagramma nella finestra di dialogo **Salva nuovo diagramma di database** e scegliere **OK**.  
  
2.  Nella finestra di dialogo **Salva** è contenuto l'elenco delle tabelle su cui influirà il salvataggio del diagramma. Scegliere **Sì** per continuare.  
  
3.  Nella finestra di dialogo **Rilevate modifiche al database** vengono elencati gli oggetti modificati che verranno cambiati per assicurare la corrispondenza con il diagramma. Scegliere **Sì** per salvare il diagramma e accettare l'elenco di modifiche.  
  
    > [!NOTE]  
    > Se il diagramma contiene tabelle e colonne eliminate dal database, salvando il diagramma verranno create nuovamente nel database solo le corrispondenti definizioni. Con questa operazione non verranno ripristinati i dati contenuti in tali oggetti prima dell'eliminazione.  
  
### <a name="to-update-your-diagram-to-match-a-modified-database"></a>Per aggiornare il diagramma in modo che corrisponda a un database modificato  
  
1.  Chiudere il diagramma senza salvare le modifiche.  
  
2.  Fare clic con il pulsante destro del mouse sul diagramma in Esplora oggetti.  
  
3.  Scegliere **Aggiorna**dal menu di scelta rapida.  
  
4.  Aprire nuovamente il diagramma.  
  
## <a name="see-also"></a>Vedere anche  
[Utilizzare diagrammi di database &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/work-with-database-diagrams-visual-database-tools.md)  
  
