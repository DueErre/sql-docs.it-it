---
title: sp_dropmessage (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 06/10/2016
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
- sp_dropmessage_TSQL
- sp_dropmessage
dev_langs: TSQL
helpviewer_keywords: sp_dropmessage
ms.assetid: 17287a15-cdde-43d1-bb18-9f920bc15db8
caps.latest.revision: "32"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f5673871097f702a8e370fefb4998b378af26d91
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2017
---
# <a name="spdropmessage-transact-sql"></a>sp_dropmessage (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Elimina un messaggio di errore definito dall'utente specificato da un'istanza di [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. È possibile visualizzare i messaggi definiti dall'utente utilizzando il **Sys. Messages** vista del catalogo.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_dropmessage [ @msgnum = ] message_number  
    [ , [ @lang = ] 'language' ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@msgnum =** ] *message_number*  
 Numero del messaggio da eliminare. *message_number* deve essere un messaggio definito dall'utente che dispone di un numero maggiore di 50000. *message_number* è **int**, con un valore predefinito è NULL.  
  
 [  **@lang =** ] **'***language***'**  
 Lingua del messaggio da eliminare. Se **tutti** è specificato, tutte le versioni localizzate di *message_number* vengono eliminati. *lingua* è **sysname**, con un valore predefinito è NULL.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
 nessuna.  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'appartenenza di **sysadmin** e **serveradmin** ruoli predefiniti del server.  
  
## <a name="remarks"></a>Osservazioni  
 A meno che non **tutti** specificato per *language*localizzato tutte le versioni di un messaggio devono essere eliminate prima degli Stati Uniti prima di poter eliminare la versione inglese (USA).  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-dropping-a-user-defined-message"></a>A. Eliminazione di un messaggio definito dall'utente  
 Nell'esempio seguente viene eliminato un messaggio definito dall'utente, numero `50001`, da **Sys. Messages**.  
  
```  
USE master;  
GO  
EXEC sp_dropmessage 50001;  
```  
  
### <a name="b-dropping-a-user-defined-message-that-includes-a-localized-version"></a>B. Eliminazione di un messaggio definito dall'utente che include una versione localizzata  
 Nell'esempio seguente viene eliminato un messaggio definito dall'utente, con numero `60000`, in cui è inclusa una versione localizzata del messaggio.  
  
```  
USE master;  
GO  
  
-- Create a user-defined message in U.S. English  
EXEC sp_addmessage   
    @msgnum = 60000,  
    @severity = 16,  
    @msgtext = N'The item named %s already exists in %s.',   
    @lang = 'us_english';  
  
-- Create a localized version of the same message.  
EXEC sp_addmessage   
    @msgnum = 60000,  
    @severity = 16,  
    @msgtext = N'L''élément nommé %1! existe déjà dans %2!',  
    @lang = 'French';  
GO  
  
-- This statement will fail as long as the localized version  
-- of the message exists.  
EXEC sp_dropmessage 60000;  
GO  
  
-- This statement will drop the message.  
EXEC sp_dropmessage  
    @msgnum = 60000,  
    @lang = 'all';  
GO  
```  
  
### <a name="c-dropping-a-localized-version-of-a-user-defined-message"></a>C. Eliminazione di una versione localizzata di un messaggio definito dall'utente  
 Nell'esempio seguente viene eliminata una versione localizzata di un messaggio definito dall'utente, con numero `60000`, senza eliminare l'intero messaggio.  
  
```  
USE master;  
GO  
  
-- Create a user-defined message in U.S. English  
EXEC sp_addmessage   
    @msgnum = 60000,  
    @severity = 16,  
    @msgtext = N'The item named %s already exists in %s.',   
    @lang = 'us_english';  
  
-- Create a localized version of the same message.  
EXEC sp_addmessage   
    @msgnum = 60000,  
    @severity = 16,  
    @msgtext = N'L''élément nommé %1! existe déjà dans %2!',  
    @lang = 'French';  
GO  
-- This statement will remove only the localized version of the   
-- message.  
EXEC sp_dropmessage  
    @msgnum = 60000,  
    @lang = 'French';  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [sp_addmessage &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md)   
 [sp_altermessage &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-altermessage-transact-sql.md)   
 [FORMATMESSAGE &#40; Transact-SQL &#41;](../../t-sql/functions/formatmessage-transact-sql.md)   
 [sys.messages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
