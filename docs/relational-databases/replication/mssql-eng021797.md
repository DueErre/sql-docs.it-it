---
title: MSSQL_ENG021797 | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: MSSQL_ENG021797 error
ms.assetid: 54d83a1e-43fd-449c-a2b2-fdda2609a534
caps.latest.revision: "14"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9c7e91a8f6f6214c01c8fdad975c90768cf5903d
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/18/2018
---
# <a name="mssqleng021797"></a>MSSQL_ENG021797
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>Dettagli messaggio  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|21797|  
|Origine evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbolico||  
|Testo del messaggio|'%s' deve essere un account di accesso di Windows valido nel formato: 'COMPUTER\Account di accesso' o 'DOMINIO\Account di accesso'. Vedere la documentazione relativa a '%s'.|  
  
## <a name="explanation"></a>Spiegazione  
 Questo errore viene generato dalle stored procedure di replica seguenti se il valore specificato per il parametro **@job_login** è Null o non valido. Questo errore può verificarsi se un membro del ruolo predefinito del database **db_owner** esegue script di precedenti versioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il modello di sicurezza in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]è cambiato ed è necessario aggiornare questi script.  
  
-   [sp_addlogreader_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)  
  
-   [sp_addqreader_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md)  
  
-   [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)  
  
-   [sp_addpushsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md)  
  
-   [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)  
  
-   [sp_addmergepushsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md)  
  
-   [sp_addmergepullsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)  
  
 Queste stored procedure possono essere eseguite da un membro del ruolo predefinito del server **sysadmin** sul server appropriato o da un membro del ruolo predefinito del database **db_owner** nel database appropriato. Ogni stored procedure crea un processo agente e consente di specificare l'account di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows in base al quale viene eseguito l'agente. Per gli utenti del ruolo **sysadmin** , i processi agente vengono creati implicitamente anche se non viene specificato un account di Windows (se viene specificato, deve essere valido). Gli agenti vengono eseguiti in base al contesto dell'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, nel server appropriato. Sebbene l'account non sia necessario, la procedura consigliata prevede di specificare un account separato per gli agenti. Per altre informazioni, vedere [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
## <a name="user-action"></a>Azione dell'utente  
 Accertarsi di specificare un account di Windows valido per il parametro **@job_login** di ogni procedura. Se si dispone di script di replica di versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], aggiornarli in modo che includano le stored procedure e i parametri necessari per [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Per altre informazioni, vedere [Aggiornare gli script di replica &#40;programmazione Transact-SQL della replica&#41;](../../relational-databases/replication/administration/upgrade-replication-scripts-replication-transact-sql-programming.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento a errori ed eventi &#40;replica&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
