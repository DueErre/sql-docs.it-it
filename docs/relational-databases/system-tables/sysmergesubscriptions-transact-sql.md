---
title: Sysmergesubscriptions (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/14/2017
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
- sysmergesubscriptions_TSQL
- sysmergesubscriptions
dev_langs: TSQL
helpviewer_keywords: sysmergesubscriptions system table
ms.assetid: 6adc78da-991d-4c08-98c3-ecb4762e0e99
caps.latest.revision: "22"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cd713b90c4d295eee99953c6561e9a7d057fc39b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="sysmergesubscriptions-transact-sql"></a>sysmergesubscriptions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Viene inclusa una riga per ogni Sottoscrittore noto ed è una tabella locale nel server di pubblicazione. Questa tabella è archiviata nei database di pubblicazione e di sottoscrizione.  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|subscriber_server|**sysname**|ID del server utilizzato per eseguire il mapping del campo srvid al valore specifico del server nella migrazione di una copia del database di sottoscrizione in un server diverso.|  
|db_name|**sysname**|Nome del database di sottoscrizione.|  
|pubid|**uniqueidentifier**|ID della pubblicazione da cui è stata creata la sottoscrizione corrente.|  
|datasource_type|**int**|Tipo di origine dati:<br /><br /> **0** = [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> **2** = OLE DB per jet.|  
|subid|**uniqueidentifier**|Numero di identificazione univoco per la sottoscrizione.|  
|replnickname|**binary**|Nome alternativo compresso per la replica.|  
|replicastate|**uniqueidentifier**|Identificatore univoco utilizzato per determinare se la sincronizzazione precedente ha avuto esito positivo confrontando il valore nel server di pubblicazione con il valore nel Sottoscrittore.|  
|status|**tinyint**|Stato della sottoscrizione:<br /><br /> **0** = inattivo.<br /><br /> **1** = attivo.<br /><br /> **2** = eliminato.|  
|subscriber_type|**int**|Tipo di Sottoscrittore:<br /><br /> **1** = globale.<br /><br /> **2** = locale.<br /><br /> **3** = anonimo.|  
|subscription_type|**int**|Tipo di sottoscrizione:<br /><br /> **0** = push.<br /><br /> **1** = pull.<br /><br /> **2** = anonimo.|  
|sync_type|**tinyint**|Tipo di sincronizzazione:<br /><br /> **1** = automatica.<br /><br /> **2** = Nessuna sincronizzazione.|  
|description|**nvarchar(255)**|Breve descrizione della sottoscrizione.|  
|priority|**real**|Viene specificata la priorità della sottoscrizione e viene consentita l'implementazione della risoluzione dei conflitti in base alla priorità È uguale a **0,00** per tutte le sottoscrizioni locali o anonime.|  
|recgen|**bigint**|Numero dell'ultima generazione ricevuta.|  
|recguid|**uniqueidentifier**|ID univoco dell'ultima generazione ricevuta.|  
|sentgen|**bigint**|Numero dell'ultima generazione inviata.|  
|sentguid|**uniqueidentifier**|ID univoco dell'ultima generazione inviata.|  
|schemaversion|**int**|Numero dell'ultimo schema ricevuto.|  
|schemaguid|**uniqueidentifier**|ID univoco dell'ultimo schema ricevuto.|  
|last_validated|**datetime**|Il **datetime** dell'ultima convalida dei dati del sottoscrittore.|  
|attempted_validate|**datetime**|L'ultimo **datetime** tentativo di convalida nella sottoscrizione.|  
|last_sync_date|**datetime**|Il **datetime** della sincronizzazione.|  
|last_sync_status|**int**|Stato della sottoscrizione:<br /><br /> **0** = tutti i processi sono in attesa di avvio.<br /><br /> **1** = uno o più processi sono in avvio.<br /><br /> **2** = tutti i processi sono stati eseguiti correttamente.<br /><br /> **3** = almeno un processo è in esecuzione.<br /><br /> **4** = tutti i processi sono pianificati e inattivi.<br /><br /> **5** = almeno un processo è il tentativo di esecuzione dopo un errore precedente.<br /><br /> **6** = almeno un processo non è stato eseguito correttamente.|  
|last_sync_summary|**sysname**|Descrizione dei risultati dell'ultima sincronizzazione.|  
|metadatacleanuptime|**datetime**|L'ultimo **datetime** dei metadati scaduti è stata rimossa dalle tabelle di sistema di replica di tipo merge.|  
|partition_id|**int**|Viene identificata la partizione precalcolata alla quale appartiene la sottoscrizione.|  
|cleanedup_unsent_changes|**bit**|Viene indicato che i metadati relativi alle modifiche non inviate sono stati rimossi nel Sottoscrittore.|  
|replica_version|**int**|Identifica la versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per il Sottoscrittore al quale appartiene la sottoscrizione. I possibili valori sono i seguenti:<br /><br /> **90** = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]<br /><br /> **100** = [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
|supportability_mode|**int**|Solo per uso interno.|  
|application_name|**nvarchar (128)**|Solo per uso interno.|  
|subscriber_number|**int**|Solo per uso interno.|  
|last_makegeneration_datetime|**datetime**|L'ultimo **datetime** che è stato eseguito il processo makegeneration per il server di pubblicazione. Per ulteriori informazioni, vedere il parametro - MakeGenerationInterval in [agente Merge repliche](../../relational-databases/replication/agents/replication-merge-agent.md).|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
