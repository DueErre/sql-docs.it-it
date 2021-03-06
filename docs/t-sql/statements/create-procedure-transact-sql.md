---
title: CREARE stored PROCEDURE (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 09/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PROC
- PROCEDURE
- CREATE PROCEDURE
- CREATE_PROC_TSQL
- PROCEDURE_TSQL
- CREATE PROC
- PROC_TSQL
- CREATE_PROCEDURE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- parameters [SQL Server], stored procedures
- table-valued parameters
- SET statement, stored procedures
- stored procedures [SQL Server], creating
- wildcard parameters [SQL Server]
- maximum size of stored procedures
- WITH RECOMPILE clause
- common language runtime [SQL Server], stored procedures
- CREATE PROCEDURE statement
- local temporary procedures [SQL Server]
- WITH ENCRYPTION clause
- output parameters [SQL Server]
- nesting stored procedures
- user-defined stored procedures [SQL Server]
- system stored procedures [SQL Server], creating
- deferred name resolution, stored procedures
- referenced tables [SQL Server]
- global temporary procedures [SQL Server]
- cursor data type
- temporary stored procedures [SQL Server]
- size [SQL Server], stored procedures
- automatic stored procedure execution
- creating stored procedures
ms.assetid: afe3d86d-c9ab-44e4-b74d-4e3dbd9cc58c
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 086151e2916335ae0d7cda3eef11a79363d3ce53
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="create-procedure-transact-sql"></a>CREATE PROCEDURE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Crea un [!INCLUDE[tsql](../../includes/tsql-md.md)] o common language runtime (CLR) stored procedure [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], Azure SQL Data Warehouse e Parallel Data Warehouse. Le stored procedure sono simili alle procedure di altri linguaggi di programmazione in quanto sono in grado di:  
  
-   Accettare parametri di input e restituire più valori sotto forma di parametri di output alla procedura o al batch che esegue la chiamata.  
  
-   Includere istruzioni di programmazione che eseguono le operazioni nel database, tra cui la chiamata di altre procedure.  
  
-   Restituire un valore di stato a una procedura o a un batch che esegue la chiamata per indicare l'esito positivo o negativo (e il motivo dell'esito negativo).  
  
 Utilizzare questa istruzione per creare una stored procedure permanenti nel database corrente o una stored procedure temporanea nel **tempdb** database.  
  
> [!NOTE]  
>  Integrazione di CLR di .NET Framework in SQL Server viene illustrata in questo argomento. Integrazione con CLR non si applica ad Azure [!INCLUDE[ssSDS](../../includes/sssds-md.md)].

