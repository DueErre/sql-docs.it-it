---
title: EXECUTE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- EXEC
- EXECUTE_TSQL
- EXECUTE
- EXEC_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- remote stored procedures [SQL Server]
- command strings [SQL Server]
- extended stored procedures [SQL Server], executing
- stored procedures [SQL Server], executing
- Transact-SQL statements, executing
- strings [SQL Server], executing
- statements [SQL Server], executing
- context switching [SQL Server], execution context
- user-defined functions [SQL Server], executing
- character strings [SQL Server], executing
- switching execution context
- EXECUTE statement
ms.assetid: bc806b71-cc55-470a-913e-c5f761d5c4b7
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: e974faeb95631f73cd8f902194329c6eb54e825f
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2018
---
# <a name="execute-transact-sql"></a>EXECUTE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Esegue una stringa di comando o una stringa di caratteri all'interno di un [!INCLUDE[tsql](../../includes/tsql-md.md)] batch o uno dei seguenti moduli: sistema stored procedure, stored procedure definita dall'utente, stored procedure CLR, funzione definita dall'utente a valori scalari o stored procedure estesa. L'istruzione EXECUTE può essere utilizzata per inviare comandi pass-through ai server collegati. È inoltre possibile impostare in modo esplicito il contesto di esecuzione di una stringa o di un comando. I metadati per il set di risultati possono essere definiti tramite le opzioni WITH RESULT SETS.
  
> [!IMPORTANT]  
>  Prima di chiamare l'istruzione EXECUTE con una stringa di caratteri, convalidare la stringa di caratteri. Non eseguire mai un comando costruito in base a input utente non convalidato.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
-- Syntax for SQL Server  
  
Execute a stored procedure or function  
[ { EXEC | EXECUTE } ]  
    {   
      [ @return_status = ]  
      { module_name [ ;number ] | @module_name_var }   
        [ [ @parameter = ] { value   
                           | @variable [ OUTPUT ]   
                           | [ DEFAULT ]   
                           }  
        ]  
      [ ,...n ]  
      [ WITH <execute_option> [ ,...n ] ]  
    }  
[;]  
  
Execute a character string  
{ EXEC | EXECUTE }   
    ( { @string_variable | [ N ]'tsql_string' } [ + ...n ] )  
    [ AS { LOGIN | USER } = ' name ' ]  
[;]  
  
Execute a pass-through command against a linked server  
{ EXEC | EXECUTE }  
    ( { @string_variable | [ N ] 'command_string [ ? ]' } [ + ...n ]  
        [ { , { value | @variable [ OUTPUT ] } } [ ...n ] ]  
    )   
    [ AS { LOGIN | USER } = ' name ' ]  
    [ AT linked_server_name ]  
[;]  
  
<execute_option>::=  
{  
        RECOMPILE   
    | { RESULT SETS UNDEFINED }   
    | { RESULT SETS NONE }   
    | { RESULT SETS ( <result_sets_definition> [,...n ] ) }  
}   
  
<result_sets_definition> ::=   
{  
    (  
         { column_name   
           data_type   
         [ COLLATE collation_name ]   
         [ NULL | NOT NULL ] }  
         [,...n ]  
    )  
    | AS OBJECT   
        [ db_name . [ schema_name ] . | schema_name . ]   
        {table_name | view_name | table_valued_function_name }  
    | AS TYPE [ schema_name.]table_type_name  
    | AS FOR XML   
}  
```  
  
```  
-- In-Memory OLTP   

Execute a natively compiled, scalar user-defined function  
[ { EXEC | EXECUTE } ]   
    {   
      [ @return_status = ]   
      { module_name | @module_name_var }   
        [ [ @parameter = ] { value   
                           | @variable   
                           | [ DEFAULT ]   
                           }  
        ]   
      [ ,...n ]   
      [ WITH <execute_option> [ ,...n ] ]   
    }  
<execute_option>::=  
{  
    | { RESULT SETS UNDEFINED }   
    | { RESULT SETS NONE }   
    | { RESULT SETS ( <result_sets_definition> [,...n ] ) }  
}  
```  
  
```  
-- Syntax for Azure SQL Database   
  
Execute a stored procedure or function  
[ { EXEC | EXECUTE } ]  
    {   
      [ @return_status = ]  
      { module_name  | @module_name_var }   
        [ [ @parameter = ] { value   
                           | @variable [ OUTPUT ]   
                           | [ DEFAULT ]   
                           }  
        ]  
      [ ,...n ]  
      [ WITH RECOMPILE ]  
    }  
[;]  
  
Execute a character string  
{ EXEC | EXECUTE }   
    ( { @string_variable | [ N ]'tsql_string' } [ + ...n ] )  
    [ AS {  USER } = ' name ' ]  
[;]  
  
<execute_option>::=  
{  
        RECOMPILE   
    | { RESULT SETS UNDEFINED }   
    | { RESULT SETS NONE }   
    | { RESULT SETS ( <result_sets_definition> [,...n ] ) }  
}   
  
<result_sets_definition> ::=   
{  
    (  
         { column_name   
           data_type   
         [ COLLATE collation_name ]   
         [ NULL | NOT NULL ] }  
         [,...n ]  
    )  
    | AS OBJECT   
        [ db_name . [ schema_name ] . | schema_name . ]   
        {table_name | view_name | table_valued_function_name }  
    | AS TYPE [ schema_name.]table_type_name  
    | AS FOR XML  
  
```  
  
```sql  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  

-- Execute a stored procedure  
[ { EXEC | EXECUTE } ]  
    procedure_name   
        [ { value | @variable [ OUT | OUTPUT ] } ] [ ,...n ] }  
[;]  
  
-- Execute a SQL string  
{ EXEC | EXECUTE }  
    ( { @string_variable | [ N ] 'tsql_string' } [ +...n ] )  
