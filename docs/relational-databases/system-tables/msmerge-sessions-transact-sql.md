---
title: MSmerge_sessions (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/06/2017
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
- MSmerge_sessions
- MSmerge_sessions_TSQL
dev_langs: TSQL
helpviewer_keywords: MSmerge_sessions system table
ms.assetid: 09ada8fc-c148-4379-9524-7826b1b0216c
caps.latest.revision: "26"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a081578000d831f85f00d8de2da725e6d078e5a8
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="msmergesessions-transact-sql"></a>MSmerge_sessions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Il **MSmerge_sessions** tabella contiene righe di cronologia con i risultati delle precedenti sessioni dei processi dell'agente di Merge. Viene aggiunta una nuova riga alla tabella per ogni esecuzione dell'agente di merge. Questa tabella è archiviata nel database di distribuzione.  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|ID della sessione del processo dell'agente di merge.|  
|**agent_id**|**int**|ID dell'agente di merge.|  
|**start_time**|**datetime**|Ora di inizio dell'esecuzione del processo.|  
|**end_time**|**datetime**|Ora di fine dell'esecuzione del processo.|  
|**duration**|**int**|Durata cumulativa, espressa in secondi, di questa sessione del processo.|  
|**delivery_time**|**int**|Numero di secondi necessari per applicare un batch di modifiche.|  
|**upload_time**|**int**|Numero di secondi necessari per il caricamento delle modifiche nel server di pubblicazione.|  
|**download_time**|**int**|Numero di secondi necessari per il download delle modifiche nel Sottoscrittore.|  
|**delivery_rate**|**float**|Numero medio di comandi recapitati al secondo.|  
|**time_remaining**|**int**|Numero stimato di secondi rimanenti in una sessione attiva.|  
|**percent_complete**|**decimal**|Percentuale stimata rispetto al totale delle modifiche già recapitate in una sessione attiva.|  
|**upload_inserts**|**int**|Numero di inserimenti applicati nel server di pubblicazione.|  
|**upload_updates**|**int**|Numero di aggiornamenti applicati nel server di pubblicazione.|  
|**upload_deletes**|**int**|Numero di eliminazioni applicate nel server di pubblicazione.|  
|**upload_conflicts**|**int**|Numero di conflitti che si sono verificati durante l'applicazione delle modifiche nel server di pubblicazione.|  
|**upload_conflicts_resolved**|**int**|Numero di conflitti che si sono verificati durante l'applicazione delle modifiche nel server di pubblicazione e che sono stati risolti.|  
|**upload_rows_retried**|**int**|Numero di righe con tentativi ripetuti di caricamento nel server di pubblicazione.|  
|**download_inserts**|**int**|Numero di inserimenti applicati nel Sottoscrittore.|  
|**download_updates**|**int**|Numero di aggiornamenti applicati nel Sottoscrittore.|  
|**download_deletes**|**int**|Numero di eliminazioni applicate nel Sottoscrittore.|  
|**download_conflicts**|**int**|Numero di conflitti che si sono verificati durante l'applicazione delle modifiche nel Sottoscrittore.|  
|**download_conflicts_resolved**|**int**|Numero di conflitti che si sono verificati durante l'applicazione delle modifiche nel Sottoscrittore e che sono stati risolti.|  
|**download_rows_retried**|**int**|Numero di righe con tentativi ripetuti di download nel Sottoscrittore.|  
|**schema_changes**|**int**|Numero di modifiche dello schema applicate durante la sessione.|  
|**metadata_rows_cleanedup**|**int**|Numero di righe di metadati rimossi durante la sessione.|  
|**runstatus**|**int**|Stato di esecuzione:<br /><br /> **1** = avvio.<br /><br /> **2** = esito positivo.<br /><br /> **3** = in corso.<br /><br /> **4** = inattivo.<br /><br /> **5** = nuovo tentativo.<br /><br /> **6** = esito negativo.|  
|**estimated_upload_changes**|**int**|Numero stimato di modifiche che devono essere applicate nel server di pubblicazione.|  
|**estimated_download_changes**|**int**|Numero stimato di modifiche che devono essere applicate nel Sottoscrittore.|  
|**connection_type**|**int**|Connessione utilizzata durante il caricamento:<br /><br /> **1** = rete locale (LAN).<br /><br /> **2** = connessione remota.<br /><br /> **3** = sincronizzazione web.|  
|**timestamp**|**timestamp**|Colonna timestamp della tabella.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
