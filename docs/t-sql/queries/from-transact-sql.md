---
title: FROM (Transact-SQL) | Documenti Microsoft
ms.custom:
- SQL2016_New_Updated
ms.date: 08/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- JOIN
- FROM_TSQL
- FROM
- JOIN_TSQL
- CROSS_TSQL
- CROSS_APPLY_TSQL
- APPLY_TSQL
- CROSS_JOIN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- OUTER APPLY operator
- hints [SQL Server], FROM clause
- SELECT statement [SQL Server], FROM clause
- ISO syntax
- DELETE statement [SQL Server], FROM clause
- CROSS APPLY operator
- FROM clause
- APPLY operator
- joins [SQL Server], FROM clause
- UPDATE statement [SQL Server], FROM clause
- derived tables
ms.assetid: 36b19e68-94f6-4539-aeb1-79f5312e4263
caps.latest.revision: 97
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 03f3352a494bef2072ca7527dd3da804a072689e
ms.contentlocale: it-it
ms.lasthandoff: 09/01/2017

---
# <a name="from-transact-sql"></a>FROM (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Specifica le tabelle, le viste, le tabelle derivate e le tabelle unite in join utilizzate nelle istruzioni DELETE, SELECT e UPDATE in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Nell'istruzione SELECT la clausola FROM è obbligatoria, tranne nel caso in cui l'elenco di selezione includa solo costanti, variabili ed espressioni aritmetiche (non nomi di colonna).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
[ FROM { <table_source> } [ ,...n ] ]   
<table_source> ::=   
{  
    table_or_view_name [ [ AS ] table_alias ]   
        [ <tablesample_clause> ]   
        [ WITH ( < table_hint > [ [ , ]...n ] ) ]   
    | rowset_function [ [ AS ] table_alias ]   
        [ ( bulk_column_alias [ ,...n ] ) ]   
    | user_defined_function [ [ AS ] table_alias ]  
    | OPENXML <openxml_clause>   
    | derived_table [ [ AS ] table_alias ] [ ( column_alias [ ,...n ] ) ]   
    | <joined_table>   
    | <pivoted_table>   
    | <unpivoted_table>  
    | @variable [ [ AS ] table_alias ]  
    | @variable.function_call ( expression [ ,...n ] )   
        [ [ AS ] table_alias ] [ (column_alias [ ,...n ] ) ]  
    | FOR SYSTEM_TIME <system_time>   
}  
<tablesample_clause> ::=  
    TABLESAMPLE [SYSTEM] ( sample_number [ PERCENT | ROWS ] )   
        [ REPEATABLE ( repeat_seed ) ]   
  
<joined_table> ::=   
{  
    <table_source> <join_type> <table_source> ON <search_condition>   
    | <table_source> CROSS JOIN <table_source>   
    | left_table_source { CROSS | OUTER } APPLY right_table_source   
    | [ ( ] <joined_table> [ ) ]   
}  
<join_type> ::=   
    [ { INNER | { { LEFT | RIGHT | FULL } [ OUTER ] } } [ <join_hint> ] ]  
    JOIN  
  
<pivoted_table> ::=  
    table_source PIVOT <pivot_clause> [ [ AS ] table_alias ]  
  
<pivot_clause> ::=  
        ( aggregate_function ( value_column [ [ , ]...n ])   
        FOR pivot_column   
        IN ( <column_list> )   
    )   
  
<unpivoted_table> ::=  
    table_source UNPIVOT <unpivot_clause> [ [ AS ] table_alias ]  
  
<unpivot_clause> ::=  
    ( value_column FOR pivot_column IN ( <column_list> ) )   
  
<column_list> ::=  
    column_name [ ,...n ]   
  
<system_time> ::=  
{  
       AS OF <date_time>  
    |  FROM <start_date_time> TO <end_date_time>  
    |  BETWEEN <start_date_time> AND <end_date_time>  
    |  CONTAINED IN (<start_date_time> , <end_date_time>)   
    |  ALL  
}  
  
    <date_time>::=  
        <date_time_literal> | @date_time_variable  
  
    <start_date_time>::=  
        <date_time_literal> | @date_time_variable  
  
    <end_date_time>::=  
        <date_time_literal> | @date_time_variable  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
FROM { <table_source> [ ,...n ] }  
  
<table_source> ::=   
{  
    [ database_name . [ schema_name ] . | schema_name . ] table_or_view_name [ AS ] table_or_view_alias  
    | derived_table [ AS ] table_alias [ ( column_alias [ ,...n ] ) ]  
    | <joined_table>  
}  
  
<joined_table> ::=   
{  
    <table_source> <join_type> <table_source> ON search_condition   
    | <table_source> CROSS JOIN <table_source> 
    | left_table_source { CROSS | OUTER } APPLY right_table_source   
    | [ ( ] <joined_table> [ ) ]   
}  
  
<join_type> ::=   
    [ INNER ] [ <join hint> ] JOIN  
    | LEFT  [ OUTER ] JOIN  
    | RIGHT [ OUTER ] JOIN  
    | FULL  [ OUTER ] JOIN  
  
<join_hint> ::=   
    REDUCE  
    | REPLICATE  
    | REDISTRIBUTE  
