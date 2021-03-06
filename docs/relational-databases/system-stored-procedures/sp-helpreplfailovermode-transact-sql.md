---
title: sp_helpreplfailovermode (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_helpreplfailovermode
- sp_helpreplfailovermode_TSQL
helpviewer_keywords: sp_helpreplfailovermode
ms.assetid: d1090e42-6840-4bf6-9aa9-327fd8987ec2
caps.latest.revision: "30"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 212775844dde7400ca3ddb17753091aa56b582f1
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="sphelpreplfailovermode-transact-sql"></a>sp_helpreplfailovermode (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Visualizza la modalità di failover corrente di una sottoscrizione. Questa stored procedure viene eseguita in qualsiasi database del Sottoscrittore. Per ulteriori informazioni sulle modalità di failover, vedere [sottoscrizioni aggiornabili per la replica transazionale](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_helpreplfailovermode [ @publisher= ] 'publisher'   
    [ , [ @publisher_db = ] 'publisher_db' ]   
    [ , [ @publication = ] 'publication' ]   
    [ , [ @failover_mode_id= ] 'failover_mode_id'OUTPUT]   
    [ , [ @failover_mode = ] 'failover_mode'OUTPUT]   
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@publisher=**] **'***publisher***'**  
 Nome del server di pubblicazione che partecipa all'aggiornamento del Sottoscrittore. *server di pubblicazione* è **sysname**, non prevede alcun valore predefinito. Il server di pubblicazione deve essere già configurato per la pubblicazione.  
  
 [  **@publisher_db =**] **'***publisher_db***'**  
 Nome del database di pubblicazione. *publisher_db* è **sysname**, non prevede alcun valore predefinito.  
  
 [  **@publication=**] **'***pubblicazione***'**  
 Nome della pubblicazione che partecipa all'aggiornamento del Sottoscrittore. *pubblicazione*è **sysname**, non prevede alcun valore predefinito.  
  
 [  **@failover_mode_id=**] **'***failover_mode_id***' OUTPUT**  
 Restituisce il valore intero della modalità di failover e un **OUTPUT** parametro. *failover_mode_id* è un **tinyint** il valore predefinito è **0**. Restituisce **0** per l'aggiornamento immediato e **1** per l'aggiornamento in coda.  
  
 [**@failover_mode=**] **'***failover_mode***' OUTPUT**  
 Restituisce la modalità di implementazione delle modifiche dei dati nel Sottoscrittore. *failover_mode* è un **nvarchar (10)** con un valore predefinito è NULL. È un **OUTPUT** parametro.  
  
|Valore|Description|  
|-----------|-----------------|  
|**controllo immediato**|Aggiornamento immediato: gli aggiornamenti implementati nel Sottoscrittore vengono propagati immediatamente al server di pubblicazione tramite il protocollo di commit in due fasi (2PC).|  
|**in coda**|Aggiornamento in coda: gli aggiornamenti implementati nel Sottoscrittore vengono archiviati in una coda.|  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_helpreplfailovermode** viene utilizzato nella replica snapshot o transazionale per le sottoscrizioni sono abilitate per l'aggiornamento immediato con aggiornamento in coda come failover, in caso di errore.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server o **db_owner** ruolo predefinito del database possono eseguire **sp_helpreplfailovermode**.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_setreplfailovermode &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-setreplfailovermode-transact-sql.md)  
  
  
