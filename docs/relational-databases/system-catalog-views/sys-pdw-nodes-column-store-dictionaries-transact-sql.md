---
title: Sys.pdw_nodes_column_store_dictionaries (Transact-SQL) | Documenti Microsoft
ms.date: 03/03/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: 7ae1c2e4-45c0-4880-a692-1f299fbcfd19
caps.latest.revision: "7"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 72c2787caf0a60e6939ba72199329b8ad79103ca
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/17/2017
---
# <a name="syspdwnodescolumnstoredictionaries-transact-sql"></a>Sys.pdw_nodes_column_store_dictionaries (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contiene una riga per ogni dizionario utilizzato negli indici columnstore. I dizionari vengono utilizzati per codificare alcuni tipi di dati, ma non tutti. Pertanto non tutte le colonne in un indice columnstore contengono dizionari. Un dizionario può essere presente come dizionario primario (per tutti i segmenti) e possibilmente per altri dizionari secondari utilizzati per un subset di segmenti della colonna.  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|**partition_id**|**bigint**|Indica l'ID della partizione. Valore univoco all'interno di un database.|  
|**hobt_id**|**bigint**|ID dell'heap o dell'indice ad albero B (HoBT) per la tabella a cui appartiene l'indice columnstore.|  
|**column_id**|**int**|ID della colonna columnstore.|  
|**dictionary_id**|**int**|ID del dizionario.|  
|**version**|**int**|Versione del formato del dizionario.|  
|**tipo**|**int**|Tipo di dizionario:<br /><br /> 1: dizionario hash contenente **int** valori<br /><br /> 2: non utilizzato<br /><br /> 3: dizionario hash contenente valori stringa<br /><br /> 4: dizionario hash contenente **float** valori|  
|**last_id**|**int**|Ultimo ID dati nel dizionario.|  
|**entry_count**|**bigint**|Numero di voci nel dizionario.|  
|**on_disc_size**|**bigint**|Dimensioni del dizionario in byte.|  
|**pdw_node_id**|**int**|Identificatore univoco di un [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] nodo.|  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione VIEW SERVER STATE.  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Data Warehouse e viste del catalogo Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [CREATE COLUMNSTORE INDEX &#40; Transact-SQL &#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md)   
 [Sys.pdw_nodes_column_store_segments &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-segments-transact-sql.md)   
 [Sys.pdw_nodes_column_store_row_groups &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-row-groups-transact-sql.md)  
  
  