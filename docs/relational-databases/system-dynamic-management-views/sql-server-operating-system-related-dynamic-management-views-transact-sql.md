---
title: Sistema operativo SQL Server correlati viste a gestione dinamica (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- operating systems [SQL Server], dynamic management objects
- SQL Operating System dynamic management objects [SQL Server]
- SQL OS dynamic management objects [SQL Server]
- dynamic management objects [SQL Server], SQL OS
ms.assetid: 3030c86a-0a74-4fed-ac0f-392e244cb965
caps.latest.revision: "29"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: bff2c765d5ca12b2a5ef83de337404af629fd240
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/17/2017
---
# <a name="sql-server-operating-system-related-dynamic-management-views-transact-sql"></a>Viste a gestione dinamica relative al sistema operativo di SQL Server (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  In questa sezione sono contenute le DMV associate al sistema operativo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SQLOS), ovvero il sistema operativo di SQL Server responsabile della gestione delle risorse del sistema operativo specifiche di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|||  
|-|-|  
|[sys.dm_os_buffer_descriptors &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-buffer-descriptors-transact-sql.md)|[Sys.dm os_memory_pools &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-pools-transact-sql.md)|  
|[Sys.dm os_child_instances &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-child-instances-transact-sql.md)|[Sys.dm os_nodes &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-nodes-transact-sql.md)|  
|[Sys.dm os_cluster_nodes &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-nodes-transact-sql.md)|[sys.dm_os_performance_counters &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)|  
|[sys.dm_os_dispatcher_pools &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-dispatcher-pools-transact-sql.md)|[Sys.dm os_process_memory &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-process-memory-transact-sql.md)|  
|[sys.dm_os_host_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-host-info-transact-sql.md)|[Sys.dm os_schedulers &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md)|  
|[Sys.dm os_hosts &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-hosts-transact-sql.md)|[Sys.dm os_stacks &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-stacks-transact-sql.md)|  
|[Sys.dm os_latch_stats &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md)|[Sys.dm os_sys_info &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)|  
|[Sys.dm os_loaded_modules &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-loaded-modules-transact-sql.md)|[Sys.dm_os_sys_memory &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-memory-transact-sql.md)|  
|[Sys.dm os_memory_brokers – &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-brokers-transact-sql.md)|[Sys.dm os_tasks &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md)|  
|[Sys.dm os_memory_cache_clock_hands &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-cache-clock-hands-transact-sql.md)|[Sys.dm os_threads &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-threads-transact-sql.md)|  
|[Sys.dm os_memory_cache_counters &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-cache-counters-transact-sql.md)|[Sys.dm os_virtual_address_dump &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-virtual-address-dump-transact-sql.md)|  
|[Sys.dm os_memory_cache_entries &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-cache-entries-transact-sql.md)|[Sys.dm os_volume_stats &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-volume-stats-transact-sql.md)|  
|[Sys.dm os_memory_cache_hash_tables &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-cache-hash-tables-transact-sql.md)|[sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)|  
|[Sys.dm os_memory_clerks &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)|[Sys.dm os_waiting_tasks &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-waiting-tasks-transact-sql.md)|  
|[Sys.dm os_memory_nodes &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-nodes-transact-sql.md)|[Sys.dm os_sys_info &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-windows-info-transact-sql.md)|  
|[Sys.dm os_memory_objects &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql.md)|[os_workers &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md)|  
  
 Le seguenti viste a gestione dinamica relative al sistema operativo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)].  
  
|||  
|-|-|  
|**Sys.dm_os_function_symbolic_name**|**su Sys.dm os_ring_buffers**|  
|**Sys.dm_os_memory_allocations**|**Sys.dm_os_sublatches**|  
|**Sys.dm_os_worker_local_storage**||  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni e viste a gestione dinamica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

