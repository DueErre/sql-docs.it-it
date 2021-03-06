---
title: sp_addarticle (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 10/28/2015
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
- sp_addarticle
- sp_addarticle_TSQL
helpviewer_keywords: sp_addarticle
ms.assetid: 0483a157-e403-4fdb-b943-23c1b487bef0
caps.latest.revision: "108"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: db34c4936cb02aaf65bd1c8117f54ad3b769f158
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="spaddarticle-transact-sql"></a>sp_addarticle (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Viene creato un articolo che viene aggiunto a una pubblicazione. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_addarticle [ @publication = ] 'publication'   
        , [ @article = ] 'article'   
    [ , [ @source_table = ] 'source_table' ]  
    [ , [ @destination_table = ] 'destination_table' ]   
    [ , [ @vertical_partition = ] 'vertical_partition' ]   
    [ , [ @type = ] 'type' ]   
    [ , [ @filter = ] 'filter' ]   
    [ , [ @sync_object= ] 'sync_object' ]   
        [ , [ @ins_cmd = ] 'ins_cmd' ]   
    [ , [ @del_cmd = ] 'del_cmd' ]   
        [ , [ @upd_cmd = ] 'upd_cmd' ]   
    [ , [ @creation_script = ] 'creation_script' ]   
    [ , [ @description = ] 'description' ]   
    [ , [ @pre_creation_cmd = ] 'pre_creation_cmd' ]   
    [ , [ @filter_clause = ] 'filter_clause' ]   
    [ , [ @schema_option = ] schema_option ]   
    [ , [ @destination_owner = ] 'destination_owner' ]   
    [ , [ @status = ] status ]   
    [ , [ @source_owner = ] 'source_owner' ]   
    [ , [ @sync_object_owner = ] 'sync_object_owner' ]   
    [ , [ @filter_owner = ] 'filter_owner' ]   
    [ , [ @source_object = ] 'source_object' ]   
    [ , [ @artid = ] article_ID  OUTPUT ]   
    [ , [ @auto_identity_range = ] 'auto_identity_range' ]   
    [ , [ @pub_identity_range = ] pub_identity_range ]   
    [ , [ @identity_range = ] identity_range ]   
    [ , [ @threshold = ] threshold ]   
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @use_default_datatypes = ] use_default_datatypes  
    [ , [ @identityrangemanagementoption = ] identityrangemanagementoption ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @fire_triggers_on_snapshot = ] 'fire_triggers_on_snapshot' ]   
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@publication =** ] **'***pubblicazione***'**  
 Nome della pubblicazione in cui è contenuto l'articolo. Deve essere un nome univoco all'interno del database. *pubblicazione* è **sysname**, non prevede alcun valore predefinito.  
  
 [  **@article =** ] **'***articolo***'**  
 Nome dell'articolo. Deve essere un nome univoco all'interno della pubblicazione. *articolo* è **sysname**, non prevede alcun valore predefinito.  
  
 [  **@source_table =** ] **'***source_table***'**  
 Questo parametro è deprecato. Utilizzare *source_object* invece.  
  
 *Questo parametro non è supportato per server di pubblicazione Oracle.*  
  
 [  **@destination_table =** ] **'***destination_table***'**  
 È il nome della tabella di destinazione (sottoscrizione), se diverso da *source_table*o la stored procedure. *destination_table* è **sysname**, il valore predefinito è NULL, vale a dire che *source_table* è uguale a *destination_table**.*  
  
 [  **@vertical_partition =** ] **'***vertical_partition***'**  
 Abilita e disabilita l'applicazione di filtri alle colonne in un articolo di tabella. *vertical_partition* è **nchar(5)**, con un valore predefinito è FALSE.  
  
 **false** non indica è presente alcun filtro verticale e pubblica tutte le colonne.  
  
 **true** Cancella tutte le colonne ad eccezione della chiave primaria dichiarata, le colonne che ammettono valori null non prevede alcun valore predefinito e colonne di chiave univoca. Le colonne vengono aggiunte utilizzando [sp_articlecolumn](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md).  
  
 [  **@type =** ] **'***tipo***'**  
 Tipo di articolo. *tipo* è **sysname**, e può essere uno dei valori seguenti.  
  
