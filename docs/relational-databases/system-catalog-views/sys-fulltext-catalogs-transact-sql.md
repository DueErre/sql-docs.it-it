---
title: sys.fulltext_catalogs (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.fulltext_catalogs_TSQL
- sys.fulltext_catalogs
- fulltext_catalogs
- fulltext_catalogs_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fulltext_catalogs catalog view
ms.assetid: cf1489ff-4819-41fa-a62a-4ed797a16207
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d4c3f1c279176dea69b27a2c1416af3d15338924
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/03/2018
---
# <a name="sysfulltextcatalogs-transact-sql"></a>sys.fulltext_catalogs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una riga per ogni catalogo full-text.  
  
> [!NOTE]  
>  Le colonne seguenti verranno rimosse in una versione futura di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **data_space_id**, **file_id**, e **percorso**. Non utilizzare queste colonne in un nuovo progetto di sviluppo e modificare non appena possibile le applicazioni in cui una di tali colonne è utilizzata.  
 
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|fulltext_catalog_id|**int**|ID del catalogo full-text. Valore univoco all'interno dei cataloghi full-text del database.|  
|name|**sysname**|Nome del catalogo. Valore univoco all'interno del database.|  
|percorso|**nvarchar(260)**|Nome della directory del catalogo nel file system.|  
|is_default|**bit**|Catalogo full-text predefinito.<br /><br /> True = Predefinito.<br /><br /> False = Non predefinito.|  
|is_accent_sensitivity_on|**bit**|Impostazione del catalogo relativa alla distinzione tra caratteri accentati/non accentati.<br /><br /> True = Distinzione tra caratteri accentati/non accentati supportata.<br /><br /> False = Distinzione tra caratteri accentati/non accentati non supportata.|  
|data_space_id|**int**|Filegroup in cui è stato creato il catalogo.|  
|file_id|**int**|ID del file full-text associato al catalogo.|  
|principal_id|**int**|ID dell'entità di database a cui appartiene il catalogo full-text.|  
|is_importing|**bit**|Indica se il catalogo full-text viene importato:<br /><br /> 1 = Il catalogo viene importato.<br /><br /> 2 = Il catalogo non viene importato.|  
  
## <a name="permissions"></a>Autorizzazioni  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [CREARE il catalogo full-text &#40; Transact-SQL &#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)   
 [ALTER FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)   
 [DROP FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/drop-fulltext-catalog-transact-sql.md)  
  
  
