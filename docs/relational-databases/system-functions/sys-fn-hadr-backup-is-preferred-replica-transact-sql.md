---
title: sys.fn_hadr_backup_is_preferred_replica  (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.fn_hadr_backup_is_preferred_replica_TSQL
- sys.fn_hadr_backup_is_preferred_replica
- fn_hadr_backup_is_preferred_replica_TSQL
- fn_hadr_backup_is_preferred_replica
dev_langs:
- TSQL
helpviewer_keywords:
- backup on secondary replicas
- active secondary replicas [SQL Server], backup on secondary replicas
- sys.fn_hadr_backup_is_preferred_replica function
ms.assetid: 61b9be77-e2f6-4da1-b2ae-a62cbe226145
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 86dd2be162ab29587589bd4388387da7cf171f6e
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/03/2018
---
# <a name="sysfnhadrbackupispreferredreplica--transact-sql"></a>sys.fn_hadr_backup_is_preferred_replica  (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Utilizzato per determinare se la replica corrente è la replica di backup preferita.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sys.fn_hadr_backup_is_preferred_replica ( 'dbname' )  
```  
  
## <a name="arguments"></a>Argomenti  
 '*dbname*'  
 Nome del database di cui eseguire il backup. *dbname* è di tipo sysname.  
  
## <a name="returns"></a>Valori di codice restituiti  
 Restituisce 1 se il database nell'istanza corrente è nella replica preferita. In caso contrario, restituisce 0.  
  
## <a name="remarks"></a>Osservazioni  
 Utilizzare questa funzione in uno script di backup per determinare se il database corrente si trova nella replica preferita per i backup. È possibile eseguire uno script in ogni replica di disponibilità. Ognuno di questi processi analizza gli stessi dati per determinare il processo da eseguire in modo tale che solo uno dei processi pianificati procede effettivamente alla fase di backup. Il codice di esempio avrà un aspetto analogo al seguente:  
  
```  
If sys.fn_hadr_backup_is_preferred_replica( @dbname ) <> 1   
BEGIN  
-- If this is not the preferred replica, exit (probably without error).  
END  
-- If this is the preferred replica, continue to do the backup.  
  
```  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-using-sysfnhadrbackupispreferredreplica"></a>A. Utilizzo di sys.fn_hadr_backup_is_preferred_replica  
 Nell'esempio seguente viene restituito 1 se il database corrente è la replica di backup preferita.  
  
```  
SELECT sys.fn_hadr_backup_is_preferred_replica ('TestDB');  
GO  
```  
  
##  <a name="RelatedTasks"></a> Attività correlate  
  
-   [Configurare il Backup su repliche di disponibilità &#40; SQL Server &#41;](../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni &#40; gruppi di disponibilità AlwaysOn Transact-SQL &#41;](../../relational-databases/system-functions/always-on-availability-groups-functions-transact-sql.md)   
 [Gruppi di disponibilità Always On &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [CREARE il gruppo di disponibilità &#40; Transact-SQL &#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)   
 [Repliche secondarie attive: Backup in repliche secondarie &#40; Sempre in gruppi di disponibilità &#41; ](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md) [Always On le viste del catalogo di gruppi di disponibilità &#40; Transact-SQL &#41;    ](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)  
  
  
