---
title: Modificare le funzioni di acquisizione dei dati (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/14/2017
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
dev_langs:
- TSQL
helpviewer_keywords:
- change data capture [SQL Server], functions
ms.assetid: e5270557-aca3-44ab-8715-daccd498b88d
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 36d2d3a46745c731b6da3835de4fbaffe384a839
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/09/2018
---
# <a name="change-data-capture-functions-transact-sql"></a>Funzioni Change Data Capture (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  I record di acquisizione dei dati delle modifiche inseriscono, aggiornano ed eliminano le attività applicate alle tabelle di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], fornendo i dettagli delle modifiche in un formato relazionale facilmente utilizzabile. Le informazioni sulla colonna che rispecchiano la struttura della colonna di una tabella di origine rilevata vengono acquisite per le righe modificate, insieme ai metadati necessari ad applicare le modifiche a un ambiente di destinazione. Per restituire informazioni sulle modifiche, sono utilizzare le funzioni seguenti.  
  
|||  
|-|-|  
|[cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)|[sys.fn_cdc_has_column_changed &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-has-column-changed-transact-sql.md)|  
|[cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)|[sys.fn_cdc_increment_lsn &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-increment-lsn-transact-sql.md)|  
|[sys.fn_cdc_decrement_lsn &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-decrement-lsn-transact-sql.md)|[sys.fn_cdc_is_bit_set &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-is-bit-set-transact-sql.md)|  
|[sys.fn_cdc_get_column_ordinal &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-get-column-ordinal-transact-sql.md)|[sys.fn_cdc_map_lsn_to_time &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-map-lsn-to-time-transact-sql.md)|  
|[sys.fn_cdc_get_max_lsn &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-get-max-lsn-transact-sql.md)|[sys.fn_cdc_map_time_to_lsn &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md)|  
|[sys.fn_cdc_get_min_lsn &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-get-min-lsn-transact-sql.md)||  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle Change Data Capture &#40;Transact-SQL&#41;](../../relational-databases/system-tables/change-data-capture-tables-transact-sql.md)   
 [Stored procedure Change Data Capture &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/change-data-capture-stored-procedures-transact-sql.md)   
 [Informazioni su Change Data Capture &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)  
  
  