```  
  
## <a name="arguments"></a>Argomenti  
\<table_source >  
 Specifica una tabella, vista, variabile di tabella o origine di tabella derivata con o senza un alias, da utilizzare nell'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)]. In un'istruzione sono consentite fino a 256 origini di tabella. Il limite varia tuttavia in base alla memoria disponibile e alla complessità delle altre espressioni nella query, ovvero alcune query specifiche potrebbero non supportare 256 origini di tabella.  
  
> [!NOTE]  
>  Nelle query con riferimenti a molte tabelle le prestazioni di esecuzione potrebbero essere ridotte. I tempi di compilazione e ottimizzazione vengono influenzati anche da fattori aggiuntivi, Queste includono la presenza di indici e viste indicizzate in ogni \<table_source > e la dimensione del \<select_list > nell'istruzione SELECT.  
  
 L'ordine delle origini di tabella dopo la parola chiave FROM non influisce sul set di risultati restituito. Quando la clausola FROM include nomi duplicati, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituisce un errore.  
  
 *table_or_view_name*  
 Nome di una tabella o di una vista.  
  
 Se la tabella o vista è presente in un altro database nella stessa istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], specificare un nome completo nel formato *database*. *schema*. *object_name*.  
  
 Se la tabella o vista è presente all'esterno dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]l, specificare un nome composto da quattro parti nel formato *server_collegato*. *catalogo*. *schema*. *oggetto*. Per altre informazioni, vedere [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md). Un nome composto da quattro parti costruito utilizzando il [OPENDATASOURCE](../../t-sql/functions/opendatasource-transact-sql.md) funziona come la parte del nome server può essere utilizzata anche per specificare l'origine della tabella remota. Quando viene specificato OPENDATASOURCE, *database_name* e *schema_name* potrebbe non essere applicabile a tutte le origini dati ed è soggetta alle funzionalità del provider OLE DB che accede all'oggetto remoto.  
  
 [COME] *table_alias*  
 È un alias per *table_source* che può essere utilizzato per convenienza o per contraddistinguere una tabella o vista in un self join o una sottoquery. Un alias è spesso un nome di tabella abbreviato utilizzato per fare riferimento a colonne specifiche delle tabelle di un join. Se lo stesso nome di colonna è presente in più di una tabella del join, in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è necessario qualificarlo con un nome di tabella o di vista oppure con un alias. Se viene definito un alias, non è possibile utilizzare il nome di tabella.  
  
 Quando viene utilizzata una tabella derivata, set di righe o funzione con valori di tabella o nella clausola di operatore (ad esempio PIVOT o UNPIVOT), la *table_alias* alla fine della clausola è il nome della tabella associata per tutte le colonne, incluse le colonne di raggruppamento restituito.  
  
 CON (\<table_hint >)  
 Specifica che Query Optimizer utilizza una strategia di ottimizzazione o di blocco con questa tabella e per questa istruzione. Per altre informazioni, vedere [Hint di tabella &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md).  
  
 *rowset_function*  

**Si applica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  

  
 Specifica una delle funzioni per i set di righe, ad esempio OPENROWSET, che restituisce un oggetto che è possibile utilizzare in sostituzione di un riferimento alla tabella. Per ulteriori informazioni su un elenco di funzioni di set di righe, vedere [funzioni Rowset &#40; Transact-SQL &#41; ](../../t-sql/functions/rowset-functions-transact-sql.md).  
  
 L'utilizzo delle funzioni OPENROWSET e OPENQUERY per specificare un oggetto remoto dipende dalle funzionalità del provider OLE DB che accede all'oggetto.  
  
 *bulk_column_alias*  

**Si applica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  

  
 Alias facoltativo da utilizzare in sostituzione del nome di colonna nel set di risultati. Gli alias di colonna sono consentiti solo nelle istruzioni SELECT che utilizzano la funzione OPENROWSET con l'opzione BULK. Quando si utilizza *bulk_column_alias*, specificare un alias per ogni colonna della tabella nello stesso ordine delle colonne nel file.  
  
> [!NOTE]  
>  Questo alias esegue l'override dell'attributo NAME negli elementi COLUMN di un file in formato XML, se presente.  
  
 *user_defined_function*  
 Specifica una funzione con valori di tabella.  
  
 OPENXML \<openxml_clause >  

**Si applica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  

  
 Consente di visualizzare un documento XML come set di righe. Per ulteriori informazioni, vedere [OPENXML &#40; Transact-SQL &#41; ](../../t-sql/functions/openxml-transact-sql.md).  
  
 *argomento derived_table*  
 Sottoquery che recupera le righe dal database. *l'argomento derived_table* viene utilizzato come input per la query esterna.  
  
 *derivato* *Table* possibile utilizzare il [!INCLUDE[tsql](../../includes/tsql-md.md)] funzionalità costruttore valore di tabella per specificare più righe. Ad esempio, `SELECT * FROM (VALUES (1, 2), (3, 4), (5, 6), (7, 8), (9, 10) ) AS MyTable(a, b);`. Per ulteriori informazioni, vedere [il costruttore di valori di tabella &#40; Transact-SQL &#41; ](../../t-sql/queries/table-value-constructor-transact-sql.md).  
  
 *column_alias*  
 Alias facoltativo da utilizzare in sostituzione del nome di colonna nel set di risultati della tabella derivata. Includere un alias di colonna per ogni colonna nell'elenco di selezione e racchiudere tra parentesi l'intero elenco di alias di colonna.  
  
 *table_or_view_name* FOR SYSTEM_TIME \<system_time >  

**Si applica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  

  
 Specifica che la tabella temporale specificata e la relativa tabella di cronologia delle versioni di sistema collegato viene restituita una versione specifica di dati  
  
\<tablesample_clause >  
 Specifica che vengono restituiti dati di esempio dalla tabella. I dati di esempio possono essere approssimativi. Questa clausola può essere utilizzata in ogni tabella primaria o unita in join in un'istruzione SELECT, UPDATE o DELETE. Non è possibile specificare TABLESAMPLE con le viste.  
  
> [!NOTE]  
>  Quando si utilizza TABLESAMPLE sui database aggiornati a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il livello di compatibilità del database viene impostato su 110 o su un valore maggiore. L'operatore PIVOT non è consentito in una query ricorsiva dell'espressione di tabella comune. Per altre informazioni, vedere [Livello di compatibilità ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
 SYSTEM  
 Metodo di campionamento dipendente dall'implementazione specificato dagli standard ISO. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è l'unico metodo di campionamento disponibile e viene applicato per impostazione predefinita. SYSTEM applica un metodo di campionamento basato su pagine in cui come campione viene scelto un set di pagine casuale dalla tabella e tutte le righe di tali pagine vengono restituite come subset campione.  
  
 *sample_number*  
 Espressione numerica costante esatta o approssimativa che rappresenta la percentuale o il numero delle righe. Quando viene specificato con PERCENT, *sample_number* viene implicitamente convertito in un **float** valore; in caso contrario, viene convertito in **bigint**. PERCENT è l'impostazione predefinita.  
  
 PERCENT  
 Specifica che un *sample_number* percento delle righe della tabella deve essere recuperati dalla tabella. Quando viene specificato PERCENT, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituisce un valore approssimativo della percentuale specificata. Quando viene specificato PERCENT il *sample_number* espressione deve restituire un valore compreso tra 0 e 100.  
  
 ROWS  
 Specifica che circa *sample_number* di righe verranno recuperate. Quando viene specificato ROWS, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituisce un'approssimazione del numero di righe specificato. Quando viene specificato ROWS, il *sample_number* espressione deve restituire un valore intero maggiore di zero.  
  
 REPEATABLE  
 Indica che il campione selezionato può essere restituito nuovamente. Quando viene specificato con lo stesso *repeat_seed* valore [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituirà lo stesso subset di righe fino a quando non sono state apportate modifiche alle righe nella tabella. Quando viene specificato con un altro *repeat_seed* valore [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verrà restituisce verosimilmente un campione diverso delle righe nella tabella. Le azioni seguenti nella tabella vengono considerate modifiche: inserimento, aggiornamento, eliminazione, ricompilazione o deframmentazione dell'indice e ripristino o collegamento del database.  
  
 *repeat_seed*  
 Espressione di tipo integer costante utilizzata da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per generare un numero casuale. *repeat_seed* è **bigint**. Se *repeat_seed* non viene specificato, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assegna un valore in modo casuale. Per uno specifico *repeat_seed* valore, il risultato del campionamento è sempre lo stesso se delle modifiche sono state applicate alla tabella. Il *repeat_seed* espressione deve restituire un numero intero maggiore di zero.  
  
 \<joined_table >  
 Set di risultati che rappresenta il prodotto di due o più tabelle. In caso di più join, utilizzare le parentesi per modificarne l'ordine standard.  
  
\<tipo di join >  
 Specifica il tipo di operazione di join.  
  
 **INTERNA**  
 Specifica che vengono restituite tutte le coppie di righe corrispondenti. Le righe senza corrispondenza vengono eliminate da entrambe le tabelle. Corrisponde al valore predefinito se non viene specificato alcun tipo di join.  
  
 FULL [OUTER]  
 Specifica che una riga della tabella di destra o di sinistra che non rispetta la condizione di join è inclusa nel set di risultati e le colonne di output che corrispondono all'altra tabella sono impostate su NULL. Questa si aggiunge a tutte le righe normalmente restituite dall'INNER JOIN.  
  
 LEFT [OUTER]  
 Specifica che, oltre alle righe restituite dall'inner join, vengono incluse nel set di risultati tutte le righe della tabella sinistra che non rispettano la condizione di join e le colonne di output dell'altra tabella sono impostate su NULL.  
  
 RIGHT [OUTER]  
 Specifica che, oltre alle righe restituite dall'inner join, vengono incluse nel set di risultati tutte le righe della tabella destra che non rispettano le condizioni di join e le colonne di output che corrispondono all'altra tabella sono impostate su NULL.  
  
\<join_hint >  
 Per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[ssSDS](../../includes/sssds-md.md)], specifica che il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] query optimizer utilizza un hint di join, o algoritmo di esecuzione, per ogni join specificato nella clausola FROM della query. Per ulteriori informazioni, vedere [hint di Join &#40; Transact-SQL &#41; ](../../t-sql/queries/hints-transact-sql-join.md).  
  
 Per [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], si applicano questi hint di join INNER join in due colonne non compatibile di distribuzione. È possibile migliorare le prestazioni di query per limitare la quantità di spostamento dei dati che si verifica durante l'elaborazione delle query. Gli hint di join consentiti per [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] sono i seguenti:  
  
 RIDURRE  
 Consente di ridurre il numero di righe da spostare per la tabella sul lato destro del join per rendere compatibili due tabelle non compatibile di distribuzione. Un hint semi-join è l'acronimo di all'hint REDUCE.  
  
 REPLICATE  
 Fa sì che i valori nella colonna di join della tabella sul lato sinistro del join devono essere replicate in tutti i nodi. La tabella di destra viene unita alla versione di tali colonne replicata.  
  
 RIDISTRIBUIRE  
 Origini dati forza due verranno distribuite nelle colonne specificate nella clausola JOIN. Per una tabella distribuita, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] esegue uno spostamento casuale. Per una tabella replicata, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] esegue uno spostamento di taglio. Per comprendere questi tipi di spostamento, vedere la sezione "DMS pianificare le operazioni di Query" nell'argomento "Informazioni sui piani di Query" il [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]. Questo hint può migliorare le prestazioni quando il piano di query utilizza uno spostamento di trasmissione per risolvere un join non compatibile di distribuzione.  
  
 JOIN  
 Indica che l'operazione di join specificata deve essere eseguita tra le viste o le origini di tabella specificate.  
  
 ON \<search_condition >  
 Specifica la condizione su cui è basato il join. La condizione può includere qualsiasi predicato, ma vengono in genere utilizzati nomi di colonne e operatori di confronto, ad esempio:  
  
```tsql
SELECT p.ProductID, v.BusinessEntityID  
FROM Production.Product AS p   
JOIN Purchasing.ProductVendor AS v  
ON (p.ProductID = v.ProductID);  
  
