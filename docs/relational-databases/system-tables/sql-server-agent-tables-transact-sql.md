---
title: Tabelle di SQL Server Agent (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- SQL Server Agent, system tables
- system tables [SQL Server], SQL Server Agent
ms.assetid: 6cb39bfd-079e-4be4-9c42-2fa234c65ce1
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 37691cad424b53dc4e89458fd231fecbdcb06497
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/03/2018
---
# <a name="sql-server-agent-tables-transact-sql"></a>Tabelle di SQL Server Agent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Negli argomenti di questa sezione vengono descritte le tabelle di sistema in cui sono archiviate le informazioni utilizzate da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Tutte le tabelle sono nello schema dbo nel database msdb.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [dbo.sysalerts](../../relational-databases/system-tables/dbo-sysalerts-transact-sql.md)  
 Contiene una riga per ogni avviso.  
  
 [dbo.syscategories](../../relational-databases/system-tables/dbo-syscategories-transact-sql.md)  
 Contiene le categorie utilizzate da [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per organizzare processi, avvisi e operatori.  
  
 [dbo.sysdownloadlist](../../relational-databases/system-tables/dbo-sysdownloadlist-transact-sql.md)  
 Include la coda delle istruzioni di download per tutti i server di destinazione.  
  
 [dbo.sysjobactivity](../../relational-databases/system-tables/dbo-sysjobactivity-transact-sql.md)  
 Contiene informazioni sull'attività e sullo stato dei processi correnti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
 [dbo.sysjobhistory](../../relational-databases/system-tables/dbo-sysjobhistory-transact-sql.md)  
 Contiene informazioni sull'esecuzione di processi pianificati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
 [dbo.sysjobs](../../relational-databases/system-tables/dbo-sysjobs-transact-sql.md)  
 Archivia le informazioni su tutti i processi pianificati da eseguire tramite [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
 [dbo.sysjobschedules](../../relational-databases/system-tables/dbo-sysjobschedules-transact-sql.md)  
 Contiene informazioni di pianificazione per i processi da eseguire tramite [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
 [dbo.sysjobservers](../../relational-databases/system-tables/dbo-sysjobservers-transact-sql.md)  
 Archivia l'associazione o la relazione di un determinato processo con uno o più server di destinazione.  
  
 [dbo.sysjobsteps](../../relational-databases/system-tables/dbo-sysjobsteps-transact-sql.md)  
 Contiene informazioni relative a tutti i passaggi di un processo da eseguire tramite [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
 [dbo.sysjobstepslogs](../../relational-databases/system-tables/dbo-sysjobstepslogs-transact-sql.md)  
 Contiene informazioni sui log dei passaggi di processi.  
  
 [dbo.sysnotifications](../../relational-databases/system-tables/dbo-sysnotifications-transact-sql.md)  
 Contiene una riga per ogni notifica.  
  
 [dbo.sysoperators](../../relational-databases/system-tables/dbo-sysoperators-transact-sql.md)  
 Contiene una riga per ogni operatore di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
 [dbo.sysproxies](../../relational-databases/system-tables/dbo-sysproxies-transact-sql.md)  
 Contiene informazioni sugli account proxy di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
 [dbo.sysproxylogin](../../relational-databases/system-tables/dbo-sysproxylogin-transact-sql.md)  
 Registra quali account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono associati ad ogni account proxy di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
 [dbo.sysproxysubsystem](../../relational-databases/system-tables/dbo-sysproxysubsystem-transact-sql.md)  
 Registra quale sottosistema di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent viene utilizzato da ogni account proxy.  
  
 [dbo.sysschedules](../../relational-databases/system-tables/dbo-sysschedules-transact-sql.md)  
 Contiene informazioni sulle pianificazioni dei processi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
 [dbo.syssessions](../../relational-databases/system-tables/dbo-syssessions-transact-sql.md)  
 Contiene la data di inizio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent per ogni sessione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Una sessione viene creata ad ogni avvio del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
 [dbo.syssubsystems](../../relational-databases/system-tables/dbo-sysproxysubsystem-transact-sql.md)  
 Contiene informazioni su tutti i sottosistemi proxy di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent disponibili.  
  
 [dbo.systargetservergroupmembers](../../relational-databases/system-tables/dbo-systargetservergroupmembers-transact-sql.md)  
 Registra i server di destinazione integrati nel gruppo multiserver specificato.  
  
 [dbo.systargetservergroups](../../relational-databases/system-tables/dbo-systargetservergroups-transact-sql.md)  
 Registra i gruppi di server di destinazione integrati nell'ambiente multiserver specificato.  
  
 [dbo.systargetservers](../../relational-databases/system-tables/dbo-systargetservers-transact-sql.md)  
 Registra i server di destinazione integrati nel dominio multiserver specificato.  
  
 [dbo.systaskids](../../relational-databases/system-tables/dbo-systaskids-transact-sql.md)  
 Contiene un mapping delle attività create in versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] su processi di [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] nella versione corrente.  
  
  
