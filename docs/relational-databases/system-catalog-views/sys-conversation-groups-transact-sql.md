---
title: Sys. conversation_groups (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- conversation_groups_TSQL
- conversation_groups
- sys.conversation_groups
- sys.conversation_groups_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.conversation_groups catalog view
ms.assetid: 3f35815e-2de4-42a2-a972-8f0141dad0b3
caps.latest.revision: "29"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6130a986c81533004d239541433f081cead97bb2
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/17/2017
---
# <a name="sysconversationgroups-transact-sql"></a>sys.conversation_groups (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Questa vista del catalogo contiene una riga per ogni gruppo di conversazioni.  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|**conversation_group_id**|**uniqueidentifier**|Identificatore del gruppo di conversazioni. Non ammette i valori Null.|  
|**service_id**|**int**|Identificatore del servizio per le conversazioni nel gruppo. Non ammette i valori Null.|  
|**is_system**|**bit**|Indica se si tratta di un'istanza di sistema. Ammette valori Null.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
  
