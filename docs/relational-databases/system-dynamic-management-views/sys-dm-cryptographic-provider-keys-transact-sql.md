---
title: sys.dm_cryptographic_provider_keys (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_cryptographic_provider_keys_TSQL
- dm_cryptographic_provider_keys_TSQL
- dm_cryptographic_provider_keys
- sys.dm_cryptographic_provider_keys
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_cryptographic_provider_keys dynamic management function
ms.assetid: 5a8c1421-c56b-44b5-96e5-4f01782a0c7c
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 84149c495867b1479e09edcd24e32c2191608fc8
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmcryptographicproviderkeys-transact-sql"></a>sys.dm_cryptographic_provider_keys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce le informazioni sulle chiavi fornite da un provider EKM (Extensible Key Management).  

 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
dm_cryptographic_provider_keys ( provider_id )  
```  
  
## <a name="arguments"></a>Argomenti  
 *provider_id*  
 Numero di identificazione del provider EKM, senza valori predefiniti.  
  
## <a name="tables-returned"></a>Tabelle restituite  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|**key_id**|**int**|Numero di identificazione della chiave nel provider.|  
|**key_name**|**nvarchar(512)**|Nome della chiave nel provider.|  
|**key_thumbprint**|**varbinary(32)**|Identificazione personale dal provider della chiave.|  
|**algorithm_id**|**int**|Numero di identificazione dell'algoritmo nel provider.|  
|**algorithm_tag**|**int**|Tag dell'algoritmo nel provider.|  
|**key_type**|**nchar(256)**|Tipo di chiave nel provider.|  
|**key_length**|**int**|Lunghezza della chiave nel provider.|  
  
## <a name="permissions"></a>Autorizzazioni  
 Quando viene eseguita una query sulla vista, verrà autenticato il contesto utente con il provider e verranno enumerate tutte le chiavi visibili all'utente.  
  
 Se l'utente non può autenticarsi con il provider EKM, non sarà restituita alcuna informazione sulle chiavi.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono illustrate le proprietà chiave per un provider con il numero di identificazione `1234567`.  
  
```  
SELECT * FROM sys.dm_cryptographic_provider_keys(1234567);  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Extensible Key Management &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)  
  
  
