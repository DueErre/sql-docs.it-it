---
title: sys.sp_xtp_bind_db_resource_pool (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/03/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_xtp_bind_db_resource_pool_TSQL
- sp_xtp_bind_db_resource_pool
- sys.sp_xtp_bind_db_resource_pool_TSQL
- sys.sp_xtp_bind_db_resource_pool
dev_langs:
- TSQL
helpviewer_keywords:
- sp_xtp_bind_db_resource_pool
- sys.sp_xtp_bind_db_resource_pool
ms.assetid: c2a78073-626b-4159-996e-1808f6bfb6d2
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8bcac671ebd335be8e6f22a1385d0c038e61e365
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/03/2018
---
# <a name="sysspxtpbinddbresourcepool-transact-sql"></a>sys.sp_xtp_bind_db_resource_pool (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  Associa il database [!INCLUDE[hek_2](../../includes/hek-2-md.md)] specificato al pool di risorse specificato. Sia il database sia il pool di risorse devono essere disponibili prima di eseguire `sys.sp_xtp_bind_db_resource_pool`.  
  
 Tramite questa procedura di sistema viene creata un'associazione tra il pool di Resource Governor identificato da resource_pool_name e il database identificato da database_name. Non è necessario che gli oggetti del database siano tutti ottimizzati per la memoria al momento dell'associazione. In assenza di questi oggetti, non viene prelevata alcuna memoria dal pool di risorse. Questa associazione verrà utilizzata da Resource Governor per gestire la memoria allocata dagli allocatori di [!INCLUDE[hek_2](../../includes/hek-2-md.md)] come descritto di seguito.  
  
 Se è già disponibile un'associazione per un database specificato, viene restituito un errore dalla procedura.  In nessun caso un database può disporre di più associazioni attive.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
  
## <a name="syntax"></a>Sintassi  
  
```sql  
sys.sp_xtp_bind_db_resource_pool 'database_name', 'resource_pool_name'  
```  
  
## <a name="arguments"></a>Argomenti  
 database_name  
 Nome di un database abilitato per [!INCLUDE[hek_2](../../includes/hek-2-md.md)] esistente.  
  
 resource_pool_name  
 Nome di un pool di risorse esistente.  
  
## <a name="messages"></a>Messaggi  
 In caso di errore, tramite `sp_xtp_bind_db_resource_pool` viene restituito uno di questi messaggi.  
  
 **Database non esiste**  
 Database_name deve fare riferimento a un database esistente. Se non è disponibile alcun database con l'ID specificato, viene restituito il messaggio seguente:   
*ID del database %d non esiste.  Utilizzare un ID di database valido per questa associazione.*  
  
```  
Msg 911, Level 16, State 18, Procedure sp_xtp_bind_db_resource_pool_internal, Line 51  
Database 'Hekaton_DB213' does not exist. Make sure that the name is entered correctly.  
```  
  
**Un database di sistema**  
 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] non è possibile creare tabelle nel database di sistema.  Pertanto, non è possibile creare un'associazione di memoria di [!INCLUDE[hek_2](../../includes/hek-2-md.md)] per un database di questo tipo.  Viene restituito l'errore seguente:  
*Database_name %s fa riferimento a un database di sistema.  Pool di risorse possono essere associati solo a un database utente.*  
  
```  
Msg 41371, Level 16, State 1, Procedure sp_xtp_bind_db_resource_pool_internal, Line 51  
Binding to a resource pool is not supported for system database 'master'. This operation can only be performed on a user database.  
```  
  
**Pool di risorse non esiste.**  
 Il pool di risorse identificato da resource_pool_name deve essere disponibile prima di eseguire `sp_xtp_bind_db_resource_pool`.  Se non è disponibile alcun pool con l'ID specificato, viene restituito l'errore seguente:  
*Il Pool di risorse %s non esiste.  Immettere un nome di pool di risorse valido.*  
  
```  
Msg 41370, Level 16, State 1, Procedure sp_xtp_bind_db_resource_pool_internal, Line 51  
Resource pool 'Pool_Hekaton' does not exist or resource governor has not been reconfigured.  
```  
  
