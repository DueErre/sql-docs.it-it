---
title: la procedura sp_monitor (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_monitor_TSQL
- sp_monitor
dev_langs: TSQL
helpviewer_keywords: sp_monitor
ms.assetid: cb628496-2f9b-40e4-b018-d0831c4cb018
caps.latest.revision: "18"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8b4ef90280e72a7afd6a8787b053115a4bffa4fa
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2017
---
# <a name="spmonitor-transact-sql"></a>sp_monitor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Visualizza statistiche su [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_monitor  
```  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Description|  
|-----------------|-----------------|  
|**last_run**|Tempo **sp_monitor** ultima esecuzione.|  
|**current_run**|Tempo **sp_monitor** è in esecuzione.|  
|**secondi**|Numero di secondi trascorsi dopo **sp_monitor** è stata eseguita.|  
|**cpu_busy**|Numero di secondi di attività della CPU del server per l'elaborazione di operazioni [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**io_busy**|Numero di secondi trascorsi per l'esecuzione di operazioni di input e output in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**inattività**|Numero di secondi durante i quali [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è rimasto inattivo.|  
|**packets_received**|Numero di pacchetti di input letti da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**packets_sent**|Numero di pacchetti di output scritti da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|**PACKET_ERRORS**|Numero di errori rilevati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] durante la lettura e la scrittura di pacchetti.|  
|**total_read**|Numero di letture eseguite da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**total_write**|Numero di scritture eseguite da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**total_errors**|Numero di errori rilevati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] durante la lettura e la scrittura.|  
|**connessioni**|Numero di accessi o tentativi di accesso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
## <a name="remarks"></a>Osservazioni  
 Tramite una serie di funzioni, in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene tenuto traccia della quantità di operazioni eseguite. L'esecuzione di **sp_monitor** Visualizza i valori correnti restituiti da queste funzioni e Mostra la quantità sono stati modificati dall'ultima volta che è stata eseguita la procedura.  
  
 Per ogni colonna, le statistiche vengono stampate nel formato *numero*(*numero*)-*numero*% o *numero*(*numero*). Il primo *numero* indica il numero di secondi (per **cpu_busy**, **io_busy**, e **inattivo**) o il numero totale (per gli altri variabili) poiché [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è stato riavviato. Il *numero* tra parentesi indica il numero di secondi o il numero totale dall'ultima volta **sp_monitor** è stata eseguita. La percentuale è la percentuale di tempo trascorso dal **sp_monitor** ultima esecuzione. Ad esempio, se il report mostra **cpu_busy** 4250 (215)-68%, la CPU è stata occupata per 4250 secondi dal [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verso l'alto, 215 secondi dall'ultimo avvio **sp_monitor** stato ultima esecuzione e il 68% del Totale tempo trascorso dal **sp_monitor** ultima esecuzione.  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'appartenenza al ruolo predefinito del server **sysadmin** .  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono restituite informazioni relative all'attività di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
USE master  
EXEC sp_monitor  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
||||  
|-|-|-|  
|**last_run**|**current_run**|**secondi**|  
|1998-03-29 11.55|1998-04-04 14.22|561|  
  
||||  
|-|-|-|  
|**cpu_busy**|**io_busy**|**inattività**|  
|190(0)-0%|187(0)-0%|148(556)-99%|  
  
||||  
|-|-|-|  
|**packets_received**|**packets_sent**|**PACKET_ERRORS**|  
|16(1)|20(2)|0(0)|  
  
|||||  
|-|-|-|-|  
|**total_read**|**total_write**|**total_errors**|**connessioni**|  
|141(0)|54920(127)|0(0)|4(0)|  
  
## <a name="see-also"></a>Vedere anche  
 [sp_who &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