```  
  
 Quando nella condizione sono specificate le colonne, non è necessario che queste abbiano lo stesso nome o lo stesso tipo di dati. Se tuttavia i tipi di dati sono diversi, è necessario che siano compatibili o supportino la conversione implicita in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se non è possibile eseguire una conversione implicita dei tipi di dati, la condizione deve convertire in modo esplicito il tipo di dati tramite la funzione CONVERT.  
  
 È possibile che alcuni predicati includano una sola delle tabelle unite in join nella clausola ON. Tali predicati potrebbero essere presenti inoltre nella clausola WHERE della query. La posizione di tali predicati non è rilevante nel caso di INNER join, ma potrebbe generare risultati diversi se vengono utilizzati OUTER join. I predicati inclusi nella clausola ON infatti vengono applicati alla tabella prima dell'esecuzione del join, mentre la clausola WHERE viene applicata semanticamente ai risultati del join.  
  
 Per ulteriori informazioni sulle condizioni di ricerca e predicati, vedere [condizione di ricerca &#40; Transact-SQL &#41; ](../../t-sql/queries/search-condition-transact-sql.md).  
  
 CROSS JOIN  
 Specifica il prodotto incrociato di due tabelle. Restituisce le righe che verrebbero restituite se non fosse specificata alcuna clausola WHERE in un join obsoleto, non SQL-92.  
  
 *left_table_source* {CROSS | OUTER} APPLY *right_table_source*  
 Specifica che il *right_table_source* di applica l'operatore viene valutato rispetto a ogni riga del *left_table_source*. Questa funzionalità è utile quando il *right_table_source* contiene una funzione con valori di tabella che accetta i valori della colonna di *left_table_source* come uno dei relativi argomenti.  
  
 È necessario specificare CROSS o OUTER con APPLY. Se si specifica CROSS, non vengono restituite righe quando il *right_table_source* viene valutato rispetto a una riga specificata del *left_table_source* e restituisce un set di risultati vuoto.  
  
 Se si specifica OUTER, viene generata una riga per ogni riga del *left_table_source* anche quando il *right_table_source* valuta in base a tale riga e restituisce un set di risultati vuoto.  
  
 Per altre informazioni, vedere la sezione Osservazioni.  
  
 *left_table_source*  
 Origine di tabella definita nell'argomento precedente. Per altre informazioni, vedere la sezione Osservazioni.  
  
 *right_table_source*  
 Origine di tabella definita nell'argomento precedente. Per altre informazioni, vedere la sezione Osservazioni.  
  
 *table_source* PIVOT \<pivot_clause >  
 Specifica che il *table_source* viene trasformata tramite pivot in base il *pivot_column*. *table_source* è una tabella o espressione di tabella. L'output è una tabella che contiene tutte le colonne di *table_source* ad eccezione di *pivot_column* e *value_column*. Le colonne di *table_source*, ad eccezione di *pivot_column* e *value_column*, sono definite colonne di raggruppamento dell'operatore pivot. Per ulteriori informazioni su PIVOT e UNPIVOT, vedere [tramite PIVOT e UNPIVOT](../../t-sql/queries/from-using-pivot-and-unpivot.md).  
  
 PIVOT esegue un'operazione di raggruppamento sulla tabella di input relativamente alle colonne di raggruppamento e restituisce una riga per ogni gruppo. Inoltre, l'output contiene una colonna per ogni valore specificato nel *column_list* che compare nella *pivot_column* del *input_table*.  
  
 Per ulteriori informazioni, vedere la sezione Osservazioni riportata di seguito.  
  
 *funzione_aggregata*  
 Funzione di aggregazione di sistema o definita dall'utente che accetta uno o più input. La funzione di aggregazione deve essere invariante rispetto ai valori Null. Una funzione di aggregazione invariante rispetto ai valori Null non considera i valori Null nel gruppo mentre valuta il valore di aggregazione.  
  
 La funzione di aggregazione di sistema COUNT(*) non è consentita.  
  
 *value_column*  
 Indica la colonna dei valori dell'operatore PIVOT. Se utilizzato con UNPIVOT, *value_column* non può essere il nome di una colonna esistente nell'input *table_source*.  
  
 PER *pivot_column*  
 Colonna pivot dell'operatore PIVOT. *pivot_column* deve essere di un tipo convertibile in modo implicito o esplicito in **nvarchar()**. Questa colonna non può essere **immagine** o **rowversion**.  
  
 Quando viene utilizzato UNPIVOT, *pivot_column* è il nome della colonna di output risultante dal raggruppamento di *table_source*. Non possono essere presenti una colonna esistente in *table_source* con lo stesso nome.  
  
 IN (*column_list* )  
 Nella clausola PIVOT Elenca i valori di *pivot_column* che diventeranno i nomi delle colonne della tabella di output. L'elenco non è possibile specificare nomi di colonna già presenti nell'input *table_source* che viene trasformata tramite pivot.  
  
 Nella clausola UNPIVOT Elenca le colonne in *table_source* che verranno raggruppate in un unico *pivot_column*.  
  
 *table_alias*  
 Nome dell'alias della tabella di output. *pivot_table_alias* deve essere specificato.  
  
 UNPIVOT \< unpivot_clause >  
 Specifica che la tabella di input viene ridotta da più colonne in *column_list* in una singola colonna denominata *pivot_column*. Per ulteriori informazioni su PIVOT e UNPIVOT, vedere [tramite PIVOT e UNPIVOT](../../t-sql/queries/from-using-pivot-and-unpivot.md).  
  
 A partire dal \<data_ora >  

**Si applica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  

  
 Restituisce una tabella con un singolo record per ogni riga contenente i valori che erano effettivi (correnti) in un momento specificato nel passato. Internamente, viene eseguita un'unione tra la tabella temporale e la relativa tabella di cronologia e i risultati vengono filtrati per restituire i valori nella riga che era valida nel punto nel tempo specificato per il  *\<data_ora >* parametro. Il valore per una riga viene considerato valido se il *system_start_time_column_name* valore è minore o uguale al  *\<data_ora >* valore del parametro e *system_end_time_ column_name* valore è maggiore di  *\<data_ora >* valore del parametro.   
  
 DA \<data_ora_inizio > TO \<data_ora_fine >

**Si applica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].

  
 Restituisce una tabella con i valori per tutte le versioni di record che erano attive all'interno dell'intervallo di tempo specificato, indipendentemente dal fatto che abbiano iniziato a essere attive prima di  *\<data_ora_inizio >* valore del parametro per FROM argomento o non siano più state attive dopo il  *\<data_ora_fine >* valore del parametro per l'argomento TO. Internamente, viene eseguita un'unione tra la tabella temporale e la relativa tabella di cronologia e i risultati vengono filtrati in modo da restituire i valori per tutte le versioni di riga che erano attive in qualsiasi momento durante l'intervallo di tempo specificato. Le righe diventate attive esattamente in corrispondenza del limite inferiore definito dall'endpoint FROM sono incluse e non sono incluse le righe diventate attive esattamente in corrispondenza del limite superiore definito dall'endpoint TO.  
  
 TRA \<data_ora_inizio > AND \<data_ora_fine >  

**Si applica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Come sopra il **FROM \<data_ora_inizio > TO \<data_ora_fine >** descrizione, ad eccezione del fatto che include le righe diventate attive in corrispondenza del limite superiore definito dal \<data_ora_fine > endpoint.  
  
 CONTAINED IN (\<data_ora_inizio >, \<data_ora_fine >)  

**Si applica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  

  
 Restituisce una tabella con i valori per tutte le versioni di record che sono state aperte e chiuse nell'intervallo di tempo specificato, definito dai due valori datetime per l'argomento CONTAINED IN. Sono incluse le righe diventate attive esattamente in corrispondenza del limite inferiore o che non sono più state attive esattamente in corrispondenza del limite superiore.  
  
 ALL  
 Restituisce una tabella con i valori da tutte le righe dalla tabella corrente sia la tabella di cronologia.  
  
## <a name="remarks"></a>Osservazioni  
 La clausola FROM supporta la sintassi SQL-92 per le tabelle unite in join e per le tabelle derivate. Nella sintassi SQL-92 sono disponibili gli operatori di join INNER, LEFT OUTER, RIGHT OUTER, FULL OUTER e CROSS.  
  
 In una clausola FROM le istruzioni UNION e JOIN sono supportate sia nelle viste, sia nelle tabelle derivate e nelle sottoquery.  
  
 Un self join è una tabella unita in join con se stessa. Nelle operazioni di inserimento e aggiornamento basate su un self join viene seguito l'ordine indicato nella clausola FROM.  
  
 Dato che in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono prese in considerazione le statistiche di distribuzione e cardinalità dei server collegati che forniscono statistiche sulla distribuzione delle colonne, non è necessario ricorrere all'hint di join REMOTE per imporre la valutazione di un join in remoto. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Query Processor analizza le statistiche remote e determina se è appropriato adottare una strategia di join remoto. L'hint di join REMOTE risulta utile per i provider che non forniscono statistiche sulla distribuzione delle colonne.  
  
## <a name="using-apply"></a>Utilizzo di APPLY  
 Entrambi gli operandi sinistro e destro dell'operatore APPLY sono espressioni di tabella. La differenza principale tra questi operandi è che il *right_table_source* possibile utilizzare una funzione con valori di tabella che accetta una colonna dal *left_table_source* come uno degli argomenti della funzione. Il *left_table_source* può includere funzioni con valori di tabella, ma non può contenere argomenti che sono colonne di *right_table_source*.  
  
 L'operatore APPLY funziona nel modo seguente per restituire l'origine di tabella per la clausola FROM:  
  
1.  Valuta *right_table_source* rispetto a ogni riga del *left_table_source* per produrre set di righe.  
  
     I valori di *right_table_source* dipendono *left_table_source*. *right_table_source* può essere rappresentato approssimativamente in questo modo: `TVF(left_table_source.row)`, dove `TVF` è una funzione con valori di tabella.  
  
2.  Combina i set di risultati che viene generati per ogni riga nella valutazione di *right_table_source* con il *left_table_source* eseguendo un'operazione UNION ALL.  
  
     L'elenco di colonne restituito dal risultato dell'operatore APPLY è il set di colonne dal *left_table_source* combinato con l'elenco di colonne di *right_table_source*.  
  
## <a name="using-pivot-and-unpivot"></a>Utilizzo di PIVOT e UNPIVOT  
 Il *pivot_column* e *value_column* sono colonne di raggruppamento utilizzate dall'operatore PIVOT. PIVOT segue il processo seguente per ottenere il set di risultati di output:  
  
1.  Esegue GROUP BY nel relativo *input_table* contro il raggruppamento colonne e restituisce una riga di output per ogni gruppo.  
  
     Le colonne di raggruppamento nella riga di output ottengono i valori di colonna corrispondente per tale gruppo di *input_table*.  
  
2.  Genera valori per le colonne nell'elenco delle colonne per ogni riga di output eseguendo le operazioni seguenti:  
  
    1.  Raggruppando le righe restituite in GROUP BY nel passaggio precedente con il *pivot_column*.  
  
         Per ogni colonna di output di *column_list*, selezionando un sottogruppo che soddisfa la condizione:  
  
         `pivot_column = CONVERT(<data type of pivot_column>, 'output_column')`  
  
    2.  *funzione_aggregata* viene valutata la *value_column* su questo sottogruppo e il risultato viene restituito come valore dell'oggetto corrispondente *output_column*. Se il sottogruppo è vuoto, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] genera un valore null per tale *output_column*. Se la funzione di aggregazione è COUNT e il sottogruppo è vuoto, viene restituito zero (0).  

> [!NOTE]
> Gli identificatori di colonna nel `UNPIVOT` clausola seguire le regole di confronto del catalogo. Per [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], le regole di confronto è sempre `SQL_Latin1_General_CP1_CI_AS`. Per [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] database parzialmente indipendenti, le regole di confronto è sempre `Latin1_General_100_CI_AS_KS_WS_SC`. Se la colonna viene combinata con altre colonne, quindi una clausola collate (`COLLATE DATABASE_DEFAULT`) è necessario per evitare conflitti.   
  
 Per ulteriori informazioni su PIVOT e UNPIVOT inclusi alcuni esempi, vedere [tramite PIVOT e UNPIVOT](../../t-sql/queries/from-using-pivot-and-unpivot.md).  
  
## <a name="permissions"></a>Permissions  
 Sono richieste le autorizzazioni per l'istruzione DELETE, SELECT o UPDATE.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-using-a-simple-from-clause"></a>A. Utilizzo di una clausola FROM semplice  
 Nell'esempio seguente vengono recuperate le colonne `TerritoryID` e `Name` dalla tabella `SalesTerritory` nel database di esempio [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```tsql    
