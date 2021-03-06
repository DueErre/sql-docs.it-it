---
title: sp_addmergearticle (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_addmergearticle
- sp_addmergearticle_TSQL
helpviewer_keywords: sp_addmergearticle
ms.assetid: 0df654ea-24e2-4c61-a75a-ecaa7a140a6c
caps.latest.revision: "69"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cd9d9ead2695338116dd3da6a60285756cb433c6
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="spaddmergearticle-transact-sql"></a>sp_addmergearticle (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aggiunge un articolo a una pubblicazione di tipo merge esistente. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_addmergearticle [ @publication = ] 'publication'   
        , [ @article = ] 'article'   
        , [ @source_object = ] 'source_object'   
    [ , [ @type = ] 'type' ]   
    [ , [ @description = ] 'description' ]   
    [ , [ @column_tracking = ] 'column_tracking' ]   
    [ , [ @status = ] 'status' ]   
    [ , [ @pre_creation_cmd = ] 'pre_creation_cmd' ]   
    [ , [ @creation_script = ] 'creation_script' ]   
    [ , [ @schema_option = ] schema_option ]   
    [ , [ @subset_filterclause = ] 'subset_filterclause' ]   
    [ , [ @article_resolver = ] 'article_resolver' ]   
    [ , [ @resolver_info = ] 'resolver_info' ]   
    [ , [ @source_owner = ] 'source_owner' ]   
    [ , [ @destination_owner = ] 'destination_owner' ]   
    [ , [ @vertical_partition = ] 'vertical_partition' ]   
    [ , [ @auto_identity_range = ] 'auto_identity_range' ]   
    [ , [ @pub_identity_range = ] pub_identity_range ]   
    [ , [ @identity_range = ] identity_range ]   
    [ , [ @threshold = ] threshold ]   
    [ , [ @verify_resolver_signature = ] verify_resolver_signature ]   
    [ , [ @destination_object = ] 'destination_object' ]   
    [ , [ @allow_interactive_resolver = ] 'allow_interactive_resolver' ]   
    [ , [ @fast_multicol_updateproc = ] 'fast_multicol_updateproc' ]   
    [ , [ @check_permissions = ] check_permissions ]   
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @published_in_tran_pub = ] 'published_in_tran_pub' ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @logical_record_level_conflict_detection = ] 'logical_record_level_conflict_detection' ]  
    [ , [ @logical_record_level_conflict_resolution = ] 'logical_record_level_conflict_resolution' ]  
    [ , [ @partition_options = ] partition_options ]  
    [ , [ @processing_order = ] processing_order ]  
    [ , [ @subscriber_upload_options = ] subscriber_upload_options ]  
    [ , [ @identityrangemanagementoption = ] 'identityrangemanagementoption' ]  
    [ , [ @delete_tracking = ] delete_tracking ]  
    [ , [ @compensate_for_errors = ] 'compensate_for_errors' ]   
    [ , [ @stream_blob_columns = ] 'stream_blob_columns' ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@publication=** ] **'***pubblicazione***'**  
 Nome della pubblicazione in cui è contenuto l'articolo. *pubblicazione* è **sysname**, non prevede alcun valore predefinito.  
  
 [  **@article=** ] **'***articolo***'**  
 Nome dell'articolo. Deve essere un nome univoco all'interno della pubblicazione. *articolo* è **sysname**, non prevede alcun valore predefinito. *articolo* deve essere nel computer locale che esegue [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e devono essere conformi alle regole per gli identificatori.  
  
 [  **@source_object=** ] **'***source_object***'**  
 Oggetto di database da pubblicare. *source_object* è **sysname**, non prevede alcun valore predefinito. Per ulteriori informazioni sui tipi di oggetti che possono essere pubblicati tramite replica di tipo merge, vedere [pubblicare dati e oggetti di Database](../../relational-databases/replication/publish/publish-data-and-database-objects.md).  
  
 [  **@type=** ] **'***tipo***'**  
 Tipo di articolo. *tipo* è **sysname**, il valore predefinito è **tabella**, e può essere uno dei valori seguenti.  
  
|Valore|Description|  
|-----------|-----------------|  
|**tabella** (impostazione predefinita)|Tabella con schema e dati. La tabella viene monitorata per determinare i dati da replicare.|  
|**Func schema solo**|Funzione con solo schema.|  
|**vista indicizzata** **solo schema**|Vista indicizzata con solo schema.|  
|**proc schema solo**|Stored procedure con solo schema.|  
|**solo schema sinonimo**|Sinonimo con solo schema.|  
|**solo schema della vista**|Vista con solo schema.|  
  
 [  **@description=** ] **'***descrizione***'**  
 Descrizione dell'articolo. *Descrizione* è **nvarchar (255)**, con un valore predefinito è NULL.  
  
 [  **@column_tracking=** ] **'***column_tracking***'**  
 Impostazione per il rilevamento a livello di colonna. *column_tracking* è **nvarchar (10)**, con un valore predefinito è FALSE. **true**Attiva rilevamento livello di colonna. **false** Disattiva rilevamento livello di colonna e mantiene il rilevamento dei conflitti a livello di riga. Se la tabella è già pubblicata in altre pubblicazioni di tipo merge, è necessario utilizzare lo stesso valore di rilevamento a livello di colonna utilizzato dagli articoli esistenti basati su questa tabella. Questo parametro è disponibile solo per gli articoli di tabelle.  
  
> [!NOTE]  
>  Se si utilizza il rilevamento a livello di riga per il rilevamento dei conflitti (impostazione predefinita), la tabella di base può includere fino a 1.024 colonne, che devono tuttavia essere filtrate dall'articolo in modo da pubblicare un massimo di 246 colonne. Se viene utilizzato il rilevamento a livello di colonna, nella tabella di base possono essere incluse al massimo 246 colonne.  
  
 [  **@status=** ] **'***stato***'**  
 Stato dell'articolo. *stato* è **nvarchar (10)**, il valore predefinito è **unsynced**. Se **active**, viene eseguito lo script di elaborazione iniziale per pubblicare la tabella. Se **unsynced**, lo script di elaborazione iniziale per pubblicare la tabella viene eseguito alla successiva esecuzione dell'agente Snapshot.  
  
 [  **@pre_creation_cmd=** ] **'***pre_creation_cmd***'**  
 Azione eseguita dal sistema se, quando si applica lo snapshot, la tabella esiste già nel Sottoscrittore. *pre_creation_cmd* è **nvarchar (10)**, e può essere uno dei valori seguenti.  
  
|Valore|Description|  
|-----------|-----------------|  
|**Nessuno**|Se la tabella esiste già nel Sottoscrittore, non viene eseguita alcuna azione.|  
|**eliminare**|Esegue un'operazione di eliminazione in base alla clausola WHERE del filtro di subset.|  
|**eliminare** (impostazione predefinita)|Elimina la tabella prima di ricrearla. Necessario per supportare [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssEW](../../includes/ssew-md.md)] sottoscrittori.|  
|**troncare**|Tronca la tabella di destinazione.|  
  
 [  **@creation_script=** ] **'***creation_script***'**  
 Percorso e nome di uno script facoltativo dello schema dell'articolo usato per creare l'articolo nel database di sottoscrizione. *creation_script* è **nvarchar (255)**, con un valore predefinito è NULL.  
  
