---
title: syspublications (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- syspublications
- syspublications_TSQL
dev_langs: TSQL
helpviewer_keywords: syspublications system table
ms.assetid: a86eb4f5-1f7b-493e-af55-3d15cf878228
caps.latest.revision: "40"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 410ba9ae2cd3329550ee7920b7213add598db5d3
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="syspublications-transact-sql"></a>syspublications (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una riga per ogni pubblicazione definita nel database. Questa tabella è archiviata nel database di pubblicazione.  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|**Descrizione**|**nvarchar(255)**|Voce descrittiva per la pubblicazione.|  
|**name**|**sysname**|Nome univoco associato alla pubblicazione.|  
|**pubid**|**int**|Colonna Identity che include un ID univoco per la pubblicazione.|  
|**repl_freq**|**tinyint**|Frequenza della replica:<br /><br /> **0** = basata sulle transazioni.<br /><br /> **1** = aggiornamento di tabella pianificato.|  
|**status**|**tinyint**|Stato:<br /><br /> **0** = inattivo.<br /><br /> **1** = attivo.|  
|**sync_method**|**tinyint**|Metodo di sincronizzazione:<br /><br /> **0** = utilità per la copia di massa in modalità nativa (**BCP**).<br /><br /> **1** = BCP in modalità carattere.<br /><br /> **3** = simultanea, il che significa che viene utilizzata in modalità nativa, ma durante lo snapshot non vengono bloccate le tabelle.<br /><br /> **4** = Concurrent_c, ovvero che viene utilizzata in modalità carattere BCP ma durante lo snapshot non vengono bloccate le tabelle.|  
|**snapshot_jobid**|**Binary (16)**|ID dell'attività pianificata.|  
|**independent_agent**|**bit**|Specifica se per la pubblicazione è disponibile un agente di distribuzione autonomo.<br /><br /> **0** = la pubblicazione utilizza un agente di distribuzione condiviso, e ogni coppia database del server di pubblicazione/sottoscrizione di database ha un solo agente condiviso.<br /><br /> **1** = è disponibile un agente di distribuzione autonomo per la pubblicazione.|  
|**immediate_sync**|**bit**|Indica se i file di sincronizzazione vengono creati o ricreati ogni volta che viene eseguito l'agente Snapshot, in cui **1** significa che vengono creati ogni volta che viene eseguito l'agente.|  
|**enabled_for_internet**|**bit**|Indica se i file di sincronizzazione per la pubblicazione vengono esposti a Internet tramite il protocollo file transfer protocol (FTP) e altri servizi, in cui **1** significa che è possibile accedere da Internet.|  
|**allow_push**|**bit**|Indica se le sottoscrizioni push sono consentite per la pubblicazione in cui **1** significa che sono consentiti.|  
|**allow_pull**|**bit**|Indica se le sottoscrizioni pull sono consentite per la pubblicazione in cui **1** significa che sono consentiti.|  
|**allow_anonymous**|**bit**|Indica se le sottoscrizioni anonime sono consentite per la pubblicazione in cui **1** significa che sono consentiti.|  
|**immediate_sync_ready**|**bit**|Indica se lo snapshot è stato generato dall'agente snapshot e se è pronto per l'utilizzo nelle nuove sottoscrizioni. Questo valore risulta significativo solo per le pubblicazioni ad aggiornamento immediato. **1** indica che lo snapshot è pronto.|  
|**allow_sync_tran**|**bit**|Specifica se è consentito creare sottoscrizioni ad aggiornamento immediato per la pubblicazione. **1** significa che le sottoscrizioni ad aggiornamento immediato sono consentite.|  
|**autogen_sync_procs**|**bit**|Specifica se la stored procedure di sincronizzazione per sottoscrizioni ad aggiornamento immediato viene generata nel server di pubblicazione. **1** significa che viene generato nel server di pubblicazione.|  
|**conservazione**|**int**|Quantità di modifiche, espressa in ore, da salvare per la pubblicazione specificata.|  
|**allowed_queued_tran**|**bit**|Specifica se disabilitare l'inserimento in coda delle modifiche apportate nel Sottoscrittore finché non è possibile applicarle al server di pubblicazione. Se **1**, le modifiche nel Sottoscrittore vengono accodate.|  
|**snapshot_in_defaultfolder**|**bit**|Specifica se i file di snapshot sono archiviati nella cartella predefinita.<br /><br /> **0** = snapshot di file sono stati archiviati nella posizione alternativa specificata da *alternate_snapshot_folder*.<br /><br /> **1** = snapshot di file sono reperibile nella cartella predefinita.|  
|**alt_snapshot_folder**|**nvarchar(255)**|Specifica la posizione della cartella alternativa per lo snapshot.|  
|**pre_snapshot_script**|**nvarchar(255)**|Specifica un puntatore a un **SQL** percorso del file. L'agente di distribuzione esegue lo script pre-snapshot prima dell'esecuzione degli script di oggetti replicati in fase di applicazione di uno snapshot in un Sottoscrittore.|  
|**post_snapshot_script**|**nvarchar(255)**|Specifica un puntatore a un **SQL** percorso del file. L'agente di distribuzione esegue lo script post-snapshot dopo l'applicazione di tutti gli altri script di oggetti replicati e dei dati durante una sincronizzazione iniziale.|  
|**compress_snapshot**|**bit**|Specifica che lo snapshot viene scritto il *alt_snapshot_folder* percorso è deve essere compresso nel [!INCLUDE[msCoName](../../includes/msconame-md.md)] formato CAB. **1** indica che lo snapshot verrà compresso.|  
|**ftp_address**|**sysname**|Indirizzo di rete del servizio FTP per il server di distribuzione. Specifica la posizione in cui i file di snapshot della pubblicazione possono essere prelevati dall'agente di distribuzione.|  
|**ftp_port**|**int**|Numero di porta del servizio FTP per il server di distribuzione. Specifica la posizione in cui i file di snapshot della pubblicazione possono essere prelevati dall'agente di distribuzione.|  
|**ftp_subdirectory**|**nvarchar(255)**|Specifica il percorso da cui l'agente di distribuzione può prelevare i file di snapshot se la pubblicazione supporta la propagazione degli snapshot tramite FTP.|  
|**ftp_login**|**sysname**|Nome utente utilizzato per la connessione al servizio FTP.|  
|**ftp_password**|**nvarchar (524)**|Password dell'utente utilizzata per la connessione al servizio FTP.|  
|**allow_dts**|**bit**|Specifica che la pubblicazione supporta le trasformazioni di dati. **1** indica che le trasformazioni DTS sono consentite.|  
|**allow_subscription_copy**|**bit**|Specifica se la funzionalità che consente di copiare i database di sottoscrizione che sottoscrivono la pubblicazione è abilitata. **1** indica che la copia è consentita.|  
|**centralized_conflicts**|**bit**|Specifica se i record dei conflitti vengono archiviati nel server di pubblicazione:<br /><br /> **0** = i record dei conflitti vengono archiviati nel server di pubblicazione e nel Sottoscrittore che ha causato il conflitto.<br /><br /> **1** = i record dei conflitti vengono archiviati nel server di pubblicazione.|  
|**conflict_retention**|**int**|Specifica il periodo di memorizzazione dei conflitti, espresso in giorni.|  
|**conflict_policy**|**int**|Specifica i criteri di risoluzione dei conflitti adottati quando viene utilizzata l'opzione per Sottoscrittori ad aggiornamento in coda. I possibili valori sono i seguenti:<br /><br /> **1** = prevale il conflitto.<br /><br /> **2** = prevale il sottoscrittore il conflitto.<br /><br /> **3** = sottoscrizione viene reinizializzata.|  
|**queue_type**|**int**|Specifica il tipo di coda da utilizzare. I possibili valori sono i seguenti:<br /><br /> **1** = msmq, che utilizza [!INCLUDE[msCoName](../../includes/msconame-md.md)] Accodamento messaggi per archiviare le transazioni.<br /><br /> **2** = sql, che utilizza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per archiviare le transazioni.<br /><br /> Nota: L'utilizzo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Accodamento messaggi è stato deprecato e non è più disponibile.|  
|**ad_guidname**|**sysname**|Specifica se la pubblicazione è pubblicata in [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory. Un valido identificatore univoco globale (GUID) specifica che la pubblicazione è pubblicata in Active Directory e il GUID è l'oggetto di pubblicazione di Active Directory corrispondente **objectGUID**. Se è NULL, la pubblicazione non è pubblicata in Active Directory.|  
|**backward_comp_level**|**int**|Livello di compatibilità del database. I possibili valori sono i seguenti:<br /><br /> **90** = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].<br /><br /> **100** = [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].<br /><br /> **110** = [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].<br /><br /> **120** = [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].|  
|**allow_initialize_from_backup**|**bit**|Indica se i Sottoscrittori possono inizializzare una sottoscrizione della pubblicazione da un backup anziché da uno snapshot iniziale. **1** significa che le sottoscrizioni possono essere inizializzate da un backup, e **0** significa che è possibile. Per altre informazioni, vedere [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).|  
|**min_autonosync_lsn**|**binary**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**replicate_ddl**|**int**|Indica se per la pubblicazione è supportata la replica dello schema. **1** indica che vengono replicate istruzioni di data definition language (DDL) eseguite nel server di pubblicazione, e **0** indica che le istruzioni DDL non vengono replicate. Per altre informazioni, vedere [Apportare modifiche allo schema nei database di pubblicazione](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md).|  
|**Opzioni**|**int**|Mappa di bit che specifica le opzioni di pubblicazione aggiuntive. I possibili valori bit per bit sono i seguenti:<br /><br /> **0x1** : abilitato per la replica peer-to-peer.<br /><br /> **0x2** -pubblicare solo le modifiche locali per la replica peer-to-peer.<br /><br /> **0x4** - enabled per non[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i sottoscrittori.<br /><br /> **0x8** : abilitato per il rilevamento dei conflitti peer-to-peer.|  
|**originator_id**|**smallint**|Identifica ogni nodo in una topologia di replica peer-to-peer per consentire il rilevamento dei conflitti. Per altre informazioni, vedere [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40; Transact-SQL &#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addpublication &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_changepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)   
 [sp_helppublication &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)  
  
  
