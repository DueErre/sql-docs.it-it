---
title: MSpeer_lsns (Transact-SQL) | Documenti Microsoft
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
- MSpeer_lsns
- MSpeer_lsns_TSQL
dev_langs: TSQL
helpviewer_keywords: MSpeer_lsns system table
ms.assetid: 0ba33907-601b-4c3d-8099-2663f680a161
caps.latest.revision: "33"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 31b5b65ff2dd13015e8ec0a53a2c6377d6c8aa58
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="mspeerlsns-transact-sql"></a>MSpeer_lsns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Il **Mspeer_lsns** tabella viene utilizzata per eseguire il mapping di ogni transazione a una sottoscrizione in una topologia di replica peer-to-peer. Questa tabella è archiviata in tutti i database di pubblicazione in una topologia di replica peer-to-peer e nel database di sottoscrizione di tutti i Sottoscrittori di una pubblicazione peer-to-peer. Per ulteriori informazioni su questo tipo di topologia di replica transazionale, vedere [la replica transazionale Peer-to-Peer](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md). Questa tabella è archiviata nel database di pubblicazione.  
  
## <a name="definition"></a>Definizione  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Identifica un LSN peer-to-peer.|  
|**last_updated**|**datetime**|Il **datetime** in cui è stato effettuato l'ultimo aggiornamento della riga.|  
|**iniziatore**|**sysname**|Nome del server di pubblicazione che ha avviato la transazione.|  
|**originator_db**|**sysname**|Nome del database in cui è stata avviata la transazione.|  
|**originator_publication**|**sysname**|Nome della pubblicazione in cui è stata avviata la transazione.|  
|**originator_publication_id**|**int**|ID della pubblicazione in cui è stata avviata la transazione.|  
|**originator_db_version**|**int**|Identifica il numero di versione del database di origine.|  
|**originator_lsn**|**int**|Identifica l'LSN nella pubblicazione di origine.|  
|**originator_version**|**int**|Identifica il numero di versione del server di pubblicazione.|  
|**originator_id**|**smallint**|Identifica ogni nodo nella topologia per consentire il rilevamento dei conflitti. Per altre informazioni, vedere [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
