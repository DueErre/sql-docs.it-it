---
title: sp_replrestart (Transact-SQL) | Documenti Microsoft
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
- sp_replrestart_TSQL
- sp_replrestart
helpviewer_keywords: sp_replrestart
ms.assetid: 111b3dbf-92f8-4670-b156-1468c63e4fc1
caps.latest.revision: "14"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a814699481f34510798bb0430fa3411bf5943ad3
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="spreplrestart-transact-sql"></a>sp_replrestart (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Questa stored procedure viene utilizzata dalla replica transazionale durante il backup e il ripristino, in modo che i dati replicati nel server di distribuzione vengano sincronizzati con i dati nel server di pubblicazione. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
> [!IMPORTANT]  
>  **sp_replrestart** è una replica interna stored procedure e deve essere utilizzata solo quando si ripristina un database pubblicato in una topologia di replica transazionale, come indicato nell'argomento [strategie di backup e ripristino Replica snapshot e transazionale](../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_replrestart  
```  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_replrestart** viene utilizzato quando il valore di numero (LSN) di sequenza del log più elevato nel server di distribuzione corrisponde il valore LSN più elevato nel server di pubblicazione.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server o **db_owner** ruolo predefinito del database possono eseguire **sp_replrestart**.  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure per la replica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