[;]  
```  
  
## <a name="arguments"></a>Argomenti  
 @*return_status*  
 Variabile di tipo integer facoltativa in cui viene archiviato lo stato di restituzione di un modulo. Prima di utilizzare questa variabile in un'istruzione EXECUTE, è necessario dichiararla nel batch, nella stored procedure o nella funzione.  
  
 Se utilizzata per richiamare una a valori scalari definita dall'utente (funzione), il @*return_status* variabile può essere di qualsiasi tipo di dati scalare.  
  
 *module_name*  
 Nome completo o non qualificato della stored procedure o della funzione con valori scalari definita dall'utente da chiamare. I nomi di modulo devono essere conforme alle regole per [identificatori](../../relational-databases/databases/database-identifiers.md). Per i nomi delle stored procedure estese la combinazione di maiuscole e minuscole è sempre rilevante, indipendentemente dalle regole di confronto del server.  
  
 Un modulo che è possibile creare in un altro database può essere eseguito se l'utente che lo esegue è il proprietario del modulo o dispone delle autorizzazioni appropriate per eseguirlo in tale database. È possibile eseguire un modulo in un altro server che esegue [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se l'utente che lo esegue dispone delle autorizzazioni appropriate per l'utilizzo di tale server (accesso remoto) e per l'esecuzione del modulo nel database specifico. Se si specifica il nome del server ma non quello del database, [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] esegue automaticamente la ricerca del modulo nel database predefinito dell'utente.  
  
 ; *numero*  
**Si applica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Numero intero facoltativo utilizzato per raggruppare le stored procedure con lo stesso nome. Questo parametro non viene usato per stored procedure estese.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 Per ulteriori informazioni sui gruppi di procedure, vedere [CREATE PROCEDURE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-procedure-transact-sql.md).  
  
 @*module_name_var*  
 Nome di una variabile definita localmente che rappresenta il nome di un modulo.  
  
 Può trattarsi di una variabile che contiene il nome di una funzione compilata in modo nativo e scalare definite dall'utente.  
  
 @*parametro*  
 Il parametro per *nome_modulo*, come definito nel modulo. I nomi dei parametri devono iniziare con il simbolo di chiocciola (@). Quando si utilizza il @*parameter_name*=*valore* form, i nomi dei parametri e le costanti non è necessario essere specificati nell'ordine in cui sono definiti nel modulo. Tuttavia, se il @*parameter_name*=*valore* modulo viene utilizzato per qualsiasi parametro, deve essere utilizzata per tutti i parametri successivi.  
  
 Per impostazione predefinita, i parametri ammettono valori Null.  
  
 *Valore*  
 Valore del parametro da passare al modulo o al comando pass-through. Se i nomi dei parametri vengono omessi, è necessario immettere i relativi valori in base all'ordine definito nel modulo.  
  
 Durante l'esecuzione di comandi pass-through in server collegati, l'ordine dei valori dei parametri dipende dal provider OLE DB del server collegato. La maggior parte dei provider OLE DB associa i valori ai parametri da sinistra a destra.  
  
 Se il valore di un parametro è il nome di un oggetto, una stringa di caratteri o un nome qualificato dal nome del database o dello schema, l'intero nome deve essere racchiuso tra virgolette singole. Se il valore di un parametro è rappresentato da una parola chiave, questa deve essere racchiusa tra virgolette doppie.  
  
 Se nel modulo è definito un valore predefinito, l'utente può eseguire il modulo senza specificare un parametro.  
  
 Il valore predefinito può essere inoltre NULL. In genere nella definizione del modulo sono specificate le operazioni da eseguire se un valore di parametro è NULL.  
  
 @*variabile*  
 Variabile in cui è archiviato un parametro o un parametro restituito.  
  
 OUTPUT  
 Specifica che il modulo o la stringa di comando restituisce un parametro. Il parametro corrispondente nel modulo o nella stringa di comando deve essere creato tramite la parola chiave OUTPUT. Specificare questa parola chiave quando come parametri si utilizzano variabili di cursore.  
  
 Se *valore* viene definito come OUTPUT di un modulo eseguito in un server collegato, qualsiasi modifica apportata al corrispondente*parametro* eseguite da OLE DB provider verrà copiato nella variabile alla fine del esecuzione del modulo.  
  
 Se vengono utilizzati i parametri di OUTPUT e si desidera utilizzare i valori restituiti in altre istruzioni del batch di chiamata o di un modulo, il valore del parametro deve essere passato come variabile, ad esempio*parametro* = @*variabile* . Non è possibile eseguire un modulo specificando la parola chiave OUTPUT per un parametro non definito come parametro OUTPUT nel modulo. Le costanti non possono essere passate al modulo utilizzando la parola chiave OUTPUT. Il parametro restituito richiede il nome di una variabile. Prima di eseguire una procedura, è necessario dichiarare il tipo dei dati della variabile e assegnare un valore.  
  
 Se si utilizza l'istruzione EXECUTE in una stored procedure remota oppure si esegue un comando pass-through in un server collegato, i parametri OUTPUT non possono essere di nessuno dei tipi di dati LOB.  
  
 I parametri restituiti possono essere di un tipo di dati qualsiasi, tranne i tipi di dati LOB.  
  
 DEFAULT  
 Valore predefinito del parametro, come definito nel modulo. Quando nel modulo è previsto un valore per un parametro privo di valore predefinito ed è stato omesso un parametro o è stata specificata la parola chiave DEFAULT, viene generato un errore.  
  
 @*string_variable*  
 Nome di una variabile locale. @*string_variable* può essere qualsiasi **char**, **varchar**, **nchar**, o **nvarchar** tipo di dati. Queste includono la **(max)** tipi di dati.  
  
 [N] '*tsql_string*'  
 Valore stringa costante. *tsql_string* può essere qualsiasi **nvarchar** o **varchar** tipo di dati. Se il valore N è incluso, la stringa viene interpretata come **nvarchar** tipo di dati.  
  
 AS \<context_specification>  
 Specifica il contesto in cui viene eseguita l'istruzione.  
  
 Account di accesso  
**Si applica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Specifica che il contesto da rappresentare è un account di accesso. L'ambito di rappresentazione è il server.  
  
 Utente  
 Specifica che il contesto da rappresentare è un utente nel database corrente. L'ambito di rappresentazione è limitato al database corrente. Un cambio di contesto a un utente del database non eredita le autorizzazioni a livello di server di tale utente.  
  
> [!IMPORTANT]  
>  Mentre il cambio di contesto all'utente del database è attivo, qualsiasi tentativo di accesso alle risorse esterne al database comporterà l'esito negativo dell'esecuzione dell'istruzione. Ciò include l'utilizzo *database* istruzioni, le query distribuite e le query che fanno riferimento a un altro database usando identificatori in tre o quattro parti.  
  
 '*nome*'  
 Nome utente o nome account di accesso valido. *nome* deve essere un membro del ruolo predefinito del server sysadmin oppure esistere come entità nel [Sys. database_principals](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md) o [Sys. server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md), rispettivamente.  
  
 *nome* non può essere un account incorporato, ad esempio NT AUTHORITY\LocalService, NT AUTHORITY\NetworkService o NT AUTHORITY\LocalSystem.  
  
 Per ulteriori informazioni, vedere [specificando un utente o un nome di accesso](#_user) più avanti in questo argomento.  
  
 [N] '*command_string*'  
 Stringa costante contenente il comando da passare al server collegato. Se il valore N è incluso, la stringa viene interpretata come **nvarchar** tipo di dati.  
  
 [?]  
 Indica i parametri per il quale i valori vengono forniti nel \<arg-list > di comandi pass-through che vengono utilizzati in EXEC('...', \<arg-list>) in \<server collegato > istruzione.  
  
 AT *linked_server_name*  
**Si applica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Specifica che *command_string* viene eseguita su *linked_server_name* e, se presenti, vengono restituiti al client. *linked_server_name* deve fare riferimento a una definizione di server collegato esistente nel server locale. Server collegati definiti tramite [sp_addlinkedserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md).  
  
 CON \<execute_option >  
 Opzioni di esecuzione possibili. Le opzioni RESULT SETS non possono essere specificate in un'istruzione INSERT...EXEC.  
  
|Nome|Definizione|  
|----------|----------------|  
|RECOMPILE|Forza la compilazione, l'utilizzo e l'eliminazione di un nuovo piano dopo l'esecuzione del modulo. Se per il modulo è disponibile un piano di query esistente, tale piano rimane nella cache.<br /><br /> Utilizzare questa opzione se il parametro fornito è atipico oppure se i dati sono cambiati notevolmente. Questa opzione non viene utilizzata per stored procedure estese. È consigliabile utilizzarla solo quando è strettamente necessario, in quanto si tratta di un'opzione onerosa.<br /><br /> **Nota:** non è possibile utilizzare WITH RECOMPILE quando si chiama una stored procedure che utilizza la sintassi OPENDATASOURCE. Quando viene specificato un nome di oggetto composto da quattro parti, l'opzione WITH RECOMPILE viene ignorata.<br /><br /> **Nota:** RECOMPILE non è supportato con le funzioni compilate in modo nativo e scalari definite dall'utente. Se è necessario ricompilare, utilizzare [sp_recompile &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-recompile-transact-sql.md).|  
|**SET DI RISULTATI NON DEFINITI**|**Si applica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].<br /><br /> Questa opzione non fornisce alcuna garanzia sugli eventuali risultati restituiti e non viene specificata alcuna definizione. L'istruzione viene eseguita senza errore se vengono restituiti risultati o se non ne vengono restituiti. RESULT SETS UNDEFINED rappresenta il comportamento predefinito se result_sets_option non viene specificato.<br /><br /> Per interpretare funzioni scalari definite dall'utente e funzioni definite dall'utente scalare compilate in modo nativo, questa opzione non è operativa perché le funzioni non restituiscono mai un set di risultati.|  
|RESULT SETS NONE|**Si applica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].<br /><br /> Garantisce che l'istruzione di esecuzione non restituirà risultati. Se vengono restituiti risultati il batch viene interrotto.<br /><br /> Per interpretare funzioni scalari definite dall'utente e funzioni definite dall'utente scalare compilate in modo nativo, questa opzione non è operativa perché le funzioni non restituiscono mai un set di risultati.|  
|*\<result_sets_definition>*|**Si applica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].<br /><br /> Garantisce che il risultato verrà restituito come specificato in result_sets_definition. Per istruzioni che restituiscono più set di risultati, specificare più *result_sets_definition* sezioni. Racchiudere ogni *result_sets_definition* tra parentesi, separate da virgole. Per ulteriori informazioni, vedere \<result_sets_definition > più avanti in questo argomento.<br /><br /> Sempre questa opzione comporta un errore per le funzioni compilate in modo nativo e scalari definite dall'utente, poiché le funzioni non restituiscono mai un set di risultati.|
  
\<result_sets_definition > **si applica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)],[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]
  
 Descrive i set di risultati restituiti dalle istruzioni eseguite. Le clausole di result_sets_definition hanno il significato seguente  
  
|Nome|Definizione|  
|----------|----------------|  
|{<br /><br /> column_name<br /><br /> data_type<br /><br /> [ COLLATE collation_name]<br /><br /> [NULL &#124; NOT NULL]<br /><br /> }|Vedere la tabella riportata di seguito.|  
|db_name|Nome del database contenente la tabella, la vista o la funzione con valori di tabella.|  
|schema_name|Nome dello schema proprietario della tabella, della vista o della funzione con valori di tabella.|  
|table_name &#124; view_name &#124; table_valued_function_name|Specifica che le colonne restituite saranno quelle specificate nella tabella, nella vista o nella funzione con valori di tabella denominata. La sintassi degli oggetti AS non supporta i sinonimi, le tabelle temporanee e le variabili di tabella.|  
|AS TYPE [schema_name.]table_type_name|Specifica che le colonne restituite saranno quelle specificate nel tipo della tabella.|  
|AS FOR XML|Specifica che i risultati XML dell'istruzione o della stored procedure chiamata dall'istruzione EXECUTE vengono convertiti nel formato come se fossero prodotti da un'istruzione SELECT … FOR XML … . Tutta la formattazione dalle direttive type nell'istruzione originale viene rimossa e i risultati vengono restituiti come se non fosse stata specificata alcuna direttiva type. AS FOR XML non converte i risultati tabulari non XML dall'istruzione o dalla stored procedure eseguita in XML.|  
  
|Nome|Definizione|  
|----------|----------------|  
|column_name|Nomi di ogni colonna. Se il numero di colonne è diverso dal set di risultati, si verifica un errore e il batch viene interrotto. Se il nome di una colonna è diverso dal set di risultati, il nome della colonna restituito verrà impostato sul nome definito.|  
|data_type|Tipi di dati di ogni colonna. Se i tipi di dati sono diversi, viene eseguita una conversione implicita al tipo di dati definito. Se la conversione ha esito negativo il batch viene interrotto|  
|COLLATE collation_name|Regole di confronto di ogni colonna. In caso di mancata corrispondenza tra regole di confronto, vengono tentate regole di confronto implicite. Se la conversione ha esito negativo il batch viene interrotto.|  
|NULL &#124; NOT NULL|Ammissione di valori Null di ogni colonna. Se l'ammissione di valori Null definita è NOT NULL e i dati restituiti contengono NULL si verifica un errore e il batch viene interrotto. Se non è specificato, il valore predefinito si allinea all'impostazione delle opzioni ANSI_NULL_DFLT_ON e ANSI_NULL_DFLT_OFF.|  
  
 Il set di risultati effettivo restituito durante l'esecuzione può essere diverso dal risultato definito tramite la clausola WITH RESULT SETS in uno dei modi seguenti: numero di set di risultati, numero di colonne, nome della colonna, ammissione di valori Null e tipo di dati. Se il numero di set di risultati è diverso, si verifica un errore e il batch viene interrotto.  
  
## <a name="remarks"></a>Osservazioni  
 È possibile specificare parametri tramite *valore* o utilizzando*parameter_name*=*valore.* Un parametro non fa parte di una transazione. Se un parametro viene modificato in una transazione per la quale verrà eseguito il rollback, il valore del parametro non viene ripristinato al suo valore precedente. Il valore restituito al chiamante corrisponde sempre al valore specificato al termine del modulo.  
  
 La nidificazione si verifica quando un modulo ne chiama un altro o quando esegue codice gestito tramite riferimenti a un modulo CLR (Common Language Runtime), un tipo definito dall'utente o una funzione di aggregazione. Il livello di nidificazione viene incrementato quando il modulo chiamato o il riferimento al codice gestito viene eseguito, mentre viene decrementato al termine dell'esecuzione del modulo chiamato o del riferimento al codice gestito. Se viene superato il numero massimo di 32 livelli di nidificazione, l'intera catena di chiamata ha esito negativo. Il livello di nidificazione corrente viene archiviato nel @@NESTLEVEL funzione di sistema.  
  
 Poiché le stored procedure remote ed estese non rientrano nell'ambito di una transazione, a meno che non siano eseguite in un'istruzione BEGIN DISTRIBUTED TRANSACTION o utilizzate con diverse opzioni di configurazione, non è possibile eseguire il rollback dei comandi eseguiti tramite chiamate a tali stored procedure. Per ulteriori informazioni, vedere [Stored procedure di sistema &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md) e [iniziare la transazione distribuita &#40; Transact-SQL &#41; ](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md).  
  
 Quando vengono utilizzate variabili cursore, se si esegue una procedura che passa una variabile cursore con un cursore assegnato, viene generato un errore.  
  
 Se l'istruzione è la prima di un batch, non è necessario specificare la parola chiave EXECUTE durante l'esecuzione dei moduli.  
  
 Per informazioni aggiuntive specifiche delle stored procedure CLR, vedere Stored procedure CLR.  
  
## <a name="using-execute-with-stored-procedures"></a>Utilizzo di EXECUTE con stored procedure  
 Se l'istruzione è la prima di un batch, non è necessario specificare la parola chiave EXECUTE durante l'esecuzione delle stored procedure.  
  
 I nomi delle stored procedure di sistema di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] iniziano con i caratteri sp_. Sono archiviati fisicamente nel [database delle risorse](../../relational-databases/databases/resource-database.md), ma sono visualizzate logicamente nello schema sys di ogni sistema e di un database definito dall'utente. Se si esegue una stored procedure di sistema in un batch oppure all'interno di un modulo quale una stored procedure o una funzione definita dall'utente, è consigliabile qualificare il nome della stored procedure con il nome dello schema sys.  
  
 I nomi delle stored procedure estese di sistema di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] iniziano con i caratteri xp_ e tali stored procedure sono incluse nello schema dbo del database master. Se si esegue una stored procedure estesa di sistema in un batch oppure all'interno di un modulo quale una stored procedure o una funzione definita dall'utente, è consigliabile qualificare il nome della stored procedure con master.dbo.  
  
 Se si esegue una stored procedure definita dall'utente in un batch o all'interno di un modulo quale una funzione o una stored procedure definita dall'utente, è consigliabile qualificare il nome della stored procedure con un nome di schema. Non è consigliabile assegnare a una stored procedure definita dall'utente lo stesso nome di una stored procedure di sistema. Per ulteriori informazioni sull'esecuzione di stored procedure, vedere [eseguire una Stored Procedure](../../relational-databases/stored-procedures/execute-a-stored-procedure.md).  
  
## <a name="using-execute-with-a-character-string"></a>Utilizzo dell'istruzione EXECUTE con una stringa di caratteri  
 Nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] le stringhe di caratteri sono limitate a 8.000 byte. Ciò richiede la concatenazione di stringhe di grandi dimensioni per l'esecuzione dinamica. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], **varchar (max)** e **nvarchar (max)** possibile specificare i tipi di dati che consentono di stringhe di caratteri da un massimo di 2 gigabyte di dati.  
  
 Le modifiche al contesto del database rimangono effettive solo fino al termine dell'esecuzione di EXECUTE. Ad esempio, dopo l'esecuzione di `EXEC` nell'istruzione seguente, il contesto di database è master.  
  
```sql  
USE master; EXEC ('USE AdventureWorks2012; SELECT BusinessEntityID, JobTitle FROM HumanResources.Employee;');  
```  
  
## <a name="context-switching"></a>Cambio di contesto  
 È possibile utilizzare la clausola `AS { LOGIN | USER } = ' name '` per cambiare il contesto di esecuzione di un'istruzione dinamica. Se il cambio di contesto viene specificato come `EXECUTE ('string') AS <context_specification>`, la durata del cambio di contesto è limitata all'ambito della query in fase di esecuzione.  
  
###  <a name="_user"></a>Specifica un utente o un nome di accesso  
 Il nome utente o nome account di accesso specificato in `AS { LOGIN | USER } = ' name '` deve esistere come entità rispettivamente in sys.database_principals o sys.server_principals. In caso contrario, l'istruzione avrà esito negativo. È inoltre necessario concedere le autorizzazioni IMPERSONATE per l'entità. A meno che il chiamante non sia il proprietario del database o membro del ruolo predefinito del server sysadmin, l'entità deve esistere anche quando l'utente effettua l'accesso al database o all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tramite l'appartenenza a un gruppo di Windows. Si suppongano ad esempio le condizioni seguenti:  
  
-   Il gruppo CompanyDomain\SQLUsers ha accesso al database Sales.  
  
-   CompanyDomain\SqlUser1 è membro del gruppo SQLUsers e pertanto può accedere implicitamente al database Sales.  
  
 Anche se companydomain\sqluser1 può accedere al database tramite l'appartenenza nel SQLUsers gruppo, l'istruzione `EXECUTE @string_variable AS USER = 'CompanyDomain\SqlUser1'` avrà esito negativo perché `CompanyDomain\SqlUser1` non esiste come entità nel database.  
  
### <a name="best-practices"></a>Procedure consigliate  
 Specificare un account di accesso o un utente che disponga almeno dei privilegi necessari per eseguire le operazioni definite nell'istruzione o nel modulo. Ad esempio, non specificare un nome account di accesso con autorizzazioni a livello di server se sono richieste solo autorizzazioni a livello di database oppure non specificare l'account di un proprietario di database a meno che siano richieste le autorizzazioni corrispondenti.  
  
## <a name="permissions"></a>Autorizzazioni  
 Per eseguire l'istruzione EXECUTE, non è necessario disporre di autorizzazioni specifiche. Sono tuttavia richieste autorizzazioni per le entità a protezione diretta a cui viene fatto riferimento all'interno della stringa EXECUTE. Se, ad esempio, la stringa include un'istruzione INSERT, il chiamante dell'istruzione EXECUTE deve disporre dell'autorizzazione INSERT per la tabella di destinazione. Le autorizzazioni vengono verificate non appena viene rilevata l'istruzione EXECUTE, anche se l'istruzione è inclusa in un modulo.  
  
 Le autorizzazioni per l'istruzione EXECUTE per un modulo vengono assegnate per impostazione predefinita al proprietario del modulo, che può quindi trasferirle ad altri utenti. Quando si esegue un modulo che esegue una stringa, la verifica delle autorizzazioni viene eseguita nel contesto dell'utente che esegue il modulo e non nel contesto dell'utente che l'ha creato. Se, tuttavia, lo stesso utente è proprietario del modulo chiamante e del modulo richiamato, la verifica delle autorizzazioni per l'istruzione EXECUTE non viene eseguita per il secondo modulo.  
  
 Se il modulo accede ad altri oggetti di database, l'esecuzione ha esito positivo se per il modulo si dispone dell'autorizzazione EXECUTE e si verifica una delle condizioni seguenti:  
  
-   Il modulo è contrassegnato come EXECUTE AS USER o SELF e il proprietario del modulo dispone delle autorizzazioni corrispondenti per l'oggetto a cui viene fatto riferimento. Per ulteriori informazioni sulla rappresentazione all'interno di un modulo, vedere [clausola EXECUTE AS &#40; Transact-SQL &#41; ](../../t-sql/statements/execute-as-clause-transact-sql.md).  
  
-   Il modulo è contrassegnato come EXECUTE AS CALLER e si dispone delle autorizzazioni corrispondenti per l'oggetto.  
  
-   Il modulo è contrassegnato come EXECUTE AS *nome_utente*, e *nome_utente* dispone delle autorizzazioni corrispondenti per l'oggetto.  
  
### <a name="context-switching-permissions"></a>Autorizzazioni per il cambio di contesto  
 Per specificare l'istruzione EXECUTE AS per un account di accesso, il chiamante deve disporre delle autorizzazioni IMPERSONATE per il nome account di accesso specificato. Per specificare l'istruzione EXECUTE AS per un utente del database, il chiamante deve disporre delle autorizzazioni IMPERSONATE per il nome utente specificato. Se non si specifica alcun contesto di esecuzione oppure se si specifica EXECUTE AS CALLER, le autorizzazioni IMPERSONATE non sono obbligatorie.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-using-execute-to-pass-a-single-parameter"></a>A. Utilizzo dell'istruzione EXECUTE per passare un parametro singolo  
 La stored procedure `uspGetEmployeeManagers` nel database [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] prevede un parametro (`@EmployeeID`). Negli esempi seguenti vengono eseguite le `uspGetEmployeeManagers` stored procedure con `Employee ID 6` come valore di parametro.  
  
```  
EXEC dbo.uspGetEmployeeManagers 6;  
GO  
```  
  
 La variabile può essere specificata in modo esplicito durante l'esecuzione.  
  
```  
EXEC dbo.uspGetEmployeeManagers @EmployeeID = 6;  
GO  
```  
  
 Se le operazioni seguenti sono la prima istruzione in un batch o un **osql** o **sqlcmd** script EXEC non è obbligatorio.  
  
```  
dbo.uspGetEmployeeManagers 6;  
GO  
--Or  
dbo.uspGetEmployeeManagers @EmployeeID = 6;  
GO  
```  
  
### <a name="b-using-multiple-parameters"></a>B. Utilizzo di più parametri  
 Nell'esempio seguente viene eseguita la stored procedure `spGetWhereUsedProductID` nel database [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. Vengono passati due parametri: il primo è un ID prodotto (`819`), il secondo (`@CheckDate,`) è un valore di tipo `datetime`.  
  
```  
DECLARE @CheckDate datetime;  
SET @CheckDate = GETDATE();  
EXEC dbo.uspGetWhereUsedProductID 819, @CheckDate;  
GO  
```  
  
### <a name="c-using-execute-tsqlstring-with-a-variable"></a>C. Utilizzo dell'istruzione EXECUTE 'tsql_string' con una variabile  
 Nell'esempio seguente viene illustrato come l'istruzione `EXECUTE` gestisca stringhe compilate in modo dinamico contenenti variabili. Nell'esempio viene creato il cursore `tables_cursor` che include un elenco di tutte le tabelle definite dall'utente nel database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)], quindi l'elenco viene utilizzato per ricompilare tutti gli indici nella tabella.  
  
```  
DECLARE tables_cursor CURSOR  
   FOR  
   SELECT s.name, t.name   
   FROM sys.objects AS t  
   JOIN sys.schemas AS s ON s.schema_id = t.schema_id  
   WHERE t.type = 'U';  