|Valore|Description|  
|-----------|-----------------|  
|**aggregazione solo schema**|Funzione di aggregazione con solo schema.|  
|**Func schema solo**|Funzione con solo schema.|  
|**logbased vista indicizzata**|Articolo di vista indicizzata basato su log. Questa proprietà non è supportata per server di pubblicazione Oracle. Per questo tipo di articolo non è necessario pubblicare separatamente la tabella di base.|  
|**vista indicizzata logbased manualboth**|Articolo di vista indicizzata basato su log con filtro manuale e vista manuale. Questa opzione è necessario specificare sia *sync_object* e *filtro* parametri. Per questo tipo di articolo non è necessario pubblicare separatamente la tabella di base. Questa proprietà non è supportata per server di pubblicazione Oracle.|  
|**vista indicizzata logbased manualfilter**|Articolo di vista indicizzata basato su log con filtro manuale. Questa opzione è necessario specificare sia *sync_object* e *filtro* parametri. Per questo tipo di articolo non è necessario pubblicare separatamente la tabella di base. Questa proprietà non è supportata per server di pubblicazione Oracle.|  
|**vista indicizzata logbased manualview**|Articolo di vista indicizzata basato su log con vista manuale. Questa opzione è necessario specificare il *sync_object* parametro. Per questo tipo di articolo non è necessario pubblicare separatamente la tabella di base. Questa proprietà non è supportata per server di pubblicazione Oracle.|  
|**solo schema della vista indicizzata**|Vista indicizzata con solo schema. Per questo tipo di articolo è necessario pubblicare anche la tabella di base.|  
|**logbased** (impostazione predefinita)|Articolo basato su un log.|  
|**logbased manualboth**|Articolo basato su log con filtro manuale e vista manuale. Questa opzione è necessario specificare sia *sync_object* e *filtro* parametri. Questa proprietà non è supportata per server di pubblicazione Oracle.|  
|**logbased manualfilter**|Articolo basato su log con filtro manuale. Questa opzione è necessario specificare sia *sync_object* e *filtro* parametri. Questa proprietà non è supportata per server di pubblicazione Oracle.|  
|**logbased manualview**|Articolo basato su log con vista manuale. Questa opzione è necessario specificare il *sync_object* parametro. Questa proprietà non è supportata per server di pubblicazione Oracle.|  
|**proc exec**|Replica l'esecuzione della stored procedure in tutti i Sottoscrittori dell'articolo. Questa proprietà non è supportata per server di pubblicazione Oracle. È consigliabile utilizzare l'opzione **serializable proc exec** anziché **proc exec**. Per ulteriori informazioni, vedere la sezione "Tipi di Stored Procedure articoli di esecuzione" in [Publishing Stored Procedure Execution nella replica transazionale](../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md). Non disponibile se l'acquisizione dati delle modifiche è abilitata.|  
|**proc schema solo**|Procedura con solo schema. Questa proprietà non è supportata per server di pubblicazione Oracle.|  
|**serializable proc exec**|Replica l'esecuzione della stored procedure solo se viene eseguita nel contesto di una transazione serializzabile. Questa proprietà non è supportata per server di pubblicazione Oracle.<br /><br /> La procedura deve essere eseguita all'interno di una transazione esplicita per l'esecuzione della procedura da replicare.|  
|**solo schema della vista**|Vista con solo schema. Questa proprietà non è supportata per server di pubblicazione Oracle. Se si usa questa opzione, è necessario pubblicare anche la tabella di base.|  
  
 [  **@filter =** ] **'***filtro***'**  
 Stored procedure creata con l'opzione FOR REPLICATION usata per filtrare la tabella in orizzontale. *filtro* è **nvarchar (386)**, con un valore predefinito è NULL. [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) e [sp_articlefilter](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md) devono essere eseguite manualmente per creare la vista e stored procedure di filtro. Se diverso da NULL, la procedura di filtro non viene creata, in quanto si presume che venga creata manualmente.  
  
 [  **@sync_object =** ] **'***sync_object***'**  
 Nome della tabella o vista usata per la creazione del file di dati che rappresenta lo snapshot per l'articolo. *sync_object* è **nvarchar (386)**, con un valore predefinito è NULL. Se NULL, [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) viene chiamato per creare automaticamente la vista utilizzata per generare il file di output. Questo errore si verifica dopo aver aggiunto tutte le colonne con [sp_articlecolumn](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md). Se il valore è diverso da NULL, non viene creata alcuna vista, in quanto si presume che venga creata manualmente.  
  
 [  **@ins_cmd =** ] **'***ins_cmd***'**  
 Tipo di comando di replica usato per replicare le operazioni di inserimento per l'articolo. *ins_cmd* è **nvarchar (255)**, e può essere uno dei valori seguenti.  
  
