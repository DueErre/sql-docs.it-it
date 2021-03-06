---
title: sysmail_help_configure_sp (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- sysmail_help_configure_sp
- sysmail_help_configure_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_configure_sp
ms.assetid: e598d4c8-3041-4965-b046-dce3a8e3d3e0
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 13f768cd5e1cbbbcfa3f5b74d7ae52d2e9f357e1
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/03/2018
---
# <a name="sysmailhelpconfiguresp-transact-sql"></a>sysmail_help_configure_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Visualizza le impostazioni di configurazione per Posta elettronica database.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sysmail_help_configure_sp  [ [ @parameter_name = ] 'parameter_name' ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [ **@parameter_name**  =] **'***parameter_name***'**  
 Nome dell'impostazione di configurazione da recuperare. Quando specificato, viene restituito il valore dell'impostazione di configurazione nel  **@parameter_value**  parametro di OUTPUT. Se non si  **@parameter_name**  è specificato, questa stored procedure restituisce un set di risultati contenente tutte le impostazioni di configurazione di posta elettronica Database nell'istanza.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="result-sets"></a>Set di risultati  
 Se non si  **@parameter_name**  viene specificato, restituisce un set di risultati con le colonne seguenti.  
  
||||  
|-|-|-|  
|Nome colonna|Tipo di dati|Description|  
|**paramname**|**nvarchar(256)**|Nome del parametro di configurazione.|  
|**paramvalue**|**nvarchar(256)**|Valore del parametro di configurazione.|  
|**description**|**nvarchar(256)**|Descrizione del parametro di configurazione.|  
  
## <a name="remarks"></a>Osservazioni  
 La stored procedure **sysmail_help_configure_sp** sono elencate le impostazioni di configurazione di posta elettronica Database corrente per l'istanza.  
  
 Quando un  **@parameter_name**  è specificato, ma viene fornito alcun parametro di output per  **@parameter_value** , questa stored procedure non genera alcun output.  
  
 La stored procedure **sysmail_help_configure_sp** nel **msdb** database ed è di proprietà di **dbo** dello schema. La procedura deve essere richiamata con un nome in tre parti se il database corrente non è **msdb**.  
  
## <a name="permissions"></a>Autorizzazioni  
 Autorizzazioni di esecuzione per questa routine per impostazione predefinita ai membri del **sysadmin** ruolo predefinito del server.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono visualizzate le impostazioni di configurazione di Posta elettronica database per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
EXECUTE msdb.dbo.sysmail_help_configure_sp ;  
```  
  
 Quello che segue è un set di risultati di esempio, modificato per adattarlo alla lunghezza di riga.  
  
```  
paramname                       paramvalue      description  
------------------------------- --------------- -----------------------------------------------------------------------------  
AccountRetryAttempts            1               Number of retry attempts for a mail server  
AccountRetryDelay               5000            Delay between each retry attempt to mail server  
DatabaseMailExeMinimumLifeTime  600             Minimum process lifetime in seconds  
DefaultAttachmentEncoding       MIME            Default attachment encoding  
LoggingLevel                    2               Database Mail logging level: normal - 1, extended - 2 (default), verbose - 3  
MaxFileSize                     1000000         Default maximum file size  
ProhibitedExtensions            exe,dll,vbs,js  Extensions not allowed in outgoing mails  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Posta elettronica database](../../relational-databases/database-mail/database-mail.md)   
 [Posta elettronica database Stored procedure &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
