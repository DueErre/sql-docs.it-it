---
title: SUSER_ID (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SUSER_ID_TSQL
- SUSER_ID
dev_langs:
- TSQL
helpviewer_keywords:
- users [SQL Server], IDs
- logins [SQL Server], IDs
- SUSER_ID function
- IDs [SQL Server], logins
- identification numbers [SQL Server], logins
- user IDs [SQL Server]
ms.assetid: 348911ab-b0b6-4867-aee7-e6f42e053a4a
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e4b00485c741857f1e3438c3e50995886900fe29
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="suserid-transact-sql"></a>SUSER_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce il numero di identificazione dell'account di accesso dell'utente.  
  
> [!NOTE]  
>  A partire da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], SUSER_ID restituisce il valore elencato come **principal_id** nella vista del catalogo **sys.server_principals**.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SUSER_ID ( [ 'login' ] )   
```  
  
## <a name="arguments"></a>Argomenti  
 **'** *login* **'**  
 Nome dell'account di accesso dell'utente. *login* è di tipo **nchar**. Se *login* viene specificato come **char**, *login* viene convertito in modo implicito in **nchar**. *login* può essere qualsiasi account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oppure qualsiasi utente o gruppo di Windows autorizzato a connettersi a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se *login* viene omesso, viene restituito il numero di identificazione dell'account di accesso dell'utente corrente. Se nel parametro è inclusa la parola NULL, verrà restituito NULL.  
  
## <a name="return-types"></a>Tipi restituiti  
 **int**  
  
## <a name="remarks"></a>Remarks  
 SUSER_ID restituisce un numero di identificazione solo per gli account di accesso che sono stati resi disponibili in modo esplicito all'interno di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questo ID viene utilizzato all'interno di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per rilevare l'appartenenza e le autorizzazioni. Questo ID non è l'equivalente del SID dell'account di accesso restituito da SUSER_SID. Se *login* è un account di accesso di SQL Server, il SID esegue il mapping a un GUID. Se *login* è un account di accesso di Windows o un gruppo di Windows, il SID esegue il mapping a un ID di sicurezza di Windows.  
  
 SUSER_SID restituisce un valore SUID solo per gli account di accesso a cui corrisponde una voce nella tabella di sistema **syslogins**.  
  
 È possibile utilizzare le funzioni di sistema nell'elenco di selezione, nella clausola WHERE e in qualsiasi posizione in cui è consentita un'espressione. Le funzioni di sistema devono essere sempre seguite dalle parentesi, anche se non si specifica alcun parametro.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene restituito il numero di identificazione dell'account di accesso `sa`.  
  
```  
SELECT SUSER_ID('sa');  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [SUSER_SID &#40;Transact-SQL&#41;](../../t-sql/functions/suser-sid-transact-sql.md)   
 [Funzioni di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
  
  
