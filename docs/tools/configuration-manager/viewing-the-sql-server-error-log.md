---
title: Visualizzare il Log degli errori SQL Server | Documenti Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: configuration-manager
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cycling SQL Server error log
- viewing SQL Server error log
- errors [SQL Server], logs
- SQL Server error log
- displaying SQL Server error log
- logs [SQL Server], SQL Server error logs
ms.assetid: 6908c21a-65e3-458f-a272-fee256d86448
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 241fcbbef1663b4fadc7128c2ad2a47d10943475
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/03/2018
---
# <a name="viewing-the-sql-server-error-log"></a>Visualizzazione del log degli errori di SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
È possibile visualizzare il contenuto del log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per verificare il corretto completamento dei processi, ad esempio le operazioni di backup e ripristino, i comandi batch e altri script e processi. La possibilità di esaminare il contenuto del log degli errori può risultare utile per individuare problemi correnti o potenziali, inclusi i messaggi di recupero automatico, in caso di arresto e riavvio di un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , i messaggi del kernel e altri messaggi di errore a livello di server.  
  
 Per visualizzare il log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è possibile utilizzare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o un editor di testo. Per ulteriori informazioni sulla visualizzazione del log degli errori, vedere [Open Log File Viewer](../../relational-databases/logs/open-log-file-viewer.md). Per impostazione predefinita, il log degli errori si trova in `Program Files\Microsoft SQL Server\MSSQL.`  *n*  `\MSSQL\LOG\ERRORLOG` e `ERRORLOG.`  *n*  file.  
  
 A ogni avvio di un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene creato un nuovo log degli errori. È tuttavia possibile usare la stored procedure di sistema [sp_cycle_errorlog](../../relational-databases/system-stored-procedures/sp-cycle-errorlog-transact-sql.md) per scorrere i file di log degli errori senza dover riavviare l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono in genere mantenute le copie di backup dei sei log precedenti e viene assegnata l'estensione 1 alla copia di backup più recente, l'estensione 2 alla penultima copia e così via. Il log degli errori corrente non ha alcuna estensione.  
  
 Tenere presente che è possibile visualizzare anche il log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] su istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che risultano offline o non possono essere avviate. Per altre informazioni, vedere [Visualizzare file di log offline](../../relational-databases/logs/view-offline-log-files.md).  
  
  