SELECT TerritoryID, Name  
FROM Sales.SalesTerritory  
ORDER BY TerritoryID ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
TerritoryID Name                            
----------- ------------------------------  
1           Northwest                       
2           Northeast                       
3           Central                         
4           Southwest                       
5           Southeast                       
6           Canada                          
7           France                          
8           Germany                         
9           Australia                       
10          United Kingdom                  
(10 row(s) affected)  
```  
  
### <a name="b-using-the-tablock-and-holdlock-optimizer-hints"></a>B. Utilizzo degli hint di ottimizzazione TABLOCK e HOLDLOCK  
 Nella transazione parziale seguente viene illustrato come impostare un blocco di tabella condiviso esplicito in `Employee` e come leggere l'indice. Il blocco viene mantenuto attivo fino al termine della transazione.  
  
```tsql    
BEGIN TRAN  
SELECT COUNT(*)   
FROM HumanResources.Employee WITH (TABLOCK, HOLDLOCK) ;  
```  
  
### <a name="c-using-the-sql-92-cross-join-syntax"></a>C. Utilizzo della sintassi CROSS JOIN di SQL-92  
 Nell'esempio seguente viene restituito il prodotto incrociato delle due tabelle `Employee` e `Department` nel database [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. Un elenco di tutte le possibili combinazioni di `BusinessEntityID` righe e tutti i `Department` vengono restituite le righe di nome.  
  
```wql    
SELECT e.BusinessEntityID, d.Name AS Department  
FROM HumanResources.Employee AS e  
CROSS JOIN HumanResources.Department AS d  
ORDER BY e.BusinessEntityID, d.Name ;  
```  
  
### <a name="d-using-the-sql-92-full-outer-join-syntax"></a>D. Utilizzo della sintassi FULL OUTER JOIN di SQL-92  
 Nell'esempio seguente vengono restituiti il nome del prodotto ed eventuali ordini di vendita corrispondenti nella tabella `SalesOrderDetail` del database [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. Vengono inoltre restituiti gli ordini di vendita per cui non è elencato alcun prodotto nella tabella `Product` e tutti i prodotti con un ordine di vendita diverso da quello elencato nella tabella `Product`.  
  
```tsql  
-- The OUTER keyword following the FULL keyword is optional.  
SELECT p.Name, sod.SalesOrderID  
FROM Production.Product AS p  
FULL OUTER JOIN Sales.SalesOrderDetail AS sod  
ON p.ProductID = sod.ProductID  
ORDER BY p.Name ;  
```  
  
### <a name="e-using-the-sql-92-left-outer-join-syntax"></a>E. Utilizzo della sintassi LEFT OUTER JOIN di SQL-92  
 Nell'esempio seguente vengono unite in join due tabelle tramite la colonna `ProductID`. Le righe della tabella sinistra prive di corrispondenza vengono mantenute. La tabella `Product` viene confrontata con la tabella `SalesOrderDetail` nelle colonne `ProductID` in ogni tabella. Tutti i prodotti, ordinati e non ordinati, vengono visualizzati nel set dei risultati.  
  
```tsql    
SELECT p.Name, sod.SalesOrderID  
FROM Production.Product AS p  
LEFT OUTER JOIN Sales.SalesOrderDetail AS sod  
ON p.ProductID = sod.ProductID  
ORDER BY p.Name ;  
```  
  
### <a name="f-using-the-sql-92-inner-join-syntax"></a>F. Utilizzo della sintassi INNER JOIN di SQL-92  
 Nell'esempio seguente vengono restituiti tutti i nomi di prodotti e gli ID degli ordini di vendita.  
  
```tsql    
-- By default, SQL Server performs an INNER JOIN if only the JOIN   
-- keyword is specified.  
SELECT p.Name, sod.SalesOrderID  
FROM Production.Product AS p  
INNER JOIN Sales.SalesOrderDetail AS sod  
ON p.ProductID = sod.ProductID  
ORDER BY p.Name ;  
```  
  
### <a name="g-using-the-sql-92-right-outer-join-syntax"></a>G. Utilizzo della sintassi RIGHT OUTER JOIN di SQL-92  
 Nell'esempio seguente vengono unite in join due tabelle tramite la colonna `TerritoryID`. Le righe della tabella destra prive di corrispondenza vengono mantenute. La tabella `SalesTerritory` viene confrontata con la tabella `SalesPerson` nella colonna `TerritoryID` in ogni tabella. Tutti i venditori vengono visualizzati nel set dei risultati, a prescindere dal fatto che siano assegnati a un'area o meno.  
  
```tsql    
SELECT st.Name AS Territory, sp.BusinessEntityID  
FROM Sales.SalesTerritory AS st   
RIGHT OUTER JOIN Sales.SalesPerson AS sp  
ON st.TerritoryID = sp.TerritoryID ;  
```  
  
### <a name="h-using-hash-and-merge-join-hints"></a>H. Utilizzo degli hint di join HASH e MERGE  
 Nell'esempio seguente viene eseguito un join delle tre tabelle `Product`, `ProductVendor` e `Vendor` per ottenere un elenco di prodotti e dei relativi fornitori. Query Optimizer unisce in join le tabelle `Product` e `ProductVendor` (`p` e `pv`) tramite un join di tipo MERGE. I risultati del join di tipo MERGE delle tabelle `Product` e `ProductVendor` (`p` e `pv`) vengono quindi uniti tramite join di tipo HASH alla tabella `Vendor` per ottenere (`p` e `pv`) e `v`.  
  
> [!IMPORTANT]  
>  Dopo avere specificato un hint di join, la parola chiave INNER non è più facoltativa e deve essere indicata in modo esplicito per l'esecuzione di un INNER JOIN.  
  
```tsql    
SELECT p.Name AS ProductName, v.Name AS VendorName  
FROM Production.Product AS p   
INNER MERGE JOIN Purchasing.ProductVendor AS pv   
ON p.ProductID = pv.ProductID  
INNER HASH JOIN Purchasing.Vendor AS v  
ON pv.BusinessEntityID = v.BusinessEntityID  
ORDER BY p.Name, v.Name ;  
```  
  
### <a name="i-using-a-derived-table"></a>I. Utilizzo di una tabella derivata  
 Nell'esempio seguente viene utilizzata una tabella derivata, con un'istruzione `SELECT` dopo la clausola `FROM`, per restituire nome e cognome di tutti i dipendenti e le città in cui abitano.  
  
```tsql    
SELECT RTRIM(p.FirstName) + ' ' + LTRIM(p.LastName) AS Name, d.City  
FROM Person.Person AS p  
INNER JOIN HumanResources.Employee e ON p.BusinessEntityID = e.BusinessEntityID   
INNER JOIN  
   (SELECT bea.BusinessEntityID, a.City   
    FROM Person.Address AS a  
    INNER JOIN Person.BusinessEntityAddress AS bea  
    ON a.AddressID = bea.AddressID) AS d  
