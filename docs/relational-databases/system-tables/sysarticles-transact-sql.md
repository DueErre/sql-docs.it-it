---
title: sysarticles (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sysarticles
- sysarticles_TSQL
dev_langs: TSQL
helpviewer_keywords: sysarticles system table
ms.assetid: 9d9d5d51-6d8f-4e42-84a9-82e58eb0301e
caps.latest.revision: "30"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2ce368158e29c1ba76442e38d374a5ddd615f75f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="sysarticles-transact-sql"></a>sysarticles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una riga per ogni articolo definito nel database locale. Questa tabella è archiviata nel database pubblicato.  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|Colonna Identity che offre un numero di ID univoco per l'articolo.|  
|**creation_script**|**nvarchar(255)**|Script dello schema per l'articolo.|  
|**del_cmd**|**nvarchar(255)**|Tipo di comando di replica utilizzato per la replica delle eliminazioni con articoli di tabella. Per altre informazioni, vedere [Specificare la modalità di propagazione delle modifiche per gli articoli transazionali](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).|  
|**Descrizione**|**nvarchar(255)**|Voce descrittiva per l'articolo.|  
|**dest_table**|**sysname**|Nome della tabella di destinazione.|  
|**filter**|**int**|ID della stored procedure, utilizzato per il partizionamento orizzontale.|  
|**filter_clause**|**ntext**|Clausola WHERE dell'articolo, utilizzata per il filtro orizzontale.|  
|**ins_cmd**|**nvarchar(255)**|Tipo di comando di replica utilizzato per la replica degli inserimenti con articoli di tabella. Per altre informazioni, vedere [Specificare la modalità di propagazione delle modifiche per gli articoli transazionali](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).|  
|**name**|**sysname**|Nome associato all'articolo, univoco all'interno della pubblicazione.|  
|**ObjID**|**int**|ID dell'oggetto di tabella pubblicato.|  
|**pubid**|**int**|ID della pubblicazione a cui appartiene l'articolo.|  
|**pre_creation_cmd**|**tinyint**|Comando preliminare per l'istruzione DROP TABLE, DELETE TABLE o TRUNCATE:<br /><br /> **0** = none.<br /><br /> **1** = DROP.<br /><br /> **2** = DELETE.<br /><br /> **3** = TRONCAMENTO.|  
|**status**|**tinyint**|Maschera di bit delle opzioni e dello stato dell'articolo, che può corrispondere al risultato dell'applicazione dell'operatore OR logico bit per bit a uno o più dei valori seguenti:<br /><br /> **1** = articolo è attivo.<br /><br /> **8** = Include il nome della colonna nelle istruzioni INSERT.<br /><br /> **16** = utilizza istruzioni con parametrizzata.<br /><br /> **24** = entrambi includono il nome della colonna nelle istruzioni INSERT e utilizza istruzioni con parametri.<br /><br /> **64** = [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> Ad esempio, un articolo attivo che utilizza istruzioni con parametri avrebbe un valore di **17** in questa colonna. Il valore **0** significa che l'articolo è inattivo e proprietà aggiuntive non definite.|  
|**sync_objid**|**int**|ID della tabella o della vista che rappresenta la definizione dell'articolo.|  
|**tipo**|**tinyint**|Tipo di articolo:<br /><br /> **1** = articolo basato su log.<br /><br /> **3** = articolo basato su log con filtro manuale.<br /><br /> **5** = articolo basato su log con vista manuale.<br /><br /> **7** = articolo basato su log con filtro manuale e vista manuale.<br /><br /> **8** = esecuzione di Stored procedure.<br /><br /> **24** = esecuzione di stored procedure serializzabile.<br /><br /> **32** = Stored procedure (solo schema).<br /><br /> **64** = vista (solo schema).<br /><br /> **128** = funzione (solo schema).|  
|**upd_cmd**|**nvarchar(255)**|Tipo di comando di replica utilizzato per la replica degli aggiornamenti con articoli di tabella. Per altre informazioni, vedere [Specificare la modalità di propagazione delle modifiche per gli articoli transazionali](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).|  
|**schema_option**|**Binary (8)**|Maschera di bit delle opzioni di generazione dello schema per l'articolo, che controllano le parti dello schema dell'articolo inserite nello script per il recapito al Sottoscrittore. Per altre informazioni sulle opzioni di schema, vedere [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md).|  
|**dest_owner**|**sysname**|Proprietario della tabella nel database di destinazione.|  
|**ins_scripting_proc**|**int**|Stored procedure o script personalizzato registrato che viene eseguito durante la replica di un'istruzione INSERT.|  
|**del_scripting_proc**|**int**|Stored procedure o script o personalizzato registrato che viene eseguito durante la replica di un'istruzione DELETE.|  
|**upd_scripting_proc**|**int**|Stored procedure o script personalizzato registrato che viene eseguito durante la replica di un'istruzione UPDATE.|  
|**custom_script**|**nvarchar (2048)**|Stored procedure o script personalizzato registrato che viene eseguito alla fine del trigger DDL.|  
|**fire_triggers_on_snapshot**|**bit**|Indica se i trigger replicati vengono eseguiti o meno quando viene applicato lo snapshot. I possibili valori sono i seguenti:<br /><br /> **0** = trigger non vengono eseguiti.<br /><br /> **1** = i trigger vengono eseguiti.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40; Transact-SQL &#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addarticle &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_changearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_helparticle &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)  
  
  
