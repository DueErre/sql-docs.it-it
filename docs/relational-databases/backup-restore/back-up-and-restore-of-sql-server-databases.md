---
title: Backup e ripristino di database SQL Server | Microsoft Docs
ms.custom: 
ms.date: 07/29/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: backup-restore
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- disaster recovery [SQL Server], see restoring [SQL Server]
- backups [SQL Server]
- restoring databases [SQL Server]
- backup [SQL Server], see backing up [SQL Server]
- databases [SQL Server], restoring
- backing up databases [SQL Server]
- restore [SQL Server], see restoring [SQL Server]
- disaster recovery [SQL Server], see backing up [SQL Server]
- backing up [SQL Server]
- Database Engine [SQL Server], backups
- databases [SQL Server], backups
ms.assetid: 570a21b3-ad29-44a9-aa70-deb2fbd34f27
caps.latest.revision: "91"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Active
ms.openlocfilehash: 959fea6c816396c70883a47c1d9f00cbd11be9dc
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/18/2018
---
# <a name="back-up-and-restore-of-sql-server-databases"></a>Backup e ripristino di database SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  In questo argomento vengono descritti i vantaggi dell'esecuzione del backup dei database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e illustrati i termini di base del backup e del ripristino. Vengono inoltre presentate alcune strategie di backup e ripristino per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e alcune considerazioni relative alla sicurezza per il backup e il ripristino di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 
  
> **Servono istruzioni dettagliate?** Questo argomento **non fornisce procedure specifiche per l'esecuzione di un backup**. Per informazioni specifiche sul backup, in fondo a questa pagina è presente una sezione di collegamenti, organizzati per attività di backup e in base all'uso di T-SQL o SQL Server Management Studio.  
  
 Il componente di backup e ripristino di SQL Server rappresenta uno strumento essenziale per la sicurezza e la protezione di dati di importanza critica archiviati nei database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per ridurre il rischio di perdita irreversibile dei dati, è necessario eseguire regolarmente il backup dei database per preservare le modifiche ai dati. Una strategia di backup e ripristino ben pianificata aiuta a proteggere i database dalla perdita di dati causata da vari tipi di guasti e problemi. Il test della strategia mediante il ripristino di un set di backup e il recupero del database assicura una efficace preparazione a reagire in qualsiasi emergenza.  
  
 Oltre alle risorse di archiviazione locale per l'archiviazione di backup, SQL Server supporta anche il backup e il ripristino dal servizio di archiviazione BLOB di Windows Azure. Per altre informazioni, vedere [Backup e ripristino di SQL Server con il servizio di archiviazione BLOB di Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md). Per i file di database archiviati tramite il servizio di archiviazione BLOB di Microsoft Azure, [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] consente di usare gli snapshot di Azure per backup quasi istantanei e operazioni di ripristino più veloci. Per altre informazioni, vedere [Backup di snapshot di file per i file di database in Azure](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md).  
  
##  <a name="why-back-up"></a>Perché è importante eseguire un backup?  
-   L'esecuzione di backup dei database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , l'esecuzione di procedure di ripristino di test sui backup e l'archiviazione delle copie di backup in una posizione esterna sicura costituiscono modi validi per evitare una perdita di dati potenzialmente irreversibile. **Il backup è l'unico modo per proteggere i dati.**

     Con backup validi di un database, è possibile recuperare i dati a seguito di molti tipi di guasti ed errori, quali:  
  
    -   Errori di funzionamento dei supporti.  
  
    -   Errori degli utenti, ad esempio l'eliminazione accidentale di una tabella.  
  
    -   Errori hardware, ad esempio un'unità disco danneggiata o la perdita definitiva di un server.  
  
    -   Calamità naturali o altre emergenze gravi. Tramite il backup di SQL Server nel servizio di archiviazione BLOB di Windows Azure, è possibile creare un backup esterno in un'area diversa dalla posizione locale da utilizzare in caso si venga colpiti da una calamità naturale.  
  
-   I backup di un database risultano inoltre utili per le attività di amministrazione di routine, ad esempio la copia di un database da un server a un altro, l'impostazione di [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] o del mirroring del database e l'archiviazione.  
  
