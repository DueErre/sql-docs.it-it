---
title: MSdynamicsnapshotjobs (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- MSdynamicsnapshotjobs_TSQL
- MSdynamicsnapshotjobs
dev_langs: TSQL
helpviewer_keywords: MSdynamicsnapshotjobs system table
ms.assetid: 4f36a325-0e3c-46c4-aeeb-416346cce0bc
caps.latest.revision: "26"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 79f353d2c95f9e7c9c8071de60bb8c2705f675b7
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="msdynamicsnapshotjobs-transact-sql"></a>MSdynamicsnapshotjobs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Il **MSdynamicsnapshotjobs** tabella tiene traccia delle informazioni sul filtro di riga con parametri applicati per generare uno snapshot dei dati filtrati. Questa tabella è archiviata nei database di pubblicazione e di sottoscrizione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**id**|**int**|ID per il processo snapshot dei dati filtrati.|  
|**name**|**sysname**|Nome del processo snapshot dei dati filtrati.|  
|**pubid**|**uniqueidentifier**|Numero di identificazione univoco della pubblicazione.|  
|**job_id**|**uniqueidentifier**|ID del processo di SQL Server Agent nel server di distribuzione.|  
|**agent_id**|**int**|L'ID di SQL Server Agent.|  
|**dynamic_filter_login**|**sysname**|Il valore utilizzato per la valutazione di [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) funzione nei filtri di riga con parametri definiti per la pubblicazione.|  
|**dynamic_filter_hostname**|**sysname**|Il valore utilizzato per la valutazione di [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) funzione nei filtri di riga con parametri definiti per la pubblicazione.|  
|**dynamic_snapshot_location**|**nvarchar(255)**|Percorso della cartella in cui verranno letti i file di snapshot in caso di utilizzo di uno snapshot di dati filtrati.|  
|**partition_id**|**int**|ID della partizione di dati a cui appartiene il processo.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
