---
title: Opzione di configurazione del server contained database authentication | Microsoft Docs
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- contained database, enabling
- contained database authentication option
ms.assetid: b80768d2-ac20-4035-a335-d9adb74b3f6e
caps.latest.revision: "11"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 63c5e522670ff77d7f600947bc9ed36b80d9b051
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/18/2018
---
# <a name="contained-database-authentication-server-configuration-option"></a>Opzione di configurazione del server contained database authentication
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Utilizzare l'opzione **contained database authentication** per abilitare database indipendenti nell'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
 Questa opzione server consente di controllare l'opzione **contained database authentication**.  
  
-   Quando l'opzione **contained database authentication** è disattivata (0) per l'istanza, non è possibile creare database indipendenti né collegarli al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
-   Quando l'opzione **contained database authentication** è attivata (1) per l'istanza, è possibile creare database indipendenti o collegarli al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 In un database indipendente sono incluse tutte le impostazioni e i metadati del database necessari per definire il database, ma non sono presenti dipendenze di configurazione nell'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] in cui è installato il database. Gli utenti possono connettersi al database senza eseguire l'autenticazione di un account di accesso al livello del [!INCLUDE[ssDE](../../includes/ssde-md.md)] . L'isolamento del database dal Motore di database consente di spostare in modo semplice il database in un'altra istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. L'inclusione di tutte le impostazioni del database nel database stesso consente ai proprietari del database di gestirne tutte le impostazioni di configurazione. Per altre informazioni sui database indipendenti, vedere [Contained Databases](../../relational-databases/databases/contained-databases.md).  

> [!NOTE]
> I database indipendenti sono sempre abilitati per [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] e [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] e non possono essere disabilitati.
  
 Se in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono contenuti database indipendenti, l'opzione **contained database authentication** può essere impostata su 0 utilizzando l'istruzione **RECONFIGURE WITH OVERRIDE** . Se si imposta l'opzione **contained database authentication** su 0, l'autenticazione per i database indipendenti verrà disabilitata.  
  
> [!IMPORTANT]  
>  Quando sono abilitati i database indipendenti, gli utenti del database con l'autorizzazione ALTER ANY USER, ad esempio i membri dei ruoli del database db_owner e db_accessadmin, possono concedere l'accesso ai database e in tal modo concedere l'accesso all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ciò significa che il controllo dell'accesso al server non è più limitato ai membri del ruolo predefinito del server sysadmin e securityadmin e agli account di accesso con l'autorizzazione CONTROL SERVER e ALTER ANY LOGIN a livello di server. Prima di consentire database indipendenti, è necessario comprenderne i rischi associati. Per altre informazioni, vedere [Security Best Practices with Contained Databases](../../relational-databases/databases/security-best-practices-with-contained-databases.md).  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono abilitati database indipendenti nell'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
```sql  
sp_configure 'contained database authentication', 1;  
GO  
RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Opzioni di configurazione del server &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
