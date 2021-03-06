---
title: sp_changearticlecolumndatatype (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/14/2017
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
- sp_changearticlecolumndatatype
- sp_changearticlecolumndatatype_TSQL
helpviewer_keywords: sp_changearticlecolumndatatype
ms.assetid: 0db80e08-fb77-4d0c-aa41-455b13ffa9b4
caps.latest.revision: "30"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1defb009948d01147e4b8f9e333cdd108c8bbba9
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="spchangearticlecolumndatatype-transact-sql"></a>sp_changearticlecolumndatatype (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Modifica il mapping del tipo di dati della colonna dell'articolo per una pubblicazione Oracle. Questa stored procedure viene eseguita in qualsiasi database del server di distribuzione.  
  
> [!NOTE]  
>  Sono disponibili per impostazione predefinita i mapping dei tipi di dati tra i tipi supportati dal server di pubblicazione. Utilizzare **sp_changearticlecolumndatatype** solo quando si esegue l'override di queste impostazioni predefinite.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_changearticlecolumndatatype [ @publication= ] 'publication'  
    [ @article = ] 'article'   
    [ @column = ] 'column'  
    [ , [ @type = ] 'type' ]  
    [ , [ @length = ] length ]  
    [ , [ @precision = ] precision ]  
    [ , [ @scale = ] scale ]  
    [ , [ @publisher = ] 'publisher'  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@publication=** ] **'***pubblicazione***'**  
 Nome della pubblicazione Oracle. *pubblicazione* è **sysname**, non prevede alcun valore predefinito.  
  
 [  **@article =** ] **'***articolo***'**  
 Nome dell'articolo. *articolo* è **sysname**, non prevede alcun valore predefinito.  
  
 [  **@column** =] **'***colonna***'**  
 Nome della colonna per cui modificare il mapping dei tipi di dati. *colonna* è **sysname**, non prevede alcun valore predefinito.  
  
 [  **@type**  =] **'***tipo***'**  
 È il nome del [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] il tipo di dati nella colonna di destinazione. *tipo* è **sysname**, con un valore predefinito è NULL.  
  
 [  **@length**  =] *lunghezza*  
 Lunghezza del tipo di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nella colonna di destinazione. *lunghezza* è **bigint**, con un valore predefinito è NULL.  
  
 [  **@precision** =] *precisione*  
 Precisione del tipo di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nella colonna di destinazione. *precisione* è **bigint**, con un valore predefinito è NULL.  
  
 [  **@publisher** =] **'***publisher***'**  
 Specifica un server di pubblicazione non [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *server di pubblicazione* è **sysname**, con un valore predefinito è NULL.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Osservazioni  
 **Sp_changearticlecolumndatatype** viene utilizzato per eseguire l'override di mapping dei tipi di dati predefiniti tra i tipi supportati di server di pubblicazione (Oracle e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]). Per visualizzare questi mapping dei tipi di dati predefiniti, eseguire [sp_getdefaultdatatypemapping](../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md).  
  
 **sp_changearticlecolumndatatype** è supportato solo per server di pubblicazione Oracle. Se si esegue questa stored procedure su una pubblicazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene generato un errore.  
  
 **sp_changearticlecolumndatatype** deve essere eseguita per ogni mapping di colonna di articolo che deve essere modificata.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server o **db_owner** ruolo predefinito del database possono eseguire **sp_changearticlecolumndatatype**.  
  
## <a name="see-also"></a>Vedere anche  
 [Modificare le proprietà di pubblicazioni e articoli](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Data Type Mapping for Oracle Publishers](../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)   
 [Stored procedure per la replica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
