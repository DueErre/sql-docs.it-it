---
title: sp_helpmergealternatepublisher (Transact-SQL) | Documenti Microsoft
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
- sp_helpmergealternatepublisher_TSQL
- sp_helpmergealternatepublisher
helpviewer_keywords: sp_helpmergealternatepublisher
ms.assetid: a96e365f-5967-4580-9d79-5bacf2d12211
caps.latest.revision: "26"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2c1b6cdc6bc5d7a19a6b7c27fc282233310da658
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="sphelpmergealternatepublisher-transact-sql"></a>sp_helpmergealternatepublisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce un elenco di tutti i server abilitati come server di pubblicazione alternativi per le pubblicazioni di tipo merge. Questa stored procedure viene eseguita nel database di sottoscrizione del Sottoscrittore.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_helpmergealternatepublisher [ @publisher = ] 'publisher', [ @publisher_db = ] 'publisher_db', [ @publication = ] 'publication'  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@publisher=**] **'***publisher***'**  
 È il nome del server di pubblicazione alternativo. *publisher* è **sysname**, non prevede alcun valore predefinito.  
  
 [  **@publisher_db=**] **'***publisher_db***'**  
 È il nome del database di pubblicazione. *publisher_db* è **sysname**, non prevede alcun valore predefinito.  
  
 [  **@publication=**] **'***pubblicazione***'**  
 È il nome della pubblicazione. *pubblicazione* è **sysname**, non prevede alcun valore predefinito.  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|**alternate_publisher**|**sysname**|Nome del server di pubblicazione alternativo.|  
|**alternate_publisher_db**|**sysname**|Nome del database di pubblicazione.|  
|**alternate_publication**|**sysname**|Nome della pubblicazione.|  
|**alternate_distributor**|**sysname**|Nome del server di distribuzione.|  
|**friendly_name**|**nvarchar(255)**|Descrizione del server di pubblicazione alternativo.|  
|**abilitato**|**bit**|Specifica se il server è un server di pubblicazione alternativo. **1** specifica che il server di pubblicazione è abilitato come server di pubblicazione alternativo. **0** specifica che non è abilitato.|  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_helpmergealternatepublisher** viene utilizzata nella replica di tipo merge.  
  
 Durante ogni sessione di merge viene eseguita una ricerca dell'elenco dei server di pubblicazione alternativi sia nel server di pubblicazione che nel Sottoscrittore. Il processo di merge aggiunge o elimina voci nell'elenco dei server di pubblicazione alternativi, in modo che entrambi gli elenchi nel Sottoscrittore e nel server di pubblicazione corrispondano.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri dell'elenco accesso pubblicazione per la pubblicazione possono eseguire **sp_helpmergealternatepublisher**.  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
