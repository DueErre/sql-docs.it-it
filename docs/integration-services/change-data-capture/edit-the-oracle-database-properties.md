---
title: "Modificare le proprietà del database Oracle | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: change-data-capture
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- oraProp
ms.assetid: 58dc99f1-ee6b-4508-bb66-2bc589611ff7
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9a83a04c01a48b85395949c9277f77b3d1ede632
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2018
---
# <a name="edit-the-oracle-database-properties"></a>Modificare le proprietà del database Oracle
  Utilizzare la scheda Oracle nell'editor delle proprietà per modificare la descrizione fornita nella pagina Create CDC database della New Instance Wizard e le informazioni di connessione al database di log mining Oracle.  
  
 Di seguito vengono illustrate le informazioni nella scheda **Oracle** .  
  
 **Nome**  
 Nome dell'istanza di CDC immesso nella pagina Create CDC Database della New Instance Wizard. Questo campo è di sola lettura, pertanto non è possibile modificare queste informazioni.  
  
 **Descrizione**  
 È possibile modificare la descrizione della nuova istanza o aggiungerne una se non è stato fatto al momento della creazione dell'istanza di CDC.  
  
 **Oracle Connect String**  
 Stringa di connessione Oracle al computer contenente il database Oracle in uso. Questo campo è di sola lettura, pertanto non è possibile modificare queste informazioni. In seguito ad alcune modifiche alla stringa di connessione, infatti, l'istanza di Oracle CDC può puntare a un altro database Oracle, danneggiando lo stato dell'istanza archiviato nella tabella **cdc.xdbcdc_config** . Qualora fossero necessarie modifiche di piccola entità, è possibile modificare la stringa di connessione direttamente nella tabella di configurazione tramite SQL Server Management Studio.  
  
 **Oracle Log Mining Authentication**  
 Per immettere le credenziali di autenticazione per il database Oracle che contiene il log miner, selezionare una delle opzioni disponibili in **Authentication**:  
  
-   **Windows Authentication**: selezionare questa opzione per utilizzare le credenziali del dominio Windows correnti. È possibile utilizzare questa opzione solo se il database Oracle è configurato per l'utilizzo dell'autenticazione di Windows.  
  
-   **Oracle Authentication**: se si seleziona questa opzione, è necessario digitare il **nome utente** e la **password** dell'utente nel database Oracle a cui si effettua la connessione.  
  
 È possibile visualizzare le proprietà del database Oracle nel visualizzatore. Quando si utilizza il visualizzatore le informazioni sono in sola lettura. Nel visualizzatore è inoltre incluso un elenco delle colonne acquisite nella tabella. Per informazioni su come accedere al visualizzatore, vedere [How to Manage a CDC Instance](../../integration-services/change-data-capture/how-to-manage-a-cdc-instance.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Modalità di gestione di un servizio CDC da CDC Designer Console](../../integration-services/change-data-capture/how-to-manage-a-cdc-service-from-the-cdc-designer-console.md)   
 [Connettersi a un database di origine Oracle](../../integration-services/change-data-capture/connect-to-an-oracle-source-database.md)   
 [Connettersi a Oracle](../../integration-services/change-data-capture/connect-to-oracle.md)  
  
  
