---
title: sp_helpmergearticle (Transact-SQL) | Documenti Microsoft
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
- sp_helpmergearticle
- sp_helpmergearticle_TSQL
helpviewer_keywords: sp_helpmergearticle
ms.assetid: 0fb9986a-3c33-46ef-87bb-297396ea5a6a
caps.latest.revision: "40"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 970c07111ba123be3262f9effb5c87a26bb14960
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="sphelpmergearticle-transact-sql"></a>sp_helpmergearticle (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce informazioni su un articolo. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione o nel database di sottoscrizione di un Sottoscrittore di ripubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_helpmergearticle [ [ @publication = ] 'publication' ]  
    [ , [ @article= ] 'article' ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@publication=**] **'***pubblicazione***'**  
 Nome della pubblicazione per cui si desidera recuperare informazioni. *pubblicazione*è **sysname**, il valore predefinito è  **%** , che restituisce informazioni su tutti gli articoli di merge inclusi in tutte le pubblicazioni nel database corrente.  
  
 [  **@article=**] **'***articolo***'**  
 Nome dell'articolo per cui si desidera ottenere informazioni. *articolo*è **sysname**, il valore predefinito è  **%** , che restituisce informazioni su tutti gli articoli di merge nella pubblicazione specificata.  
  
## <a name="result-set"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Identificatore dell'articolo.|  
|**name**|**sysname**|Nome dell'articolo.|  
|**source_owner**|**sysname**|Nome del proprietario dell'oggetto di origine.|  
|**source_object**|**sysname**|Nome dell'oggetto di origine da cui aggiungere l'articolo.|  
|**sync_object_owner**|**sysname**|Nome del proprietario della vista che definisce l'articolo pubblicato.|  
|**sync_object**|**sysname**|Nome dell'oggetto personalizzato utilizzato per stabilire i dati iniziali per la partizione.|  
|**Descrizione**|**nvarchar(255)**|Descrizione dell'articolo.|  
|**status**|**tinyint**|Stato dell'articolo. I possibili valori sono i seguenti:<br /><br /> **1** = inattivo<br /><br /> **2** = attivo<br /><br /> **5** = l'operazione di data definition language (DDL) in sospeso<br /><br /> **6** = operazione DDL con un nuovo snapshot generato<br /><br /> Nota: Quando un articolo viene reinizializzato, i valori di **5** e **6** vengono modificati in **2**.|  
|**creation_script**|**nvarchar(255)**|Percorso e nome di uno script di schema dell'articolo facoltativo utilizzato per la creazione dell'articolo nel database di sottoscrizione.|  
|**conflict_table**|**nvarchar(270)**|Nome della tabella in cui sono archiviati i conflitti di inserimento o aggiornamento.|  
|**article_resolver**|**nvarchar(255)**|Sistema di risoluzione personalizzato per l'articolo.|  
|**subset_filterclause**|**nvarchar (1000)**|Clausola WHERE che specifica il filtro orizzontale.|  
|**pre_creation_command**|**tinyint**|Metodo di creazione preliminare. I possibili valori sono i seguenti:<br /><br /> **0** = nessuno<br /><br /> **1** = eliminazione<br /><br /> **2** = eliminazione<br /><br /> **3** = tronca|  
|**schema_option**|**Binary (8)**|Mappa di bit dell'opzione di generazione dello schema per l'articolo. Per informazioni su questa opzione, vedere [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) o [sp_changemergearticle](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md).|  
|**tipo**|**smallint**|Tipo di articolo. I possibili valori sono i seguenti:<br /><br /> **10** = tabella<br /><br /> **32** = stored procedure<br /><br /> **64** = vista o vista indicizzata<br /><br /> **128** = funzione definita dall'utente<br /><br /> **160** = solo schema sinonimo|  
|**column_tracking**|**int**|Impostazione per il rilevamento a livello di colonna; dove **1** significa che il rilevamento a livello di colonna, e **0** rilevamento a livello di colonna è disattivato.|  
|**resolver_info**|**nvarchar(255)**|Nome del sistema di risoluzione dell'articolo.|  
|**vertical_partition**|**bit**|Se l'articolo è partizionato verticalmente. dove **1** significa che l'articolo è partizionato verticalmente, e **0** significa che non lo è.|  
|**destination_owner**|**sysname**|Proprietario dell'oggetto di destinazione. È applicabile solo per gli articoli di schema di tipo merge per stored procedure, viste e funzioni definite dall'utente.|  
|**identity_support**|**int**|Se Gestione degli intervalli di valori identity automatico è abilitata. dove **1** è abilitato e **0** è disabilitato.|  
|**pub_identity_range**|**bigint**|Dimensioni di intervallo da utilizzare per l'assegnazione di nuovi valori Identity. Per ulteriori informazioni, vedere la sezione "Replica di tipo Merge" di [replicare colonne Identity](../../relational-databases/replication/publish/replicate-identity-columns.md).|  
|**identity_range**|**bigint**|Dimensioni di intervallo da utilizzare per l'assegnazione di nuovi valori Identity. Per ulteriori informazioni, vedere la sezione "Replica di tipo Merge" di [replicare colonne Identity](../../relational-databases/replication/publish/replicate-identity-columns.md).|  
|**soglia**|**int**|Valore percentuale utilizzato per i sottoscrittori che eseguono [!INCLUDE[ssEW](../../includes/ssew-md.md)] o versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. **soglia** determina quando l'agente di Merge assegna un nuovo intervallo di valori identity. Quando viene utilizzata la percentuale di valori specificata in threshold, l'agente di merge crea un nuovo intervallo di valori Identity. Per ulteriori informazioni, vedere la sezione "Replica di tipo Merge" di [replicare colonne Identity](../../relational-databases/replication/publish/replicate-identity-columns.md).|  
|**verify_resolver_signature**|**int**|Se una firma digitale viene verificata prima di utilizzare un sistema di risoluzione nella replica di tipo merge; dove **0** significa che non viene verificata la firma, e **1** significa che la firma viene verificata per stabilire se proviene da una fonte attendibile.|  
|**destination_object**|**sysname**|Nome dell'oggetto di destinazione. È applicabile solo per gli articoli di schema di tipo merge per stored procedure, viste e funzioni definite dall'utente.|  
|**allow_interactive_resolver**|**int**|Se il sistema di risoluzione interattivo viene utilizzato in un articolo; dove **1** significa che viene utilizzato questo resolver, e **0** significa che non è utilizzato.|  
|**fast_multicol_updateproc**|**int**|Abilita o disabilita l'agente di Merge per applicare le modifiche a più colonne nella stessa riga in un'unica istruzione UPDATE; dove **1** significa che più colonne vengono aggiornate in un'unica istruzione, e **0** significa che separano le istruzioni UPDATE è problemi di ogni colonna aggiornata.|  
|**check_permissions**|**int**|Valore integer che rappresenta la mappa di bit delle autorizzazioni a livello di tabella da verificare. Per un elenco di valori possibili, vedere [sp_addmergearticle &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md).|  
|**processing_order**|**int**|Ordine di applicazione delle modifiche dei dati agli articoli di una pubblicazione.|  
|**upload_options**|**tinyint**|Imposta le restrizioni per gli aggiornamenti eseguiti in un Sottoscrittore con una sottoscrizione client. I possibili valori sono i seguenti.<br /><br /> **0** = non esistono restrizioni per gli aggiornamenti eseguiti in un sottoscrittore con una sottoscrizione client; tutte le modifiche vengono caricate nel server di pubblicazione.<br /><br /> **1** = sono consentite modifiche in un sottoscrittore con una sottoscrizione client, ma non vengono caricate nel server di pubblicazione.<br /><br /> **2** = non sono consentite modifiche in un sottoscrittore con una sottoscrizione client.<br /><br /> Per altre informazioni, vedere [Ottimizzare le prestazioni della replica di tipo merge con gli articoli di solo download](../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md).|  
|**identityrangemanagementoption**|**int**|Se Gestione degli intervalli di valori identity automatico è abilitata. dove **1** è abilitato e **0** è disabilitato.|  
|**delete_tracking**|**bit**|Se le eliminazioni vengono replicate. dove **1** significa che le eliminazioni vengono replicate, e **0** significa che non lo siano.|  
|**compensate_for_errors**|**bit**|Indica se vengono eseguite azioni di compensazione quando si verificano errori durante la sincronizzazione. dove **1** indica che vengono eseguite azioni di compensazione e **0** significa che non vengono eseguite azioni di compensazione.|  
|**partition_options**|**tinyint**|Definisce il modo in cui vengono partizionati i dati nell'articolo. Ciò consente di ottimizzare le prestazioni se tutte le righe appartengono a un'unica partizione o a un'unica sottoscrizione. *partition_options* può essere uno dei valori seguenti.<br /><br /> **0** = il filtro per l'articolo è statico oppure non restituisce un subset univoco di dati per ogni partizione; ovvero, è una partizione "sovrapposta".<br /><br /> **1** = le partizioni sono sovrapposte e gli aggiornamenti language (DML) di manipolazione dei dati apportati nel Sottoscrittore non è possibile modificare la partizione a cui appartiene una riga.<br /><br /> **2** = il filtro dell'articolo restituisce partizioni non sovrapposte, ma più sottoscrittori ricevono la stessa partizione.<br /><br /> **3** = il filtro dell'articolo restituisce partizioni non sovrapposte, univoche per ogni sottoscrizione.|  
|**artid**|**uniqueidentifier**|Identificatore univoco dell'articolo.|  
|**pubid**|**uniqueidentifier**|Identificatore univoco della pubblicazione in cui viene pubblicato l'articolo.|  
|**stream_blob_columns**|**bit**|Indica se viene utilizzata l'ottimizzazione del flusso di dati per la replica di colonne BLOB. **1** significa che viene utilizzata l'ottimizzazione, e **0** significa che non viene utilizzata l'ottimizzazione.|  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_helpmergearticle** viene utilizzata nella replica di tipo merge.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **db_owner** ruolo predefinito del database nel database di pubblicazione, il **replmonitor** ruolo nel database di distribuzione o l'elenco di accesso per una pubblicazione può eseguire **sp_helpmergearticle**.  
  
## <a name="example"></a>Esempio  
 [!code-sql[HowTo#sp_helpmergearticle](../../relational-databases/replication/codesnippet/tsql/sp-helpmergearticle-tran_1.sql)]  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzare e modificare le proprietà di articolo](../../relational-databases/replication/publish/view-and-modify-article-properties.md)   
 [sp_addmergearticle &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)   
 [sp_changemergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)   
 [sp_dropmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md)   
 [Stored procedure per la replica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
