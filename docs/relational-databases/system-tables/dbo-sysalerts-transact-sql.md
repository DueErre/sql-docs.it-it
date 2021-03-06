---
title: dbo.sysalerts (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 10/24/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dbo.sysalerts
- sysalerts_TSQL
- dbo.sysalerts_TSQL
- sysalerts
dev_langs:
- TSQL
helpviewer_keywords:
- sysalerts system table
ms.assetid: a2c2f50d-61f3-4951-996a-add5ad092cc2
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7565ee20e5fdec3a94c413b8204629ce6ee2f48d
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/03/2018
---
# <a name="dbosysalerts-transact-sql"></a>dbo.sysalerts (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una riga per ogni avviso. Un avviso è un messaggio inviato in risposta a un evento con cui è possibile inoltrare messaggi all'esterno dell'ambiente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tramite posta elettronica o cercapersone. Un avviso può generare inoltre un'attività.  Questa tabella è archiviata nel **msdb** database.
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|ID dell'avviso.|  
|**name**|**sysname**|Nome dell'avviso.|  
|**event_source**|**nvarchar(100)**|Origine dell'evento: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**event_category_id**|**int**|Riservato per utilizzi futuri.|  
|**event_id**|**int**|Riservato per utilizzi futuri.|  
|**message_id**|**int**|Definite dall'utente ID messaggio o un riferimento a **sysmessages** messaggio che attiva l'avviso.|  
|**severity**|**int**|Livello di gravità che attiva l'avviso.|  
|**enabled**|**tinyint**|Stato dell'avviso:<br /><br /> **0** = Disabled.<br /><br /> **1** = abilitato.|  
|**delay_between_responses**|**int**|Intervallo espresso in secondi tra due notifiche dell'avviso.|  
|**last_occurrence_date**|**int**|Data dell'ultima occorrenza dell'avviso.|  
|**last_occurrence_time**|**int**|Ora dell'ultima occorrenza dell'avviso.|  
|**last_response_date**|**int**|Data dell'ultima notifica dell'avviso.|  
|**last_response_time**|**int**|Ora dell'ultima notifica dell'avviso.|  
|**notification_message**|**nvarchar(512)**|Informazioni aggiuntive inviate con l'avviso.|  
|**include_event_description**|**tinyint**|Maschera di bit che indica se la descrizione dell'evento viene inviata tramite posta elettronica, cercapersone o Net send. Vedere grafico sotto per i valori.|  
|**database_name**|**nvarchar(512)**|Database in cui è necessario che si verifichi l'avviso affinché venga attivato.|  
|**event_description_keyword**|**nvarchar(100)**|Modello a cui deve corrispondere l'errore affinché venga attivato l'avviso.|  
|**occurrence_count**|**int**|Numero di occorrenze dell'avviso.|  
|**count_reset_date**|**int**|Numero di giorni (date) verrà reimpostata su **0**.|  
|**count_reset_time**|**int**|Ora del numero di giorni viene reimpostato su **0**.|  
|**job_id**|**uniqueidentifier**|ID dell'attività eseguita quando si verifica l'avviso.|  
|**has_notification**|**int**|Numero di operatori che ricevono una notifica tramite posta elettronica quando si verifica un avviso.|  
|**flags**|**int**|Riservato.|  
|**performance_condition**|**nvarchar(512)**|Riservato.|  
|**category_id**|**int**|Riservato.|  
  
 ## <a name="remarks"></a>Osservazioni

Nella tabella seguente vengono illustrati i valori per la maschera di bit include_event_description. Il valore decimale viene restituito da dbo.sysalerts. 

|Decimal | BINARY | Significato |
|------|------|------|
|0 |0000 |Nessun messaggio |
|1 |0001 |Posta elettronica |
|2 |0010 |cercapersone |
|3 |0011 |posta elettronica e cercapersone |
|4 |0100 |Net send |
|5 |0101 |Messaggio di posta elettronica e net send |
|6 |0110 |Cercapersone e net send |
|7 |0111 |Messaggio di posta elettronica, cercapersone e net send |
  