ON p.BusinessEntityID = d.BusinessEntityID  
ORDER BY p.LastName, p.FirstName;  
```  
  
### <a name="j-using-tablesample-to-read-data-from-a-sample-of-rows-in-a-table"></a>J. Utilizzo di TABLESAMPLE per leggere i dati di un campione di righe in una tabella  
 Nell'esempio seguente viene utilizzata l'opzione `TABLESAMPLE` nella clausola `FROM` per restituire approssimativamente il `10` percento di tutte le righe della tabella `Customer`.  
  
```tsql    
SELECT *  
FROM Sales.Customer TABLESAMPLE SYSTEM (10 PERCENT) ;  
```  
  
### <a name="k-using-apply"></a>K. Utilizzo di APPLY  
 Nell'esempio seguente si presuppone che nel database siano presenti le tabelle seguenti con lo schema seguente:  
  
-   `Departments`: `DeptID`, `DivisionID`, `DeptName`, `DeptMgrID`  
  
-   `EmpMgr`: `MgrID`, `EmpID`  
  
-   `Employees`: `EmpID`, `EmpLastName`, `EmpFirstName`, `EmpSalary`  
  
 È anche presente una funzione con valori di tabella, `GetReports(MgrID)` che restituisce un elenco di tutti i dipendenti (`EmpID`, `EmpLastName`, `EmpSalary`) che sono subordinati direttamente o indirettamente all'ID `MgrID` specificato.  
  
 In questo esempio viene utilizzato `APPLY` per restituire tutti i reparti e tutti i dipendenti in ogni reparto. Se uno specifico reparto non ha dipendenti, non verranno restituite righe per tale reparto.  
  
```tsql
SELECT DeptID, DeptName, DeptMgrID, EmpID, EmpLastName, EmpSalary  
FROM Departments d CROSS APPLY dbo.GetReports(d.DeptMgrID) ;  
```  
  
 Se si desidera che la query restituisca righe per i reparti senza dipendenti, restituendo valori Null per le colonne `EmpID`, `EmpLastName` e `EmpSalary`, utilizzare invece `OUTER APPLY`.  
  
```tsql
SELECT DeptID, DeptName, DeptMgrID, EmpID, EmpLastName, EmpSalary  
FROM Departments d OUTER APPLY dbo.GetReports(d.DeptMgrID) ;  
```  
  
### <a name="l-using-cross-apply"></a>L. Utilizzo di CROSS APPLY  
 Nell'esempio seguente viene recuperato uno snapshot di tutti i piani di query disponibili nella cache dei piani, eseguendo una query sulla DMV `sys.dm_exec_cached_plans` per recuperare gli handle per tutti i piani di query nella cache. Successivamente viene specificato l'operatore `CROSS APPLY` per passare gli handle del piano a `sys.dm_exec_query_plan`. L'output Showplan XML per ogni piano disponibile nella cache dei piani viene indicato nella colonna `query_plan` della tabella restituita.  
  
```tsql
USE master;  
GO  
SELECT dbid, object_id, query_plan   
FROM sys.dm_exec_cached_plans AS cp   
CROSS APPLY sys.dm_exec_query_plan(cp.plan_handle);   
GO  
```  
  
### <a name="m-using-for-systemtime"></a>M. Utilizzo di FOR SYSTEM_TIME  
  
**Si applica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 L'esempio seguente usa l'argomento date_time_literal_or_variable FOR SYSTEM_TIME AS OF per restituire le righe di tabella che erano effettivi (correnti) a partire da 1 gennaio 2014.  
  
```tsql
SELECT DepartmentNumber,   
    DepartmentName,   
    ManagerID,   
    ParentDepartmentNumber   