**Pool_name fa riferimento a un pool di sistema riservato**  
 I nomi di pool "INTERNAL" e "DEFAULT" sono riservati ai pool di sistema.  Non è possibile associare in modo esplicito un database a uno di questi.  Se viene immesso un nome di pool di sistema, viene restituito l'errore seguente:  
*Il Pool di risorse %s è un pool di risorse di sistema.  Il pool di risorse di sistema non può essere associato in modo esplicito a un database tramite questa procedura.*  
  
```  
Msg 41373, Level 16, State 1, Procedure sp_xtp_bind_db_resource_pool_internal, Line 51  
Database 'Hekaton_DB' cannot be explicitly bound to the resource pool 'internal'. A database can only be bound only to a user resource pool.  
```  
  
**Il database è già associato a un altro Pool di risorse**  
 Un database può essere associato a un solo pool di risorse in qualsiasi momento. Le associazioni di database ai pool di risorse devono essere rimosse in modo esplicito prima che possano essere associate a un altro pool. See [sys.sp_xtp_unbind_db_resource_pool &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-unbind-db-resource-pool-transact-sql.md).  
*Database %s è già associato al pool di risorse %s.  È necessario annullare prima di poter creare una nuova associazione.*  
  
```  
Msg 41372, Level 16, State 1, Procedure sp_xtp_bind_db_resource_pool_internal, Line 54  
Database 'Hekaton_DB' is currently bound to a resource pool. A database must be unbound before creating a new binding.  
```  
  
 Quando l'operazione viene completata, tramite `sp_xtp_bind_db_resource_pool` viene restituito il messaggio riportato di seguito.  
  
**Associazione completata**  
 Quando l'operazione viene completata, tramite la funzione viene restituito il seguente messaggio di operazione riuscita, che viene registrato in SQL ERRORLOG  
*Un'associazione di risorsa è stata creata correttamente tra il database con ID %d e il pool di risorse con ID %d.*  
  
## <a name="examples"></a>Esempi  
A.  Nell'esempio di codice seguente viene associato il database Hekaton_DB al pool di risorse Pool_Hekaton.  
  
```sql  
sys.sp_xtp_bind_db_resource_pool N'Hekaton_DB', N'Pool_Hekaton'  
```  
 
 L'associazione viene applicata alla successiva connessione del database.  
 
 B. Esempio espanso di esempio che include alcuni controlli di base precedente.  Eseguire l'istruzione seguente [!INCLUDE[tsql](../../includes/tsql-md.md)] in[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]\:
 
```sql
DECLARE @resourcePool sysname = N'Pool_Hekaton';
DECLARE @database sysname = N'Hekaton_DB';

-- Check whether resource pool exists
IF NOT EXISTS (
    SELECT * FROM sys.resource_governor_resource_pools WHERE name = @resourcePool
    )
BEGIN
    SELECT N'Resource pool "' + @resourcePool + N'" does not exist or resource governor has not been reconfigured.';
END
-- Check whether database is already bound to a resource pool
ELSE IF EXISTS (
    SELECT p.name
    FROM sys.databases d
    JOIN sys.resource_governor_resource_pools p
    ON d.resource_pool_id = p.pool_id
    WHERE d.name = @database
    )
BEGIN
    SELECT N'Database "' + @database + N'" is currently bound to resource pool "' + @resourcePool  + N'". A database must be unbound before creating a new binding.';
END
-- Bind resource pool to database.
ELSE BEGIN
    EXEC sp_xtp_bind_db_resource_pool @database, @resourcePool; 
END 
``` 
  
## <a name="requirements"></a>Requisiti  
  
-   Sia il database specificato da `database_name` sia il pool di risorse specificato da `resource_pool_name` devono essere disponibili prima di poter essere associati.  
  
-   È richiesta l'autorizzazione CONTROL SERVER.  
  
## <a name="see-also"></a>Vedere anche  
 [Associazione di un database con tabelle con ottimizzazione per la memoria a un pool di risorse](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)   
 [Sys.sp_xtp_unbind_db_resource_pool &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-unbind-db-resource-pool-transact-sql.md)  
  
  
