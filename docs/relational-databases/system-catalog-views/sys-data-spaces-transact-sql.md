---
title: data_spaces (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- data_spaces
- sys.data_spaces_TSQL
- sys.data_spaces
- data_spaces_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.data_spaces catalog view
ms.assetid: f39d55fe-2c0f-472d-a77f-cebc6fea95b5
caps.latest.revision: "34"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f17714f7c16d120891873692769d0d2f764c2626
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="sysdataspaces-transact-sql"></a>sys.data_spaces (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Contiene una riga per ogni spazio dati. Può essere un filegroup, uno schema di partizione o un filegroup di dati FILESTREAM.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|name|**sysname**|Nome dello spazio dati, univoco all'interno del database.|  
|data_space_id|**int**|Numero identificativo dello spazio dati, univoco all'interno del database.|  
|tipo|**Char(2)**|Tipo di spazio dati:<br /><br /> FG = filegroup<br /><br /> FD = filegroup di dati FILESTREAM<br /><br /> FX = filegroup di tabelle con ottimizzazione per la memoria<br /><br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> PS = schema di partizione|  
|type_desc|**nvarchar(60)**|Descrizione del tipo di spazio dati:<br /><br /> FILESTREAM_DATA_FILEGROUP<br /><br /> MEMORY_OPTIMIZED_DATA_FILEGROUP<br /><br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> PARTITION_SCHEME<br /><br /> ROWS_FILEGROUP|  
|is_default|**bit**|1 = spazio dati predefinito. Viene utilizzato quando non si specifica un filegroup o una partizione in un'istruzione CREATE TABLE o CREATE INDEX.<br /><br /> 0 = non è lo spazio dati predefinito.|  
|is_system|**bit**|**Si applica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 1 = Lo spazio dei dati viene utilizzato per i frammenti dell'indice full-text.<br /><br /> 0 = Lo spazio dei dati non viene utilizzato per i frammenti dell'indice full-text.|  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'appartenenza al ruolo public. Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Spazi dei dati &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/data-spaces-transact-sql.md)   
 [Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [Sys.destination_data_spaces &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-destination-data-spaces-transact-sql.md)   
 [Sys. FileGroups &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [Sys. partition_schemes &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-schemes-transact-sql.md)   
 [L'esecuzione di query di catalogo di sistema SQL Server domande frequenti](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [OLTP in memoria &#40;ottimizzazione per la memoria&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
