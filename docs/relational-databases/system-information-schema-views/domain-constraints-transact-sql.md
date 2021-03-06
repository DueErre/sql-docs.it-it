---
title: DOMAIN_CONSTRAINTS (Transact-SQL) | Documenti Microsoft
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
- DOMAIN_CONSTRAINTS
- DOMAIN_CONSTRAINTS_TSQL
dev_langs: TSQL
helpviewer_keywords:
- INFORMATION_SCHEMA.DOMAIN_CONSTRAINTS view
- DOMAIN_CONSTRAINTS view
ms.assetid: 436c4480-f1e3-403f-b2bd-de04539afe3c
caps.latest.revision: "28"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1e39387eb33957487c57764152d9532c2acd8dde
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="domainconstraints-transact-sql"></a>DOMAIN_CONSTRAINTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Restituisce una riga per ogni tipo di dati alias nel database corrente a cui è associata una regola e a cui può accedere l'utente corrente.  
  
 Per recuperare informazioni da queste viste, specificare il nome completo di **INFORMATION_SCHEMA.** *view_name*.  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|**CONSTRAINT_CATALOG**|**nvarchar (**128**)**|Database in cui esiste la regola.|  
|**CONSTRAINT_SCHEMA**|**nvarchar (**128**)**|Nome dello schema che contiene il vincolo.<br /><br /> **\*\*Importante \* \***  non utilizzare viste INFORMATION_SCHEMA per determinare lo schema di un oggetto. L'unica modalità affidabile per cercare lo schema di un oggetto consiste nell'eseguire una query sulla vista del catalogo sys.objects.|  
|**CONSTRAINT_NAME**|**sysname**|Nome della regola.|  
|**DOMAIN_CATALOG**|**nvarchar (**128**)**|Database in cui è incluso il tipo di dati alias.|  
|**DOMAIN_SCHEMA**|**nvarchar (**128**)**|Nome dello schema che include il tipo di dati alias.<br /><br /> **\*\*Importante \* \***  non utilizzare viste INFORMATION_SCHEMA per determinare lo schema di un tipo di dati. L'unica modalità affidabile per cercare lo schema di un tipo consiste nell'utilizzare la funzione TYPEPROPERTY.|  
|**NOME_DOMINIO**|**sysname**|Tipo di dati alias.|  
|**IS_DEFERRABLE**|**varchar (**2**)**|Specifica se è possibile posticipare la verifica dei vincoli. Restituisce sempre NO.|  
|**INITIALLY_DEFERRED**|**varchar (**2**)**|Specifica se la verifica dei vincoli viene inizialmente posticipata. Restituisce sempre NO.|  
  
## <a name="see-also"></a>Vedere anche  
 [Viste di sistema &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Viste degli schemi delle informazioni &#40; Transact-SQL &#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [Sys. Objects &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [Sys. Types &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)  
  
  