FROM DEPARTMENT  
FOR SYSTEM_TIME AS OF '2014-01-01'  
WHERE ManagerID = 5;
```  
  
 L'esempio seguente usa il date_time_literal_or_variable FOR SYSTEM_TIME FROM all'argomento date_time_literal_or_variable per restituire tutte le righe che erano attive durante il periodo definito come a partire da 1 gennaio 2013 e terminando con il 1 ° gennaio 2014 escluso il limite superiore.  
  
```tsql
SELECT DepartmentNumber,   
    DepartmentName,   
    ManagerID,   
    ParentDepartmentNumber   
FROM DEPARTMENT  
FOR SYSTEM_TIME FROM '2013-01-01' TO '2014-01-01'  
WHERE ManagerID = 5;
```  
  
 L'esempio seguente usa il date_time_literal_or_variable per SYSTEM_TIME tra e argomento date_time_literal_or_variable per restituire tutte le righe che erano attive durante il periodo definito come a partire da 1 gennaio 2013 e terminando con il 1 ° gennaio 2014 inclusivo del limite superiore.  
  
```tsql
SELECT DepartmentNumber,   
    DepartmentName,   
    ManagerID,   
    ParentDepartmentNumber   
FROM DEPARTMENT  
FOR SYSTEM_TIME BETWEEN '2013-01-01' AND '2014-01-01'  
WHERE ManagerID = 5;
```  
  
 Nell'esempio seguente viene utilizzato per argomento SYSTEM_TIME CONTAINED IN (date_time_literal_or_variable, date_time_literal_or_variable) per restituire tutte le righe che sono state aperte e chiuse durante il periodo definito come a partire da 1 gennaio 2013 e che termina con 1 ° gennaio 2014.  
  
```tsql
SELECT DepartmentNumber,   
    DepartmentName,   
    ManagerID,   
    ParentDepartmentNumber   