##  <a name="glossary-of-backup-terms"></a>Glossario dei termini di backup
 **eseguire un backup** [verbo]  
 Operazione di copia di dati o record di log da un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o dal relativo log delle transazioni in un dispositivo di backup, ad esempio un disco, per creare un backup dei dati o del log.  
  
 **backup** [sostantivo]  
 Copia dei dati utilizzabile per il ripristino e il recupero in seguito a un errore. I backup di un database possono essere utilizzati anche per ripristinare una copia del database in una nuova posizione.  
  
Dispositivo di**backup**   
 Dispositivo disco o nastro nel quale vengono scritti i backup di SQL Server e da cui è possibile eseguirne il ripristino. I backup di SQL Server possono anche essere scritti in un servizio di archiviazione BLOB di Microsoft Azure e viene usato il formato **URL** per specificare la destinazione e il nome del file di backup. Per altre informazioni, vedere [Backup e ripristino di SQL Server con il servizio di archiviazione BLOB di Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md).  
  
**supporti di backup**  
 Uno o più nastri o file del disco in cui sono stati scritti uno o più backup.  
  
**backup dei dati**  
 Backup dei dati in un database completo (backup del database), database parziale (backup parziale) o set di file di dati o di filegroup (backup di file).  
  
**backup del database**  
 Backup di un database. I backup completi del database rappresentano l'intero database al momento del completamento del backup. I backup differenziali del database contengono solo le modifiche apportate al database a partire dal backup del database più recente.  
  
**backup differenziale**  
 Backup dei dati basato sull'ultimo backup completo di un database completo o parziale o di un set di file di dati o di filegroup (base differenziale) che contiene solo i dati modificati rispetto a quella base.  
  
**backup completo**  
 Backup dei dati che include tutti i dati in un database specifico o in un set di filegroup o file, oltre a una parte di log sufficiente al recupero di tali dati.  
  
**backup di log**  
 Backup dei log delle transazioni che include tutti i record di log di cui non è stato eseguito il backup in un backup di log precedente. (modello di recupero con registrazione completa)  
  
**recuperare**  
 Riportare un database a uno stato stabile e coerente.  
  
**recovery**  
 Fase di avvio del database o di ripristino con recupero che porta il database in uno stato coerente a livello di transazioni.  
  
**modello di recupero**  
 Proprietà del database che controlla la manutenzione del log delle transazioni su un database. Sono tre i modelli di recupero disponibili: con registrazione minima, con registrazione completa e con registrazione minima delle operazioni bulk. Il modello di recupero del database ne determina i requisiti di backup e di ripristino.  
  
**ripristino**  
 Processo multifase che copia tutti i dati e le pagine di log da un backup di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a un database specificato ed esegue il rollforward di tutte le transazioni registrate nel backup applicando le modifiche registrate in modo da aggiornare i dati.  
  
 ##  <a name="backup-and-restore-strategies"></a>Strategie di backup e ripristino  
 Il backup e il ripristino dei dati devono essere personalizzati per uno specifico ambiente e devono funzionare con le risorse disponibili. Per un utilizzo affidabile delle funzionalità di backup e ripristino è pertanto necessaria un'apposita strategia. Una strategia ben progettata a tale scopo ottimizza la disponibilità dei dati e ne riduce al minimo la perdita, rispettando al contempo le esigenze aziendali specifiche.  
  