OPEN tables_cursor;  
DECLARE @schemaname sysname;  
DECLARE @tablename sysname;  
FETCH NEXT FROM tables_cursor INTO @schemaname, @tablename;  
WHILE (@@FETCH_STATUS <> -1)  
BEGIN;  
   EXECUTE ('ALTER INDEX ALL ON ' + @schemaname + '.' + @tablename + ' REBUILD;');  
   FETCH NEXT FROM tables_cursor INTO @schemaname, @tablename;  
END;  
PRINT 'The indexes on all tables have been rebuilt.';  
CLOSE tables_cursor;  
DEALLOCATE tables_cursor;  
GO  
  
```  
  
### <a name="d-using-execute-with-a-remote-stored-procedure"></a>D. Utilizzo dell'istruzione EXECUTE con una stored procedure remota  
 Nell'esempio seguente viene eseguita la stored procedure `uspGetEmployeeManagers` nel server remoto `SQLSERVER1` e lo stato restituito, che indica se la stored procedure è stata eseguita correttamente o meno, viene archiviato in `@retstat`.  
  
**Si applica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
```  
DECLARE @retstat int;  
EXECUTE @retstat = SQLSERVER1.AdventureWorks2012.dbo.uspGetEmployeeManagers @BusinessEntityID = 6;  
```  
  
### <a name="e-using-execute-with-a-stored-procedure-variable"></a>E. Utilizzo dell'istruzione EXECUTE con una variabile di stored procedure  
 Nell'esempio seguente viene creata una variabile che rappresenta il nome di una stored procedure.  
  
```sql  
DECLARE @proc_name varchar(30);  
SET @proc_name = 'sys.sp_who';  
EXEC @proc_name;  
  
