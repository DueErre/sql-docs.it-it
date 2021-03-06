---
title: partition_functions (Transact-SQL) | Documenti Microsoft
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
- sys.partition_functions_TSQL
- partition_functions
- sys.partition_functions
- partition_functions_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.partition_functions catalog view
ms.assetid: 96515727-728b-4bea-804a-36ce915b8b75
caps.latest.revision: "37"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a440995a63e75705c0a7b5d3c56e1e649c6defbe
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="syspartitionfunctions-transact-sql"></a>sys.partition_functions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  Contiene una riga per ogni funzione di partizione in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome della funzione di partizione. Valore univoco all'interno del database.|  
|**function_id**|**int**|ID della funzione di partizione. Valore univoco all'interno del database.|  
|**tipo**|**Char(2)**|Tipo di funzione.<br /><br /> R = Intervallo|  
|**type_desc**|**nvarchar(60)**|Tipo di funzione.<br /><br /> RANGE|  
|**fan-out**|**int**|Numero di partizioni create dalla funzione.|  
|**boundary_value_on_right**|**bit**|Per il partizionamento per intervalli.<br /><br /> 1 = Il valore limite è incluso nell'intervallo RIGHT del limite.<br /><br /> 0 = LEFT.|  
|**is_system**||**Si applica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 1 = L'oggetto viene utilizzato per i frammenti dell'indice full-text.<br /><br /> 0 = L'oggetto non viene utilizzato per i frammenti dell'indice full-text.|  
|**create_date**|**datetime**|Data di creazione della funzione.|  
|**modify_date**|**datetime**|Data dell'ultima modifica della funzione eseguita mediante un'istruzione ALTER.|  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'appartenenza al ruolo **public** . Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo delle funzioni di partizione &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/partition-function-catalog-views-transact-sql.md)   
 [Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Sys.partition_range_values &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-range-values-transact-sql.md)   
 [Sys. partition_parameters &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-parameters-transact-sql.md)  
  
  