Passare a [semplici esempi](#Simple) per ignorare i dettagli della sintassi e ottenere un esempio semplice di un base stored procedure.
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
-- Transact-SQL Syntax for Stored Procedures in SQL Server and Azure SQL Database  
  
CREATE [ OR ALTER ] { PROC | PROCEDURE } 
    [schema_name.] procedure_name [ ; number ]   
    [ { @parameter [ type_schema_name. ] data_type }  
        [ VARYING ] [ = default ] [ OUT | OUTPUT | [READONLY]  
    ] [ ,...n ]   
[ WITH <procedure_option> [ ,...n ] ]  
[ FOR REPLICATION ]   
AS { [ BEGIN ] sql_statement [;] [ ...n ] [ END ] }  
[;]  
  
<procedure_option> ::=   
    [ ENCRYPTION ]  
    [ RECOMPILE ]  
    [ EXECUTE AS Clause ]  
```  
  
```  
-- Transact-SQL Syntax for CLR Stored Procedures  
  
CREATE [ OR ALTER ] { PROC | PROCEDURE } 
    [schema_name.] procedure_name [ ; number ]   
    [ { @parameter [ type_schema_name. ] data_type }   
        [ = default ] [ OUT | OUTPUT ] [READONLY]  
    ] [ ,...n ]   
[ WITH EXECUTE AS Clause ]  
AS { EXTERNAL NAME assembly_name.class_name.method_name }  
[;]  
```  
  
```  
-- Transact-SQL Syntax for Natively Compiled Stored Procedures  
  
CREATE [ OR ALTER ] { PROC | PROCEDURE } [schema_name.] procedure_name  
    [ { @parameter data_type } [ NULL | NOT NULL ] [ = default ] 
        [ OUT | OUTPUT ] [READONLY] 
    ] [ ,... n ]  
  WITH NATIVE_COMPILATION, SCHEMABINDING [ , EXECUTE AS clause ]  
AS  
{  
  BEGIN ATOMIC WITH (set_option [ ,... n ] )  
sql_statement [;] [ ... n ]  
 [ END ]  
}  
 [;]  
  
<set_option> ::=  
    LANGUAGE =  [ N ] 'language'  
  | TRANSACTION ISOLATION LEVEL =  { SNAPSHOT | REPEATABLE READ | SERIALIZABLE }  
  | [ DATEFIRST = number ]  
  | [ DATEFORMAT = format ]  
  | [ DELAYED_DURABILITY = { OFF | ON } ]  
```  
  
```  
-- Transact-SQL Syntax for Stored Procedures in Azure SQL Data Warehouse
-- and Parallel Data Warehouse  
  
-- Create a stored procedure   
CREATE { PROC | PROCEDURE } [ schema_name.] procedure_name  
    [ { @parameterdata_type } [ OUT | OUTPUT ] ] [ ,...n ]  
AS { [ BEGIN ] sql_statement [;][ ,...n ] [ END ] }  
[;]  
```  
  
## <a name="arguments"></a>Argomenti
O ALTER  
 **Si applica a**: Azure [!INCLUDE[ssSDS](../../includes/sssds-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partire da [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1).  
  
 Modifica la procedura, se esiste già.
 
 *schema_name*  
 Nome dello schema a cui appartiene la procedura. Le procedure sono associate a schema. Se durante la creazione della procedura non viene specificato un nome dello schema, viene assegnato automaticamente lo schema predefinito dell'utente che sta creando la procedura.  
  
 *procedure_name*  
 Nome della procedura. I nomi delle procedure devono essere conformi alle regole per [identificatori](../../relational-databases/databases/database-identifiers.md) e deve essere univoco all'interno dello schema.  
  
 Evitare di utilizzare il **sp _** prefisso per la denominazione delle procedure. Questo prefisso viene usato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per definire le procedure di sistema. L'utilizzo del prefisso può comportare l'interruzione del codice dell'applicazione, se è presente una procedura di sistema con lo stesso nome.  
  
 Stored procedure temporanee locali o globali possono essere create utilizzando un simbolo di cancelletto (#) prima di *procedure_name* (*#procedure_name*) per stored procedure temporanee locali e due simboli di cancelletto per temporanea globale procedure (*# # procedure_name*). Una stored procedure temporanea locale è visibile solo alla connessione da cui è stata creata e, alla chiusura di quest'ultima, viene eliminata. Una stored procedure temporanea globale è disponibile per tutte le connessioni e viene eliminata al termine dell'ultima sessione che la usano. Non è possibile specificare nomi temporanei per le procedure CLR.  
  
 Il nome completo di una procedura o di una stored procedure temporanea globale, inclusi i simboli ##, non deve superare i 128 caratteri. Il nome completo di una stored procedure temporanea locale, incluso il simbolo #, non deve superare i 116 caratteri.  
  
 **;**  *numero*  
 **Si applica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Integer facoltativo usato per raggruppare le procedure con lo stesso nome. Tali procedure possono essere eliminate contemporaneamente tramite un'istruzione DROP PROCEDURE.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 Procedure numerate non è possibile utilizzare il **xml** o CLR definito dall'utente, tipi e non può essere utilizzato in una Guida di piano.  
  
 **@***parametro*  
 Parametro dichiarato nella procedura. Specificare un nome di parametro utilizzando il simbolo di chiocciola (**@**) come primo carattere. Il nome del parametro deve essere conforme alle regole per [identificatori](../../relational-databases/databases/database-identifiers.md). Poiché i parametri sono locali rispetto alla procedura, è possibile usare gli stessi nomi di parametro in altre procedure.  
  
 È possibile dichiarare uno o più parametri con un limite massimo di 2.100. Il valore di ogni parametro dichiarato deve essere specificato dall'utente quando viene chiamata la procedura, a meno che non venga indicato un valore predefinito per il parametro oppure il valore venga impostato in modo da corrispondere a quello di un altro parametro. Se una stored procedure contiene [parametri con valori di tabella](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)e il parametro è presente nella chiamata, viene passata una tabella vuota. I parametri possono rappresentare solo espressioni costanti, non nomi di tabella, nomi di colonna o nomi di altri oggetti di database. Per altre informazioni, vedere [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md).  
  
 Se viene specificata l'opzione FOR REPLICATION, non è possibile dichiarare alcun parametro.  
  
 [ *type_schema_name***.** ] *data_type*  
 Tipo di dati del parametro e schema a cui appartiene il tipo di dati.  
  
**Linee guida per [!INCLUDE[tsql](../../includes/tsql-md.md)] procedure**:  
  
-   Tutti [!INCLUDE[tsql](../../includes/tsql-md.md)] tipi di dati possono essere usati come parametri.  
  
-   Per creare parametri con valori di tabella è possibile usare il tipo di tabella definito dall'utente. I parametri con valori di tabella possono essere solo parametri di input e devono essere associati alla parola chiave READONLY. Per ulteriori informazioni, vedere [utilizzare parametri &#40; motore di Database &#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)  
  
-   **cursore** tipi di dati possono essere solo parametri OUTPUT e devono essere associati alla parola chiave VARYING.  
  
**Linee guida per le procedure CLR**:  
  
-   Tutti i tipi di dati nativi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per cui è presente un equivalente nel codice gestito possono essere usati come parametri. Per ulteriori informazioni sulla corrispondenza tra tipi CLR e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipi di dati di sistema, vedere [Mapping dei dati di parametro CLR](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md). Per ulteriori informazioni su [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipi di dati di sistema e la relativa sintassi, vedere [tipi di dati &#40; Transact-SQL &#41; ](../../t-sql/data-types/data-types-transact-sql.md).  
  
-   Con valori di tabella o **cursore** tipi di dati non possono essere utilizzati come parametri.  
  
-   Se al parametro è stato assegnato un tipo di dati CLR definito dall'utente, è necessario disporre dell'autorizzazione EXECUTE per il tipo.  
  
VARYING  
 Specifica il set di risultati supportato come parametro di output. Questo parametro viene creato in modo dinamico dalla procedura e il relativo contenuto può variare. Si applica solo a **cursore** parametri. Questa opzione non è valida per le procedure CLR.  
  
*impostazione predefinita*  
 Valore predefinito per un parametro. Se un valore predefinito è definito per un parametro, è possibile eseguire la procedura senza specificare un valore per tale parametro. Il valore predefinito deve essere una costante oppure NULL. Il formato del valore della costante può essere un carattere jolly; in questo modo sarà possibile usare la parola chiave LIKE quando si passa il parametro nella procedura.   
  
 I valori predefiniti vengono registrati nella **sys** colonna solo per le procedure CLR. Tale colonna è NULL per [!INCLUDE[tsql](../../includes/tsql-md.md)] parametri di routine.  
  
OUT | OUTPUT  
 Indica che si tratta di un parametro di output. Utilizzare i parametri di output per restituire valori al chiamante della procedura. **testo**, **ntext**, e **immagine** parametri non possono essere utilizzati come parametri di OUTPUT, a meno che la procedura è una stored procedure CLR. Un parametro di output può essere un segnaposto del cursore, a meno che non si tratti di una procedura CLR. Un tipo di dati con valori di tabella non può essere specificato come parametro di output di una procedura.  
  
READONLY  
 Indica che il parametro non può essere aggiornato o modificato all'interno del corpo della procedura. Se si tratta di un tipo di parametro con valori di tabella, è necessario specificare la parola chiave READONLY.  
  
RECOMPILE  
 Indica che il [!INCLUDE[ssDE](../../includes/ssde-md.md)] non memorizzati nella cache un piano di query per questa procedura, imponendo che devono essere elaborate ogni volta che viene eseguita. Per ulteriori informazioni sui motivi della ricompilazione forzata, vedere [ricompilare una Stored Procedure](../../relational-databases/stored-procedures/recompile-a-stored-procedure.md). Questa opzione non può essere usata per procedure CLR o se si specifica FOR REPLICATION.  
  
 Per indicare il [!INCLUDE[ssDE](../../includes/ssde-md.md)] di ignorare i piani di query per le singole query all'interno di una stored procedure, utilizzare l'hint per la query RECOMPILE nella definizione della query. Per altre informazioni, vedere [Hint per la query &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md).  
  
ENCRYPTION  
 **Si applica a**: SQL Server ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Indica che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] converte il testo originale dell'istruzione CREATE PROCEDURE in un formato offuscato. L'output dell'offuscamento non è visibile direttamente nelle viste del catalogo in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il testo offuscato non può essere recuperato da utenti che non hanno accesso a file di database o tabelle di sistema. Tuttavia, il testo è disponibile per gli utenti con privilegi di accesso a tabelle di sistema tramite il [porta DAC](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md) o accesso diretto a file di database. Inoltre, agli utenti che possono collegare un debugger al processo del server è consentito recuperare la procedura decrittografata dalla memoria in fase di esecuzione. Per ulteriori informazioni sull'accesso ai metadati di sistema, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
 Questa opzione non è valida per le procedure CLR.  
  
 Le procedure create con questa opzione non possono essere pubblicate durante la replica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
EXECUTE AS *clausola*  
 Specifica il contesto di sicurezza in cui deve essere eseguita la procedura.  
  
 Stored procedure compilate in modo nativo, a partire [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], non sono previste limitazioni in EXECUTE AS clausola. In [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] il SELF, OWNER e *'user_name'* clausole sono supportate con le stored procedure compilate in modo nativo.  
  
 Per altre informazioni, vedere [Clausola EXECUTE AS &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md).  
  
FOR REPLICATION  
 **Si applica a**: SQL Server ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Specifica che la procedura viene creata per la replica. Di conseguenza, non può essere eseguita nel Sottoscrittore. Una procedura creata con l'opzione FOR REPLICATION viene usata come filtro di procedura ed eseguita solo durante la replica. Se viene specificata l'opzione FOR REPLICATION, non è possibile dichiarare alcun parametro. Inoltre, l'opzione FOR REPLICATION non può essere specificata per procedure CLR. L'opzione RECOMPILE viene ignorata per le procedure create con l'opzione FOR REPLICATION.  
  
 Oggetto `FOR REPLICATION` procedure è un tipo di oggetto **RF** in **Sys. Objects** e **Procedures**.  
  
 {[BEGIN] *sql_statement* [;] [ ...  *n*  ] [Fine]}  
 Una o più istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] che includono il corpo della procedura. Per racchiudere le istruzioni è possibile usare le parole chiave facoltative BEGIN ed END. Per informazioni, vedere le sezioni Procedure consigliate, Osservazioni generali e Limitazioni e restrizioni riportate di seguito.  
  
NOME esterno *nome_assembly***.** *class_name***.** *nome_metodo*  
 **Si applica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Specifica il metodo di un assembly [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] affinché una procedura CLR vi faccia riferimento. *CLASS_NAME* deve essere un valore valido [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] identificatore e deve esistere come classe nell'assembly. Se la classe dispone di un nome completo dello spazio dei nomi che utilizza un punto (**.**) per separare le varie parti dello spazio dei nomi, il nome della classe deve essere delimitato da parentesi quadre (**[]**) o virgolette (**""**). Il metodo specificato deve essere un metodo statico della classe.  
  
 Per impostazione predefinita, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non può eseguire il codice CLR. È possibile creare, modificare e rilasciare gli oggetti di database che fanno riferimento a moduli CLR; Tuttavia, non è possibile eseguire questi riferimenti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] finché non si abilita il [opzione clr enabled](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md). Per abilitare l'opzione, usare [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
> [!NOTE]  
>  Le procedure CLR non sono supportate in un database indipendente.  
  
ATOMIC WITH  
 **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Indica l'esecuzione atomica di stored procedure. Viene eseguito il commit delle modifiche o il rollback di tutte le modifiche tramite la generazione di un'eccezione. Il blocco ATOMIC WITH è obbligatorio per le stored procedure compilate in modo nativo.  
  
 Se la procedura esegue RETURN (in modo esplicito tramite l'istruzione RETURN o in modo implicito completando l'esecuzione), viene eseguito il commit del lavoro svolto dalla procedura. Se la procedura esegue THROW, viene eseguito il rollback del lavoro svolto dalla procedura.  
  
 XACT_ABORT è ON per impostazione predefinita in un blocco atomico e non può essere modificato. XACT_ABORT specifica se in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene eseguito automaticamente il rollback della transazione corrente quando un'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] genera un errore di run-time.  
  
 Le opzioni SET seguenti sono sempre impostate su ON nel blocco ATOMIC e non possono essere modificate.  
-   CONCAT_NULL_YIELDS_NULL  
-   QUOTED_IDENTIFIER, ARITHABORT  
-   NOCOUNT  
-   ANSI_NULLS  
-   ANSI_WARNINGS  
  
Le opzioni SET non possono essere modificate nei blocchi ATOMIC. Le opzioni SET della sessione utente non vengono usate nell'ambito delle stored procedure compilate in modo nativo. Queste opzioni vengono fissate in fase di compilazione.  
  
Le operazioni BEGIN, ROLLBACK e COMMIT non possono essere usate in un blocco atomico.  
  
 Esiste un solo blocco ATOMIC per stored procedure compilata in modo nativo, nell'ambito esterno della procedura. I blocchi non possono essere nidificati. Per ulteriori informazioni sui blocchi atomici, vedere [Natively Compiled Stored Procedures](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md).  
  
**NULL** | NON È NULL  
 Determina se i valori Null sono supportati in un parametro. Il valore predefinito è NULL.  
  
NATIVE_COMPILATION  
 **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Indica che la procedura è compilata in modo nativo. NATIVE_COMPILATION, SCHEMABINDING ed EXECUTE AS possono essere specificati in qualsiasi ordine. Per ulteriori informazioni, vedere [Natively Compiled Stored Procedures](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md).  
  
SCHEMABINDING  
 **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Assicura che le tabelle a cui si fa riferimento in una procedura non possano essere eliminate o modificate. SCHEMABINDING è obbligatorio nelle stored procedure compilate in modo nativo. (Per ulteriori informazioni, vedere [Natively Compiled Stored Procedures](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md).) Le restrizioni SCHEMABINDING sono uguali a quelle delle funzioni definite dall'utente. Per ulteriori informazioni, vedere la sezione SCHEMABINDING in [CREATE FUNCTION &#40; Transact-SQL &#41; ](../../t-sql/statements/create-function-transact-sql.md).  
  
LANGUAGE = [N] 'lingua'  
 **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Equivalente a [SET LANGUAGE &#40; Transact-SQL &#41; ](../../t-sql/statements/set-language-transact-sql.md) opzione della sessione. LANGUAGE = [N] 'lingua' è obbligatorio.  
  
TRANSACTION ISOLATION LEVEL  
 **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Obbligatorio per stored procedure compilate in modo nativo. Specifica il livello di isolamento della transazione della stored procedure. Sono disponibili le opzioni seguenti:  
  
 Per ulteriori informazioni su queste opzioni, vedere [SET TRANSACTION ISOLATION LEVEL &#40; Transact-SQL &#41; ](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md).  
  
REPEATABLE READ  
 Specifica che le istruzioni non possono leggere i dati modificati da altre transazioni, ma di cui non è ancora stato eseguito il commit. Se un'altra transazione modifica i dati letti dalla transazione corrente, la transazione corrente.  
  
SERIALIZABLE  
 Specifica quanto segue:  
-   Le istruzioni non possono leggere dati modificati da altre transazioni ma di cui non è ancora stato eseguito il commit.  
-   Se un'altra transazione modifica i dati letti dalla transazione corrente, la transazione corrente.  
-   Se un'altra transazione inserisce nuove righe con valori di chiave che rientrerebbero nell'intervallo di chiavi lette da qualsiasi istruzione nella transazione corrente, la transazione corrente.  
  
SNAPSHOT  
 Specifica che i dati letti da qualsiasi istruzione in una transazione sono la versione consistente dal punto di dati presenti all'inizio della transazione.  
  
DATEFIRST = *numero*  
 **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Specifica il primo giorno della settimana come numero compreso tra 1 e 7. DATEFIRST è facoltativo. Se viene omesso, l'impostazione viene desunta dalla lingua specificata.  
  
 Per ulteriori informazioni, vedere [SET DATEFIRST &#40; Transact-SQL &#41; ](../../t-sql/statements/set-datefirst-transact-sql.md).  
  
DATEFORMAT = *formato*  
 **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Specifica l'ordine delle parti della data relative a mese, giorno e anno per l'interpretazione di stringhe di caratteri date, smalldatetime, datetime, datetime2 e datetimeoffset. DATEFORMAT è facoltativo. Se viene omesso, l'impostazione viene desunta dalla lingua specificata.  
  
 Per ulteriori informazioni, vedere [SET DATEFORMAT &#40; Transact-SQL &#41; ](../../t-sql/statements/set-dateformat-transact-sql.md).  
  
DELAYED_DURABILITY = { OFF | ON }  
 **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Il commit delle transazioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può essere completamente durevole, ovvero l'impostazione predefinita di SQL Server, oppure con durabilità ritardata.  
  
 Per ulteriori informazioni, vedere [controllo della durabilità delle transazioni](../../relational-databases/logs/control-transaction-durability.md).  

## <a name="Simple"></a>Esempi semplici

Per iniziare, di seguito sono riportati due esempi rapidi:  
`SELECT DB_NAME() AS ThisDB;`Restituisce il nome del database corrente.  
È possibile eseguire il wrapping tale istruzione in una stored procedure, ad esempio:  
```sql  
CREATE PROC What_DB_is_this     
AS   
SELECT DB_NAME() AS ThisDB; 
```   
Chiamare la stored procedure con istruzione:`EXEC What_DB_is_this;`   

Leggermente più complessa, consiste nel fornire un parametro di input per rendere la procedura più flessibile. Esempio:  
```sql   
CREATE PROC What_DB_is_that @ID int   
AS    
SELECT DB_NAME(@ID) AS ThatDB;   
```   
Specificare un numero di id di database quando si chiama la routine. Ad esempio, `EXEC What_DB_is_that 2;` restituisce `tempdb`.   

Vedere [esempi](#Examples) verso la fine di questo argomento per ulteriori esempi.     
    
## <a name="best-practices"></a>Procedure consigliate  
 Sebbene non siano elencate tutte le procedure consigliate, questi suggerimenti possono migliorare le prestazioni della procedura.  
  
-   Usare l'istruzione SET NOCOUNT ON come prima istruzione nel corpo della procedura, ovvero posizionarla subito dopo la parola chiave AS. In questo modo vengono disabilitati i messaggi restituiti al client da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dopo l'esecuzione delle istruzioni SELECT, INSERT, UPDATE, MERGE e DELETE. Le prestazioni generali del database e dell'applicazione vengono migliorate eliminando questo overhead di rete. Per informazioni, vedere [SET NOCOUNT &#40; Transact-SQL &#41; ](../../t-sql/statements/set-nocount-transact-sql.md).  
  
-   Usare i nomi degli schemi quando si creano oggetti di database nella procedura o vi si fa riferimento. Richiede meno tempo di elaborazione il [!INCLUDE[ssDE](../../includes/ssde-md.md)] per risolvere i nomi di oggetto, se non dispone di più schemi di ricerca. Impedisce inoltre l'autorizzazione e i problemi di accesso causati da schema predefinito dell'utente viene assegnato quando vengono creati oggetti senza specificare lo schema.  
  
-   Evitare l'esecuzione del wrapping di funzioni attorno alle colonne specificate nelle clausole WHERE e JOIN. In tal modo le colonne vengono rese non deterministiche e si evita l'utilizzo di indici in Query Processor.  
  
-   Evitare l'utilizzo di funzioni scalari nelle istruzioni SELECT che restituiscono molte righe di dati. Poiché la funzione scalare deve essere applicata a ogni riga, il comportamento risultante assomiglia all'elaborazione basata su righe e ciò comporta un peggioramento delle prestazioni.  
  
-   Evitare l'utilizzo di `SELECT *`. Specificare invece i nomi delle colonne necessarie. In questo modo è possibile evitare alcuni errori del [!INCLUDE[ssDE](../../includes/ssde-md.md)] che causano l'arresto dell'esecuzione della procedura. Ad esempio, un `SELECT *` istruzione che restituisce dati da una tabella di 12 colonne e quindi tali dati vengono inseriti in una tabella temporanea di 12 colonne viene completata finché il numero o viene modificato l'ordine delle colonne delle tabelle.  
  
-   Evitare l'elaborazione o la restituzione di troppi dati. Non appena possibile, restringere i risultati nel codice della procedura in modo che le operazioni successive effettuate dalla procedura vengano eseguite usando il set di dati più piccolo possibile. Inviare solo i dati essenziali all'applicazione client. L'operazione è più efficace dell'invio di dati aggiuntivi nella rete, nonché dell'imposizione all'applicazione client di usare set di risultati inutilmente grandi.  
  
-   Utilizzare le transazioni esplicite tramite BEGIN/COMMIT della transazione e mantenere le transazioni più brevi possibili. Transazioni lunghe implicano un blocco dei record più lungo e un rischio maggiore di deadlock.  
  
-   Per la gestione degli errori all'interno di una procedura usare la funzionalità TRY…CATCH di [!INCLUDE[tsql](../../includes/tsql-md.md)] che consente di incapsulare un blocco intero di istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)]. In questo modo vengono garantiti un minor overhead delle prestazioni e una segnalazione errori più precisa con un utilizzo inferiore della programmazione.  
  
-   Usare la parola chiave DEFAULT in tutte le colonne della tabella a cui viene fatto riferimento dalle istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE TABLE o ALTER TABLE presenti nel corpo della procedura. In questo modo si impedisce il passaggio di NULL alle colonne che non ammettono valori null.  
  
-   Usare NULL o NOT NULL per ogni colonna di una tabella temporanea. Le opzioni ANSI_DFLT_ON e ANSI_DFLT_OFF consentono di controllare la modalità di assegnazione dell'attributo NULL o NOT NULL alle colonne da parte del [!INCLUDE[ssDE](../../includes/ssde-md.md)] quando tale attributo non è specificato in un'istruzione CREATE TABLE o ALTER TABLE. Se in una connessione viene eseguita una procedura con opzioni impostate in modo diverso rispetto alla connessione in cui la procedura è stata creata, è possibile che il supporto di valori Null e il funzionamento delle colonne della tabella creata per la seconda connessione siano diversi. Se l'attributo NULL o NOT NULL viene dichiarato in modo esplicito per ogni colonna, le tabelle temporanee vengono create con lo stesso supporto di valori Null per tutte le connessioni in cui viene eseguita la procedura.  
  
-   Usare le istruzioni di modifica che consentono di convertire i valori Null e in cui è inclusa la logica che permette di eliminare le righe con valori Null dalle query. Tenere presente che in [!INCLUDE[tsql](../../includes/tsql-md.md)], NULL non è vuota o valore "nothing". Si tratta di un segnaposto per un valore sconosciuto e può causare un comportamento imprevisto, soprattutto quando si eseguono query per set di risultati o si usano le funzioni di aggregazione.  
  
-   Usare l'operatore UNION ALL invece dell'operatore UNION oppure OR, a meno che non siano necessari valori distinct. L'operatore UNION ALL richiede un minor overhead di elaborazione poiché i duplicati non vengono esclusi dal set di risultati.  
  
## <a name="general-remarks"></a>Osservazioni generali  
 Non è prevista una dimensione massima predefinita per una procedura.  
  
 Le variabili specificate nella procedura possono essere definite dall'utente o variabili di sistema, ad esempio @@SPID.  
  
 Alla prima esecuzione, la procedura viene compilata in modo da determinare un piano di accesso ottimale per il recupero dei dati. Se il piano generato rimane archiviato nell'apposita cache del [!INCLUDE[ssDE](../../includes/ssde-md.md)], può essere riutilizzato nelle successive esecuzioni della procedura.  
  
 È possibile eseguire automaticamente una o più procedure all'avvio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Le procedure devono essere create dall'amministratore di sistema nel **master** database ed eseguite le **sysadmin** ruolo predefinito del server come un processo in background. In queste procedure non è possibile usare parametri di input o output. Per ulteriori informazioni, vedere [eseguire una Stored Procedure](../../relational-databases/stored-procedures/execute-a-stored-procedure.md).  
  
 Le procedure vengono nidificate quando una procedura consente la chiamata di un'altra o l'esecuzione di codice gestito facendo riferimento a una routine, un tipo o una funzione di aggregazione CLR. È possibile nidificare fino a 32 livelli di procedure e riferimenti a codice gestito. Il livello di nidificazione viene incrementato di un'unità quando viene avviata l'esecuzione della procedura o del riferimento al codice gestito chiamato e viene ridotto di un'unità quando ne viene completata l'esecuzione. I metodi richiamati all'interno del codice gestito non vengono inclusi nel limite del livello di nidificazione. Tuttavia, quando tramite una stored procedure CLR vengono eseguite operazioni di accesso ai dati tramite il provider gestito SQL Server, nel passaggio dal codice gestito a SQL viene aggiunto un ulteriore livello di nidificazione.  
  
 Il tentativo di superare il livello di nidificazione massimo causa l'esito negativo dell'intera catena di chiamata. È possibile utilizzare il @@NESTLEVEL funzione per restituire il livello di nidificazione dell'esecuzione della stored procedure corrente.  
  
## <a name="interoperability"></a>Interoperabilità  
 Quando viene creata o modificata una procedura [!INCLUDE[ssDE](../../includes/ssde-md.md)], nel [!INCLUDE[tsql](../../includes/tsql-md.md)] vengono salvate le impostazioni di entrambe le opzioni SET QUOTED_IDENTIFIER e SET ANSI_NULLS. Queste impostazioni originali vengono usate quando viene eseguita la procedura. Pertanto, le impostazioni di sessione del client per le opzioni SET QUOTED_IDENTIFIER e SET ANSI_NULLS vengono ignorate durante l'esecuzione della procedura.  
  
 Altre opzioni SET, ad esempio SET ARITHABORT, SET ANSI_WARNINGS o SET ANSI_PADDINGS, non vengono salvate quando viene creata o modificata una procedura. Se la logica della procedura dipende da una particolare impostazione, includere un'istruzione SET all'inizio della procedura per garantire l'utilizzo dell'impostazione adeguata. Quando un'istruzione SET viene eseguita da una procedura, l'impostazione rimane attiva solo fino al termine dell'esecuzione della procedura. L'impostazione viene quindi ripristinata al valore assegnato alla procedura quando è stata chiamata. In tal modo nei singoli client è possibile impostare le opzioni desiderate senza influire sulla logica della procedura.  
  
 In una procedura è possibile specificare qualsiasi istruzione SET, ad eccezione di SET SHOWPLAN_TEXT e SET SHOWPLAN_ALL. Queste devono essere le uniche istruzioni in un batch. L'opzione SET scelta rimane attiva durante l'esecuzione della procedura, dopodiché viene ripristinata l'impostazione precedente.  
  
> [!NOTE]  
>  SET_ANSI_WARNINGS non viene applicata quando vengono passati parametri in una procedura, in una funzione definita dall'utente oppure in caso di dichiarazione e impostazione delle variabili in un'istruzione batch. Ad esempio, se una variabile viene definita come **char**(3), quindi impostare un valore maggiore di tre caratteri, i dati vengono troncati alla dimensione definita e l'inserimento o istruzione di aggiornamento ha esito positivo.  
  
## <a name="limitations-and-restrictions"></a>Limitazioni e restrizioni  
 L'istruzione CREATE PROCEDURE non può essere usata in combinazione con altre istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] all'interno di un singolo batch.  
  
 Le istruzioni seguenti non possono essere usate in un qualsiasi punto del corpo di una stored procedure.  
  
||||  
|-|-|-|  
|CREATE AGGREGATE|CREATE SCHEMA|SET SHOWPLAN_TEXT|  
|CREATE DEFAULT|CREATE o ALTER TRIGGER|SET SHOWPLAN_XML|  
|CREATE o ALTER FUNCTION|CREATE o ALTER VIEW|Utilizzare *database_name*|  
|CREATE o ALTER PROCEDURE|SET PARSEONLY||  
|CREATE RULE|SET SHOWPLAN_ALL||  
  
 Una procedura può fare riferimento a tabelle che non esistono ancora. In fase di creazione viene eseguito solo un controllo della sintassi. La procedura non viene compilata fino alla prima esecuzione ed è solo durante la compilazione che vengono risolti tutti gli oggetti a cui viene fatto riferimento nella procedura. Pertanto, una procedura con sintassi corretta che fa riferimento a tabelle che non esistono possibile creata correttamente. Tuttavia, la procedura ha esito negativo in fase di esecuzione se le tabelle di riferimento non esiste.  
  
 Non è possibile specificare un nome di funzione come valore predefinito di un parametro o come valore passato a un parametro durante l'esecuzione di una procedura. Tuttavia, è possibile passare una funzione come variabile, come illustrato nell'esempio seguente.  
  
```  
-- Passing the function value as a variable.  
DECLARE @CheckDate datetime = GETDATE();  
EXEC dbo.uspGetWhereUsedProductID 819, @CheckDate;   
GO  
```  
  
 Se la procedura consente di apportare modifiche in un'istanza remota di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], non è possibile eseguire il rollback delle modifiche. Le procedure remote non partecipano alle transazioni.  
  
 Affinché il [!INCLUDE[ssDE](../../includes/ssde-md.md)] faccia riferimento al metodo corretto quando viene eseguito l'overload in .NET Framework, il metodo specificato nella clausola EXTERNAL NAME deve soddisfare i requisiti seguenti:  
  
-   Essere dichiarato come metodo statico.  
  
-   Ricevere lo stesso numero di parametri della procedura.  
  
-   Usare tipi di parametro compatibili con i tipi di dati dei parametri corrispondenti della procedura di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per informazioni sulla corrispondenza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipi di dati per il [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] tipi di dati, vedere [Mapping dei dati di parametro CLR](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md).  
  
## <a name="metadata"></a>Metadati  
 Nella tabella seguente sono elencate le viste del catalogo e le DMV utilizzabili per restituire informazioni sulle stored procedure.  
  
|Visualizza|Description|  
|----------|-----------------|  
|[sys.sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)|Viene restituita la definizione di una procedura [!INCLUDE[tsql](../../includes/tsql-md.md)]. Il testo di una procedura creata con l'opzione ENCRYPTION non può essere visualizzato utilizzando il **Sys. sql_modules** vista del catalogo.|  
|[sys.assembly_modules](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)|Vengono restituite informazioni su una procedura CLR.|  
|[sys.parameters](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)|Vengono restituite informazioni sui parametri definiti in una procedura.|  
|[Sys. sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) [Sys.dm sql_referenced_entities](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md) [Sys.dm sql_referencing_entities](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)|Vengono restituiti gli oggetti a cui una procedura fa riferimento.|  
  
 Per stimare le dimensioni di una procedura compilata, usare i seguenti contatori di Performance Monitor.  
  
|Nome dell'oggetto di Performance Monitor|Nome del contatore di Performance Monitor|  
|-------------------------------------|--------------------------------------|  
|SQLServer: Plan Cache Object|Percentuale riscontri cache|  
||Pagine cache|  
||Conteggio oggetti cache*|  
  
 * Questi contatori sono disponibili per diverse categorie di oggetti della cache incluse ad hoc [!INCLUDE[tsql](../../includes/tsql-md.md)], preparato [!INCLUDE[tsql](../../includes/tsql-md.md)], procedure, trigger e così via. Per ulteriori informazioni, vedere [SQL Server, pianificare oggetto Cache](../../relational-databases/performance-monitor/sql-server-plan-cache-object.md).  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>Permissions  
 Richiede **CREATE PROCEDURE** autorizzazione per il database e **ALTER** autorizzazione per lo schema in cui viene creata la procedura o richiede l'appartenenza di **db_ddladmin** ruolo predefinito del database.  
  
 Per le stored procedure CLR, è necessario essere proprietari dell'assembly a cui fa riferimento nella clausola EXTERNAL NAME o **riferimenti** autorizzazione tale assembly.  
  
##  <a name="mot"></a>CREARE PROCEDURE e tabelle con ottimizzazione per la memoria  
 Le tabelle con ottimizzazione per la memoria è possibile accedere tramite le stored procedure tradizionali e compilate in modo nativo. Procedure native sono nella maggior parte dei casi il modo più efficiente.
Per ulteriori informazioni, vedere [Natively Compiled Stored Procedures](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md).  
  
 L'esempio seguente viene illustrato come creare una stored procedure compilata in modo nativo che accede a una tabella con ottimizzazione per la memoria `dbo.Departments`:  
  
```sql  
CREATE PROCEDURE dbo.usp_add_kitchen @dept_id int, @kitchen_count int NOT NULL  
WITH EXECUTE AS OWNER, SCHEMABINDING, NATIVE_COMPILATION  
AS  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
  
  UPDATE dbo.Departments  
  SET kitchen_count = ISNULL(kitchen_count, 0) + @kitchen_count  
  WHERE id = @dept_id  
END;  
GO  
```  
  
 Una procedura creata senza NATIVE_COMPILATION non può essere modificata in una stored procedure compilata in modo nativo. 
  
 Per informazioni sulla programmabilità nelle stored procedure compilate in modo nativo, supportate della superficie di attacco di query e sugli operatori, vedere [funzionalità supportate per moduli T-SQL compilati in modo nativo](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md).  
  
## <a name="Examples"></a> Esempi  
  
|Category|Elementi di sintassi inclusi|  
|--------------|------------------------------|  
|[Sintassi di base](#BasicSyntax)|CREATE PROCEDURE|  
|[Passaggio di parametri](#Parameters)|@parameter <br> &nbsp;&nbsp;• = predefinito <br> &nbsp;&nbsp;• L'OUTPUT <br> &nbsp;&nbsp;tipo di parametro con valori di tabella • <br> &nbsp;&nbsp;• CURSOR VARYING.|  
|[Modifica dei dati tramite una stored procedure](#Modify)|UPDATE|  
|[Gestione degli errori](#Error)|TRY…CATCH|  
|[Offuscamento della definizione di procedure](#Encrypt)|WITH ENCRYPTION|  
|[Forzare la ricompilazione di stored Procedure](#Recompile)|WITH RECOMPILE|  
|[Impostazione del contesto di sicurezza](#Security)|EXECUTE AS|  
  
###  <a name="BasicSyntax"></a>Sintassi di base  
 Negli esempi contenuti in questa sezione vengono illustrate le funzionalità di base dell'istruzione CREATE PROCEDURE tramite la sintassi minima necessaria.  
  
#### <a name="a-creating-a-simple-transact-sql-procedure"></a>A. Creazione di una procedura Transact-SQL semplice  
 Nell'esempio seguente viene creata una stored procedure tramite cui vengono restituiti tutti i dipendenti (per cui vengono indicati il nome e il cognome), le relative posizioni e i nomi dei reparti di appartenenza da una vista nel database [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. In questa procedura non viene usato alcun parametro. Nell'esempio vengono quindi illustrati tre metodi di esecuzione della procedura.  
  
```sql  
CREATE PROCEDURE HumanResources.uspGetAllEmployees  
AS  
    SET NOCOUNT ON;  
    SELECT LastName, FirstName, JobTitle, Department  
    FROM HumanResources.vEmployeeDepartment;  
GO  
  
SELECT * FROM HumanResources.vEmployeeDepartment;  
```  
  
 Il `uspGetEmployees` procedure può essere eseguita nei modi seguenti:  
  
```sql  
EXECUTE HumanResources.uspGetAllEmployees;  
GO  
-- Or  
EXEC HumanResources.uspGetAllEmployees;  
GO  
-- Or, if this procedure is the first statement within a batch:  
HumanResources.uspGetAllEmployees;  
```  
  
#### <a name="b-returning-more-than-one-result-set"></a>B. Restituzione di più di un set di risultati  
 Tramite la procedura seguente vengono restituiti due set di risultati.  
  
```sql  
CREATE PROCEDURE dbo.uspMultipleResults   
AS  
SELECT TOP(10) BusinessEntityID, Lastname, FirstName FROM Person.Person;  
SELECT TOP(10) CustomerID, AccountNumber FROM Sales.Customer;  
GO  
```  
  
#### <a name="c-creating-a-clr-stored-procedure"></a>C. Creazione di una stored procedure CLR  
 Nell'esempio seguente viene creato il `GetPhotoFromDB` routine che fa riferimento il `GetPhotoFromDB` metodo il `LargeObjectBinary` classe nel `HandlingLOBUsingCLR` assembly. Prima della creazione, la procedura di `HandlingLOBUsingCLR` assembly viene registrato nel database locale.  
  
**Si applica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] (se si utilizza un assembly creato da *assembly_bits.*  
  
```sql  
CREATE ASSEMBLY HandlingLOBUsingCLR  
FROM '\\MachineName\HandlingLOBUsingCLR\bin\Debug\HandlingLOBUsingCLR.dll';  
GO  
CREATE PROCEDURE dbo.GetPhotoFromDB  
(  
    @ProductPhotoID int,  
    @CurrentDirectory nvarchar(1024),  
    @FileName nvarchar(1024)  
)  
AS EXTERNAL NAME HandlingLOBUsingCLR.LargeObjectBinary.GetPhotoFromDB;  
GO  
```  
  
###  <a name="Parameters"></a>Passaggio di parametri  
 Negli esempi di questa sezione viene illustrato l'utilizzo dei parametri di input e di output per il passaggio di valori a e da una stored procedure.  
  
#### <a name="d-creating-a-procedure-with-input-parameters"></a>D. Creazione di una procedura con parametri di input  
 Nell'esempio seguente viene creata una stored procedure tramite cui vengono restituite informazioni per un dipendente specifico passando i valori relativi al nome e al cognome del dipendente. In questa procedura vengono accettate solo corrispondenze esatte per i parametri passati.  
  
```sql  
IF OBJECT_ID ( 'HumanResources.uspGetEmployees', 'P' ) IS NOT NULL   
    DROP PROCEDURE HumanResources.uspGetEmployees;  
GO  
CREATE PROCEDURE HumanResources.uspGetEmployees   
    @LastName nvarchar(50),   
    @FirstName nvarchar(50)   
AS   
  
    SET NOCOUNT ON;  
    SELECT FirstName, LastName, JobTitle, Department  
    FROM HumanResources.vEmployeeDepartment  
    WHERE FirstName = @FirstName AND LastName = @LastName;  
GO  
  
```  
  
 Il `uspGetEmployees` procedure può essere eseguita nei modi seguenti:  
  
```  
EXECUTE HumanResources.uspGetEmployees N'Ackerman', N'Pilar';  
-- Or  
EXEC HumanResources.uspGetEmployees @LastName = N'Ackerman', @FirstName = N'Pilar';  
GO  
-- Or  
EXECUTE HumanResources.uspGetEmployees @FirstName = N'Pilar', @LastName = N'Ackerman';  
GO  
-- Or, if this procedure is the first statement within a batch:  
HumanResources.uspGetEmployees N'Ackerman', N'Pilar';  
  
```  
  
#### <a name="e-using-a-procedure-with-wildcard-parameters"></a>E. Utilizzo di una procedura con parametri di caratteri jolly  
 Nell'esempio seguente viene creata una stored procedure tramite cui vengono restituite informazioni per i dipendenti passando valori completi o parziali relativi al nome e al cognome dei dipendenti. Schema di questa procedura corrisponde ai parametri passati oppure, se non specificato, utilizza i valori predefiniti (cognomi che iniziano con la lettera `D`).  
  
```sql  
IF OBJECT_ID ( 'HumanResources.uspGetEmployees2', 'P' ) IS NOT NULL   
    DROP PROCEDURE HumanResources.uspGetEmployees2;  
GO  
CREATE PROCEDURE HumanResources.uspGetEmployees2   
    @LastName nvarchar(50) = N'D%',   
    @FirstName nvarchar(50) = N'%'  
AS   
    SET NOCOUNT ON;  
    SELECT FirstName, LastName, JobTitle, Department  
    FROM HumanResources.vEmployeeDepartment  
    WHERE FirstName LIKE @FirstName AND LastName LIKE @LastName;  
```  
  
 Il `uspGetEmployees2` procedura può essere eseguita in molte combinazioni. Di seguito sono riportate solo alcune delle combinazioni possibili.  
  
```sql  
EXECUTE HumanResources.uspGetEmployees2;  
-- Or  
EXECUTE HumanResources.uspGetEmployees2 N'Wi%';  
-- Or  
EXECUTE HumanResources.uspGetEmployees2 @FirstName = N'%';  
-- Or  
EXECUTE HumanResources.uspGetEmployees2 N'[CK]ars[OE]n';  
-- Or  
EXECUTE HumanResources.uspGetEmployees2 N'Hesse', N'Stefen';  
-- Or  
EXECUTE HumanResources.uspGetEmployees2 N'H%', N'S%';  
```  
  
#### <a name="f-using-output-parameters"></a>F. Utilizzo di parametri OUTPUT  
 Nell'esempio seguente viene creata la procedura `uspGetList`. che restituisce un elenco di prodotti il cui prezzo non supera un determinato importo. In questo esempio viene illustrato l'utilizzo di più istruzioni `SELECT` e di più parametri `OUTPUT`. I parametri OUTPUT consentono a una procedura esterna, un batch o più istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] di accedere a un valore impostato durante l'esecuzione della procedura.  
  
```sql  
IF OBJECT_ID ( 'Production.uspGetList', 'P' ) IS NOT NULL   
    DROP PROCEDURE Production.uspGetList;  
GO  
CREATE PROCEDURE Production.uspGetList @Product varchar(40)   
    , @MaxPrice money   
    , @ComparePrice money OUTPUT  
    , @ListPrice money OUT  
AS  
    SET NOCOUNT ON;  
    SELECT p.[Name] AS Product, p.ListPrice AS 'List Price'  
    FROM Production.Product AS p  
    JOIN Production.ProductSubcategory AS s   
      ON p.ProductSubcategoryID = s.ProductSubcategoryID  
    WHERE s.[Name] LIKE @Product AND p.ListPrice < @MaxPrice;  
-- Populate the output variable @ListPprice.  
SET @ListPrice = (SELECT MAX(p.ListPrice)  
        FROM Production.Product AS p  
        JOIN  Production.ProductSubcategory AS s   
          ON p.ProductSubcategoryID = s.ProductSubcategoryID  
        WHERE s.[Name] LIKE @Product AND p.ListPrice < @MaxPrice);  
-- Populate the output variable @compareprice.  
SET @ComparePrice = @MaxPrice;  
GO  
```  
  
 Eseguire `uspGetList` per restituire un elenco dei prodotti di [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] (biciclette) con un prezzo inferiore a `$700`. Il `OUTPUT` parametri `@Cost` e `@ComparePrices` vengono utilizzati con il linguaggio del flusso di controllo per restituire un messaggio nel **messaggi** finestra.  
  
> [!NOTE]  
>  La variabile OUTPUT deve essere definita sia quando viene creata la procedura che quando viene usata la variabile. Il nome del parametro e il nome di variabile non è necessario corrispondenti. Tuttavia, il tipo di dati e la posizione del parametro devono corrispondere, a meno che non `@ListPrice`  =  *variabile* viene utilizzato.  
  
```sql  
DECLARE @ComparePrice money, @Cost money ;  
EXECUTE Production.uspGetList '%Bikes%', 700,   
    @ComparePrice OUT,   
    @Cost OUTPUT  
IF @Cost <= @ComparePrice   
BEGIN  
    PRINT 'These products can be purchased for less than   
    $'+RTRIM(CAST(@ComparePrice AS varchar(20)))+'.'  
END  
ELSE  
    PRINT 'The prices for all products in this category exceed   
    $'+ RTRIM(CAST(@ComparePrice AS varchar(20)))+'.';  
```  
  
 Di seguito è riportato il set di risultati parziale:  
  
 ```   
 Product                     List Price  
 --------------------------  ----------  
 Road-750 Black, 58          539.99  
 Mountain-500 Silver, 40     564.99  
 Mountain-500 Silver, 42     564.99  
 ...  
 Road-750 Black, 48          539.99  
 Road-750 Black, 52          539.99  
   
 (14 row(s) affected)   
  
 These items can be purchased for less than $700.00.
 ```  
  
#### <a name="g-using-a-table-valued-parameter"></a>G. Utilizzo di un parametro con valori di tabella  
 Nell'esempio seguente viene usato un tipo di parametro con valori di tabella per inserire più righe in una tabella. Nell'esempio viene creato il tipo di parametro, viene dichiarata una variabile di tabella per farvi riferimento, viene riempito l'elenco di parametri e, successivamente, vengono passati i valori a una stored procedure, usati da quest'ultima per inserire più righe in una tabella.  
  
```sql  
/* Create a table type. */  
CREATE TYPE LocationTableType AS TABLE   
( LocationName VARCHAR(50)  
, CostRate INT );  
GO  
  
/* Create a procedure to receive data for the table-valued parameter. */  
CREATE PROCEDURE usp_InsertProductionLocation  
    @TVP LocationTableType READONLY  
    AS   
    SET NOCOUNT ON  
    INSERT INTO [AdventureWorks2012].[Production].[Location]  
           ([Name]  
           ,[CostRate]  
           ,[Availability]  
           ,[ModifiedDate])  
        SELECT *, 0, GETDATE()  
        FROM  @TVP;  
GO  
  
/* Declare a variable that references the type. */  
DECLARE @LocationTVP   
AS LocationTableType;  
  
/* Add data to the table variable. */  
INSERT INTO @LocationTVP (LocationName, CostRate)  
    SELECT [Name], 0.00  
    FROM   
    [AdventureWorks2012].[Person].[StateProvince];  
  
/* Pass the table variable data to a stored procedure. */  
EXEC usp_InsertProductionLocation @LocationTVP;  
GO  
```  
  
##### <a name="h-using-an-output-cursor-parameter"></a>H. Utilizzo di un parametro OUTPUT di tipo cursore  
 Nell'esempio seguente viene usato il parametro OUTPUT di tipo cursore per passare nuovamente al batch, alla procedura o al trigger chiamante un cursore locale rispetto a una procedura.  
  
 Creare innanzitutto la procedura che consente di dichiarare e, successivamente, di aprire un cursore nella tabella `Currency`:  
  
```sql  
CREATE PROCEDURE dbo.uspCurrencyCursor   
    @CurrencyCursor CURSOR VARYING OUTPUT  
AS  
    SET NOCOUNT ON;  
    SET @CurrencyCursor = CURSOR  
    FORWARD_ONLY STATIC FOR  
      SELECT CurrencyCode, Name  
      FROM Sales.Currency;  
    OPEN @CurrencyCursor;  
GO  
```  
  
 Eseguire quindi un batch che consente di dichiarare una variabile locale di cursore, di eseguire la procedura per assegnare il cursore alla variabile locale e, successivamente, di recuperare le righe dal cursore.  
  
```sql  
DECLARE @MyCursor CURSOR;  
EXEC dbo.uspCurrencyCursor @CurrencyCursor = @MyCursor OUTPUT;  
WHILE (@@FETCH_STATUS = 0)  
BEGIN;  
     FETCH NEXT FROM @MyCursor;  
END;  
CLOSE @MyCursor;  
DEALLOCATE @MyCursor;  
GO  
```  
  
###  <a name="Modify"></a>Modifica dei dati tramite una Stored Procedure  
 Negli esempi contenuti in questa sezione viene illustrato come inserire o modificare i dati di tabelle o viste includendo un'istruzione DML (Data Manipulation Language) nella definizione della procedura.  
  
#### <a name="i-using-update-in-a-stored-procedure"></a>I. Utilizzo di UPDATE in una stored procedure  
 Nell'esempio seguente viene usata un'istruzione UPDATE in una stored procedure. Per la stored procedure sono previsti un unico parametro di input `@NewHours` e un unico parametro di output `@RowCount`. Il `@NewHours` valore del parametro viene utilizzato nell'istruzione UPDATE per aggiornare la colonna `VacationHours` nella tabella `HumanResources.Employee`. Il parametro di output `@RowCount` viene usato per restituire il numero di righe interessate a una variabile locale. Un'espressione CASE viene usata nella clausola SET per determinare in modo condizionale il valore impostato per `VacationHours`. Quando un dipendente percepisce una paga oraria (`SalariedFlag` = 0), `VacationHours` viene impostato sul numero corrente di ore più il valore specificato in `@NewHours`. In caso contrario, `VacationHours` viene impostato sul valore specificato in `@NewHours`.  
  
```sql  
CREATE PROCEDURE HumanResources.Update_VacationHours  
@NewHours smallint  
AS   
SET NOCOUNT ON;  
UPDATE HumanResources.Employee  
SET VacationHours =   
    ( CASE  
         WHEN SalariedFlag = 0 THEN VacationHours + @NewHours  
         ELSE @NewHours  
       END  
    )  
WHERE CurrentFlag = 1;  
GO  
  
EXEC HumanResources.Update_VacationHours 40;  
```  
  
###  <a name="Error"></a>Gestione degli errori  
 Negli esempi contenuti in questa sezione vengono illustrati i metodi per gestire gli errori che potrebbero verificarsi durante l'esecuzione della stored procedure.  
  
#### <a name="j-using-trycatch"></a>J. Utilizzo di TRY…CATCH  
 Nell'esempio seguente viene illustrato l'utilizzo di un costrutto TRY…CATCH per restituire informazioni sugli errori rilevati durante l'esecuzione di una stored procedure.  
  
```sql  
CREATE PROCEDURE Production.uspDeleteWorkOrder ( @WorkOrderID int )  
AS  
SET NOCOUNT ON;  
BEGIN TRY  
   BEGIN TRANSACTION   
   -- Delete rows from the child table, WorkOrderRouting, for the specified work order.  
   DELETE FROM Production.WorkOrderRouting  
   WHERE WorkOrderID = @WorkOrderID;  
  
   -- Delete the rows from the parent table, WorkOrder, for the specified work order.  
   DELETE FROM Production.WorkOrder  
   WHERE WorkOrderID = @WorkOrderID;  
  
   COMMIT  
  
END TRY  
BEGIN CATCH  
  -- Determine if an error occurred.  
  IF @@TRANCOUNT > 0  
     ROLLBACK  
  
  -- Return the error information.  
  DECLARE @ErrorMessage nvarchar(4000),  @ErrorSeverity int;  
  SELECT @ErrorMessage = ERROR_MESSAGE(),@ErrorSeverity = ERROR_SEVERITY();  
  RAISERROR(@ErrorMessage, @ErrorSeverity, 1);  
END CATCH;  
  
GO  
EXEC Production.uspDeleteWorkOrder 13;  
  
/* Intentionally generate an error by reversing the order in which rows 
   are deleted from the parent and child tables. This change does not 
   cause an error when the procedure definition is altered, but produces 
   an error when the procedure is executed.  
*/  
ALTER PROCEDURE Production.uspDeleteWorkOrder ( @WorkOrderID int )  
AS  
  
BEGIN TRY  
   BEGIN TRANSACTION   
      -- Delete the rows from the parent table, WorkOrder, for the specified work order.  
   DELETE FROM Production.WorkOrder  
   WHERE WorkOrderID = @WorkOrderID;  
  
   -- Delete rows from the child table, WorkOrderRouting, for the specified work order.  
   DELETE FROM Production.WorkOrderRouting  
   WHERE WorkOrderID = @WorkOrderID;  
  
   COMMIT TRANSACTION  
  
END TRY  
BEGIN CATCH  
  -- Determine if an error occurred.  
  IF @@TRANCOUNT > 0  
     ROLLBACK TRANSACTION  
  
  -- Return the error information.  
  DECLARE @ErrorMessage nvarchar(4000),  @ErrorSeverity int;  
  SELECT @ErrorMessage = ERROR_MESSAGE(),@ErrorSeverity = ERROR_SEVERITY();  
  RAISERROR(@ErrorMessage, @ErrorSeverity, 1);  
END CATCH;  
GO  
-- Execute the altered procedure.  
EXEC Production.uspDeleteWorkOrder 15;  
  
DROP PROCEDURE Production.uspDeleteWorkOrder;  
```  
  
###  <a name="Encrypt"></a>Offuscamento della definizione di Procedure  
 Negli esempi contenuti in questa sezione viene illustrato come offuscare la definizione della stored procedure.  
  
#### <a name="k-using-the-with-encryption-option"></a>K. Utilizzo dell'opzione WITH ENCRYPTION  
 Nell'esempio seguente viene creata la procedura `HumanResources.uspEncryptThis`.  
  
**Si applica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], Database SQL.  
  
```sql  
CREATE PROCEDURE HumanResources.uspEncryptThis  
WITH ENCRYPTION  
AS  
    SET NOCOUNT ON;  
    SELECT BusinessEntityID, JobTitle, NationalIDNumber, 
        VacationHours, SickLeaveHours   
    FROM HumanResources.Employee;  
GO  
```  
  
 Il `WITH ENCRYPTION` opzione consente di offuscare la definizione della routine quando l'esecuzione di query nel catalogo di sistema o tramite i metadati funzioni, come illustrato negli esempi seguenti.  
  
 Run `sp_helptext`:  
  
```sql  
EXEC sp_helptext 'HumanResources.uspEncryptThis';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `The text for object 'HumanResources.uspEncryptThis' is encrypted.`  
  
 Eseguire una query direttamente il `sys.sql_modules` vista del catalogo:  
  
```sql  
SELECT definition FROM sys.sql_modules  
WHERE object_id = OBJECT_ID('HumanResources.uspEncryptThis');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 definition  
 --------------------------------  
 NULL  
 ```  
  
###  <a name="Recompile"></a>Forzare la ricompilazione di stored Procedure  
 Negli esempi contenuti in questa sezione viene usata la clausola WITH RECOMPILE per forzare la ricompilazione della procedura a ogni esecuzione.  
  
#### <a name="l-using-the-with-recompile-option"></a>L. Utilizzo dell'opzione WITH RECOMPILE  
 Il `WITH RECOMPILE` clausola è utile quando i parametri specificati per la procedura non sono tipici e quando un nuovo piano di esecuzione non deve essere memorizzato nella cache o archiviato in memoria.  
  
```sql  
IF OBJECT_ID ( 'dbo.uspProductByVendor', 'P' ) IS NOT NULL   
    DROP PROCEDURE dbo.uspProductByVendor;  
GO  
CREATE PROCEDURE dbo.uspProductByVendor @Name varchar(30) = '%'  
WITH RECOMPILE  
AS  
    SET NOCOUNT ON;  
    SELECT v.Name AS 'Vendor name', p.Name AS 'Product name'  
    FROM Purchasing.Vendor AS v   
    JOIN Purchasing.ProductVendor AS pv   
      ON v.BusinessEntityID = pv.BusinessEntityID   
    JOIN Production.Product AS p   
      ON pv.ProductID = p.ProductID  
    WHERE v.Name LIKE @Name;  
```  
  
###  <a name="Security"></a>Impostazione del contesto di sicurezza  
 Negli esempi contenuti in questa sezione viene usata la clausola EXECUTE AS per impostare il contesto di sicurezza in cui viene eseguita la stored procedure.  
  
#### <a name="m-using-the-execute-as-clause"></a>M. Utilizzo della clausola EXECUTE AS  
 Nell'esempio seguente viene illustrato l'utilizzo di [EXECUTE AS](../../t-sql/statements/execute-as-clause-transact-sql.md) clausola per specificare il contesto di sicurezza in cui è possibile eseguire una stored procedure. Nell'esempio, l'opzione `CALLER` specifica che la procedura può essere eseguita nel contesto dell'utente che lo chiama.  
  
```sql  
CREATE PROCEDURE Purchasing.uspVendorAllInfo  
WITH EXECUTE AS CALLER  
AS  
    SET NOCOUNT ON;  
    SELECT v.Name AS Vendor, p.Name AS 'Product name',   
      v.CreditRating AS 'Rating',   
      v.ActiveFlag AS Availability  
    FROM Purchasing.Vendor v   
    INNER JOIN Purchasing.ProductVendor pv  
      ON v.BusinessEntityID = pv.BusinessEntityID   
    INNER JOIN Production.Product p  
      ON pv.ProductID = p.ProductID   
    ORDER BY v.Name ASC;  
GO  
```  
  
#### <a name="n-creating-custom-permission-sets"></a>N. Creazione di set di autorizzazioni personalizzate  
 Nell'esempio seguente viene usata la clausola EXECUTE AS per creare autorizzazioni personalizzate per un'operazione sul database. Per alcune operazioni, ad esempio TRUNCATE TABLE, non è possibile concedere le autorizzazioni. Incorporando l'istruzione TRUNCATE TABLE in una stored procedure e specificando che tale procedura venga eseguita come un utente che dispone di autorizzazioni per la modifica della tabella è possibile estendere le autorizzazioni per il troncamento della tabella all'utente al quale si concedono le autorizzazioni EXECUTE sulla procedura.  
  
```sql  
CREATE PROCEDURE dbo.TruncateMyTable  
WITH EXECUTE AS SELF  
AS TRUNCATE TABLE MyDB..MyTable;  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Esempi: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="o-create-a-stored-procedure-that-runs-a-select-statement"></a>O. Creare una Stored Procedure che esegue un'istruzione SELECT  
 Questo esempio mostra la sintassi di base per la creazione e l'esecuzione di una routine. Quando si esegue un batch, CREATE PROCEDURE deve essere la prima istruzione. Ad esempio, per creare la seguente stored procedure in [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)], prima di impostare il contesto del database e quindi eseguire l'istruzione CREATE PROCEDURE.  
  
```sql  
-- Uses AdventureWorksDW database  
  
--Run CREATE PROCEDURE as the first statement in a batch.  
CREATE PROCEDURE Get10TopResellers   
AS   
BEGIN  
    SELECT TOP (10) r.ResellerName, r.AnnualSales  
    FROM DimReseller AS r  
    ORDER BY AnnualSales DESC, ResellerName ASC;  
END  
;  
  
--Show 10 Top Resellers  
EXEC Get10TopResellers;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [ALTER PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-procedure-transact-sql.md)   
 [Il controllo di flusso Language &#40; Transact-SQL &#41;](~/t-sql/language-elements/control-of-flow.md)   
 [Cursori](../../relational-databases/cursors.md)   
 [Tipi di dati &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [DROP PROCEDURE &#40; Transact-SQL &#41;](../../t-sql/statements/drop-procedure-transact-sql.md)   
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [ESEGUIRE AS &#40; Transact-SQL &#41;](../../t-sql/statements/execute-as-transact-sql.md)   
 [Stored procedure &#40;Motore di database&#41;](../../relational-databases/stored-procedures/stored-procedures-database-engine.md)   
 [sp_procoption &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-procoption-transact-sql.md)   
 [sp_recompile &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-recompile-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)   
 [sys.procedures &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-procedures-transact-sql.md)   
 [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)   
 [sys.assembly_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)   
 [numbered_procedures &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-numbered-procedures-transact-sql.md)   
 [numbered_procedure_parameters &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-numbered-procedure-parameters-transact-sql.md)   
 [OBJECT_DEFINITION &#40;Transact-SQL&#41;](../../t-sql/functions/object-definition-transact-sql.md)   
 [Creazione di una stored procedure](../../relational-databases/stored-procedures/create-a-stored-procedure.md)   
 [Utilizzare i valori di tabella parametri &#40; motore di Database &#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)   
 [sys.dm_sql_referenced_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)   
 [sys.dm_sql_referencing_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)  
  
  