```  
  
### <a name="f-using-execute-with-default"></a>F. Utilizzo dell'istruzione EXECUTE con la parola chiave DEFAULT  
 Nell'esempio seguente viene creata una stored procedure con valori predefiniti per il primo e il terzo parametro. Quando si esegue la procedura, se nella chiamata non viene passato alcun valore oppure viene specificato il valore predefinito, i valori predefiniti vengono utilizzati per il primo e il terzo parametro. Si notino i vari utilizzi della parola chiave `DEFAULT`.  
  
```  
IF OBJECT_ID(N'dbo.ProcTestDefaults', N'P')IS NOT NULL  
   DROP PROCEDURE dbo.ProcTestDefaults;  
GO  
-- Create the stored procedure.  
CREATE PROCEDURE dbo.ProcTestDefaults (  
@p1 smallint = 42,   
@p2 char(1),   
@p3 varchar(8) = 'CAR')  
AS   
   SET NOCOUNT ON;  
   SELECT @p1, @p2, @p3  
;  
GO  
  
```  
  
 La stored procedure `Proc_Test_Defaults` può essere eseguita in molte combinazioni.  
  
```  
-- Specifying a value only for one parameter (@p2).  
EXECUTE dbo.ProcTestDefaults @p2 = 'A';  
-- Specifying a value for the first two parameters.  
EXECUTE dbo.ProcTestDefaults 68, 'B';  
-- Specifying a value for all three parameters.  
EXECUTE dbo.ProcTestDefaults 68, 'C', 'House';  
-- Using the DEFAULT keyword for the first parameter.  
EXECUTE dbo.ProcTestDefaults @p1 = DEFAULT, @p2 = 'D';  
-- Specifying the parameters in an order different from the order defined in the procedure.  
EXECUTE dbo.ProcTestDefaults DEFAULT, @p3 = 'Local', @p2 = 'E';  
-- Using the DEFAULT keyword for the first and third parameters.  
EXECUTE dbo.ProcTestDefaults DEFAULT, 'H', DEFAULT;  
EXECUTE dbo.ProcTestDefaults DEFAULT, 'I', @p3 = DEFAULT;  
  