#### <a name="important"></a>Importante! 
**Archiviare il database e i backup su dispositivi separati. In caso contrario, se nel dispositivo contenente il database si verifica un errore, i backup non saranno disponibili. L'archiviazione dei dati e dei backup su dispositivi separati migliora inoltre le prestazioni di I/O sia per la scrittura dei backup che per l'uso in produzione del database.**  
  
 Tale strategia prevede una parte relativa al backup e una parte relativa al ripristino. La parte della strategia relativa al backup definisce il tipo e la frequenza delle operazioni di backup, il tipo e la velocità dell'hardware necessario, le modalità di esecuzione di test dei backup, nonché i percorsi e le modalità di archiviazione dei relativi supporti, incluse le considerazioni relative alla sicurezza. La parte della strategia relativa al ripristino definisce il responsabile dell'esecuzione delle operazioni di ripristino e la modalità di esecuzione di tali operazioni in modo da realizzare gli obiettivi relativi alla disponibilità del database e ridurre al minimo il rischio di perdita dei dati. È consigliabile documentare le procedure di backup e ripristino e mantenerne una copia nella documentazione relativa alle procedure operative aziendali.  
  
 La progettazione di una strategia di backup e ripristino efficace richiede operazioni accurate di pianificazione, implementazione e testing. È necessario eseguire test. Una strategia di backup può essere considerata efficace solo dopo il completamento del ripristino dei backup in tutte le combinazioni incluse nella strategia. È necessario considerare una vasta gamma di fattori, tra cui:  
  
-   Obiettivi di produzione dell'organizzazione per i database, in particolar modo i requisiti relativi alla disponibilità e alla protezione dalla perdita dei dati.  
  
-   Caratteristiche di ogni database, ovvero dimensioni, tipo di utilizzo, tipo di contenuto, requisiti relativi ai dati e così via.  
  
-   Vincoli relativi alle risorse, ad esempio hardware, personale, spazio per l'archiviazione dei supporti di backup, sicurezza fisica dei supporti archiviati e così via.  

### <a name="impact-of-the-recovery-model-on-backup-and-restore"></a>Impatto del modello di recupero sulle operazioni di backup e di ripristino  
 Le operazioni di backup e di ripristino si verificano nel contesto di un modello di recupero, ovvero una proprietà del database tramite la quale si controlla la modalità di gestione del log delle transazioni. Il modello di recupero di un database determina inoltre i tipi di scenari di backup e ripristino supportati per il database. In genere, in un database viene utilizzato il modello di recupero con registrazione minima o il modello di recupero con registrazione completa. Il modello di recupero con registrazione completa può essere integrato passando al modello di recupero con registrazione minima delle operazioni bulk prima delle operazioni bulk. Per un'introduzione a questi modelli di recupero e alla loro influenza sulla gestione del log delle transazioni, vedere [Log delle transazioni (SQL Server)](https://msdn.microsoft.com/library/ms190925(SQL.130).aspx)  
  
 Il modello di recupero migliore per un database dipende dalle esigenze aziendali. Per evitare la gestione del log delle transazioni e semplificare le operazioni di backup e ripristino, è possibile utilizzare il modello di recupero con registrazione minima. Per ridurre al minimo il rischio di perdita di dati, aumentando tuttavia il numero di operazioni amministrative, è possibile utilizzare il modello di recupero con registrazione completa. Per informazioni sull'effetto dei modelli di recupero sulle operazioni di backup e ripristino, vedere [Panoramica del backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md).  
  
### <a name="design-your-backup-strategy"></a>Progettare la strategia di backup  
 Dopo aver selezionato un modello di recupero che soddisfa le esigenze aziendali per un determinato database, è necessario pianificare e implementare una strategia di backup corrispondente. La strategia ottimale dipende da una serie di fattori. Di seguito vengono riportati i più significativi:  
  
-   Numero di ore giornaliere per cui è necessario garantire l'accesso delle applicazioni al database.  
  
     Se è possibile prevedere un periodo di minore attività, è consigliabile pianificare i backup completi del database durante tale periodo.  
  
-   Frequenza prevista per l'esecuzione di modifiche e aggiornamenti.  
  
     Se le modifiche sono frequenti, considerare gli aspetti seguenti:  
  
    -   Nel modello di recupero con registrazione minima è consigliabile pianificare backup differenziali nei periodi intermedi tra i backup completi del database. Con un backup differenziale è possibile acquisire solo le modifiche successive all'ultimo backup completo del database.  
  
    -   Nel modello di recupero con registrazione completa è necessario pianificare backup frequenti del log. La pianificazione di backup differenziali nei periodi intermedi tra i backup completi consente di ridurre i tempi di ripristino limitando il numero di backup del log da ripristinare in seguito al ripristino dei dati.  
  
