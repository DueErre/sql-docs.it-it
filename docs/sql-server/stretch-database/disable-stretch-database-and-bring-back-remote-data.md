---
title: Disabilitare Stretch Database e ripristinare i dati remoti | Microsoft Docs
ms.custom: 
ms.date: 08/05/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: stretch-database
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Stretch Database, disabling
- disabling Stretch Database
ms.assetid: c1bbb24e-47e3-46aa-b786-fcadf9fb65ce
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fdaf098327c8cd6e6abcd830e72627a4fa2f30c8
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/09/2018
---
# <a name="disable-stretch-database-and-bring-back-remote-data"></a>Disabilitare Stretch Database e ripristinare i dati remoti
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


  Per disabilitare Stretch Database in una tabella, selezionare **Stretch** per una tabella in SQL Server Management Studio. Selezionare quindi una delle opzioni seguenti.  
  
-   **Disabilita |Ripristina dati da Azure**. Copiare i dati remoti per la tabella da Azure a SQL Server e quindi disabilitare Stretch Database per la tabella. Questa operazione comporta costi di trasferimento dati e non può essere annullata.  
  
-   **Disabilita | Lascia dati in Azure**. Disabilitare Stretch Database per una tabella.  Abbandonare i dati remoti per la tabella in Azure.  
  
 È anche possibile usare Transact-SQL per disabilitare Stretch Database per una tabella o un database.  
  
 Dopo aver disabilitato Stretch Database per una tabella, si interrompe la migrazione dei dati e i risultati delle query non includono più risultati dalla tabella remota.  
  
 Se si vuole sospendere la migrazione dei dati, vedere [Pause and resume data migration &#40;Stretch Database&#41; (Sospendere e riprendere la migrazione dei dati (Estensione database))](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md).  
  
> [!NOTE]
> La disabilitazione di Stretch Database per una tabella o per un database non elimina l'oggetto remoto. Se si vuole eliminare la tabella remota o il database remoto, è necessario eliminarlo tramite il portale di gestione di Azure. Gli oggetti remoti continuano a generare costi di Azure fino a quando non vengono eliminati. Per altre informazioni, vedere [Prezzi di SQL Server Stretch Database](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/).  
  
## <a name="disable-stretch-database-for-a-table"></a>Disabilitare Stretch Database per una tabella  
  
### <a name="use-sql-server-management-studio-to-disable-stretch-database-for-a-table"></a>Usare SQL Server Management Studio per disabilitare Stretch Database per una tabella  
  
1.  In Esplora oggetti di SQL Server Management Studio selezionare la tabella per cui si vuole disabilitare Stretch Database.  
  
2.  Fare clic con il pulsante destro del mouse e scegliere **Estendi**e quindi selezionare una delle opzioni seguenti.  
  
    -   **Disabilita |Ripristina dati da Azure**. Copiare i dati remoti per la tabella da Azure a SQL Server e quindi disabilitare Stretch Database per la tabella. Questo comando non può essere annullato.  
  
        > [!NOTE]
        > Copiare i dati remoti per la tabella da Azure a SQL Server comporta costi per il trasferimento dei dati. Per altre informazioni, vedere [Dettagli prezzi dei trasferimenti di dati](https://azure.microsoft.com/pricing/details/data-transfers/).  
  
         Dopo aver copiato tutti i dati remoti da Azure a SQL Server, l'estensione viene disabilitata per la tabella.  
  
    -   **Disabilita | Lascia dati in Azure**. Disabilitare Stretch Database per una tabella.  Abbandonare i dati remoti per la tabella in Azure.  
  
    > [!NOTE]
    > La disabilitazione di Stretch Database per una tabella non comporta l'eliminazione dei dati remoti o della tabella remota. Se si vuole eliminare la tabella remota, è necessario eliminarla tramite il portale di gestione di Azure. La tabella remota continua a generare costi di Azure fino a quando non viene eliminata. Per altre informazioni, vedere [Prezzi di SQL Server Stretch Database](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/).  
  
### <a name="use-transact-sql-to-disable-stretch-database-for-a-table"></a>Usare Transact-SQL per disabilitare Stretch Database per una tabella  
  
-   Per disabilitare l'estensione per una tabella e copiare i dati remoti per la tabella da Azure a SQL Server, eseguire il comando seguente. Dopo aver copiato tutti i dati remoti da Azure a SQL Server, l'estensione viene disabilitata per la tabella.

    Questo comando non può essere annullato.  
  
    ```sql  
    USE <Stretch-enabled database name>;
    GO
    ALTER TABLE <Stretch-enabled table name>  
       SET ( REMOTE_DATA_ARCHIVE ( MIGRATION_STATE = INBOUND ) ) ; 
    GO 
    ```  
  
    > [!NOTE]
    > Copiare i dati remoti per la tabella da Azure a SQL Server comporta costi per il trasferimento dei dati. Per altre informazioni, vedere [Dettagli prezzi dei trasferimenti di dati](https://azure.microsoft.com/pricing/details/data-transfers/).    
  
-   Per disabilitare l'estensione per una tabella e abbandonare i dati remoti, eseguire il comando seguente.  
  
    ```sql  
    USE <Stretch-enabled database name>;
    GO
    ALTER TABLE <Stretch-enabled table name>  
       SET ( REMOTE_DATA_ARCHIVE = OFF_WITHOUT_DATA_RECOVERY ( MIGRATION_STATE = PAUSED ) ) ; 
    GO
    ```  
  
> [!NOTE]
> La disabilitazione di Stretch Database per una tabella non comporta l'eliminazione dei dati remoti o della tabella remota. Se si vuole eliminare la tabella remota, è necessario eliminarla tramite il portale di gestione di Azure. La tabella remota continua a generare costi di Azure fino a quando non viene eliminata. Per altre informazioni, vedere [Prezzi di SQL Server Stretch Database](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/).  
  
## <a name="disable-stretch-database-for-a-database"></a>Disabilitare Stretch Database per un database  
 Per poter disabilitare Stretch Database per un database, è prima necessario disabilitare Stretch Database nelle singole tabelle abilitate per Stretch nel database.  
  
### <a name="use-sql-server-management-studio-to-disable-stretch-database-for-a-database"></a>Usare SQL Server Management Studio per disabilitare Stretch Database per un database  
  
1.  In Esplora oggetti di SQL Server Management Studio selezionare il database per cui si vuole disabilitare Stretch Database.  
  
2.  Fare clic con il pulsante destro del mouse e scegliere **Attività**, selezionare **Estendi**e quindi **Disabilita**.  
  
> [!NOTE]
> La disabilitazione di Stretch Database per un database non comporta l'eliminazione del database remoto. Se si vuole eliminare il database remoto, è necessario eliminarlo tramite il portale di gestione di Azure. Il database remoto continua a generare costi di Azure fino a quando non viene eliminato. Per altre informazioni, vedere [Prezzi di SQL Server Stretch Database](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/).  
  
### <a name="use-transact-sql-to-disable-stretch-database-for-a-database"></a>Usare Transact-SQL per disabilitare Stretch Database per un database  
 Eseguire il comando seguente.  
  
```sql  
ALTER DATABASE <Stretch-enabled database name>  
    SET REMOTE_DATA_ARCHIVE = OFF ;  
GO 
```  
  
> [!NOTE]
> La disabilitazione di Stretch Database per un database non comporta l'eliminazione del database remoto. Se si vuole eliminare il database remoto, è necessario eliminarlo tramite il portale di gestione di Azure. Il database remoto continua a generare costi di Azure fino a quando non viene eliminato. Per altre informazioni, vedere [Prezzi di SQL Server Stretch Database](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/).  
  
## <a name="see-also"></a>Vedere anche  
 [Opzioni di ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [Pause and resume data migration &#40;Stretch Database&#41; (Sospendere e riprendere la migrazione dei dati (Estensione database))](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md)  
  
  
