---
title: Sys. internal_tables (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.internal_tables
- internal_tables
- sys.internal_tables_TSQL
- internal_tables_TSQL
dev_langs: TSQL
helpviewer_keywords:
- internal tables
- sys.internal_tables catalog view
ms.assetid: a5821c70-f150-4676-8476-3a31f7403dca
caps.latest.revision: "52"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cc5ab8560914be149128c55f563bc9e5b422d4d5
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="sysinternaltables-transact-sql"></a>sys.internal_tables (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce una riga per ogni oggetto che rappresenta una tabella interna. Le tabelle interne vengono generate automaticamente da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per supportare varie funzionalità. Quando ad esempio si crea un indice XML primario, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] crea automaticamente una tabella interna per rendere persistenti i dati del documento XML suddiviso. Le tabelle interne vengono visualizzate nel **sys** schema di ogni database e dispongono di nomi univoci, generati dal sistema che indicano la funzione, ad esempio, **xml_index_nodes_2021582240_32001** o  **queue_messages_1977058079**  
  
 Le tabelle interne non includono dati accessibili all'utente e i loro schemi sono fissi e non modificabili. Non è possibile fare riferimento ai nomi delle tabelle interne nelle istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)]. È ad esempio, non è possibile eseguire un'istruzione quale SELECT \* FROM  *\<internal_table_name >*. È tuttavia possibile eseguire query sulle viste del catalogo per vedere i metadati delle tabelle interne.  
  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|**\<Colonne ereditate da Sys. Objects >**||Per un elenco di colonne ereditate da questa vista, vedere [Sys. Objects &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).|  
|**internal_type**|**tinyint**|Tipo di tabella interna:<br /><br /> 201 = **queue_messages**<br /><br /> 202 = **xml_index_nodes**<br /><br /> 203 = **fulltext_catalog_freelist**<br /><br /> 205 = **query_notification**<br /><br /> 206 = **service_broker_map**<br /><br /> 207 = **extended_indexes** (ad esempio, un indice spaziale)<br /><br /> 208 = **filestream_tombstone**<br /><br /> 209 = **change_tracking**<br /><br /> 210 = **tracked_committed_transactions**|  
|**internal_type_desc**|**nvarchar(60)**|Descrizione del tipo di tabella interna:<br /><br /> QUEUE_MESSAGES<br /><br /> XML_INDEX_NODES<br /><br /> FULLTEXT_CATALOG_FREELIST<br /><br /> FULLTEXT_CATALOG_MAP<br /><br /> QUERY_NOTIFICATION<br /><br /> SERVICE_BROKER_MAP<br /><br /> EXTENDED_INDEXES<br /><br /> FILESTREAM_TOMBSTONE<br /><br /> CHANGE_TRACKING<br /><br /> TRACKED_COMMITTED_TRANSACTIONS|  
|**parent_ID**|**int**|ID del padre, indipendentemente dal fatto che sia definito o meno a livello di ambito dello schema. 0 in assenza del padre.<br /><br /> **queue_messages** = **object_id** della coda<br /><br /> **xml_index_nodes** = **object_id** dell'indice xml<br /><br /> **fulltext_catalog_freelist** = **fulltext_catalog_id** del catalogo full-text<br /><br /> **fulltext_index_map** = **object_id** dell'indice full-text<br /><br /> **query_notification**, o **service_broker_map** = 0<br /><br /> **extended_indexes** = **object_id** di un indice esteso, ad esempio un indice spaziale<br /><br /> **object_id** della tabella per la tabella è abilitato il rilevamento = **change_tracking**|  
|**parent_minor_id**|**int**|ID secondario del padre.<br /><br /> **xml_index_nodes** = **index_id** dell'indice XML<br /><br /> **extended_indexes** = **index_id** di un indice esteso, ad esempio un indice spaziale<br /><br /> 0 = **queue_messages**, **fulltext_catalog_freelist**, **fulltext_index_map**, **query_notification**,  **service_broker_map**, o **change_tracking**|  
|**lob_data_space_id**|**int**|Un valore diverso da zero rappresenta l'ID dello spazio dei dati (filegroup o schema di partizione) contenente i dati LOB (Large Object) per questa tabella.|  
|**filestream_data_space_id**|**int**|Riservato per utilizzi futuri.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="remarks"></a>Osservazioni  
 Le tabelle interne sono collocate nello stesso filegroup dell'entità padre. È possibile utilizzare la query del catalogo illustrata nell'esempio F seguente per restituire il numero di pagine utilizzate dalle tabelle interne per i dati all'interno di righe, all'esterno di righe e LOB (Large Object).  
  
 È possibile utilizzare il [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md) procedure di sistema per restituire i dati di utilizzo dello spazio per le tabelle interne. **sp_spaceused** indica lo spazio di tabelle interne nei modi seguenti:  
  
-   Quando il nome di una coda è specificato, viene fatto riferimento alla tabella interna sottostante associata alla coda e viene indicato l'utilizzo dello spazio da parte della tabella.  
  
-   Le pagine utilizzate dalle tabelle interne di indici XML, gli indici spaziali e indici full-text sono inclusi nel **index_size** colonna. Quando viene specificato un nome di tabella o vista indicizzata, le pagine per gli indici XML, gli indici spaziali e indici full-text per l'oggetto vengono incluse nelle colonne **riservato** e **index_size**.  
  
## <a name="examples"></a>Esempi  
 Negli esempi seguenti viene illustrato come eseguire query sui metadati delle tabelle interne utilizzando le viste del catalogo.  
  
### <a name="a-show-internal-tables-that-inherit-columns-from-the-sysobjects-catalog-view"></a>A. Visualizzazione delle tabelle interne che ereditano le colonne dalla vista del catalogo sys.objects  
  
```  
SELECT * FROM sys.objects WHERE type = 'IT';  
```  
  
### <a name="b-return-all-internal-table-metadata-including-that-which-is-inherited-from-sysobjects"></a>B. Restituzione di tutti i metadati delle tabelle interne, inclusi quelli ereditati da sys.objects  
  
```  
SELECT * FROM sys.internal_tables;  
```  
  
### <a name="c-return-internal-table-columns-and-column-data-types"></a>C. Restituzione delle colonne delle tabelle interne e dei tipi di dati colonna  
  
```  
SELECT SCHEMA_NAME(itab.schema_id) AS schema_name  
    ,itab.name AS internal_table_name  
    ,typ.name AS column_data_type   
    ,col.*  
FROM sys.internal_tables AS itab  
JOIN sys.columns AS col ON itab.object_id = col.object_id  
JOIN sys.types AS typ ON typ.user_type_id = col.user_type_id  
ORDER BY itab.name, col.column_id;  
```  
  
### <a name="d-return-internal-table-indexes"></a>D. Restituzione degli indici delle tabelle interne  
  
```  
SELECT SCHEMA_NAME(itab.schema_id) AS schema_name  
    , itab.name AS internal_table_name  
    , idx.*  
FROM sys.internal_tables AS itab  
JOIN sys.indexes AS idx ON itab.object_id = idx.object_id  
ORDER BY itab.name, idx.index_id;  
```  
  
### <a name="e-return-internal-table-statistics"></a>E. Restituzione delle statistiche delle tabelle interne  
  
```  
SELECT SCHEMA_NAME(itab.schema_id) AS schema_name  
    ,itab.name AS internal_table_name  
    , s.*  
FROM sys.internal_tables AS itab  
JOIN sys.stats AS s ON itab.object_id = s.object_id  
ORDER BY itab.name, s.stats_id;  
```  
  
### <a name="f-return-internal-table-partition-and-allocation-unit-information"></a>F. Restituzione delle informazioni sulle partizioni e sulle unità di allocazione delle tabelle interne  
  
```  
SELECT SCHEMA_NAME(itab.schema_id) AS schema_name  
    ,itab.name AS internal_table_name  
    ,idx.name AS heap_or_index_name  
    ,p.*  
    ,au.*  
FROM sys.internal_tables AS itab  
JOIN sys.indexes AS idx  
--     JOIN to the heap or the clustered index  
    ON itab.object_id = idx.object_id AND idx.index_id IN (0,1)  
JOIN   sys.partitions AS p   
    ON p.object_id = idx.object_id AND p.index_id = idx.index_id  
JOIN   sys.allocation_units AS au  
--     IN_ROW_DATA (type 1) and ROW_OVERFLOW_DATA (type 3) => JOIN to partition's Hobt  
--     else LOB_DATA (type 2) => JOIN to the partition ID itself.  
ON au.container_id =    
    CASE au.type   
        WHEN 2 THEN p.partition_id   
        ELSE p.hobt_id   
    END  
ORDER BY itab.name, idx.index_id;  
```  
  
### <a name="g-return-internal-table-metadata-for-xml-indexes"></a>G. Restituzione dei metadati delle tabelle interne per gli indici XML  
  
```  
SELECT t.name AS parent_table  
    ,t.object_id AS parent_table_id  
    ,it.name AS internal_table_name  
    ,it.object_id AS internal_table_id  
    ,xi.name AS primary_XML_index_name  
    ,xi.index_id as primary_XML_index_id  
FROM sys.internal_tables AS it  
JOIN sys.tables AS t   
    ON it.parent_id = t.object_id  
JOIN sys.xml_indexes AS xi   
    ON it.parent_id = xi.object_id  
    AND it.parent_minor_id  = xi.index_id  
WHERE it.internal_type_desc = 'XML_INDEX_NODES';  
GO  
```  
  
### <a name="h-return-internal-table-metadata-for-service-broker-queues"></a>H. Restituzione dei metadati delle tabelle interne per le code di Service Broker  
  
```  
SELECT q.name AS queue_name  
    ,q.object_id AS queue_id  
    ,it.name AS internal_table_name  
    ,it.object_id AS internal_table_id  
FROM sys.internal_tables AS it  
JOIN sys.service_queues  AS  q ON it.parent_id = q.object_id  
WHERE it.internal_type_desc = 'QUEUE_MESSAGES';  
GO  
```  
  
## <a name="i-return-internal-table-metadata-for-all-service-broker-services"></a>I. Restituzione dei metadati delle tabelle interne per tutti i servizi di Service Broker  
  
```  
SELECT *   
FROM tempdb.sys.internal_tables   
WHERE internal_type_desc = 'SERVICE_BROKER_MAP';  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Oggetto viste del catalogo &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  
  
  
