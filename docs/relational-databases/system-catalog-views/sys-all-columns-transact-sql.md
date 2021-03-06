---
title: Sys.ALL_COLUMNS (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- all_columns_TSQL
- all_columns
- sys.all_columns_TSQL
- sys.all_columns
dev_langs: TSQL
helpviewer_keywords: sys.all_columns catalog view
ms.assetid: 40e04fe9-0b64-4799-84c0-57f128b2bdc2
caps.latest.revision: "48"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d422394e7d23f4bef5554d420a5ca28bc53492de
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="sysallcolumns-transact-sql"></a>sys.all_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Visualizza l'unione di tutte le colonne appartenenti agli oggetti definiti dall'utente e agli oggetti di sistema.  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|object_id|**int**|ID dell'oggetto a cui appartiene la colonna.|  
|name|**sysname**|Nome della colonna. Valore univoco all'interno dell'oggetto.|  
|column_id|**int**|ID della colonna. Valore univoco all'interno dell'oggetto.<br /><br /> È possibile che gli ID di colonna non siano sequenziali.|  
|system_type_id|**tinyint**|ID del tipo di sistema della colonna.|  
|user_type_id|**int**|ID del tipo di colonna definito dall'utente.<br /><br /> Per restituire il nome del tipo, creare un join al [Sys. Types](../../relational-databases/system-catalog-views/sys-types-transact-sql.md) vista per la colonna del catalogo.|  
|max_length|**smallint**|Lunghezza massima in byte della colonna.<br /><br /> -1 = la colonna è di tipo di dati **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, o **xml**.<br /><br /> Per **testo** colonne, il valore max_length sarà 16 o il valore impostato dall'opzione 'text in row' di sp_tableoption.|  
|precisione|**tinyint**|Precisione della colonna se la colonna è di tipo numerico. In caso contrario, 0.|  
|scala|**tinyint**|Scala della colonna se la colonna è di tipo numerico. In caso contrario, 0.|  
|collation_name|**sysname**|Nome delle regole di confronto della colonna se la colonna è di tipo carattere. In caso contrario, NULL.|  
|is_nullable|**bit**|1 = La colonna ammette valori Null.|  
|is_ansi_padded|**bit**|1 = La colonna utilizza l'opzione ANSI_PADDING ON se è di tipo carattere, binary o variant.<br /><br /> 0 = La colonna non è di tipo carattere, binary o variant.|  
|is_rowguidcol|**bit**|1 = La colonna è una parola chiave ROWGUIDCOL dichiarata.|  
|is_identity|**bit**|1 = La colonna ha valori Identity|  
|is_computed|**bit**|1 = La colonna è una colonna calcolata.|  
|is_filestream|**bit**|1 = La colonna è stata dichiarata in modo che utilizzi l'archiviazione filestream.|  
|is_replicated|**bit**|1 = La colonna viene replicata.|  
|is_non_sql_subscribed|**bit**|1 = La colonna dispone di Sottoscrittore non [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|is_merge_published|**bit**|1 = La colonna è inclusa in una pubblicazione di tipo merge.|  
|is_dts_replicated|**bit**|1 = La colonna viene replicata tramite [!INCLUDE[ssIS](../../includes/ssis-md.md)].|  
|is_xml_document|**bit**|1 = Il contenuto è un documento XML completo.<br /><br /> 0 = Il contenuto è un frammento di documento o la colonna non è di tipo XML.|  
|xml_collection_id|**int**|Diverso da zero se il tipo di dati della colonna è **xml** e XML è tipizzato. Il valore sarà l'ID della raccolta contenente lo spazio dei nomi dell'XML Schema di convalida della colonna.<br /><br /> 0 = Nessuna raccolta di XML Schema.|  
|default_object_id|**int**|ID dell'oggetto predefinito, indipendentemente dal fatto che sia autonoma [sp_bindefault](../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md), o un vincolo DEFAULT inline, a livello di colonna. La colonna parent_object_id di un oggetto predefinito inline a livello di colonna è un riferimento alla tabella stessa.<br /><br /> 0 = nessun valore predefinito.|  
|rule_object_id|**int**|ID della regola autonoma associata alla colonna tramite sys.sp_bindrule.<br /><br /> 0 = Nessuna regola autonoma.<br /><br /> Per i vincoli CHECK a livello di colonna, vedere [Sys. CHECK_CONSTRAINTS &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md).|  
|is_sparse|bit|1 = La colonna è di tipo sparse. Per altre informazioni, vedere [Usare le colonne di tipo sparse](../../relational-databases/tables/use-sparse-columns.md).|  
|is_column_set|bit|1 = La colonna è un set di colonne. Per altre informazioni, vedere [Usare set di colonne](../../relational-databases/tables/use-column-sets.md).|  
|generated_always_type|**tinyint**|**Si applica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Il valore numerico che rappresenta il tipo di colonna:<br /><br /> 0 = NOT_APPLICABLE<br /><br /> 1 = AS_ROW_START<br /><br /> 2 = AS_ROW_END|  
|generated_always_type_desc|**nvarchar(60)**|**Si applica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> La descrizione del tipo di colonna:<br /><br /> NOT_APPLICABLE<br /><br /> AS_ROW_START<br /><br /> AS_ROW_END|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetto viste del catalogo &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [L'esecuzione di query di catalogo di sistema SQL Server domande frequenti](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [Sys.system_columns &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-system-columns-transact-sql.md)   
 [Sys. computed_columns &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-computed-columns-transact-sql.md)  
  
  
