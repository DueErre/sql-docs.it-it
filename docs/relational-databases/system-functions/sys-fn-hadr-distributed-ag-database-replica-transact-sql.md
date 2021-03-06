---
title: sys.fn_hadr_distributed_ag_database_replica (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/14/2016
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
- sys.fn_hadr_distributed_ag_database_replica
- sys.fn_hadr_distributed_ag_database_replica_TSQL
- fn_hadr_distributed_ag_database_replica
- fn_hadr_distributed_ag_database_replica_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fn_hadr_distributed_ag_database_replica
ms.assetid: 0e6202a1-e872-4f53-99d7-c16b6f712efc
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 89480a854ec65a0894fcaf0cf912d0d3eb68ea24
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/03/2018
---
# <a name="sysfnhadrdistributedagdatabasereplica-transact-sql"></a>sys.fn_hadr_distributed_ag_database_replica (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Utilizzato per eseguire il mapping di un database in un gruppo di disponibilità distribuita per il database nel gruppo di disponibilità locale.  
   
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sys.fn_hadr_distributed_ag_database_replica( lag_Id, database_id )  
```  
  
## <a name="arguments"></a>Argomenti  
 '*lag_Id*'  
 È l'identificatore del gruppo di disponibilità distribuito. *lag_Id* è di tipo **uniqueidentifier**.  
  
 '*database_id*'  
 È l'identificatore del database in un gruppo di disponibilità distribuito. *database_id* è di tipo **uniqueidentifier**.  
  
## <a name="tables-returned"></a>Tabelle restituite  
 Restituisce le informazioni seguenti.  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|**group_database_id**|**uniqueidentifier**|ID del database nel gruppo di disponibilità locale.|  
  
## <a name="examples"></a>Esempi  
  
### <a name="using-sysfnhadrdistributedagdatabasereplica"></a>Using sys.fn_hadr_distributed_ag_database_replica  
 Nell'esempio seguente passa l'ID del database in un gruppo di disponibilità distribuito. Restituisce una tabella con l'ID del database associato al gruppo di disponibilità locale.  
  
```  
DECLARE @lagId uniqueidentifier = '4A03D1A8-4AE6-B153-E7E9-ED22A546008D'  
DECLARE @databaseId uniqueidentifier = '3FFA882A-C4C3-5B9E-A203-8F44BD9659F7'  
  
SELECT * FROM sys.fn_hadr_distributed_ag_database_replica(@lagId, @databaseId)  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni &#40; gruppi di disponibilità AlwaysOn Transact-SQL &#41;](../../relational-databases/system-functions/always-on-availability-groups-functions-transact-sql.md)   
 [Gruppi di disponibilità Always On &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Gruppi di disponibilità distribuiti &#40; Sempre in gruppi di disponibilità &#41;](../../database-engine/availability-groups/windows/distributed-availability-groups-always-on-availability-groups.md)   
 [CREARE il gruppo di disponibilità &#40; Transact-SQL &#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [ALTER AVAILABILITY GROUP &#40; Transact-SQL &#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)  
  
  