```  
  
### <a name="g-using-execute-with-at-linkedservername"></a>G. Utilizzo dell'istruzione EXECUTE con il parametro AT linked_server_name  
 Nell'esempio seguente una stringa di comando viene passata a un server remoto. Verrà creato un server collegato `SeattleSales` che punta a un'altra istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ed esegue un'istruzione DDL (`CREATE TABLE`) in tale server collegato.  
  
**Si applica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
```  
EXEC sp_addlinkedserver 'SeattleSales', 'SQL Server'  
GO  
EXECUTE ( 'CREATE TABLE AdventureWorks2012.dbo.SalesTbl   
(SalesID int, SalesName varchar(10)) ; ' ) AT SeattleSales;  
GO  
```  
  
### <a name="h-using-execute-with-recompile"></a>H. Utilizzo dell'istruzione EXECUTE WITH RECOMPILE  
 Nell'esempio seguente viene eseguita la `Proc_Test_Defaults` stored procedure e forza un nuovo piano di query da compilare, utilizzo e l'eliminazione dopo l'esecuzione del modulo.  
  
```  
EXECUTE dbo.Proc_Test_Defaults @p2 = 'A' WITH RECOMPILE;  
GO  
```  
  
### <a name="i-using-execute-with-a-user-defined-function"></a>I. Utilizzo dell'istruzione EXECUTE con una funzione definita dall'utente  
 Nell'esempio seguente viene eseguita la funzione scalare definita dall'utente `ufnGetSalesOrderStatusText` nel database [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. Viene utilizzata la variabile `@returnstatus` per archiviare il valore restituito dalla funzione. Per la funzione è previsto un parametro di input (`@Status`) Ciò viene definito come un **tinyint** tipo di dati.  
  
```  
DECLARE @returnstatus nvarchar(15);  
SET @returnstatus = NULL;  
EXEC @returnstatus = dbo.ufnGetSalesOrderStatusText @Status = 2;  
PRINT @returnstatus;  
GO  
```  
  
### <a name="j-using-execute-to-query-an-oracle-database-on-a-linked-server"></a>J. Utilizzo dell'istruzione EXECUTE per eseguire query su un database Oracle in un server collegato  
 Nell'esempio seguente vengono eseguite più istruzioni `SELECT` nel server Oracle remoto. Viene innanzitutto aggiunto il server Oracle come server collegato e quindi viene creato l'account di accesso per il server collegato.  
  
**Si applica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
```  
-- Setup the linked server.  
EXEC sp_addlinkedserver    
        @server='ORACLE',  
        @srvproduct='Oracle',  
        @provider='OraOLEDB.Oracle',   
        @datasrc='ORACLE10';  
  
EXEC sp_addlinkedsrvlogin   
    @rmtsrvname='ORACLE',  
    @useself='false',   
    @locallogin=null,   
    @rmtuser='scott',   
    @rmtpassword='tiger';  
  
EXEC sp_serveroption 'ORACLE', 'rpc out', true;  
GO  
  
-- Execute several statements on the linked Oracle server.  
EXEC ( 'SELECT * FROM scott.emp') AT ORACLE;  
GO  
EXEC ( 'SELECT * FROM scott.emp WHERE MGR = ?', 7902) AT ORACLE;  
GO  
DECLARE @v INT;   
SET @v = 7902;  
EXEC ( 'SELECT * FROM scott.emp WHERE MGR = ?', @v) AT ORACLE;  
GO   
```  
  
### <a name="k-using-execute-as-user-to-switch-context-to-another-user"></a>K. Utilizzo dell'istruzione EXECUTE AS USER per cambiare contesto a un altro utente  
 Nell'esempio seguente viene eseguita una stringa [!INCLUDE[tsql](../../includes/tsql-md.md)] che crea una tabella e viene quindi specificata la clausola `AS USER` per cambiare il contesto di esecuzione dell'istruzione dal chiamante a `User1`. Il [!INCLUDE[ssDE](../../includes/ssde-md.md)] controllerà le autorizzazioni di `User1` quando viene eseguita l'istruzione. `User1` deve esistere come utente nel database e deve disporre delle autorizzazioni necessarie per creare tabelle nello schema `Sales`. In caso contrario, l'istruzione avrà esito negativo.  
  
```  
EXECUTE ('CREATE TABLE Sales.SalesTable (SalesID int, SalesName varchar(10));')  
AS USER = 'User1';  
GO  
```  
  
### <a name="l-using-a-parameter-with-execute-and-at-linkedservername"></a>L. Utilizzo di un parametro con EXECUTE e AT linked_server_name  
 Nell'esempio seguente una stringa di comando viene passata a un server remoto utilizzando un punto interrogativo (`?`) come segnaposto per un parametro. Viene quindi creato un server collegato `SeattleSales` che punta a un'altra istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e viene eseguita un'istruzione `SELECT` applicata a tale server collegato. L'istruzione `SELECT` utilizza il punto interrogativo come segnaposto per il parametro `ProductID` (`952`), specificato dopo l'istruzione.  
  
**Si applica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
```  
-- Setup the linked server.  
EXEC sp_addlinkedserver 'SeattleSales', 'SQL Server'  
GO  
-- Execute the SELECT statement.  
EXECUTE ('SELECT ProductID, Name   
    FROM AdventureWorks2012.Production.Product  
    WHERE ProductID = ? ', 952) AT SeattleSales;  
GO  
```  
  
### <a name="m-using-execute-to-redefine-a-single-result-set"></a>M. Utilizzo di EXECUTE per ridefinire un singolo set di risultati  
 In alcuni degli esempi precedenti è stato eseguito `EXEC dbo.uspGetEmployeeManagers 6;` che ha restituito 7 colonne. Nell'esempio seguente viene illustrato l'utilizzo della sintassi `WITH RESULT SET` per modificare i nomi e i tipi di dati del set di risultati ottenuto.  
  
**Si applica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)],[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]
  
```  
EXEC uspGetEmployeeManagers 16  
WITH RESULT SETS  
(   
   ([Reporting Level] int NOT NULL,  
    [ID of Employee] int NOT NULL,  
    [Employee First Name] nvarchar(50) NOT NULL,  
    [Employee Last Name] nvarchar(50) NOT NULL,  
    [Employee ID of Manager] nvarchar(max) NOT NULL,  
    [Manager First Name] nvarchar(50) NOT NULL,  
    [Manager Last Name] nvarchar(50) NOT NULL )  
);  
  
```  
  
### <a name="n-using-execute-to-redefine-a-two-result-sets"></a>N. Utilizzo di EXECUTE per ridefinire due set di risultati  
 Quando si esegue un'istruzione che restituisce più di un set di risultati, definire ogni set di risultati previsto. Nell'esempio seguente in [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] viene creata una stored procedure che restituisce due set di risultati. Quindi la procedura viene eseguita utilizzando il **WITH RESULT SETS** clausola e specificando i risultati di due definizioni di set.  
  
**Si applica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)],[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]
  
```  
--Create the procedure  
CREATE PROC Production.ProductList @ProdName nvarchar(50)  
AS  
-- First result set  
SELECT ProductID, Name, ListPrice  
    FROM Production.Product  
    WHERE Name LIKE @ProdName;  
-- Second result set   
SELECT Name, COUNT(S.ProductID) AS NumberOfOrders  
    FROM Production.Product AS P  
    JOIN Sales.SalesOrderDetail AS S  
        ON P.ProductID  = S.ProductID   
    WHERE Name LIKE @ProdName  
    GROUP BY Name;  
GO  
  
-- Execute the procedure   
EXEC Production.ProductList '%tire%'  
WITH RESULT SETS   
(  
    (ProductID int,   -- first result set definition starts here  
    Name Name,  
    ListPrice money)  
    ,                 -- comma separates result set definitions  
    (Name Name,       -- second result set definition starts here  
    NumberOfOrders int)  
);  
  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Esempi: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="example-o-basic-procedure-execution"></a>Esempio /o: esecuzione di Procedure di base  
 Esegue una stored procedure:  
  
```  
EXEC proc1;  
```  
  
 Chiamata di una stored procedure con nome determinato in fase di esecuzione:  
  
```  
EXEC ('EXEC ' + @var);  
```  
  
 Chiamare una stored procedure da all'interno di una stored procedure:  
  
```  
CREATE sp_first AS EXEC sp_second; EXEC sp_third;  
```  
  
### <a name="example-p-executing-strings"></a>Esempio p: l'esecuzione di stringhe  
 Esecuzione di una stringa SQL:  
  
```  
EXEC ('SELECT * FROM sys.types');  
```  
  
 Esecuzione di una stringa annidata:  
  
```  
EXEC ('EXEC (''SELECT * FROM sys.types'')');  
```  
  
 L'esecuzione di una variabile di stringa:  
  
```  
DECLARE @stringVar nvarchar(100);  
SET @stringVar = N'SELECT name FROM' + ' sys.sql_logins';  
EXEC (@stringVar);  
```  
  
### <a name="example-q-procedures-with-parameters"></a>Esempio d: le procedure con parametri  
 Nell'esempio seguente crea una stored procedure con parametri e vengono illustrate le 3 modalità per eseguire la stored procedure:  
  
```  
-- Uses AdventureWorks  
  
CREATE PROC ProcWithParameters  
    @name nvarchar(50),  
@color nvarchar (15)  
AS   
SELECT ProductKey, EnglishProductName, Color FROM [dbo].[DimProduct]  
WHERE EnglishProductName LIKE @name  
AND Color = @color;  
GO  
  
-- Executing using positional parameters  
EXEC ProcWithParameters N'%arm%', N'Black';  
-- Executing using named parameters in order  
EXEC ProcWithParameters @name = N'%arm%', @color = N'Black';  
-- Executing using named parameters out of order  
EXEC ProcWithParameters @color = N'Black', @name = N'%arm%';  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [@@NESTLEVEL &#40;Transact-SQL&#41;](../../t-sql/functions/nestlevel-transact-sql.md)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [Clausola EXECUTE AS &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md)   
 [Utilità osql](../../tools/osql-utility.md)   
 [Entità &#40;motore di database&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [REVERT &#40;Transact-SQL&#41;](../../t-sql/statements/revert-transact-sql.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [Utilità sqlcmd](../../tools/sqlcmd-utility.md)   
 [SUSER_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/suser-name-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [USER_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/user-name-transact-sql.md)   
 [OPENDATASOURCE &#40; Transact-SQL &#41;](../../t-sql/functions/opendatasource-transact-sql.md)   
 [Funzioni scalari definite dall'utente per OLTP in memoria](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md)  
  
  
