---
title: Sys. backup_devices (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/14/2017
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
- backup_devices_TSQL
- backup_devices
- sys.backup_devices
- sys.backup_devices_TSQL
dev_langs: TSQL
helpviewer_keywords:
- backup devices [SQL Server], viewing information
- sys.backup_devices catalog view
ms.assetid: 457edaa4-aca1-4bd3-bf8d-734490b80fcd
caps.latest.revision: "32"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f034c59979d5c64ba464c2da0df52f7b711a53fc
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/17/2017
---
# <a name="sysbackupdevices-transact-sql"></a>sys.backup_devices (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una riga per ogni dispositivo di backup registrato mediante **sp_addumpdevice** o creato in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
||  
|-|  
|**Si applica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (da[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a [versione corrente](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome del dispositivo di backup, univoco nel set.|  
|**tipo**|**tinyint**|Tipo di dispositivo di backup:<br /><br /> 2 = Disco<br /><br /> 3 = Disco floppy (obsoleto)<br /><br /> 5 = Nastro<br /><br /> 6 = Pipe (obsoleto)<br /><br /> 7 = Dispositivo virtuale (per l'utilizzo facoltativo da fornitori di terze parti)<br /><br /> In genere, vengono utilizzati solo disco (2) e nastro (5).|  
|**type_desc**|**nvarchar(60)**|Descrizione del tipo di dispositivo di backup:<br /><br /> DISK<br /><br /> DISKETTE (obsoleto)<br /><br /> TAPE<br /><br /> PIPE (obsoleto)<br /><br /> VIRTUAL_DEVICE (per l'utilizzo facoltativo da fornitori di terze parti)<br /><br /> In genere, vengono utilizzati solo DISK e TAPE.|  
|**physical_name**|**nvarchar (260)**|Nome o percorso del file fisico del dispositivo di backup.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [Dispositivi di backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [sp_addumpdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)   
 [Viste del catalogo di database e file &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)   
 [Domande frequenti sull'esecuzione di query nel catalogo di sistema di SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  