---
title: sys.dm_tran_transactions_snapshot (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/30/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_tran_transactions_snapshot
- dm_tran_transactions_snapshot
- sys.dm_tran_transactions_snapshot_TSQL
- dm_tran_transactions_snapshot_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_transactions_snapshot dynamic management view
ms.assetid: 03f64883-07ad-4092-8be0-31973348c647
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f73b2955b25e17cd9c4aea963acb277f11bc3351
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmtrantransactionssnapshot-transact-sql"></a>sys.dm_tran_transactions_snapshot (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Restituisce una tabella virtuale per il **sequence_number** di transazioni che sono attive quando ogni transazione snapshot viene avviata. Le informazioni restituite da questa vista semplificano l'esecuzione delle operazioni seguenti:  
  
-   Individuare il numero di transazioni snapshot attive.  
  
-   Identificare le modifiche dei dati ignorate da una determinata transazione snapshot. Se all'avvio di una transazione snapshot una transazione risulta attiva, tutte le modifiche dei relativi dati vengono ignorate dalla transazione snapshot, anche dopo il commit della transazione.  
  
 Ad esempio, si consideri il seguente output da **Sys.dm tran_transactions_snapshot**:  
  
```  
transaction_sequence_num snapshot_id snapshot_sequence_num  
------------------------ ----------- ---------------------  
59                       0           57  
59                       0           58  
60                       0           57  
60                       0           58  
60                       0           59  
60                       3           57  
60                       3           58  
60                       3           59  
60                       3           60  
```  
  
 La colonna `transaction_sequence_num` identifica il numero di sequenza (XSN) delle transazioni snapshot correnti. L'output ne visualizza due: `59` e `60`. La colonna `snapshot_sequence_num` identifica il numero di sequenza delle transazioni che risultano attive all'avvio delle singole transazioni snapshot.  
  
 L'output indica che la transazione snapshot XSN-59 viene avviata durante l'esecuzione di due transazioni attive, XSN-57 e XSN-58. Se in XSN-57 o XSN-58 si apportano modifiche ai dati, XSN-59 le ignora e utilizza il controllo delle versioni delle righe per mantenere una vista consistente dal punto di vista transazionale del database.  
  
 La transazione snapshot XSN-60 ignora le modifiche dei dati eseguite non solo da XSN-57 e XSN-58, ma anche da XSN 59.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
dm_tran_transactions_snapshot  
```  
  
## <a name="table-returned"></a>Tabella restituita  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|**transaction_sequence_num**|**bigint**|Numero di sequenza di una transazione snapshot.|  
|**snapshot_id**|**int**|ID dello snapshot per ogni istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] avviata in Read committed con il controllo delle versioni delle righe. Questo valore viene utilizzato per generare una vista consistente dal punto di vista transazionale del database che supporta ogni query eseguita in Read committed utilizzando il controllo delle versioni delle righe.|  
|**snapshot_sequence_num**|**bigint**|Numero di sequenza di una transazione attiva all'avvio della transazione snapshot.|  
  
## <a name="permissions"></a>Autorizzazioni  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è necessaria l'autorizzazione VIEW SERVER STATE nel server.  
  
 In [!INCLUDE[ssSDS](../../includes/sssds-md.md)] livelli Premium richiede l'autorizzazione VIEW DATABASE STATE nel database. In [!INCLUDE[ssSDS](../../includes/sssds-md.md)] livelli Standard e Basic richiede il [!INCLUDE[ssSDS](../../includes/sssds-md.md)] account amministratore.  
  
## <a name="remarks"></a>Osservazioni  
 Quando una transazione snapshot viene avviata, il [!INCLUDE[ssDE](../../includes/ssde-md.md)] registra tutte le transazioni attive in quel momento. **Sys.dm tran_transactions_snapshot** restituisce queste informazioni per tutte le transazioni snapshot attive.  
  
 Ogni transazione viene identificata da un numero di sequenza della transazione assegnato all'inizio della transazione. Le transazioni hanno inizio quando viene eseguita un'istruzione BEGIN TRANSACTION o BEGIN WORK. Tuttavia, il [!INCLUDE[ssDE](../../includes/ssde-md.md)] assegna il numero di sequenza della transazione con l'esecuzione della prima istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] che accede ai dati dopo l'istruzione BEGIN TRANSACTION o BEGIN WORK. I numeri di sequenza delle transazioni vengono aumentati di un'unità.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni e viste a gestione dinamica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funzioni e viste a gestione dinamica relative alle transazioni &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  

