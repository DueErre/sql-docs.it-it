---
title: Sys. master_files (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.master_files
- master_files_TSQL
- sys.master_files_TSQL
- master_files
dev_langs: TSQL
helpviewer_keywords: sys.master_files catalog view
ms.assetid: 803b22f2-0016-436b-a561-ce6f023d6b6a
caps.latest.revision: "56"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 1c0ee418f8b04c8a549fb107698bd1f2df5648b2
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="sysmasterfiles-transact-sql"></a>sys.master_files (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  Contiene una riga per file di database archiviato nel database master. Questa è una singola vista a livello di sistema.  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|database_id|**int**|ID del database al quale è associato il file corrente. Il masterdatabase_id è sempre 1.|  
|file_id|**int**|ID del file all'interno del database. Il file_id primario è sempre 1.|  
|file_guid|**uniqueidentifier**|Identificatore univoco del file.<br /><br /> NULL = Il database è stato aggiornato da una versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|tipo|**tinyint**|Tipo di file:<br /><br /> 0 = Righe<br /><br /> 1 = Log<br /><br /> 2 = FILESTREAM<br /><br /> 3 = [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> 4 = Full-text (cataloghi full-text precedenti a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]; i cataloghi full-text aggiornati a oppure creati in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o versioni successive indicheranno un tipo di file 0).|  
|type_desc|**nvarchar(60)**|Descrizione del tipo di file:<br /><br /> ROWS<br /><br /> LOG<br /><br /> FILESTREAM<br /><br /> FULLTEXT (cataloghi full-text precedenti a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]).|  
|data_space_id|**int**|ID dello spazio dati al quale appartiene il file. Lo spazio dati è un filegroup.<br /><br /> 0 = File di log|  
|name|**sysname**|Nome logico del file nel database.|  
|physical_name|**nvarchar (260)**|Nome del file del sistema operativo.|  
|state|**tinyint**|Stato del file:<br /><br /> 0 = ONLINE<br /><br /> 1 = RESTORING<br /><br /> 2 = RECOVERING<br /><br /> 3 = RECOVERY_PENDING<br /><br /> 4 = SUSPECT<br /><br /> 5 = [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> 6 = OFFLINE<br /><br /> 7 = DEFUNCT|  
|state_desc|**nvarchar(60)**|Descrizione dello stato del file:<br /><br /> ONLINE<br /><br /> RESTORING<br /><br /> RECOVERING<br /><br /> RECOVERY_PENDING<br /><br /> SUSPECT<br /><br /> OFFLINE<br /><br /> DEFUNCT<br /><br /> Per ulteriori informazioni, vedere [degli stati di File](../../relational-databases/databases/file-states.md).|  
|size|**int**|Dimensioni del file corrente espresse in pagine da 8 KB. Per uno snapshot del database, il valore size corrisponde allo spazio massimo utilizzabile dallo snapshot per il file.<br /><br /> Nota: Questo campo viene popolato con zero per i contenitori FILESTREAM. Query di *Sys. database_files* vista per le dimensioni effettive dei contenitori FILESTREAM del catalogo.|  
|max_size|**int**|Dimensioni massime del file espresse in pagine da 8 KB.<br /><br /> 0 = Non è consentito alcun aumento.<br /><br /> -1 = La dimensione del file aumenterà finché il disco è pieno.<br /><br /> 268435456 = La dimensione del file di log aumenterà fino al valore massimo di 2 TB.<br /><br /> Nota: I database che vengono aggiornati con una dimensione del file di log senza limiti restituirà -1 per la dimensione massima del file di log.|  
|growth|**int**|0 = La dimensione del file è fissa e non aumenterà.<br /><br /> >0 = Il file aumenterà automaticamente.<br /><br /> Se is_percent_growth = 0, viene applicato un incremento in unità pari a pagine da 8 KB, con un arrotondamento al blocco di 64 KB più prossimo.<br /><br /> Se is_percent_growth = 1, il valore dell'aumento di dimensioni è espresso come percentuale (numero intero).|  
|is_media_read_onlyF|**bit**|1 = Il file si trova in un supporto con accesso in sola lettura.<br /><br /> 0 = Il file si trova in un supporto con accesso in lettura/scrittura.|  
|is_read_only|**bit**|1 = Il file è contrassegnato per l'accesso in sola lettura.<br /><br /> 0 = Il file è contrassegnato per l'accesso in lettura/scrittura.|  
|is_sparse|**bit**|1 = il file è di tipo sparse.<br /><br /> 0 = il file non è di tipo sparse.<br /><br /> Per altre informazioni, vedere [Visualizzare le dimensioni del file sparse di uno snapshot del database &#40;Transact-SQL&#41;](../../relational-databases/databases/view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md).|  
|is_percent_growth|**bit**|1 = L'aumento del file è una percentuale.<br /><br /> 0 = Dimensione dell'aumento assoluto in pagine.|  
|is_name_reserved|**bit**|1 = Il nome file eliminato è riutilizzabile. È necessario eseguire un backup del log prima di poter riutilizzare il nome (name o physical_name) come nuovo nome file.<br /><br /> 0 = Il nome file non è disponibile per il riutilizzo.|  
|create_lsn|**Numeric(25,0)**|Numero di sequenza del file di log (LSN) in corrispondenza del quale il file è stato creato.|  
|drop_lsn|**Numeric(25,0)**|Numero di sequenza del file di log (LSN) in corrispondenza del quale il file è stato eliminato.|  
|read_only_lsn|**Numeric(25,0)**|Numero di sequenza del file di log (LSN) in corrispondenza del quale la modalità del filegroup contenente il file è passata da lettura/scrittura a sola lettura (la modifica più recente).|  
|read_write_lsn|**Numeric(25,0)**|Numero di sequenza del file di log in corrispondenza del quale la modalità del filegroup contenente il file è passata da sola lettura a lettura/scrittura (la modifica più recente).|  
|differential_base_lsn|**Numeric(25,0)**|Base per backup differenziali. Gli extent di dati modificati dopo tale LSN verranno inclusi in un backup differenziale.|  
|differential_base_guid|**uniqueidentifier**|Identificatore univoco del backup di base in base al quale verrà eseguito un backup differenziale.|  
|differential_base_time|**datetime**|Tempo corrispondente a differential_base_lsn.|  
|redo_start_lsn|**Numeric(25,0)**|Numero di sequenza del file di log in corrispondenza del quale deve iniziare l'esecuzione del successivo rollforward.<br /><br /> NULL a meno che state = RESTORING o state = RECOVERY_PENDING.|  
|redo_start_fork_guid|**uniqueidentifier**|Identificatore univoco del fork di recupero. Il valore first_fork_guid del successivo backup del log ripristinato deve corrispondere a questo valore. Rappresenta lo stato corrente del contenitore.|  
|redo_target_lsn|**Numeric(25,0)**|Numero di sequenza del file di log (LSN) in corrispondenza del quale è possibile arrestare l'esecuzione del rollforward online sul file.<br /><br /> NULL a meno che state = RESTORING o state = RECOVERY_PENDING.|  
|redo_target_fork_guid|**uniqueidentifier**|Fork di recupero in corrispondenza del quale è possibile recuperare il contenitore. Abbinato a redo_target_lsn.|  
|backup_lsn|**Numeric(25,0)**|Numero di sequenza del file di log del backup dei dati o del backup differenziale del file più recente.|  
|credential_id|**int**|Il `credential_id` da `sys.credentials` utilizzato per archiviare il file. Ad esempio, quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è in esecuzione in una macchina virtuale di Azure e il database sono memorizzati nell'archiviazione blob di Azure, una credenziale è configurata con le credenziali di accesso al percorso di archiviazione.|  
  
> [!NOTE]  
>  In caso di eliminazione o ricompilazione di indici di grandi dimensioni oppure di eliminazione o troncamento di tabelle di grandi dimensioni, in [!INCLUDE[ssDE](../../includes/ssde-md.md)] le deallocazioni di pagine effettive e i relativi blocchi associati vengono posticipati fino all'esecuzione del commit della transazione. Le operazioni di eliminazione posticipate non rendono immediatamente disponibile lo spazio allocato. I valori restituiti da sys.master_files subito dopo l'eliminazione o il troncamento di un oggetto di grandi dimensioni possono pertanto non riflettere l'effettivo spazio su disco disponibile.  
  
## <a name="permissions"></a>Permissions  
 Le autorizzazioni minime necessarie per visualizzare la riga corrispondente sono CREATE DATABASE, ALTER ANY DATABASE o VIEW ANY DEFINITION.  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo di database e file &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)   
 [Stati di file](../../relational-databases/databases/file-states.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [Filegroup e file di database](../../relational-databases/databases/database-files-and-filegroups.md)  
  
  
