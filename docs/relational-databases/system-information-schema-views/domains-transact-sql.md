---
title: DOMINI (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-information-schema-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DOMAINS_TSQL
- DOMAINS
dev_langs: TSQL
helpviewer_keywords:
- DOMAINS view
- INFORMATION_SCHEMA.DOMAINS view
ms.assetid: f0b734d5-816f-4b10-a60c-615931b515c2
caps.latest.revision: "44"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2ab3416e33aa79bcb499451b5b4ffa7b50fe4efd
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="domains-transact-sql"></a>DOMAINS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Restituisce una riga per ogni tipo di dati alias accessibile dall'utente corrente nel database corrente.  
  
 Per recuperare informazioni da queste viste, specificare il nome completo di **INFORMATION_SCHEMA.** *view_name*.  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|**DOMAIN_CATALOG**|**nvarchar (**128**)**|Database in cui è incluso il tipo di dati alias.|  
|**DOMAIN_SCHEMA**|**nvarchar (**128**)**|Nome dello schema che contiene il tipo di dati alias.<br /><br /> **\*\*Importante \* \***  non utilizzare viste INFORMATION_SCHEMA per determinare lo schema di un tipo di dati. L'unica modalità affidabile per cercare lo schema di un tipo consiste nell'utilizzare la funzione TYPEPROPERTY.|  
|**NOME_DOMINIO**|**sysname**|Tipo di dati alias.|  
|**DATA_TYPE**|**sysname**|Tipo di dati di sistema.|  
|**CHARACTER_MAXIMUM_LENGTH**|**int**|Lunghezza massima espressa in caratteri per i dati di tipo binario, carattere, text o image.<br /><br /> -1 per **xml** e i dati del tipo di valori di grandi dimensioni. Per gli altri tipi di dati viene restituito NULL. Per altre informazioni, vedere [Tipi di dati &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md).|  
|**CHARACTER_OCTET_LENGTH**|**int**|Lunghezza massima espressa in byte per i dati di tipo binario, carattere, text o image.<br /><br /> -1 per **xml** e i dati del tipo di valori di grandi dimensioni. Per gli altri tipi di dati viene restituito NULL.|  
|**COLLATION_CATALOG**|**varchar (**6**)**|Viene restituito sempre NULL.|  
|**COLLATION_SCHEMA**|**varchar (**3**)**|Viene restituito sempre NULL.|  
|**COLLATION_NAME**|**nvarchar (**128**)**|Restituisce il nome univoco per l'ordinamento, se la colonna è di tipo carattere o **testo** tipo di dati. Per gli altri tipi di dati viene restituito NULL.|  
|**CHARACTER_SET_CATALOG**|**varchar (**6**)**|Restituisce **master**. Indica il database in cui si trova, il set di caratteri se la colonna è di tipo carattere o **testo** tipo di dati. Per gli altri tipi di dati viene restituito NULL.|  
|**CHARACTER_SET_SCHEMA**|**varchar (**3**)**|Viene restituito sempre NULL.|  
|**CHARACTER_SET_NAME**|**nvarchar (**128**)**|Restituisce il nome univoco per il carattere impostato se questa colonna è di tipo carattere o **testo** tipo di dati. Per gli altri tipi di dati viene restituito NULL.|  
|**NUMERIC_PRECISION**|**tinyint**|Precisione dei dati numerici approssimati, dei dati numerici esatti, dei dati integer o dei dati in valuta. Per gli altri tipi di dati viene restituito NULL.|  
|**NUMERIC_PRECISION_RADIX**|**smallint**|Base di precisione dei dati numerici approssimati, dei dati numerici esatti, dei dati integer o dei dati in valuta. Per gli altri tipi di dati viene restituito NULL.|  
|**NUMERIC_SCALE**|**tinyint**|Scala dei dati numerici approssimati, dei dati numerici esatti, dei dati integer o dei dati in valuta. Per gli altri tipi di dati viene restituito NULL.|  
|**DATETIME_PRECISION**|**smallint**|Codice di sottotipo per **datetime** e ISO **intervallo** tipo di dati. Per gli altri tipi di dati in questa colonna viene restituito NULL.|  
|**DOMAIN_DEFAULT**|**nvarchar (**4000**)**|Testo effettivo dell'istruzione di definizione [!INCLUDE[tsql](../../includes/tsql-md.md)].|  
  
## <a name="see-also"></a>Vedere anche  
 [Viste di sistema &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Viste degli schemi delle informazioni &#40; Transact-SQL &#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [Sys.syscharsets &#40; Transact-SQL &#41;](../../relational-databases/system-compatibility-views/sys-syscharsets-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)   
 [Sys. Types &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)  
  
  
