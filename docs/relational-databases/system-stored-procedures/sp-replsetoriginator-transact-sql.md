---
title: sp_replsetoriginator (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/06/2017
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
- sp_replsetoriginator
- sp_replsetoriginator_TSQL
helpviewer_keywords: sp_replsetoriginator
ms.assetid: 030e5226-0585-439f-b8cd-36f48367d86d
caps.latest.revision: "29"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2c4fc0aa2ee6dcb1b410c55977469d7d62c6f1dd
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="spreplsetoriginator-transact-sql"></a>sp_replsetoriginator (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Utilizzata per richiamare il rilevamento e la gestione di loopback nella replica transazionale bidirezionale. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_replsetoriginator [ @server_name= ] 'server_name'   
    , [ @database_name= ] 'database_name'  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@server_name=**] **'***nome_server***'**  
 Nome del server in cui viene applicata la transazione. *originating_server* è **sysname**, non prevede alcun valore predefinito.  
  
 [  **@database_name=**] **'***database_name***'**  
 Nome del database in cui viene applicata la transazione. *originating_db* è **sysname**, non prevede alcun valore predefinito.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_replsetoriginator** viene eseguita dall'agente di distribuzione per registrare l'origine delle transazioni applicate dalla replica. Queste informazioni vengono utilizzate per richiamare il rilevamento di loopback per le sottoscrizioni transazionali bidirezionali per cui è stata impostata la proprietà di loopback.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** nel server di pubblicazione, i membri del ruolo predefinito del server di **db_owner** ruolo predefinito del database nel database di pubblicazione oppure gli utenti nell'elenco di accesso (PAL) alla pubblicazione possono eseguire **sp_replsetoriginator**.  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