-   Ambito previsto per le modifiche, ovvero solo in parti ridotte del database o in gran parte del database.  
  
     Per un database di dimensioni estese in cui le modifiche sono concentrate in una parte dei file o dei filegroup, i backup parziali e/o i backup del file possono risultare utili. Per altre informazioni, vedere [Backup parziali &#40; SQL Server &#41;](../../relational-databases/backup-restore/partial-backups-sql-server.md) e [Backup dei file completo &#40; SQL Server &#41;](../../relational-databases/backup-restore/full-file-backups-sql-server.md).  
  
-   Quantità di spazio su disco necessaria per un backup completo del database.  
  
 ### <a name="estimate-the-size-of-a-full-database-backup"></a>Stimare le dimensioni di un backup completo del database  
 Prima di implementare una strategia di backup e ripristino, stimare quanto spazio su disco verrà utilizzato da un backup del database completo. Con l'operazione di backup i dati contenuti nel database vengono copiati nel file di backup. Poiché il backup include soltanto i dati presenti nel database, ma non lo spazio inutilizzato, le dimensioni del backup risultano di solito inferiori a quelle del database originale. È possibile stimare la dimensione di un backup del database completo tramite la stored procedure di sistema **sp_spaceused**. Per altre informazioni, vedere [sp_spaceused &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md).  
  
### <a name="schedule-backups"></a>Pianificare le operazioni di backup  
 L'esecuzione di un'operazione di backup ha un effetto minimo sulle transazioni in esecuzione; è possibile quindi eseguire le operazioni di backup durante le operazioni normali. È possibile eseguire un backup di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con un effetto minimo sui carichi di lavoro di produzione.  
   
>  Per informazioni sulle restrizioni di concorrenza durante il backup, vedere [Panoramica del backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md).  
  
 Dopo aver stabilito i tipi di backup necessari e la frequenza di esecuzione per ogni tipo, è consigliabile pianificare backup regolari come parte di un piano di manutenzione per il database. Per informazioni sui piani di manutenzione e su come crearli per i backup di database e di log, vedere [Use the Maintenance Plan Wizard](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md).  
  
### <a name="test-your-backups"></a>Eseguire test dei backup  
 Una strategia di ripristino può essere considerata efficace solo dopo l'esecuzione di test dei backup. È essenziale testare accuratamente la strategia di backup per ogni database ripristinando una copia del database in un sistema di prova. È necessario testare il ripristino di tutti i tipi di backup che si desidera utilizzare.  
  
 È consigliabile mantenere un manuale operativo per ogni database, in cui indicare la posizione dei backup, i nomi dei dispositivi di backup (se presenti) e il tempo necessario per il ripristino dei backup di prova.  
  
## <a name="more-about-backup-tasks"></a>Altre informazioni sulle operazioni di backup  
-   [Creare un piano di manutenzione](../../relational-databases/maintenance-plans/create-a-maintenance-plan.md)  
  
-   [Creazione di un processo](http://msdn.microsoft.com/library/b35af2b6-6594-40d1-9861-4d5dd906048c)  
  
-   [Pianificare un processo](http://msdn.microsoft.com/library/f626390a-a3df-4970-b7a7-a0529e4a109c)  
  
## <a name="working-with-backup-devices-and-backup-media"></a>Uso dei dispositivi di backup e dei supporti di backup  
-   [Definire un dispositivo di backup logico per un file su disco &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-disk-file-sql-server.md)  
  
-   [Definire un dispositivo di backup logico per un'unità nastro &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
-   [Specificare un disco o un nastro come destinazione di backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/specify-a-disk-or-tape-as-a-backup-destination-sql-server.md)  
  
-   [Eliminare un dispositivo di backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/delete-a-backup-device-sql-server.md)  
  
-   [Impostare la data di scadenza di un backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/set-the-expiration-date-on-a-backup-sql-server.md)  
  
-   [Visualizzare il contenuto di un nastro o di un file di backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [Visualizzare i file di dati e i file di log in un set di backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-data-and-log-files-in-a-backup-set-sql-server.md)  
  
-   [Visualizzare le proprietà e il contenuto di un dispositivo di backup logico &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
-   [Ripristinare un backup da un dispositivo &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-backup-from-a-device-sql-server.md)  
  
## <a name="creating-backups"></a>Creazione di backup  
**Nota** Per eseguire backup parziali o di sola copia, è necessario usare l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)][BACKUP](../../t-sql/statements/backup-transact-sql.md) rispettivamente con l'opzione PARTIAL o COPY_ONLY.  
  
 ### <a name="using-ssms"></a>Utilizzo di SSMS   
-   [Creare un backup completo del database &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [Eseguire il backup di un log delle transazioni &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
-   [Backup di file e filegroup &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)  
  
-   [Creare un backup differenziale del database &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
 ### <a name="using-t-sql"></a>Uso di T-SQL  
-   [Usare Resource Governor per limitare l'utilizzo della CPU da parte della compressione dei backup &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)  
  
-   [Esecuzione del backup del log delle transazioni quando il database è danneggiato &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md)  
  
-   [Abilitare o disabilitare il checksum di backup durante il backup o il ripristino &#40;SQL Server&#41;](../../relational-databases/backup-restore/enable-or-disable-backup-checksums-during-backup-or-restore-sql-server.md)  
  
-   [Specificare se un'operazione di backup o ripristino viene arrestata o prosegue in seguito a un errore &#40;SQL Server&#41;](../../relational-databases/backup-restore/specify-if-backup-or-restore-continues-or-stops-after-error.md)  
  
## <a name="restore-data-backups"></a>Ripristinare backup di dati 
### <a name="using-ssms"></a>Utilizzo di SSMS 
-   [Ripristinare un backup del database tramite SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)  
  
-   [Ripristinare un database in un percorso nuovo &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)  
  
-   [Ripristinare un backup differenziale del database &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-differential-database-backup-sql-server.md)  
  
-   [Ripristino di file e filegroup &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-sql-server.md)  
  
### <a name="using-t-sql"></a>Uso di T-SQL
-   [Ripristinare un backup del database nel modello di recupero con registrazione minima &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-a-database-backup-under-the-simple-recovery-model-transact-sql.md)  
  
-   [Ripristinare un database fino al punto di errore nel modello di recupero con registrazione completa &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-database-to-point-of-failure-full-recovery.md)  
  
-   [Ripristinare file e filegroup sovrascrivendo file esistenti &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-over-existing-files-sql-server.md)  
  
-   [Ripristinare file in un percorso nuovo &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-to-a-new-location-sql-server.md)  
  
-   [Ripristinare il database master &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-the-master-database-transact-sql.md)  

## <a name="restore-transaction-logs-full-recovery-model"></a>Ripristinare il log delle transazioni (modello di recupero con registrazione completa)
### <a name="using-ssms"></a>Utilizzo di SSMS  
-   [Ripristinare un database fino a una transazione contrassegnata &#40;SQL Server Management Studio&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)  
  
-   [Ripristinare un backup del log delle transazioni &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
-   [Ripristinare un database di SQL Server fino a un punto specifico &#40;Modello di recupero con registrazione completa&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
  
 ### <a name="using-t-sql"></a>Uso di T-SQL 
-   [Ripristinare un database di SQL Server fino a un punto specifico &#40;modello di recupero con registrazione completa&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
 
-   [Riavviare un'operazione di ripristino interrotta &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restart-an-interrupted-restore-operation-transact-sql.md)  
  
-   [Recuperare un database senza il ripristino dei dati &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/recover-a-database-without-restoring-data-transact-sql.md)  
 
## <a name="more-information-and-resources"></a>Altre informazioni e risorse
 [Panoramica del backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)   
 [Panoramica del ripristino e del recupero &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Backup e ripristino di database di Analysis Services](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)   
 [Backup e ripristino di indici e cataloghi full-text](../../relational-databases/search/back-up-and-restore-full-text-catalogs-and-indexes.md)   
 [Backup e ripristino di database replicati](../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)   
 [Log delle transazioni &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [Modelli di recupero &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)   
 [Set di supporti, gruppi di supporti e set di backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)  
  
  