FROM DEPARTMENT  
FOR SYSTEM_TIME CONTAINED IN ( '2013-01-01', '2014-01-01' )  
WHERE ManagerID = 5;
```  
  
 Nell'esempio seguente viene utilizzata una variabile anziché un valore letterale per fornire i valori limite per la query.  
  
```tsql
DECLARE @AsOfFrom datetime2 = dateadd(month,-12, sysutcdatetime());
DECLARE @AsOfTo datetime2 = dateadd(month,-6, sysutcdatetime());
  
SELECT DepartmentNumber,   
    DepartmentName,   
    ManagerID,   
    ParentDepartmentNumber   
FROM DEPARTMENT  
FOR SYSTEM_TIME FROM @AsOfFrom TO @AsOfTo  
WHERE ManagerID = 5;
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Esempi: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="n-using-a-simple-from-clause"></a>N. Utilizzo di una clausola FROM semplice  
 Nell'esempio seguente viene recuperato il `SalesTerritoryID` e `SalesTerritoryRegion` le colonne di `DimSalesTerritory` tabella.  
  
```tsql
-- Uses AdventureWorks  
  
SELECT SalesTerritoryKey, SalesTerritoryRegion  
FROM DimSalesTerritory  
ORDER BY SalesTerritoryKey;  
```  
  
### <a name="o-using-the-inner-join-syntax"></a>O. Utilizzo della sintassi INNER JOIN  
 Nell'esempio seguente viene restituito il `SalesOrderNumber`, `ProductKey`, e `EnglishProductName` le colonne di `FactInternetSales` e `DimProduct` tabelle in cui la chiave di join, `ProductKey`, corrisponde in entrambe le tabelle. Il `SalesOrderNumber` e `EnglishProductName` colonne ciascuna presente in uno dei, solo le tabelle, pertanto non è necessario specificare l'alias di tabella con le colonne seguenti, come illustrato; questi alias sono inclusi per migliorare la leggibilità. La parola **AS** prima di un alias di nome non è obbligatorio ma è consigliabile per migliorare la leggibilità e conforme allo standard ANSI.  
  
```tsql
-- Uses AdventureWorks  
  
SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
FROM FactInternetSales AS fis 
INNER JOIN DimProduct AS dp  
    ON dp.ProductKey = fis.ProductKey;  
```  
  
 Poiché il `INNER` (parola chiave) non è necessaria per gli inner join, la stessa query può essere scritta come:  
  
```tsql
-- Uses AdventureWorks  
  
SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
FROM FactInternetSales AS fis 
JOIN DimProduct AS dp  
ON dp.ProductKey = fis.ProductKey;  
```  
  
 Oggetto `WHERE` clausola può inoltre essere utilizzata con questa query per limitare i risultati. In questo esempio limita i risultati ai `SalesOrderNumber` valori superiori a 'SO5000':  
  
```tsql
-- Uses AdventureWorks  
  
SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
FROM FactInternetSales AS fis 
JOIN DimProduct AS dp  
    ON dp.ProductKey = fis.ProductKey  
WHERE fis.SalesOrderNumber > 'SO50000'  
ORDER BY fis.SalesOrderNumber;  
```  
  
### <a name="p-using-the-left-outer-join-and-right-outer-join-syntax"></a>P. Utilizzando la sintassi LEFT OUTER JOIN e RIGHT OUTER JOIN  
 I join di esempio seguente il `FactInternetSales` e `DimProduct` tabelle nel `ProductKey` colonne. La sintassi di outer join sinistro mantiene le righe senza corrispondenza da sinistra (`FactInternetSales`) nella tabella. Poiché il `FactInternetSales` tabella non contiene alcuna `ProductKey` valori che non corrispondono il `DimProduct` tabella, questa query restituisce le stesse righe del primo esempio di inner join precedente.  
  
```tsql
-- Uses AdventureWorks  
  
SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
FROM FactInternetSales AS fis 
LEFT OUTER JOIN DimProduct AS dp  
    ON dp.ProductKey = fis.ProductKey;  
```  
  
 Questa query può essere scritta anche senza il `OUTER` (parola chiave).  
  
 In right outer join, le righe non corrispondenti della tabella di destra vengono mantenute. L'esempio seguente restituisce le stesse righe come nell'esempio di outer join sinistro sopra.  
  
```tsql
-- Uses AdventureWorks  
  
SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
FROM DimProduct AS dp 
RIGHT OUTER JOIN FactInternetSales AS fis  
    ON dp.ProductKey = fis.ProductKey;  
```  
  
 La query seguente utilizza il `DimSalesTerritory` tabella come tabella di sinistra in un left outer join. Recupera il `SalesOrderNumber` i valori di `FactInternetSales` tabella. Se non sono presenti ordini per un particolare `SalesTerritoryKey`, la query restituirà un valore NULL per il `SalesOrderNumber` per tale riga. Questa query viene ordinata in base il `SalesOrderNumber` colonna, in modo che qualsiasi i valori null in questa colonna verrà visualizzata nella parte superiore dei risultati.  
  
