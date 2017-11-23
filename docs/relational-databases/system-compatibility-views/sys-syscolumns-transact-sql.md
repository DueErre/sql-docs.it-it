---
title: Sys.syscolumns (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-enginel, sql-data-warehouse, pdw
ms.service: 
ms.component: system-compatibility-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.syscolumns
- sys.syscolumns_TSQL
- syscolumns_TSQL
- syscolumns
dev_langs: TSQL
helpviewer_keywords:
- syscolumns system table
- sys.syscolumns compatibility view
ms.assetid: 863fd87b-ff33-4ac5-9aa9-df21140681da
caps.latest.revision: "32"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 94f43de0bf804d366b599c053d8dddadf51d809f
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/17/2017
---
# <a name="syssyscolumns-transact-sql"></a>sys.syscolumns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Restituisce una riga per ogni colonna di ogni tabella e vista e una riga per ogni parametro di una stored procedure nel database.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome della colonna o del parametro della procedura.|  
|**id**|**int**|ID di oggetto della tabella a cui appartiene la colonna o ID della stored procedure a cui è associato il parametro.|  
|**tipoX**|**tinyint**|Tipo di archiviazione fisica da **Sys. Types**.|  
|**typestat**|**tinyint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**xusertype**|**smallint**|ID del tipo di dati esteso definito dall'utente. Causa un errore di overflow o restituisce NULL se il numero di tipi di dati è maggiore di 32.767.|  
|**lunghezza**|**smallint**|Lunghezza massima di archiviazione fisica da **sys**. **tipi**.|  
|**xprec**|**tinyint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**XScale**|**tinyint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**colid**|**smallint**|ID di colonna o di parametro.|  
|**Sfalsamento x**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**bitpos**|**tinyint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**riservato**|**tinyint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**colstat**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**cdefault**|**int**|ID del valore predefinito della colonna.|  
|**dominio**|**int**|ID della regola o vincolo CHECK per la colonna.|  
|**numero**|**smallint**|Numero di sottoprocedura quando la procedura è raggruppata.<br /><br /> 0 = Voci non di procedura|  
|**colorder**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**autoval**|**varbinary (8000)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**offset**|**smallint**|Offset nella riga in cui appare la colonna.|  
|**collationid**|**int**|ID delle regole di confronto della colonna. NULL per le colonne non di tipo carattere.|  
|**status**|**tinyint**|Mappa di bit utilizzata per descrivere una proprietà della colonna o del parametro:<br /><br /> 0x08 = La colonna ammette valori Null.<br /><br /> 0x10 = ANSI padding era attivata quando **varchar** o **varbinary** sono state aggiunte colonne. Gli spazi vuoti finali vengono mantenuti per **varchar** e gli zeri finali vengono mantenuti per **varbinary** colonne.<br /><br /> 0x40 = Il parametro è un parametro OUTPUT.<br /><br /> 0x80 = La colonna è una colonna Identity.|  
|**tipo**|**tinyint**|Tipo di archiviazione fisica da **sys**. **tipi**.|  
|**usertype**|**smallint**|ID del tipo di dati definito dall'utente da **Sys. Types**. Causa un errore di overflow o restituisce NULL se il numero di tipi di dati è maggiore di 32.767.|  
|**printfmt**|**varchar (255)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**Prec**|**smallint**|Livello di precisione della colonna.<br /><br /> -1 = **xml** o tipo di valori di grandi dimensioni.|  
|**scala**|**int**|Scala della colonna.<br /><br /> NULL = Tipo di dati non numerico.|  
|**calcolato**|**int**|Flag che indica se si tratta di una colonna calcolata:<br /><br /> 0 = Non calcolata<br /><br /> 1 = Calcolata|  
|**isoutparam**|**int**|Indica se il parametro della procedura è un parametro di output:<br /><br /> 1 = True<br /><br /> 0 = False|  
|**IsNullable**|**int**|Indica se la colonna ammette valori Null:<br /><br /> 1 = True<br /><br /> 0 = False|  
|**regole di confronto**|**sysname**|Nome delle regole di confronto della colonna. NULL se non si tratta di una colonna di tipo carattere.|  
  
## <a name="see-also"></a>Vedere anche  
 [Mapping di tabelle di sistema di viste di sistema &#40; Transact-SQL &#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Viste della compatibilità &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  