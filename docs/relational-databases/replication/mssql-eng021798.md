---
title: MSSQL_ENG021798 | Microsoft Docs
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
helpviewer_keywords: MSSQL_ENG021798 error
ms.assetid: 596f5092-75ab-4a19-8582-588687c7b089
caps.latest.revision: "16"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d86a467105329bf4d7504be6b765b46084242a20
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/18/2018
---
# <a name="mssqleng021798"></a>MSSQL_ENG021798
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>Dettagli messaggio  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|21798|  
|Origine evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbolico||  
|Testo del messaggio|Per continuare è necessario aggiungere il processo agente '%s' tramite '%s'. Vedere la documentazione relativa a '%s'.|  
  
## <a name="explanation"></a>Spiegazione  
 Per creare una pubblicazione, è necessario essere un membro del ruolo predefinito del server **sysadmin** sul server di pubblicazione o del ruolo predefinito del database **db_owner** nel database di pubblicazione. Se si un è membro del ruolo **db_owner** , questo errore viene generato nei casi in cui:  
  
-   Vengono eseguiti script da [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]. Il modello di sicurezza in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]è cambiato ed è necessario aggiornare questi script.  
  
-   La stored procedure **sp_addpublication** viene eseguita prima di eseguire [sp_addlogreader_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md). Questo vale per tutte le pubblicazioni transazionali.  
  
-   La stored procedure **sp_addpublication** viene eseguita prima di eseguire [sp_addqreader_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md). Questo vale per le pubblicazioni transazionali abilitate per le sottoscrizioni ad aggiornamento in coda (valore TRUE per il parametro **@allow_queued_tran** di **sp_addpublication**).  
  
 Le stored procedure **sp_addlogreader_agent** e **sp_addqreader_agent** creano ognuna un processo agente e consentono di specificare l'account di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows in base al quale viene eseguito l'agente. Per gli utenti del ruolo **sysadmin** , i processi agente vengono creati implicitamente se non vengono eseguite **sp_addlogreader_agent** e **sp_addqreader_agent** . Gli agenti vengono eseguiti in base al contesto dell'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, nel server di distribuzione. Sebbene **sp_addlogreader_agent** e **sp_addqreader_agent** non siano necessarie per gli utenti del ruolo **sysadmin** , la procedura consigliata prevede di specificare un account separato per gli agenti. Per altre informazioni, vedere [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
## <a name="user-action"></a>Azione dell'utente  
 Accertarsi di eseguire le procedure nell'ordine corretto. Per altre informazioni, vedere [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md). Se si dispone di script di replica di versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], aggiornarli in modo che includano le stored procedure e i parametri richiesti da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni successive. Per altre informazioni, vedere [Aggiornare gli script di replica &#40;programmazione Transact-SQL della replica&#41;](../../relational-databases/replication/administration/upgrade-replication-scripts-replication-transact-sql-programming.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento a errori ed eventi &#40;replica&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
