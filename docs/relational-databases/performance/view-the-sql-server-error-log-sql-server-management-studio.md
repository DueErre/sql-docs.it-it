---
title: Visualizzare il log degli errori di SQL Server (SQL Server Management Studio) | Microsoft Docs
ms.custom: 
ms.date: 09/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- viewing logs
- displaying logs
- errors [SQL Server], logs
- logs [SQL Server], SQL Server error logs
- logs [SQL Server], viewing
ms.assetid: 55f468ba-146c-4ab3-95cd-d35d051afd12
caps.latest.revision: "14"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Active
ms.openlocfilehash: a8823906fc96755dd70862e0a362562b956d2739
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/18/2018
---
# <a name="view-the-sql-server-error-log-sql-server-management-studio"></a>Visualizzare il log degli errori di SQL Server (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Il log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contiene eventi definiti dall'utente e alcuni eventi di sistema necessari per la risoluzione dei problemi. 

## <a name="view-the-logs"></a>Visualizzare i log

1. In SQL Server Management Studio selezionare **Esplora oggetti**. Per aprire **Esplora oggetti** selezionare F8. In alternativa, nel menu principale fare clic su **Visualizza** e quindi selezionare **Esplora oggetti**:
    
    ![Object_Explorer](../../relational-databases/performance/media/object-explorer.png) 

2. In **Esplora oggetti**connettersi a un'istanza di SQL Server e quindi espandere l'istanza.
  
3. Trovare ed espandere la sezione **Gestione** (presupponendo di avere le autorizzazioni necessarie per visualizzarla).

4. Fare clic con il pulsante destro del mouse su **Log di SQL Server**, scegliere **Visualizza** e quindi **Log di SQL Server**.

    ![Visualizza log di SQL server in SSMS](../../relational-databases/performance/media/view-sqlserver-log-ssms.png) 
 
5. Viene visualizzato il **Visualizzatore file di log** (potrebbero essere necessari alcuni minuti), con un elenco dei log che è possibile visualizzare.
  
  ## <a name="see-also"></a>Vedere anche
  Per altre informazioni, vedere l'utile post di [MSSQLTips.com](https://www.mssqltips.com/) [Identify location of the SQL Server Error Log file (Identificare la posizione del file di log degli errori di SQL Server)](https://www.mssqltips.com/sqlservertip/2506/identify-location-of-the-sql-server-error-log-file/).

