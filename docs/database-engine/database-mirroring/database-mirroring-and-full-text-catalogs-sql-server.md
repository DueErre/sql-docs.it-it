---
title: Mirroring di database e cataloghi full-text (SQL Server) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: database-mirroring
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- database mirroring [SQL Server], interoperability
- full-text catalogs [SQL Server], database mirroring
- catalogs [SQL Server], database mirroring
ms.assetid: e34072ae-fe8a-462d-bb03-02fa0987f793
caps.latest.revision: "50"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6dd18bfa76758bdc8ec5dfd666a2c006d66ad295
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/18/2018
---
# <a name="database-mirroring-and-full-text-catalogs-sql-server"></a>Mirroring di database e cataloghi full-text (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Per eseguire il mirroring di un database che include un catalogo full-text, eseguire le consuete operazioni di backup per creare un backup completo del database principale e quindi ripristinare il backup per copiare il database nel server mirror. Per altre informazioni, vedere [Preparazione di un database mirror per il mirroring &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md).  
  
## <a name="full-text-catalog-and-indexes-before-failover"></a>Catalogo e indici full-text prima del failover  
 Il catalogo full-text di un nuovo database mirror corrisponde a quello disponibile al momento del backup del database. Dopo l'avvio del mirroring del database, tutte le modifiche a livello di catalogo apportate dall'istruzione (CREATE FULLTEXT CATALOG, ALTER FULLTEXT CATALOG, DROP FULLTEXT CATALOG) vengono registrare e inviate al server mirror per la riproduzione nel database mirror. Le modifiche a livello di indice, invece, non vengono replicate nel database mirror perché non vengono registrate nel server principale. Pertanto, quando cambia il contenuto del catalogo full-text nel database principale, il contenuto del catalogo full-text nel database mirror non sarà sincronizzato.  
  
## <a name="full-text-indexes-after-failover"></a>Indici full-text dopo il failover  
 Dopo un failover, la ricerca completa di un indice full-text sul nuovo server principale può risultare utile o necessaria nelle situazioni seguenti:  
  
-   Se è disabilitato il rilevamento delle modifiche su un indice full-text, è necessario avviare una ricerca per indicizzazione completa utilizzando l'istruzione seguente:  
  
     ALTER FULLTEXT INDEX ON *nome_tabella* START FULL POPULATION  
  
-   Se un indice full-text è configurato per il rilevamento automatico delle modifiche, l'indice viene sincronizzato automaticamente. La sincronizzazione, tuttavia, determina un rallentamento delle prestazioni full-text. In caso di rallentamento eccessivo delle prestazioni, è possibile eseguire una ricerca per indicizzazione completa disattivando il rilevamento delle modifiche e quindi reimpostando il rilevamento automatico:  
  
    -   Per disattivare il rilevamento delle modifiche:  
  
         ALTER FULLTEXT INDEX ON *nome_tabella* SET CHANGE_TRACKING OFF  
  
    -   Per impostare il rilevamento automatico delle modifiche:  
  
         ALTER FULLTEXT INDEX ON *nome_tabella* SET CHANGE_TRACKING AUTO  
  
    > [!NOTE]  
    >  Per determinare se il rilevamento automatico delle modifiche è attivo, è possibile usare la funzione [OBJECTPROPERTYEX](../../t-sql/functions/objectpropertyex-transact-sql.md) per eseguire una query sulla proprietà **TableFullTextBackgroundUpdateIndexOn** della tabella.  
  
 Per altre informazioni, vedere [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md).  
  
> [!NOTE]  
>  L'avvio di una ricerca per indicizzazione dopo un failover viene eseguito esattamente come l'avvio di una ricerca per indicizzazione dopo un ripristino.  
  
## <a name="after-forcing-service"></a>Dopo la forzatura del servizio  
 Dopo la forzatura del servizio nel server mirror, con possibile perdita di dati, avviare una ricerca per indicizzazione completa. Il metodo da utilizzare per l'avvio di una ricerca per indicizzazione completa dipende dall'attivazione o disattivazione del rilevamento delle modifiche nell'indice full-text. Per ulteriori informazioni, vedere "Indici full-text dopo il failover" più indietro in questo argomento.  
  
## <a name="see-also"></a>Vedere anche  
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [DROP FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-fulltext-index-transact-sql.md)   
 [Mirroring del database &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [Backup e ripristino di indici e cataloghi full-text](../../relational-databases/search/back-up-and-restore-full-text-catalogs-and-indexes.md)  
  
  