> [!NOTE]  
>  Gli script di creazione non vengono eseguiti nei Sottoscrittori [!INCLUDE[ssEW](../../includes/ssew-md.md)].  
  
 [  **@schema_option=** ] *schema_option*  
 Mappa di bit dell'opzione di generazione dello schema per l'articolo specificato. *schema_option* è **Binary (8)**e può essere il [| (OR bit per bit) ](../../t-sql/language-elements/bitwise-or-transact-sql.md) prodotto di uno o più dei valori seguenti.  
  
|Valore|Description|  
|-----------|-----------------|  
|**0x00**|Disabilita la creazione di script tramite l'agente Snapshot e utilizza lo script di creazione preliminare dello schema definito in *creation_script*.|  
|**0x01**|Genera le istruzioni per la creazione di oggetti (CREATE TABLE, CREATE PROCEDURE e così via). Questo è il valore predefinito per gli articoli di stored procedure.|  
|**0x10**|Genera un indice cluster corrispondente. Anche se questa opzione non viene impostata, se sono già definiti in una tabella pubblicata, gli indici correlati alle chiavi primarie e i vincoli UNIQUE vengono generati.|  
|**0x20**|Converte i tipi di dati definiti dall'utente (UDT) in tipi di dati di base nel Sottoscrittore. Questa opzione non può essere usata quando è presente un vincolo CHECK o DEFAULT su una colonna UDT, se una colonna UDT è inclusa nella chiave primaria o se una colonna calcolata fa riferimento a una colonna UDT.|  
|**0x40**|Genera indici non cluster corrispondenti. Anche se questa opzione non viene impostata, se sono già definiti in una tabella pubblicata, gli indici correlati alle chiavi primarie e i vincoli UNIQUE vengono generati.|  
|**0x80**|Replica i vincoli PRIMARY KEY. Vengono inoltre replicati tutti gli indici correlati al vincolo, anche se le opzioni **0x10** e **0x40** non sono abilitati.|  
|**0x100**|Replica gli eventuali trigger dell'utente di un articolo di tabella.|  
|**0x200**|Replica i vincoli FOREIGN KEY. Se la tabella con riferimenti non fa parte di una pubblicazione, tutti i vincoli FOREIGN KEY in una tabella pubblicata non vengono replicati.|  
|**0x400**|Replica i vincoli CHECK.|  
|**0x800**|Replica i valori predefiniti.|  
|**0x1000**|Replica le regole di confronto a livello di colonna.|  
|**0x2000**|Replica le proprietà estese associate all'oggetto di origine dell'articolo pubblicato.|  
|**0x4000**|Replica i vincoli UNIQUE. Vengono inoltre replicati tutti gli indici correlati al vincolo, anche se le opzioni **0x10** e **0x40** non sono abilitati.|  
|**0x8000**|Questa opzione non è valida per i server di pubblicazione che eseguono [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o versioni successive.|  
|**0x10000.**|Replica i vincoli CHECK come NOT FOR REPLICATION in modo che i vincoli non vengono imposti durante la sincronizzazione.|  
|**0x20000**|Replica i vincoli FOREIGN KEY come NOT FOR REPLICATION in modo che i vincoli non vengono imposti durante la sincronizzazione.|  
|**0x40000**|Replica i filegroup associati a una tabella o un indice partizionato.|  
|**0x80000**|Replica lo schema di partizione per una tabella partizionata.|  
|**0x100000**|Replica lo schema di partizione per un indice partizionato.|  
|**0x200000**|Replica le statistiche della tabella.|  
|**0x400000**|Replica le associazioni predefinite.|  
|**0x800000**|Replica le associazioni di regole.|  
|**0x1000000**|Replica l'indice full-text.|  
|**0x2000000**|Raccolte di XML schema associata a **xml** colonne non vengono replicate.|  
|**0x4000000**|Replica gli indici su **xml** colonne.|  
|**0x8000000**|Crea gli eventuali schemi non ancora presenti nel Sottoscrittore.|  
|**0x10000000**|Converte **xml** colonne **ntext** nel Sottoscrittore.|  
|**0x20000000**|Tipi di dati dell'oggetto converte di grandi dimensioni (**nvarchar (max)**, **varchar (max)**, e **varbinary (max)**) introdotto in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ai tipi di dati che sono supportati in [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)].|  
|**0x40000000**|Replica le autorizzazioni.|  
|**0x80000000**|Esegue un tentativo di rimozione delle dipendenze dagli oggetti che non fanno parte della pubblicazione.|  
|**0x100000000**|Utilizzare questa opzione per replicare l'attributo FILESTREAM se viene specificato in **varbinary (max)** colonne. Non specificare questa opzione se si stanno replicando tabelle nei Sottoscrittori [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. La replica di tabelle con colonne FILESTREAM in [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] sottoscrittori non è supportata, indipendentemente dall'impostazione di questa opzione dello schema. Vedere l'opzione correlata **0x800000000**.|  
|**0x200000000**|Converte i tipi di dati data e ora (**data**, **ora**, **datetimeoffset**, e **datetime2**) introdotto in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ai dati tipi supportati nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**0x400000000**|Replica l'opzione di compressione per dati e indici. Per altre informazioni, vedere [Data Compression](../../relational-databases/data-compression/data-compression.md).|  
|**0x800000000**|Impostare questa opzione per archiviare i dati FILESTREAM nel relativo filegroup nel Sottoscrittore. Se questa opzione non è impostata, i dati FILESTREAM vengono archiviati nel filegroup predefinito. Tramite la replica non vengono creati filegroup, pertanto, se si imposta questa opzione, è necessario creare il filegroup prima di applicare lo snapshot nel Sottoscrittore. Per ulteriori informazioni su come creare gli oggetti prima di applicare lo snapshot, vedere [eseguire script prima e dopo l'applicazione dello Snapshot](../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md).<br /><br /> Vedere l'opzione correlata **0x100000000**.|  
|**0x1000000000**|Converte i tipi common language runtime (CLR) definito dall'utente (UDT) in **varbinary (max)** in modo che le colonne di tipo definito dall'utente possono essere replicate nei Sottoscrittori che eseguono [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
|**0x2000000000**|Converte il **hierarchyid** tipo di dati **varbinary (max)** in modo che le colonne di tipo **hierarchyid** possano essere replicate nei Sottoscrittori che eseguono [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Per ulteriori informazioni su come usare **hierarchyid** colonne nelle tabelle replicate, vedere [hierarchyid &#40; Transact-SQL &#41; ](../../t-sql/data-types/hierarchyid-data-type-method-reference.md).|  
|**0x4000000000**|Replica gli eventuali indici filtrati sulla tabella. Per ulteriori informazioni sugli indici filtrati, vedere [Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md).|  
|**0x8000000000**|Converte il **geography** e **geometry** tipi di dati di **varbinary (max)** in modo che le colonne di questi tipi possono essere replicate nei Sottoscrittori che eseguono [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
|**0x10000000000**|Replica gli indici su colonne di tipo **geography** e **geometry**.|  
  
 Se è NULL, il sistema genera automaticamente un'opzione di schema valida per l'articolo. Il **opzioni predefinite dello Schema** tabella nella sezione Osservazioni vengono illustrati i valori viene scelto in base al tipo di articolo. Inoltre, non tutti *schema_option* valori validi per ogni tipo di replica e il tipo di articolo. Il **opzioni di Schema valide** tabella nella sezione Osservazioni vengono illustrate le opzioni che possono essere specificate per un tipo di articolo specificato.  
  
> [!NOTE]  
>  Il *schema_option* parametro influisce solo sulle opzioni di replica per lo snapshot iniziale. Dopo aver generato dall'agente Snapshot e applicato al sottoscrittore lo schema iniziale, la replica delle modifiche dello schema di pubblicazione al sottoscrittore eseguita in base alle regole di replica modifiche dello schema e *replicate_ddl* impostazione del parametro specificato in [sp_addmergepublication](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md). Per altre informazioni, vedere [Apportare modifiche allo schema nei database di pubblicazione](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md).  
  
 [  **@subset_filterclause=** ] **'***subset_filterclause***'**  
 Clausola WHERE che specifica il filtraggio orizzontale di un articolo di tabella senza la parola WHERE. *subset_filterclause* di **nvarchar (1000)**, con valore predefinito è una stringa vuota.  
  
> [!IMPORTANT]  
>  Per motivi relativi alle prestazioni, è consigliabile evitare di applicare funzioni ai nomi di colonna nelle clausole di filtro di riga con parametri, come `LEFT([MyColumn]) = SUSER_SNAME()`. Se si utilizza [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) in una clausola di filtro e si sostituisce il valore di HOST_NAME, potrebbe essere necessario convertire i tipi di dati tramite [CONVERTIRE](../../t-sql/functions/cast-and-convert-transact-sql.md). Per ulteriori informazioni sulle procedure consigliate in questo caso, vedere la sezione "Si esegue l'override del valore di HOST_NAME ()" in [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
 [  **@article_resolver=** ] **'***article_resolver***'**  
 Sistema di risoluzione basato su COM utilizzato per risolvere i conflitti nell'articolo di tabella oppure assembly .NET Framework richiamato per eseguire una logica di business personalizzata sull'articolo di tabella. *article_resolver* è **varchar (255)**, con un valore predefinito è NULL. I valori disponibili per questi parametri sono elencati nell'argomento relativo ai sistemi di risoluzione personalizzati [!INCLUDE[msCoName](../../includes/msconame-md.md)]. Se il valore specificato non corrisponde a uno dei sistemi di risoluzione [!INCLUDE[msCoName](../../includes/msconame-md.md)], in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene utilizzato il sistema di risoluzione specificato anziché quello di sistema. Utilizzare **sp_enumcustomresolvers** per enumerare l'elenco dei sistemi di risoluzione personalizzati disponibili. Per ulteriori informazioni, vedere [eseguire logica di Business durante la sincronizzazione di tipo Merge](../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md) e [Advanced Merge Replication Conflict Detection and risoluzione](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md).  
  
 [  **@resolver_info=** ] **'***resolver_info***'**  
 Specifica le informazioni aggiuntive necessarie per un sistema di risoluzione personalizzato. Alcuni sistemi di risoluzione [!INCLUDE[msCoName](../../includes/msconame-md.md)] richiedono una colonna come input. *resolver_info* è **nvarchar (255)**, con un valore predefinito è NULL. Per altre informazioni, vedere [Sistemi di risoluzione dei conflitti basati su Microsoft COM](../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-resolvers.md).  
  
 [  **@source_owner=** ] **'***source_owner***'**  
 È il nome del proprietario del *source_object*. *source_owner* è **sysname**, con un valore predefinito è NULL. Se il valore è NULL, l'utente corrente verrà considerato il proprietario.  
  
 [  **@destination_owner=** ] **'***destination_owner***'**  
 Proprietario dell'oggetto nel database di sottoscrizione, se diverso da 'dbo'. *destination_owner* è **sysname**, con un valore predefinito è NULL. Se NULL, 'dbo' verrà considerato il proprietario.  
  
 [  **@vertical_partition=** ] **'***column_filter***'**  
 Abilita e disabilita l'applicazione di filtri alle colonne in un articolo di tabella. *vertical_partition* è **nvarchar (5)** con un valore predefinito è FALSE.  
  
 **false** non indica è presente alcun filtro verticale e pubblica tutte le colonne.  
  
 **true** Cancella tutte le colonne ad eccezione della chiave primaria dichiarata e le colonne ROWGUID. Le colonne vengono aggiunte utilizzando **sp_mergearticlecolumn**.  
  
 [  **@auto_identity_range=** ] **'***automatic_identity_range***'**  
 Abilita e disabilita la gestione automatica degli intervalli di valori Identity per l'articolo di tabella specificato di una pubblicazione al momento della creazione. *auto_identity_range* è **nvarchar (5)**, con un valore predefinito è FALSE. **true** intervallo di valori identity automatico consente la gestione, mentre **false** la disabilita.  
  
> [!NOTE]  
>  *auto_identity_range* è stata deprecata e viene fornito solo per la compatibilità. È consigliabile utilizzare *identityrangemanagementoption* per specificare opzioni di gestione di intervalli di valori identity. Per altre informazioni, vedere [Replicare colonne Identity](../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
 [  **@pub_identity_range=** ] *pub_identity_range*  
 Controlla le dimensioni dell'intervallo di valori Identity allocato a un Sottoscrittore con una sottoscrizione server, quando è attivata la gestione automatica degli intervalli di valori Identity. L'intervallo di valori Identity è riservato al Sottoscrittore di ripubblicazione per l'assegnazione ai propri Sottoscrittori. *pub_identity_range* è **bigint**, con un valore predefinito è NULL. Se è necessario specificare questo parametro *identityrangemanagementoption* è **auto** o se *auto_identity_range* è **true**.  
  
 [  **@identity_range=** ] *identity_range*  
 Controlla le dimensioni dell'intervallo di valori Identity assegnato al server di pubblicazione e al Sottoscrittore quando è attivata la gestione automatica degli intervalli di valori Identity. *identity_range* è **bigint**, con un valore predefinito è NULL. Se è necessario specificare questo parametro *identityrangemanagementoption* è **auto** o se *auto_identity_range* è **true**.  
  
> [!NOTE]  
>  *identity_range* controlla le dimensioni di intervallo di valori identity nei utilizzando versioni precedenti di sottoscrittori di ripubblicazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [  **@threshold=** ] *soglia*  
 Valore percentuale che determina quando l'agente di merge assegna un nuovo intervallo di valori Identity. Quando la percentuale di valori specificato in *soglia* è utilizzato, l'agente di Merge crea un nuovo intervallo di valori identity. *soglia* è **int**, con un valore predefinito è NULL. Se è necessario specificare questo parametro *identityrangemanagementoption* è **auto** o se *auto_identity_range* è **true**.  
  
 [  **@verify_resolver_signature=** ] *verify_resolver_signature*  
 Specifica se una firma digitale viene verificata prima dell'utilizzo di un sistema di risoluzione nella replica di tipo merge. *verify_resolver_signature* è **int**, con un valore predefinito è 1.  
  
 **0** specifica che la firma non verrà verificata.  
  
 **1** specifica che la firma verrà verificata per stabilire se proviene da una fonte attendibile.  
  
 [  **@destination_object=** ] **'***destination_object***'**  
 Nome dell'oggetto nel database di sottoscrizione. *destination_object* è **sysname**, con un valore predefinito di ciò che è  **@source_object** . È possibile specificare questo parametro solo se l'articolo include solo lo schema, come nel caso di stored procedure, viste e funzioni definite dall'utente. Se l'articolo specificato non è un articolo di tabella, il valore in  *@source_object*  sostituisce il valore nel *destination_object*.  
  
 [  **@allow_interactive_resolver=** ] **'***allow_interactive_resolver***'**  
 Abilita o disabilita l'utilizzo del sistema di risoluzione interattivo in un articolo. *allow_interactive_resolver* è **nvarchar (5)**, con un valore predefinito è FALSE. **true** consente l'utilizzo di risoluzione interattivo per l'articolo; **false** la disabilita.  
  
> [!NOTE]  
>  Il sistema di risoluzione interattivo non è supportato dai Sottoscrittori [!INCLUDE[ssEW](../../includes/ssew-md.md)].  
  
 [  **@fast_multicol_updateproc=** ] **'***fast_multicol_updateproc***'**  
 Questo parametro è deprecato ed è ancora disponibile per compatibilità con gli script di versioni precedenti.  
  
 [  **@check_permissions=** ] *check_permissions*  
 Mappa di bit delle autorizzazioni a livello di tabella verificate quando l'agente di merge applica le modifiche nel server di pubblicazione. Se l'account di accesso o l'account utente del server di pubblicazione utilizzato per il processo di merge non dispone delle autorizzazioni corrette per le tabelle, le modifiche non valide vengono registrate come conflitti. *check_permissions* è **int**e può essere il [| (OR bit per bit) ](../../t-sql/language-elements/bitwise-or-transact-sql.md) prodotto di uno o più dei valori seguenti.  
  
|Valore|Description|  
|-----------|-----------------|  
|**0x00** (impostazione predefinita)|Le autorizzazioni non vengono controllate.|  
|**0x10**|Le autorizzazioni vengono controllate nel server di pubblicazione prima di consentire il caricamento delle operazioni di inserimento eseguite nel Sottoscrittore.|  
|**0x20**|Le autorizzazioni vengono controllate nel server di pubblicazione prima di consentire il caricamento delle operazioni di aggiornamento eseguite nel Sottoscrittore.|  
|**0x40**|Le autorizzazioni vengono controllate nel server di pubblicazione prima di consentire il caricamento delle operazioni di eliminazione eseguite nel Sottoscrittore.|  
  
 [  **@force_invalidate_snapshot=** ] *force_invalidate_snapshot*  
 Segnala che l'azione eseguita da questa stored procedure potrebbe invalidare uno snapshot esistente. *force_invalidate_snapshot* è un **bit**, con un valore predefinito è 0.  
  
 **0** specifica che aggiunta di un articolo non invalidano lo snapshot. Se la stored procedure rileva che la modifica richiede un nuovo snapshot, viene generato un errore e non viene apportata alcuna modifica.  
  
 **1** specifica che l'aggiunta di un articolo potrebbe invalidare lo snapshot potrebbe non essere valido e se sono disponibili sottoscrizioni che richiedono un nuovo snapshot, consente lo snapshot esistente deve essere contrassegnato come obsoleto e di generarne uno nuovo. *force_invalidate_snapshot* è impostato su **1** quando si aggiunge un articolo a una pubblicazione con uno snapshot esistente.  
  
 [  **@published_in_tran_pub=** ] **'***published_in_tran_pub***'**  
 Indica che un articolo in una pubblicazione di tipo merge viene pubblicato anche in una pubblicazione transazionale. *published_in_tran_pub* è **nvarchar (5)**, con un valore predefinito è FALSE. **true** specifica che l'articolo è pubblicato anche in una pubblicazione transazionale.  
  
 [  **@force_reinit_subscription=** ] *force_reinit_subscription*  
 Segnala che l'azione eseguita dalla stored procedure potrebbe richiedere la reinizializzazione delle sottoscrizioni esistenti. *force_reinit_subscription* è un **bit**, con un valore predefinito è 0.  
  
 **0** indica che l'aggiunta di un articolo non causano la reinizializzazione della sottoscrizione. Se la stored procedure rileva che la modifica richiede la reinizializzazione delle sottoscrizioni esistenti, viene generato un errore e non viene apportata alcuna modifica.  
  
 **1** indica che le modifiche apportate all'articolo di merge causano reinizializzazione delle sottoscrizioni esistenti e concede l'autorizzazione per la reinizializzazione della sottoscrizione. *force_reinit_subscription* è impostato su **1** quando *subset_filterclause* specifica un filtro di riga con parametri.  
  
 [  **@logical_record_level_conflict_detection=** ] **'***logical_record_level_conflict_detection***'**  
 Specifica il livello di rilevamento dei conflitti per un articolo membro di un record logico. *logical_record_level_conflict_detection* è **nvarchar (5)**, con un valore predefinito è FALSE.  
  
 **true** specifica che verrà rilevato un conflitto se vengono apportate modifiche in qualsiasi punto del record logico.  
  
 **false** specifica che viene utilizzato il rilevamento dei conflitti predefinito come specificato da *column_tracking*. Per altre informazioni, vedere [Raggruppare modifiche alle righe correlate con record logici](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).  
  
> [!NOTE]  
>  Poiché i record logici non sono supportati da [!INCLUDE[ssEW](../../includes/ssew-md.md)] sottoscrittori, è necessario specificare un valore di **false** per *logical_record_level_conflict_detection* per supportare tali sottoscrittori.  
  
 [  **@logical_record_level_conflict_resolution=** ] **'***logical_record_level_conflict_resolution***'**  
 Specifica il livello di risoluzione dei conflitti per un articolo membro di un record logico. *logical_record_level_conflict_resolution* è **nvarchar (5)**, con un valore predefinito è FALSE.  
  
 **true** specifica che l'intero record logico prevalente sovrascrive il record logico perdente.  
  
 **false** specifica che righe confermate non sono vincolate al record logico. Se *logical_record_level_conflict_detection* è **true**, quindi *logical_record_level_conflict_resolution* deve inoltre essere impostato su **true**. Per altre informazioni, vedere [Raggruppare modifiche alle righe correlate con record logici](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).  
  
> [!NOTE]  
>  Poiché i record logici non sono supportati da [!INCLUDE[ssEW](../../includes/ssew-md.md)] sottoscrittori, è necessario specificare un valore di **false** per *logical_record_level_conflict_resolution* per supportare tali sottoscrittori.  
  
 [  **@partition_options=** ] *partition_options*  
 Definisce il modo in cui vengono partizionati i dati nell'articolo. Ciò consente di ottimizzare le prestazioni se tutte le righe appartengono a un'unica partizione o a un'unica sottoscrizione. *partition_options* è **tinyint**, e può essere uno dei valori seguenti.  
  
|Valore|Description|  
|-----------|-----------------|  
|**0** (predefinito)|Il filtro applicato all'articolo è statico oppure non restituisce un subset di dati univoco per ogni partizione, ovvero si creano partizioni sovrapposte.|  
|**1**|Le partizioni sono sovrapposte e gli aggiornamenti DML (Data Manipulation Language) eseguiti nel Sottoscrittore non possono modificare la partizione a cui appartiene una riga.|  
|**2**|Il filtro applicato all'articolo restituisce partizioni non sovrapposte, ma più Sottoscrittori possono ricevere la stessa partizione.|  
|**3**|Il filtro applicato all'articolo restituisce partizioni non sovrapposte univoche per ogni sottoscrizione.|  
  
> [!NOTE]  
>  Se la tabella di origine per un articolo è già pubblicata in un'altra pubblicazione, il valore di *partition_options* deve essere lo stesso per entrambi gli articoli.  
  
 [  **@processing_order=** ] *processing_order*  
 Indica l'ordine di elaborazione degli articoli in una pubblicazione di tipo merge. *processing_order* è **int**, con un valore predefinito è 0. **0** specifica che l'articolo non è ordinato e qualsiasi altro valore rappresenta il valore ordinale dell'ordine di elaborazione per l'articolo. Gli articoli vengono elaborati in ordine crescente in base al valore. Se i due articoli hanno lo stesso valore, l'ordine di elaborazione è determinato dall'ordine di nome alternativo dell'articolo nel [sysmergearticles](../../relational-databases/system-tables/sysmergearticles-transact-sql.md) tabella di sistema. Per altre informazioni, vedere [Specificare l'ordine di elaborazione degli articoli di merge](../../relational-databases/replication/merge/specify-the-processing-order-of-merge-articles.md).  
  
 [  **@subscriber_upload_options=** ] *subscriber_upload_options*  
 Specifica le restrizioni per gli aggiornamenti eseguiti in un Sottoscrittore con una sottoscrizione client. Per altre informazioni, vedere [Ottimizzare le prestazioni della replica di tipo merge con gli articoli di solo download](../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md). *subscriber_upload_options* è **tinyint**, e può essere uno dei valori seguenti.  
  
|Valore|Description|  
|-----------|-----------------|  
|**0** (predefinito)|Nessuna restrizione. Le modifiche eseguite nel Sottoscrittore vengono caricate nel server di pubblicazione.|  
|**1**|Sono consentite modifiche in un Sottoscrittore, ma tali modifiche non vengono caricate nel server di pubblicazione.|  
|**2**|Non sono consentite modifiche nel Sottoscrittore.|  
  
 Modifica *subscriber_upload_options* richiede la sottoscrizione venga reinizializzata chiamando [sp_reinitmergepullsubscription &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-reinitmergepullsubscription-transact-sql.md).  
  
> [!NOTE]  
>  Se la tabella di origine per un articolo è già pubblicata in un'altra pubblicazione, il valore di *subscriber_upload_options* deve essere lo stesso per entrambi gli articoli.  
  
 [  **@identityrangemanagementoption=** ] *identityrangemanagementoption*  
 Specifica la modalità di gestione degli intervalli di valori Identity per l'articolo. *identityrangemanagementoption* è **nvarchar (10)**, e può essere uno dei valori seguenti.  
  
|Valore|Description|  
|-----------|-----------------|  
|**Nessuno**|Disabilita la gestione degli intervalli di valori Identity.|  
|**Manuale**|Contrassegna la colonna Identity con NOT FOR REPLICATION per consentire la gestione manuale degli intervalli di valori Identity.|  
|**Automatico**|Imposta la gestione automatica degli intervalli di valori Identity.|  
|NULL(default)|Per impostazione predefinita **Nessuno**quando il valore di *auto_identity_range* non **true**.|  
  
 Per garantire la compatibilità con le versioni precedenti, quando il valore di *identityrangemanagementoption* è NULL, il valore di *auto_identity_range* è selezionata. Tuttavia, quando il valore di *identityrangemanagementoption* non è NULL, il valore di *auto_identity_range* viene ignorato. Per altre informazioni, vedere [Replicare colonne Identity](../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
 [  **@delete_tracking=** ] **'***delete_tracking***'**  
 Indica se viene eseguita la replica delle eliminazioni. *delete_tracking* è **nvarchar (5)**, con un valore predefinito è TRUE. **false** indica che le eliminazioni non vengono replicate, e **true** indica che le eliminazioni vengono replicate, situazione corrispondente al normale funzionamento della replica di tipo merge. Quando *delete_tracking* è impostato su **false**, le righe eliminate nel Sottoscrittore devono essere rimosse manualmente nel server di pubblicazione e le righe eliminate nel server di pubblicazione devono essere rimosse manualmente nel Sottoscrittore.  
  
> [!IMPORTANT]  
>  Impostazione *delete_tracking* a **false** risultati non convergenza. Se la tabella di origine per un articolo è già pubblicata in un'altra pubblicazione, il valore di *delete_tracking* deve essere lo stesso per entrambi gli articoli.  
  
> [!NOTE]  
>  *delete_tracking* opzioni non possono essere impostate utilizzando il **Creazione guidata nuova pubblicazione** o **proprietà pubblicazione** la finestra di dialogo.  
  
 [  **@compensate_for_errors=** ] **'***compensate_for_errors***'**  
 Specifica se devono essere eseguite azioni di compensazione quando vengono rilevati errori durante la sincronizzazione. *compensate_for_errors si*s **nvarchar (5)**, con un valore predefinito è FALSE. Se impostato su **true**, le modifiche che non è possibile applicare un sottoscrittore o server di pubblicazione durante la sincronizzazione sempre causare azioni di compensazione per annullare la modifica; tuttavia, una configurata in modo non corretto sottoscrittore che genera un errore di può provocare modifiche in altri sottoscrittori e server di pubblicazione per essere annullata. **false** Disabilita queste azioni, tuttavia, gli errori di compensazione vengono comunque registrate con compensazione e le successive operazioni di unione continua a tentare di applicare le modifiche fino a quando non è riuscita.  
  
> [!IMPORTANT]  
>  Anche se i dati nelle righe interessate potrebbero sembrare non convergenti, non appena vengono risolti gli eventuali errori generati le modifiche potranno essere applicate e si otterrà la convergenza dei dati. Se la tabella di origine per un articolo è già pubblicata in un'altra pubblicazione, il valore di *compensate_for_errors* deve essere lo stesso per entrambi gli articoli.  
  
 [  **@stream_blob_columns=** ] **'***stream_blob_columns***'**  
 Specifica se viene utilizzata l'ottimizzazione del flusso di dati per la replica di colonne BLOB (Binary Large Object). *stream_blob_columns* è **nvarchar (5)**, con un valore predefinito è FALSE. **true** indica che l'ottimizzazione verrà tentato di eseguire. *stream_blob_columns* è impostata su true se FILESTREAM è abilitato. In questo modo, la replica dei dati FILESTREAM può essere eseguita in maniera ottimale e si riduce l'utilizzo della memoria. Per forzare gli articoli di tabella FILESTREAM non vengano utilizzati flussi blob, utilizzare **sp_changemergearticle** impostare *stream_blob_columns* su false.  
  
> [!IMPORTANT]  
>  L'abilitazione di questa ottimizzazione della memoria può ridurre le prestazioni dell'agente di merge durante la sincronizzazione. È consigliabile utilizzare questa opzione solo se vengono replicate colonne contenenti più megabyte di dati.  
  
> [!NOTE]  
>  Alcune funzionalità di replica di tipo merge, come i record logici, può comunque impedire l'ottimizzazione del flusso durante la replica di oggetti binari di grandi dimensioni anche con *stream_blob_columns* impostato su **true**.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_addmergearticle** viene utilizzata nella replica di tipo merge.  
  
 Quando si pubblicano gli oggetti, nei Sottoscrittori vengono copiate le relative definizioni. Per la pubblicazione di un oggetto di database che dipende da altri oggetti, è necessario pubblicare tutti gli oggetti a cui fa riferimento. Se ad esempio si pubblica una vista che dipende da una tabella, sarà necessario pubblicare anche la tabella.  
  
 Se si specifica un valore di **3** per *partition_options*, può essere presente una sola sottoscrizione per ogni partizione di dati dell'articolo. Se si crea una seconda sottoscrizione nella quale il criterio di filtro porta alla restituzione della stessa partizione della sottoscrizione esistente, quest'ultima viene eliminata.  
  
 Quando si specifica un valore pari a 3 per *partition_options*, dei metadati sono puliti ogni volta che viene eseguito l'agente di Merge e lo snapshot partizionato scade più rapidamente. Quando si utilizza questa opzione è consigliabile prendere in considerazione l'abilitazione di snapshot partizionati richiesti dal Sottoscrittore. Per altre informazioni, vedere [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md).  
  
 Aggiunta di un articolo con un filtro orizzontale statico, utilizzando *subset_filterclause*, a una pubblicazione esistente con articoli che includono filtri con parametri richiede la reinizializzazione delle sottoscrizioni.  
  
 Quando si specifica *processing_order*, si consiglia di lasciare gap tra i valori dell'ordine articolo, che rende più semplice impostare nuovi valori in futuro. Ad esempio, se si dispone di tre articoli denominati Articolo1, articolo2 e articolo3, impostare *processing_order* su 10, 20 e 30, anziché 1, 2 e 3. Per altre informazioni, vedere [Specificare l'ordine di elaborazione degli articoli di merge](../../relational-databases/replication/merge/specify-the-processing-order-of-merge-articles.md).  
  
## <a name="default-schema-option-table"></a>Tabella delle opzioni predefinite dello schema  
 La tabella seguente descrive il valore predefinito impostato dalla stored procedure se viene specificato un valore NULL per *schema_option*, che dipende dal tipo di articolo.  
  
|Tipo di articolo|Valore delle opzioni di schema|  
|------------------|-------------------------|  
|**Func schema solo**|**0x01**|  
|**solo schema della vista indicizzata**|**0x01**|  
|**proc schema solo**|**0x01**|  
|**table**|**0x0C034FD1**  -  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni successive con snapshot in modalità nativa.<br /><br /> **0x08034FF1**  -  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni successive con snapshot in modalità carattere.|  
|**solo schema della vista**|**0x01**|  
  
> [!NOTE]  
>  Se la pubblicazione supporta le versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], l'opzione dello schema predefinito per **tabella** è **0x30034FF1**.  
  
## <a name="valid-schema-option-table"></a>Tabella delle opzioni di schema valide  
 Nella tabella seguente vengono descritti i valori consentiti *schema_option* in base al tipo di articolo.  
  
|Tipo di articolo|Valori delle opzioni di schema|  
|------------------|--------------------------|  
|**Func schema solo**|**0x01** e **0x2000**|  
|**solo schema della vista indicizzata**|**0x01**, **0x040**, **0x0100**, **0x2000**, **0x40000**, **0x1000000**, e **0x200000**|  
|**proc schema solo**|**0x01** e **0x2000**|  
|**table**|Tutte le opzioni.|  
|**solo schema della vista**|**0x01**, **0x040**, **0x0100**, **0x2000**, **0x40000**, **0x1000000**, e **0x200000**|  
  
## <a name="example"></a>Esempio  
 [!code-sql[HowTo#sp_AddMergeArticle](../../relational-databases/replication/codesnippet/tsql/sp-addmergearticle-trans_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'appartenenza al ruolo predefinito del server **sysadmin** o al ruolo predefinito del database **db_owner** .  
  
## <a name="see-also"></a>Vedere anche  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [Pubblicare dati e oggetti di database](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Replica di colonne Identity](../../relational-databases/replication/publish/replicate-identity-columns.md)   
 [sp_changemergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)   
 [sp_dropmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md)   
 [sp_helpmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)   
 [Stored procedure per la replica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
