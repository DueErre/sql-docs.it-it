---
title: MSpeer_topologyresponse (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- MSpeer_topologyresponse
- MSpeer_topologyresponse_TSQL
dev_langs: TSQL
helpviewer_keywords: MSpeer_topologyresponse
ms.assetid: 1bc5c0c6-c432-405c-89fd-e953d173a247
caps.latest.revision: "10"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 059fa8cb441bde356e2020a7bf6ffa11e3417ad3
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="mspeertopologyresponse-transact-sql"></a>MSpeer_topologyresponse (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Utilizzata nella replica peer-to-peer per archiviare la risposta di ogni nodo a una richiesta di stato di topologia. Questa tabella è archiviata nel database di pubblicazione.  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|request_id|**int**|Identifica una voce di richiesta di stato di topologia nella [MSpeer_topologyrequest](../../relational-databases/system-tables/mspeer-topologyrequest-transact-sql.md) tabella.|  
|peer|**sysname**|Nome dell'istanza del server che ha generato la risposta.|  
|peer_version|**int**|Identifica il numero di versione del server di pubblicazione.|  
|peer_db|**sysname**|Database di sottoscrizione del peer che ha generato la risposta.|  
|originator_id|**int**|Identifica ogni nodo nella topologia per consentire il rilevamento dei conflitti. Per altre informazioni, vedere [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).|  
|peer_conflict_retention|**int**|Periodo di tempo, espresso in giorni, in cui i metadati vengono archiviati nelle tabelle dei conflitti.|  
|received_date|**datetime**|Ora di ricezione della richiesta di topologia.|  
|connection_info|**xml**|Informazioni sul nodo che ha risposto alla richiesta.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