```tsql
-- Uses AdventureWorks  
  
SELECT dst.SalesTerritoryKey, dst.SalesTerritoryRegion, fis.SalesOrderNumber  
FROM DimSalesTerritory AS dst 
LEFT OUTER JOIN FactInternetSales AS fis  
    ON dst.SalesTerritoryKey = fis.SalesTerritoryKey  
ORDER BY fis.SalesOrderNumber;  
```  
  
 Questa query potrebbe essere riscritta con un right outer join per recuperare gli stessi risultati:  
  
```tsql
-- Uses AdventureWorks  
  
SELECT dst.SalesTerritoryKey, dst.SalesTerritoryRegion, fis.SalesOrderNumber  
FROM FactInternetSales AS fis 
RIGHT OUTER JOIN DimSalesTerritory AS dst  
    ON fis.SalesTerritoryKey = dst.SalesTerritoryKey  
ORDER BY fis.SalesOrderNumber;  
```  
  
### <a name="q-using-the-full-outer-join-syntax"></a>Q. Utilizzo della sintassi FULL OUTER JOIN  
 Nell'esempio seguente viene illustrato un full outer join, che restituisce tutte le righe da entrambe le tabelle unite in join, ma restituisce NULL per i valori che non corrispondono, l'altra tabella.  
  
```tsql
-- Uses AdventureWorks  
  
SELECT dst.SalesTerritoryKey, dst.SalesTerritoryRegion, fis.SalesOrderNumber  
FROM DimSalesTerritory AS dst 
FULL OUTER JOIN FactInternetSales AS fis  
    ON dst.SalesTerritoryKey = fis.SalesTerritoryKey  
ORDER BY fis.SalesOrderNumber;  
```  
  
 Questa query può essere scritta anche senza il `OUTER` (parola chiave).  
  
```tsql
-- Uses AdventureWorks  
  
SELECT dst.SalesTerritoryKey, dst.SalesTerritoryRegion, fis.SalesOrderNumber  
FROM DimSalesTerritory AS dst 
FULL JOIN FactInternetSales AS fis  
    ON dst.SalesTerritoryKey = fis.SalesTerritoryKey  
ORDER BY fis.SalesOrderNumber;  
```  
  
### <a name="r-using-the-cross-join-syntax"></a>R. Utilizzo della sintassi CROSS JOIN  
 L'esempio seguente restituisce il prodotto incrociato del `FactInternetSales` e `DimSalesTerritory` tabelle. Un elenco di tutte le possibili combinazioni di `SalesOrderNumber` e `SalesTerritoryKey` vengono restituiti. Si noti l'assenza del `ON` clausola della query di cross join.  
  
```tsql
-- Uses AdventureWorks  
  
SELECT dst.SalesTerritoryKey, fis.SalesOrderNumber  
FROM DimSalesTerritory AS dst 
CROSS JOIN FactInternetSales AS fis  
ORDER BY fis.SalesOrderNumber;  
```  
  
### <a name="s-using-a-derived-table"></a>S. Utilizzo di una tabella derivata  
 Nell'esempio seguente viene utilizzata una tabella derivata (un `SELECT` istruzione dopo il `FROM` clausola) per restituire il `CustomerKey` e `LastName` colonne di tutti i clienti nel `DimCustomer` tabella `BirthDate` valori entro il 1 ° gennaio 1970 e il cognome 'Smith'.  
  
```tsql
-- Uses AdventureWorks  
  
SELECT CustomerKey, LastName  
FROM  
   (SELECT * FROM DimCustomer  
    WHERE BirthDate > '01/01/1970') AS DimCustomerDerivedTable  
WHERE LastName = 'Smith'  
ORDER BY LastName;  
```  
  
### <a name="t-reduce-join-hint-example"></a>T. RIDURRE l'esempio di hint di join  
 L'esempio seguente usa il `REDUCE` hint di join per l'elaborazione della tabella derivata all'interno della query. Quando si utilizza il `REDUCE` hint di join nella query, il `fis.ProductKey` viene proiettata, replicato e apportate distinte e quindi unita in join a `DimProduct` durante la riproduzione casuale di `DimProduct` su `ProductKey`. La tabella derivata risultante viene distribuita in `fis.ProductKey`.  
  
```tsql
-- Uses AdventureWorks  
  
EXPLAIN SELECT SalesOrderNumber  
FROM  
   (SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
    FROM DimProduct AS dp   
      INNER REDUCE JOIN FactInternetSales AS fis   
          ON dp.ProductKey = fis.ProductKey  
   ) AS dTable  
ORDER BY SalesOrderNumber;  
```  
  
### <a name="u-replicate-join-hint-example"></a>U. Esempio di hint di join di replica  
 In questo esempio viene illustrata la stessa query come nell'esempio precedente, tranne il fatto che un `REPLICATE` hint di join viene utilizzato anziché il `REDUCE` hint di join. Utilizzare il `REPLICATE` hint fa sì che i valori nel `ProductKey` colonna (join) dal `FactInternetSales` tabella devono essere replicate in tutti i nodi. Il `DimProduct` tabella è unita in join alla versione replicata di tali valori.  
  
```tsql
-- Uses AdventureWorks  
  
EXPLAIN SELECT SalesOrderNumber  
FROM  
   (SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
    FROM DimProduct AS dp   
      INNER REPLICATE JOIN FactInternetSales AS fis  
          ON dp.ProductKey = fis.ProductKey  
   ) AS dTable  
ORDER BY SalesOrderNumber;  
```  
  
### <a name="v-using-the-redistribute-hint-to-guarantee-a-shuffle-move-for-a-distribution-incompatible-join"></a>V. Utilizzo dell'hint REDISTRIBUTE per garantire uno spostamento casuale per un join non compatibile di distribuzione  
 La query seguente utilizza l'hint di query di ridistribuzione in un join non compatibile di distribuzione. In questo modo si garantisce che il query optimizer utilizzerà uno spostamento casuale nel piano di query. Ciò garantisce inoltre che il piano di query non utilizzerà uno spostamento di trasmissione che consente di spostare una tabella distribuita a una tabella replicata.  
  
 Nell'esempio seguente, l'hint REDISTRIBUTE imposto uno spostamento casuale per la tabella FactInternetSales ProductKey è la colonna di distribuzione per DimProduct e non è la colonna di distribuzione per FactInternetSales.  
  
```tsql
-- Uses AdventureWorks  
  
EXPLAIN  
SELECT dp.ProductKey, fis.SalesOrderNumber, fis.TotalProductCost  
FROM DimProduct AS dp 
INNER REDISTRIBUTE JOIN FactInternetSales AS fis  
    ON dp.ProductKey = fis.ProductKey;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [FREETEXTTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/freetexttable-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [OPENQUERY &#40; Transact-SQL &#41;](../../t-sql/functions/openquery-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Operatori &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)   
 [IN &#40; Transact-SQL &#41;](../../t-sql/queries/where-transact-sql.md)  