|Valore|Description|  
|-----------|-----------------|  
|**NONE**|Non viene eseguita alcuna azione.|  
|**CALL sp_Msins _**<br /> ***tabella*** (impostazione predefinita)<br /><br /> oppure<br /><br /> **CHIAMARE custom_stored_procedure_name**|Chiama una stored procedure per l'esecuzione nel Sottoscrittore. Per utilizzare questo metodo di replica, utilizzare *schema_option* per specificare la creazione automatica della stored procedure oppure creare la stored procedure specificata nel database di destinazione di ogni sottoscrittore dell'articolo. *custom_stored_procedure* è il nome di una stored procedure creata dall'utente. **sp_Msins _*tabella** * contiene il nome della tabella di destinazione anziché il *Table* fa parte del parametro. Quando *destination_owner* è specificato, viene anteposto al nome della tabella di destinazione. Ad esempio, per il **ProductCategory** tabella di proprietà di **produzione** schema nel Sottoscrittore, il parametro deve essere `CALL sp_MSins_ProductionProductCategory`. Per un articolo in una topologia di replica peer-to-peer, *Table* viene aggiunto con un valore GUID. Specifica di *custom_stored_procedure* non è supportata per Sottoscrittori aggiornabili.|  
|**SQL** o NULL|Replica un'istruzione INSERT. All'istruzione INSERT vengono passati i valori per tutte le colonne pubblicate nell'articolo. Questo comando viene replicato quando si eseguono operazioni di inserimento:<br /><br /> `INSERT INTO <table name> VALUES (c1value, c2value, c3value, ..., cnvalue)`|  
  
 Per altre informazioni, vedere [Specificare la modalità di propagazione delle modifiche per gli articoli transazionali](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
 [  **@del_cmd =**] **'***del_cmd***'**  
 Tipo di comando di replica usato per replicare le operazioni di eliminazione per l'articolo. *del_cmd* è **nvarchar (255)**, e può essere uno dei valori seguenti.  
  
|Valore|Description|  
|-----------|-----------------|  
|**NONE**|Non viene eseguita alcuna azione.|  
|**CALLsp_MSdel_**<br /> ***tabella*** (impostazione predefinita)<br /><br /> oppure<br /><br /> **CHIAMARE custom_stored_procedure_name**|Chiama una stored procedure per l'esecuzione nel Sottoscrittore. Per utilizzare questo metodo di replica, utilizzare *schema_option* per specificare la creazione automatica della stored procedure oppure creare la stored procedure specificata nel database di destinazione di ogni sottoscrittore dell'articolo. *custom_stored_procedure* è il nome di una stored procedure creata dall'utente. **sp_Msdel _*tabella** * contiene il nome della tabella di destinazione anziché il *Table* fa parte del parametro. Quando *destination_owner* è specificato, viene anteposto al nome della tabella di destinazione. Ad esempio, per il **ProductCategory** tabella di proprietà di **produzione** schema nel Sottoscrittore, il parametro deve essere `CALL sp_MSdel_ProductionProductCategory`. Per un articolo in una topologia di replica peer-to-peer, *Table* viene aggiunto con un valore GUID. Specifica di *custom_stored_procedure* non è supportata per Sottoscrittori aggiornabili.|  
|**Sp_Msdel _ XCALL**<br /> ***table***<br /><br /> oppure<br /><br /> **Custom_stored_procedure_name XCALL**|Chiama una stored procedure che accetta i parametri di stile XCALL. Per utilizzare questo metodo di replica, utilizzare *schema_option* per specificare la creazione automatica della stored procedure oppure creare la stored procedure specificata nel database di destinazione di ogni sottoscrittore dell'articolo. L'impostazione di una stored procedure creata dall'utente non è consentita per l'aggiornamento dei Sottoscrittori.|  
|**SQL** o NULL|Replica un'istruzione DELETE. All'istruzione DELETE vengono passati tutti i valori relativi alle colonne chiave primaria. Questo comando viene replicato quando si eseguono operazioni di eliminazione:<br /><br /> `DELETE FROM <table name> WHERE pkc1 = pkc1value AND pkc2 = pkc2value AND pkcn = pkcnvalue`|  
  
 Per altre informazioni, vedere [Specificare la modalità di propagazione delle modifiche per gli articoli transazionali](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
 [  **@upd_cmd =**] **'***upd_cmd***'**  
 Tipo di comando di replica usato per replicare le operazioni di aggiornamento per l'articolo. *upd_cmd* è **nvarchar (255)**, e può essere uno dei valori seguenti.  
  
|Valore|Description|  
|-----------|-----------------|  
|**NONE**|Non viene eseguita alcuna azione.|  
|**Sp_Msupd _ chiamate**<br /> ***table***<br /><br /> oppure<br /><br /> **CHIAMARE custom_stored_procedure_name**|Chiama una stored procedure per l'esecuzione nel Sottoscrittore. Per utilizzare questo metodo di replica, utilizzare *schema_option* per specificare la creazione automatica della stored procedure oppure creare la stored procedure specificata nel database di destinazione di ogni sottoscrittore dell'articolo.|  
|**Sp_Msupd _ MCALL**<br /> ***table***<br /><br /> oppure<br /><br /> **Custom_stored_procedure_name MCALL**|Chiama una stored procedure che accetta i parametri di stile MCALL. Per utilizzare questo metodo di replica, utilizzare *schema_option* per specificare la creazione automatica della stored procedure oppure creare la stored procedure specificata nel database di destinazione di ogni sottoscrittore dell'articolo. *custom_stored_procedure* è il nome di una stored procedure creata dall'utente. **sp_Msupd _*tabella** * contiene il nome della tabella di destinazione anziché il *Table* fa parte del parametro. Quando *destination_owner* è specificato, viene anteposto al nome della tabella di destinazione. Ad esempio, per il **ProductCategory** tabella di proprietà di **produzione** schema nel Sottoscrittore, il parametro deve essere `MCALL sp_MSupd_ProductionProductCategory`. Per un articolo in una topologia di replica peer-to-peer, *Table* viene aggiunto con un valore GUID. L'impostazione di una stored procedure creata dall'utente non è consentita per l'aggiornamento dei Sottoscrittori.|  
|**Sp_Msupd _ SCALL**<br /> ***tabella*** (impostazione predefinita)<br /><br /> oppure<br /><br /> **Custom_stored_procedure_name SCALL**|Chiama una stored procedure che accetta i parametri di stile SCALL. Per utilizzare questo metodo di replica, utilizzare *schema_option* per specificare la creazione automatica della stored procedure oppure creare la stored procedure specificata nel database di destinazione di ogni sottoscrittore dell'articolo. *custom_stored_procedure* è il nome di una stored procedure creata dall'utente. **sp_Msupd _*tabella** * contiene il nome della tabella di destinazione anziché il *Table* fa parte del parametro. Quando *destination_owner* è specificato, viene anteposto al nome della tabella di destinazione. Ad esempio, per il **ProductCategory** tabella di proprietà di **produzione** schema nel Sottoscrittore, il parametro deve essere `SCALL sp_MSupd_ProductionProductCategory`. Per un articolo in una topologia di replica peer-to-peer, *Table* viene aggiunto con un valore GUID. L'impostazione di una stored procedure creata dall'utente non è consentita per l'aggiornamento dei Sottoscrittori.|  
|**Sp_Msupd _ XCALL**<br /> ***table***<br /><br /> oppure<br /><br /> **Custom_stored_procedure_name XCALL**|Chiama una stored procedure che accetta i parametri di stile XCALL. Per utilizzare questo metodo di replica, utilizzare *schema_option* per specificare la creazione automatica della stored procedure oppure creare la stored procedure specificata nel database di destinazione di ogni sottoscrittore dell'articolo. L'impostazione di una stored procedure creata dall'utente non è consentita per l'aggiornamento dei Sottoscrittori.|  
|**SQL** o NULL|Replica un'istruzione UPDATE. All'istruzione UPDATE vengono passati tutti i valori delle colonne e i valori delle colonne chiave primaria. Questo comando viene replicato quando si eseguono operazioni di aggiornamento:<br /><br /> `UPDATE <table name> SET c1 = c1value, SET c2 = c2value, SET cn = cnvalue WHERE pkc1 = pkc1value AND pkc2 = pkc2value AND pkcn = pkcnvalue`|  
  
> [!NOTE]  
>  Nel Sottoscrittore vengono propagate quantità di dati diverse a seconda che si utilizzi la sintassi CALL, MCALL o XCALL. Tramite la sintassi CALL vengono passati tutti i valori di tutte le colonne inserite ed eliminate, tramite la sintassi di SCALL vengono passati solo i valori delle colonne modificate, mentre tramite la sintassi XCALL vengono passati i valori di tutte le colonne, modificate o meno, insieme al valore precedente della colonna. Per altre informazioni, vedere [Specificare la modalità di propagazione delle modifiche per gli articoli transazionali](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
 [  **@creation_script =**] **'***creation_script***'**  
 Percorso e nome di uno script facoltativo dello schema dell'articolo usato per creare l'articolo nel database di sottoscrizione. *creation_script* è **nvarchar (255)**, con un valore predefinito è NULL.  
  
 [  **@description =**] **'***descrizione***'**  
 Voce descrittiva per l'articolo. *Descrizione* è **nvarchar (255)**, con un valore predefinito è NULL.  
  
 [  **@pre_creation_cmd =**] **'***pre_creation_cmd***'**  
 Specifica l'azione eseguita dal sistema se nel Sottoscrittore viene rilevato un oggetto esistente con lo stesso nome durante l'applicazione dello snapshot per l'articolo. *pre_creation_cmd* è **nvarchar (10)**, e può essere uno dei valori seguenti.  
  
|Valore|Description|  
|-----------|-----------------|  
|**Nessuno**|Non utilizza alcun comando.|  
|**eliminare**|Elimina i dati dalla tabella di destinazione prima di applicare lo snapshot. Se l'articolo è filtrato in modo orizzontale, vengono eliminati solo i dati nelle colonne specificate dalla clausola di filtro. Valore non supportato per i server di pubblicazione Oracle quando è definito un filtro orizzontale.|  
|**eliminare** (impostazione predefinita)|Rimuove la tabella di destinazione.|  
|**troncare**|Tronca la tabella di destinazione. Questo valore non è valido per i Sottoscrittori ODBC o OLE DB.|  
  
 [  **@filter_clause=**] **'***filter_clause***'**  
 Clausola di restrizione (WHERE) che definisce un filtro orizzontale. Quando si specifica la clausola di restrizione, omettere la parola chiave WHERE. *filter_clause* è **ntext**, con un valore predefinito è NULL. Per altre informazioni, vedere [Filtrare i dati pubblicati](../../relational-databases/replication/publish/filter-published-data.md).  
  
 [  **@schema_option =**] *schema_option*  
 Maschera di bit dell'opzione di generazione dello schema per l'articolo specificato. *schema_option* è **Binary (8)**e può essere il [| (OR bit per bit) ](../../t-sql/language-elements/bitwise-or-transact-sql.md) prodotto di uno o più dei valori seguenti:  
  
> [!NOTE]  
>  Se è NULL, il sistema genera automaticamente un'opzione di schema valida per l'articolo in base alle proprietà dell'articolo. Il **opzioni predefinite dello Schema** tabella nella sezione Osservazioni vengono indicati i valori verranno scelti in base alla combinazione del tipo di articolo e il tipo di replica.  
  
|Valore|Description|  
|-----------|-----------------|  
|**0x00**|Disabilita la creazione di script tramite l'agente Snapshot e utilizza *creation_script*.|  
|**0x01**|Genera lo script per la creazione di oggetti (CREATE TABLE, CREATE PROCEDURE e così via). Corrisponde al valore predefinito per gli articoli di stored procedure.|  
|**0x02**|Genera le stored procedure che propagano le eventuali modifiche per l'articolo.|  
|**0x04**|Gli script per le colonne Identity vengono creati tramite la proprietà IDENTITY.|  
|**0x08**|Replicare **timestamp** colonne. Se non impostato, **timestamp** colonne vengono replicate come **binario**.|  
|**0x10**|Genera un indice cluster corrispondente. Anche se questa opzione non viene impostata, se sono già definiti in una tabella pubblicata, gli indici correlati alle chiavi primarie e i vincoli UNIQUE vengono generati.|  
|**0x20**|Converte i tipi di dati definiti dall'utente (UDT) in tipi di dati di base nel Sottoscrittore. Questa opzione non può essere usata quando è presente un vincolo CHECK o DEFAULT su una colonna UDT, se una colonna UDT è inclusa nella chiave primaria o se una colonna calcolata fa riferimento a una colonna UDT. *Non supportato per il server di pubblicazione Oracle*.|  
|**0x40**|Genera indici non cluster corrispondenti. Anche se questa opzione non viene impostata, se sono già definiti in una tabella pubblicata, gli indici correlati alle chiavi primarie e i vincoli UNIQUE vengono generati.|  
|**0x80**|Replica i vincoli PRIMARY KEY. Vengono inoltre replicati tutti gli indici correlati al vincolo, anche se le opzioni **0x10** e **0x40** non sono abilitati.|  
|**0x100**|Replica gli eventuali trigger dell'utente di un articolo di tabella. *Non supportato per il server di pubblicazione Oracle*.|  
|**0x200**|Replica i vincoli FOREIGN KEY. Se la tabella con riferimenti non fa parte di una pubblicazione, tutti i vincoli di chiave esterna su una tabella pubblicata non vengono replicati. *Non supportato per il server di pubblicazione Oracle*.|  
|**0x400**|Replica i vincoli CHECK. *Non supportato per il server di pubblicazione Oracle*.|  
|**0x800**|Replica i valori predefiniti. *Non supportato per il server di pubblicazione Oracle*.|  
|**0x1000**|Replica le regole di confronto a livello di colonna.<br /><br /> **Nota:** questa opzione deve essere impostata per i server di pubblicazione Oracle abilitare i confronti tra maiuscole e minuscole.|  
|**0x2000**|Replica le proprietà estese associate all'oggetto di origine dell'articolo pubblicato. *Non supportato per il server di pubblicazione Oracle*.|  
|**0x4000**|Replica i vincoli UNIQUE. Vengono inoltre replicati tutti gli indici correlati al vincolo, anche se le opzioni **0x10** e **0x40** non sono abilitati.|  
|**0x8000**|Questa opzione non è valida per i server di pubblicazione [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
|**0x10000.**|Replica i vincoli CHECK come NOT FOR REPLICATION in modo che i vincoli non vengono imposti durante la sincronizzazione.|  
|**0x20000**|Replica i vincoli FOREIGN KEY come NOT FOR REPLICATION in modo che i vincoli non vengono imposti durante la sincronizzazione.|  
|**0x40000**|Replica i filegroup associati a una tabella o un indice partizionato.|  
|**0x80000**|Replica lo schema di partizione per una tabella partizionata.|  
|**0x100000**|Replica lo schema di partizione per un indice partizionato.|  
|**0x200000**|Replica le statistiche della tabella.|  
|**0x400000**|Associazioni predefinite|  
|**0x800000**|Associazioni regola|  
|**0x1000000**|Indice full-text|  
|**0x2000000**|Raccolte di XML schema associata a **xml** colonne non vengono replicate.|  
|**0x4000000**|Replica gli indici su **xml** colonne.|  
|**0x8000000**|Crea gli schemi non ancora presenti nel Sottoscrittore.|  
|**0x10000000**|Converte **xml** colonne **ntext** nel Sottoscrittore.|  
|**0x20000000**|Tipi di dati dell'oggetto converte di grandi dimensioni (**nvarchar (max)**, **varchar (max)**, e **varbinary (max)**) introdotto in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ai tipi di dati che sono supportati in [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)].|  
|**0x40000000**|Replica le autorizzazioni.|  
|**0x80000000**|Tenta di eliminare le dipendenze da tutti gli oggetti che non fanno parte della pubblicazione.|  
|**0x100000000**|Utilizzare questa opzione per replicare l'attributo FILESTREAM se viene specificato in **varbinary (max)** colonne. Non specificare questa opzione se si stanno replicando tabelle nei Sottoscrittori [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. La replica di tabelle con colonne FILESTREAM in [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] sottoscrittori non è supportata, indipendentemente dall'impostazione di questa opzione dello schema.<br /><br /> Vedere l'opzione correlata **0x800000000**.|  
|**0x200000000**|Converte i tipi di dati data e ora (**data**, **ora**, **datetimeoffset**, e **datetime2**) introdotto in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ai dati tipi supportati nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**0x400000000**|Replica l'opzione di compressione per dati e indici. Per altre informazioni, vedere [Data Compression](../../relational-databases/data-compression/data-compression.md).|  
|**0x800000000**|Impostare questa opzione per archiviare i dati FILESTREAM nel relativo filegroup nel Sottoscrittore. Se questa opzione non è impostata, i dati FILESTREAM vengono archiviati nel filegroup predefinito. Tramite la replica non vengono creati filegroup, pertanto, se si imposta questa opzione, è necessario creare il filegroup prima di applicare lo snapshot nel Sottoscrittore. Per ulteriori informazioni su come creare gli oggetti prima di applicare lo snapshot, vedere [eseguire script prima e dopo l'applicazione dello Snapshot](../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md).<br /><br /> Vedere l'opzione correlata **0x100000000**.|  
|**0x1000000000**|Converte i tipi common language runtime (CLR) definito dall'utente (UDT) che sono maggiori di 8000 byte a **varbinary (max)** in modo che le colonne di tipo definito dall'utente possono essere replicate nei Sottoscrittori che eseguono [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
|**0x2000000000**|Converte il **hierarchyid** tipo di dati **varbinary (max)** in modo che le colonne di tipo **hierarchyid** possano essere replicate nei Sottoscrittori che eseguono [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Per ulteriori informazioni su come usare **hierarchyid** colonne nelle tabelle replicate, vedere [hierarchyid &#40; Transact-SQL &#41; ](../../t-sql/data-types/hierarchyid-data-type-method-reference.md).|  
|**0x4000000000**|Replica gli eventuali indici filtrati sulla tabella. Per ulteriori informazioni sugli indici filtrati, vedere [Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md).|  
|**0x8000000000**|Converte il **geography** e **geometry** tipi di dati di **varbinary (max)** in modo che le colonne di questi tipi possono essere replicate nei Sottoscrittori che eseguono [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
|**0x10000000000**|Replica gli indici su colonne di tipo **geography** e **geometry**.|  
|**0x20000000000**|Replica l'attributo SPARSE per le colonne. Per ulteriori informazioni su questo attributo, vedere [utilizzare le colonne di tipo Sparse](../../relational-databases/tables/use-sparse-columns.md).|  
|**0x40000000000**|Attivazione di scripting per l'agente snapshot per creare una tabella con ottimizzazione per la memoria nel server di sottoscrizione.|  
|**0x80000000000**|Converte un indice cluster in indice non cluster per gli articoli con ottimizzazione per la memoria.|  
|**0x400000000000**|Consente di replicare tutti gli indici columnstore non cluster sulle tabelle|  
|**0x800000000000**|Consente di replicare tutti gli indici columnstore non cluster flitered sulle tabelle.|  
|NULL|La replica imposta automaticamente *schema_option* su un valore predefinito, il cui valore dipende da altre proprietà dell'articolo. Nella tabella "Opzioni predefinite dello schema" riportata nella sezione Osservazioni vengono descritte le opzioni predefinite dello schema in base a tipo di articolo e tipo di replica.<br /><br /> Per impostazione predefinita non[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pubblicazioni è **0x050D3**.|  
  
 Non tutti i *schema_option* valori validi per ogni tipo di replica e il tipo di articolo. Il **opzioni di Schema valide** tabella nella sezione Osservazioni vengono illustrate le opzioni di schema valide che possono essere scelti in base alla combinazione del tipo di articolo e il tipo di replica.  
  
 [  **@destination_owner =**] **'***destination_owner***'**  
 Nome del proprietario dell'oggetto di destinazione. *destination_owner* è **sysname**, con un valore predefinito è NULL. Quando *destination_owner* non viene specificato, il proprietario viene impostato automaticamente in base alle regole seguenti:  
  
|Condizione|Proprietario oggetto di destinazione|  
|---------------|------------------------------|  
|La pubblicazione utilizza la copia bulk in modalità nativa per generare lo snapshot iniziale, che supporta solo Sottoscrittori [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|Per impostazione predefinita il valore di *source_owner*.|  
|Pubblicazione da un server di pubblicazione non [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|Corrispondente per impostazione predefinita al proprietario del database di destinazione.|  
|La pubblicazione utilizza la copia bulk in modalità carattere per generare lo snapshot iniziale, che supporta Sottoscrittori non [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|Non assegnato.|  
  
 Per supportare non[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sottoscrittori, *destination_owner* deve essere NULL.  
  
 [  **@status=**] *stato*  
 Specifica se l'articolo è attivo e offre ulteriori opzioni per la propagazione delle modifiche. *stato* è **tinyint**e può essere il [| (OR bit per bit) ](../../t-sql/language-elements/bitwise-or-transact-sql.md) prodotto di uno o più dei valori seguenti.  
  
|Valore|Descrizione|  
|-----------|-----------------|  
|**1**|L'articolo è attivo.|  
|**8**|Include il nome della colonna nelle istruzioni INSERT.|  
|**16** (impostazione predefinita)|Utilizza istruzioni con parametri.|  
|**24**|Include il nome della colonna nelle istruzioni INSERT e utilizza istruzioni con parametri.|  
|**64**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
 Ad esempio, un articolo attivo che utilizza istruzioni con parametri includerà il valore 17 in questa colonna. Il valore **0** significa che l'articolo è inattivo e proprietà aggiuntive non definite.  
  
 [  **@source_owner =**] **'***source_owner***'**  
 Proprietario dell'oggetto di origine. *source_owner* è **sysname**, con un valore predefinito è NULL. *source_owner* deve essere specificato per i server di pubblicazione Oracle.  
  
 [  **@sync_object_owner =**] **'***sync_object_owner***'**  
 Proprietario della vista che definisce l'articolo pubblicato. *sync_object_owner* è **sysname**, con un valore predefinito è NULL.  
  
 [  **@filter_owner =**] **'***filter_owner***'**  
 Proprietario del filtro. *filter_owner* è **sysname**, con un valore predefinito è NULL.  
  
 [  **@source_object =**] **'***source_object***'**  
 Oggetto di database da pubblicare. *source_object* è **sysname**, con un valore predefinito è NULL. Se *source_table* è NULL, *source_object* non può essere NULL. *source_object* deve essere usato al posto della *source_table*. Per ulteriori informazioni sui tipi di oggetti che possono essere pubblicati utilizzando la replica transazionale o snapshot, vedere [pubblicare dati e oggetti di Database](../../relational-databases/replication/publish/publish-data-and-database-objects.md).  
  
 [  **@artid =** ] *article_ID* **OUTPUT**  
 ID del nuovo articolo. *article_id* è **int** con valore predefinito è NULL che è un parametro di OUTPUT.  
  
 [  **@auto_identity_range =** ] **'***auto_identity_range***'**  
 Abilita e disabilita la gestione automatica degli intervalli di valori Identity in una pubblicazione al momento della creazione. *auto_identity_range* è **nvarchar (5)**, e può essere uno dei valori seguenti:  
  
|Valore|Description|  
|-----------|-----------------|  
|**true**|Abilita la gestione automatica degli intervalli di valori Identity.|  
|**false**|Viene disabilitata la gestione automatica degli intervalli di valori Identity.|  
|NULL(default)|Gestione degli intervalli di identità è l'impostazione *identityrangemanagementoption*.|  
  
> [!NOTE]  
>  *auto_identity_range* è stata deprecata e viene fornito solo per la compatibilità. È consigliabile utilizzare *identityrangemanagementoption* per specificare opzioni di gestione di intervalli di valori identity. Per altre informazioni, vedere [Replicare colonne Identity](../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
 [  **@pub_identity_range =** ] *pub_identity_range*  
 Controlla le dimensioni dell'intervallo nel server di pubblicazione se l'articolo include *identityrangemanagementoption* impostato su **auto** o *auto_identity_range* impostato su **true** . *pub_identity_range* è **bigint**, con un valore predefinito è NULL. *Non supportato per il server di pubblicazione Oracle*.  
  
 [  **@identity_range =** ] *identity_range*  
 Controlla le dimensioni dell'intervallo nel Sottoscrittore se l'articolo include *identityrangemanagementoption* impostato su **auto** o *auto_identity_range* impostato su **true** . *identity_range* è **bigint**, con un valore predefinito è NULL. Utilizzato quando *auto_identity_range* è impostato su **true**. *Non supportato per il server di pubblicazione Oracle*.  
  
 [  **@threshold =** ] *soglia*  
 Valore percentuale che determina quando l'agente di distribuzione assegna un nuovo intervallo di valori Identity. Quando la percentuale di valori specificato in *soglia* è utilizzato, l'agente di distribuzione crea un nuovo intervallo di valori identity. *soglia* è **bigint**, con un valore predefinito è NULL. Utilizzato quando *identityrangemanagementoption* è impostato su **auto** o *auto_identity_range* è impostato su **true**. *Non supportato per il server di pubblicazione Oracle*.  
  
 [  **@force_invalidate_snapshot =** ] *force_invalidate_snapshot*  
 Segnala che l'azione eseguita da questa stored procedure potrebbe invalidare uno snapshot esistente. *force_invalidate_snapshot* è un **bit**, con un valore predefinito è 0.  
  
 **0** specifica che aggiunta di un articolo non invalidano lo snapshot. Se la stored procedure rileva che la modifica richiede un nuovo snapshot, viene generato un errore e non viene apportata alcuna modifica.  
  
 **1** specifica che l'aggiunta di un articolo potrebbe invalidare lo snapshot potrebbe non essere valido e se esistono sottoscrizioni che richiedono un nuovo snapshot, fornisce l'autorizzazione per lo snapshot esistente deve essere contrassegnato come obsoleto e un nuovo snapshot da generare.  
  
 [  **@use_default_datatypes =** ] *use_default_datatypes*  
 Indica se vengono usati i mapping predefiniti dei tipi di dati delle colonne quando si pubblica un articolo da un server di pubblicazione Oracle. *use_default_datatypes* è di tipo bit e il valore predefinito è 1.  
  
 **1** = la colonna di articolo predefiniti vengono utilizzati i mapping. Mapping dei tipi di dati predefiniti possono essere visualizzati eseguendo [sp_getdefaultdatatypemapping](../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md).  
  
 **0** = vengono definiti mapping della colonna personalizzato degli articoli e pertanto [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) non viene chiamato da **sp_addarticle**.  
  
 Quando *use_default_datatypes* è impostato su **0**, è necessario eseguire [sp_changearticlecolumndatatype](../../relational-databases/system-stored-procedures/sp-changearticlecolumndatatype-transact-sql.md) una volta per ogni mapping di colonna viene modificata dal valore predefinito. Dopo aver definiti tutti i mapping di colonna personalizzata, è necessario eseguire [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md).  
  
> [!NOTE]  
>  Questo parametro deve essere usato solo per i server di pubblicazione Oracle. Impostazione *use_default_datatypes* a **0** per un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server di pubblicazione genera un errore.  
  
 [  **@identityrangemanagementoption =** ] *identityrangemanagementoption*  
 Specifica la modalità di gestione degli intervalli di valori Identity per l'articolo. *identityrangemanagementoption* è **nvarchar (10)**, e può essere uno dei valori seguenti.  
  
|Valore|Description|  
|-----------|-----------------|  
|**Nessuno**|La replica non esegue la gestione degli intervalli dei valori Identity espliciti. Questa opzione è consigliabile solo per compatibilità con versioni precedenti di SQL Server. Non consentito per la replica peer-to-peer.|  
|**Manuale**|Contrassegna la colonna Identity con NOT FOR REPLICATION per consentire la gestione manuale degli intervalli di valori Identity.|  
|**Automatico**|Imposta la gestione automatica degli intervalli di valori Identity.|  
|NULL(default)|Per impostazione predefinita **Nessuno** quando il valore di *auto_identity_range* non **true**. Per impostazione predefinita **manuale** predefinita una topologia peer-to-peer (*auto_identity_range* viene ignorato).|  
  
 Per garantire la compatibilità con le versioni precedenti, quando il valore di *identityrangemanagementoption* è NULL, il valore di *auto_identity_range* è selezionata. Tuttavia, quando il valore di *identityrangemanagementoption* non è NULL, il valore di *auto_identity_range* viene ignorato.  
  
 Per altre informazioni, vedere [Replicare colonne Identity](../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
 [  **@publisher =** ] **'***publisher***'**  
 Specifica un server di pubblicazione non [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *server di pubblicazione* è **sysname**, con un valore predefinito è NULL.  
  
> [!NOTE]  
>  *server di pubblicazione* non deve essere utilizzato quando si aggiunge un articolo a una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server di pubblicazione.  
  
 [  **@fire_triggers_on_snapshot =** ] **'***fire_triggers_on_snapshot***'**  
 Indica se i trigger utente replicati vengono eseguiti quando viene applicato lo snapshot iniziale. *fire_triggers_on_snapshot* è **nvarchar (5)**, con un valore predefinito è FALSE. **true** significa che i trigger utente su una tabella replicata vengono eseguiti quando viene applicato lo snapshot. Affinché i trigger di replica, il valore di maschera di bit di *schema_option* deve includere il valore **0x100**.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_addarticle** viene utilizzata nella replica snapshot o transazionale.  
  
 Per impostazione predefinita, vengono escluse dalla pubblicazione le colonne della tabella di origine con tipo di dati non supportato dalla replica. Se si desidera pubblicare tale colonna, è necessario eseguire [sp_articlecolumn](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) per aggiungere la colonna.  
  
 Per l'aggiunta di un articolo a una pubblicazione che supporta la replica transazionale peer-to-peer sono valide le restrizioni seguenti:  
  
-   È necessario specificare istruzioni con parametri per tutti gli articoli basati su log. È necessario includere **16** nel *stato* valore.  
  
-   Il nome e il proprietario della tabella di destinazione devono corrispondere a quelli della tabella di origine.  
  
-   Non è possibile filtrare l'articolo in modo orizzontale o verticale.  
  
-   La gestione automatica degli intervalli di valori Identity non è supportata. È necessario specificare il valore manual per *identityrangemanagementoption*.  
  
-   Se un **timestamp** esiste una colonna nella tabella, è necessario includere 0x08 in *schema_option* per replicare la colonna come **timestamp**.  
  
-   Il valore **SQL** non può essere specificato per *ins_cmd*, *upd_cmd*, e *del_cmd*.  
  
 Per altre informazioni, vedere [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).  
  
 Quando si pubblicano gli oggetti, nei Sottoscrittori vengono copiate le relative definizioni. Per la pubblicazione di un oggetto di database che dipende da altri oggetti, è necessario pubblicare tutti gli oggetti a cui fa riferimento. Se ad esempio si pubblica una vista che dipende da una tabella, sarà necessario pubblicare anche la tabella.  
  
 Se *vertical_partition* è impostato su **true**, **sp_addarticle** posticipa la creazione della vista fino alla [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) viene chiamato (dopo l'ultimo [sp_articlecolumn](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) viene aggiunto).  
  
 Se la pubblicazione consente l'aggiornamento di sottoscrizioni e la tabella pubblicata non dispone di un **uniqueidentifier** colonna **sp_addarticle** aggiunge un **uniqueidentifier** colonna alla tabella automaticamente.  
  
 Durante la replica a un sottoscrittore che non è un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (replica eterogenea), solo [!INCLUDE[tsql](../../includes/tsql-md.md)] sono supportate le istruzioni per **inserire**, **aggiornamento**e **Eliminare** comandi.  
  
 Quando l'agente di lettura log è in esecuzione, l'aggiunta di un articolo a una pubblicazione peer-to-peer può causare un deadlock tra l'agente di lettura log e il processo tramite cui viene aggiunto l'articolo. Per evitare questo problema, prima di aggiungere un articolo a una pubblicazione peer-to-peer usare Monitoraggio replica per arrestare l'agente di lettura log sul nodo in cui si aggiunge l'articolo. Riavviare l'agente di lettura log dopo aver aggiunto l'articolo.  
  
 Quando si imposta `@del_cmd = 'NONE'` o `@ins_cmd = 'NONE'`, la propagazione di **aggiornare** comandi potrebbero essere interessati anche non inviando i comandi quando si verifica un aggiornamento associato. Per aggiornamento associato si intende un tipo di istruzione UPDATE dal server di pubblicazione che replica come coppia DELETE/INSERT nel sottoscrittore.  
  
## <a name="default-schema-options"></a>Opzioni predefinite dello schema  
 La tabella seguente descrive il valore predefinito impostato dalla replica se *schema_options* non è specificato dall'utente, in cui questo valore dipende dal tipo di replica (indicato nella parte superiore) e il tipo di articolo (indicato nella prima colonna).  
  
|Tipo di articolo|Tipo di replica||  
|------------------|----------------------|------|  
||Transazionale|Snapshot|  
|**aggregazione solo schema**|**0x01**|**0x01**|  
|**Func schema solo**|**0x01**|**0x01**|  
|**solo schema della vista indicizzata**|**0x01**|**0x01**|  
|**logbased vista indicizzata**|**0x30F3**|**0x3071**|  
|**vista indicizzata logbase manualboth**|**0x30F3**|**0x3071**|  
|**vista indicizzata logbased manualfilter**|**0x30F3**|**0x3071**|  
|**vista indicizzata logbased manualview**|**0x30F3**|**0x3071**|  
|**logbased**|**0x30F3**|**0x3071**|  
|**logbased manualfilter**|**0x30F3**|**0x3071**|  
|**logbased manualview**|**0x30F3**|**0x3071**|  
|**proc exec**|**0x01**|**0x01**|  
|**proc schema solo**|**0x01**|**0x01**|  
|**serializable proc exec**|**0x01**|**0x01**|  
|**solo schema della vista**|**0x01**|**0x01**|  
  
> [!NOTE]  
>  Se una pubblicazione è abilitata per l'aggiornamento, in coda un *schema_option* valore **0x80** viene aggiunto il valore predefinito indicato nella tabella. Il valore predefinito *schema_option* per non[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pubblicazione è **0x050D3**.  
  
## <a name="valid-schema-options"></a>Opzioni di schema valide  
 La tabella seguente descrive i valori consentiti di *schema_option* in base al tipo di replica (indicato nella parte superiore) e il tipo di articolo (indicato nella prima colonna).  
  
|Tipo di articolo|Tipo di replica||  
|------------------|----------------------|------|  
||Transazionale|Snapshot|  
|**logbased**|Tutte le opzioni|Tutte le opzioni ma **0x02**|  
|**logbased manualfilter**|Tutte le opzioni|Tutte le opzioni ma **0x02**|  
|**logbased manualview**|Tutte le opzioni|Tutte le opzioni ma **0x02**|  
|**logbased vista indicizzata**|Tutte le opzioni|Tutte le opzioni ma **0x02**|  
|**vista indicizzata logbased manualfilter**|Tutte le opzioni|Tutte le opzioni ma **0x02**|  
|**vista indicizzata logbased manualview**|Tutte le opzioni|Tutte le opzioni ma **0x02**|  
|**vista indicizzata logbase manualboth**|Tutte le opzioni|Tutte le opzioni ma **0x02**|  
|**proc exec**|**0x01**, **0x20**, **0x2000**, **0x400000**, **0x800000**, **0x2000000**, **0x8000000**, **0x10000000**, **0x20000000**, **0x40000000**, e **0x80000000**|**0x01**, **0x20**, **0x2000**, **0x400000**, **0x800000**, **0x2000000**, **0x8000000**, **0x10000000**, **0x20000000**, **0x40000000**, e **0x80000000**|  
|**serializable proc exec**|**0x01**, **0x20**, **0x2000**, **0x400000**, **0x800000**, **0x2000000**, **0x8000000**, **0x10000000**, **0x20000000**, **0x40000000**, e **0x80000000**|**0x01**, **0x20**, **0x2000**, **0x400000**, **0x800000**, **0x2000000**, **0x8000000**, **0x10000000**, **0x20000000**, **0x40000000**, e **0x80000000**|  
|**proc schema solo**|**0x01**, **0x20**, **0x2000**, **0x400000**, **0x800000**, **0x2000000**, **0x8000000**, **0x10000000**, **0x20000000**, **0x40000000**, e **0x80000000**|**0x01**, **0x20**, **0x2000**, **0x400000**, **0x800000**, **0x2000000**, **0x8000000**, **0x10000000**, **0x20000000**, **0x40000000**, e **0x80000000**|  
|**solo schema della vista**|**0x01**, **0x010**, **0x020**, **0x040**, **0x0100**, **0x2000**, **0x40000**, **0x100000**, **0x200000**, **0x400000**, **0x800000**,  **0x2000000**, **0x8000000**, **0x40000000**, e **0x80000000**|**0x01**, **0x010**, **0x020**, **0x040**, **0x0100**, **0x2000**, **0x40000**, **0x100000**, **0x200000**, **0x400000**, **0x800000**,  **0x2000000**, **0x8000000**, **0x40000000**, e **0x80000000**|  
|**Func schema solo**|**0x01**, **0x20**, **0x2000**, **0x400000**, **0x800000**, **0x2000000**, **0x8000000**, **0x10000000**, **0x20000000**, **0x40000000**, e **0x80000000**|**0x01**, **0x20**, **0x2000**, **0x400000**, **0x800000**, **0x2000000**, **0x8000000**, **0x10000000**, **0x20000000**, **0x40000000**, e **0x80000000**|  
|**solo schema della vista indicizzata**|**0x01**, **0x010**, **0x020**, **0x040**, **0x0100**, **0x2000**, **0x40000**, **0x100000**, **0x200000**, **0x400000**, **0x800000**,  **0x2000000**, **0x8000000**, **0x40000000**, e **0x80000000**|**0x01**, **0x010**, **0x020**, **0x040**, **0x0100**, **0x2000**, **0x40000**, **0x100000**, **0x200000**, **0x400000**, **0x800000**,  **0x2000000**, **0x8000000**, **0x40000000**, e **0x80000000**|  
  
> [!NOTE]  
>  Per le pubblicazioni ad aggiornamento in coda, il *schema_option* valori di **0x8000** e **0x80** deve essere abilitato. Supportato *schema_option* i valori del parametro non[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pubblicazioni sono: **0x01**, **0x02**, **0x10**,  **0x40**, **0x80**, **0x1000**, **0x4000** e **0X8000**.  
  
## <a name="example"></a>Esempio  
 [!code-sql[HowTo#sp_AddTranArticle](../../relational-databases/replication/codesnippet/tsql/sp-addarticle-transact-sql_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server o **db_owner** ruolo predefinito del database possono eseguire **sp_addarticle**.  
  
## <a name="see-also"></a>Vedere anche  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [sp_articlecolumn &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sp_articlefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md)   
 [sp_articleview &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)   
 [sp_changearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_helparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [sp_helparticlecolumns &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md)   
 [Stored procedure per la replica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [Pubblicare dati e oggetti di database](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
