---
title: Nuove caratteristiche di data e ora con precedenti versioni di SQL Server (OLE DB) | Documenti Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-date-time
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 96976bac-018c-47cc-b1b2-fa9605eb55e5
caps.latest.revision: "27"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 63d848005d0a1745070caf209f52f49dd80db1d2
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2018
---
# <a name="new-date-and-time-features-with-previous-sql-server-versions-ole-db"></a>Nuove caratteristiche di data e ora con precedenti versioni di SQL Server (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  In questo argomento viene descritto il comportamento previsto quando un'applicazione client che utilizza caratteristiche avanzate di data e ora comunica con una versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriore [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]e quando un client compilato con una versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client precedente a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] invia comandi a un server che supporta le avanzate funzionalità di data e ora.  
  
## <a name="down-level-client-behavior"></a>Comportamento dei client legacy  
 Applicazioni client che utilizzano una versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client precedenti a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] visualizzare i tipi di data/ora di nuovo come **nvarchar** colonne. Il contenuto delle colonne è costituito da rappresentazioni letterali. Per ulteriori informazioni, vedere la sezione "Dati formatta: stringhe e valori letterali" di [supporto tipo di dati per OLE DB data e ora miglioramenti](../../relational-databases/native-client-ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md). Le dimensioni di colonna corrispondono alla lunghezza massima in valori letterali per la precisione specificata per la colonna.  
  
 Le API di catalogo restituiranno metadati consistenti con il codice del tipo di dati legacy restituito al client (ad esempio, **nvarchar**) e la rappresentazione legacy associata (ad esempio, il formato letterale appropriato). Il nome del tipo di dati restituito, tuttavia, coinciderà con il nome effettivo del tipo di dati di [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
 Quando un'applicazione client legacy viene eseguita in un [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (o versioni successive) in cui le modifiche dello schema di data/ora sono stati apportati tipi di server, il comportamento previsto è come segue:  
  
|Tipo di client OLE DB|Tipo di SQL Server 2005|Tipo di SQL Server 2008 (o versioni successive)|Conversione risultati (da server a client)|Conversione parametri (da client a server)|  
|------------------------|--------------------------|---------------------------------------|--------------------------------------------|-----------------------------------------------|  
|DBTYPE_DBDATE|DateTime|Data|OK|OK|  
|DBTYPE_DBTIMESTAMP|||Campi dell'ora impostati su zero.|Se il campo dell'ora è diverso da zero, IRowsetChange avrà esito negativo a causa di troncamento della stringa.|  
|DBTYPE_DBTIME||Time(0)|OK|OK|  
|DBTYPE_DBTIMESTAMP|||Campi della data impostati sulla data corrente.|Se i secondi frazionari sono diversi da zero, IRowsetChange avrà esito negativo a causa di troncamento della stringa.<br /><br /> La data viene ignorata.|  
|DBTYPE_DBTIME||Time(7)|Esito negativo: valore letterale di ora non valido.|OK|  
|DBTYPE_DBTIMESTAMP|||Esito negativo: valore letterale di ora non valido.|OK|  
|DBTYPE_DBTIMESTAMP||Datetime2(3)|OK|OK|  
|DBTYPE_DBTIMESTAMP||Datetime2 (7)|OK|OK|  
|DBTYPE_DBDATE|Smalldatetime|Data|OK|OK|  
|DBTYPE_DBTIMESTAMP|||Campi dell'ora impostati su zero.|Se il campo dell'ora è diverso da zero, IRowsetChange avrà esito negativo a causa di troncamento della stringa.|  
|DBTYPE_DBTIME||Time(0)|OK|OK|  
|DBTYPE_DBTIMESTAMP|||Campi della data impostati sulla data corrente.|Se i secondi frazionari sono diversi da zero, IRowsetChange avrà esito negativo a causa di troncamento della stringa.<br /><br /> La data viene ignorata.|  
|DBTYPE_DBTIMESTAMP||datetime2(0)|OK|OK|  
  
 OK indica che un funzionamento corretto in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] corrisponde a un corretto funzionamento anche in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (o versioni successive).  
  
 Sono state prese in considerazione solo le modifiche dello schema comuni indicate di seguito:  
  
-   Utilizzo di un nuovo tipo nei casi in cui logicamente un'applicazione richiede solo un valore di data o di ora. Tuttavia, l'applicazione è stato forzato l'utilizzo **datetime** o **smalldatetime** perché non sono disponibili i tipi separati di data e ora.  
  
-   Utilizzo di un nuovo tipo per ottenere precisione o accuratezza maggiore nei secondi frazionari.  
  
-   Il passaggio a **datetime2** perché si tratta del tipo di dati preferito per data e ora.  
  
 Le applicazioni che utilizzano i metadati del server ottenuto tramite i set di righe dello schema o di ICommandWithParameters:: GetParameterInfo impostare informazioni sul tipo di parametro tramite ICommandWithParameters:: SetParameterInfo avrà esito negativo durante le conversioni client in cui la stringa rappresentazione di un tipo di origine è maggiore rispetto alla rappresentazione di stringa del tipo di destinazione. Ad esempio, se un'associazione client utilizza DBTYPE_DBTIMESTAMP e la colonna server è una data, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client convertirà il valore di "aaaa-mm-gg hh", ma i metadati del server verranno restituiti come **nvarchar (10)**. L'overflow risultante restituisce DBSTATUS_E_CATCONVERTVALUE. Problemi simili si verificano con le conversioni di dati da IRowsetChange, perché i metadati di set di righe vengono impostati dai metadati del set di risultati.  
  
### <a name="parameter-and-rowset-metadata"></a>Metadati per parametri e set di righe  
 In questa sezione descrive i metadati per parametri, le colonne di risultati e set di righe dello schema per i client che vengono compilati con una versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client precedenti a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
#### <a name="icommandwithparametersgetparameterinfo"></a>ICommandWithParameters::GetParameterInfo  
 La struttura DBPARAMINFO restituisce le informazioni seguenti tramite il *prgParamInfo* parametro:  
  
|Tipo di parametro|wType|ulParamSize|bPrecision|bScale|  
|--------------------|-----------|-----------------|----------------|------------|  
|data|DBTYPE_WSTR|10|~0|~0|  
|time|DBTYPE_WSTR|8, 10..16|~0|~0|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|  
|datetime|DBTYPE_DBTIMESTAMP|16|23|3|  
|datetime2|DBTYPE_WSTR|19,21..27|~0|~0|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|~0|~0|  
  
 Si noti che alcuni di questi intervalli di valori non sono continui. Nell'intervallo 8,10..16, ad esempio, non è presente il valore 9. Ciò è dovuto all'aggiunta di un separatore decimale quando la precisione frazionaria è maggiore di zero.  
  
#### <a name="icolumnsrowsetgetcolumnsrowset"></a>IColumnsRowset::GetColumnsRowset  
 Vengono restituite le colonne seguenti:  
  
|Tipo di colonna|DBCOLUMN_TYPE|DBCOLUMN_COLUMNSIZE|DBCOLUMN_PRECISION|DBCOLUMN_SCALE, DBCOLUMN_DATETIMEPRECISION|  
|-----------------|--------------------|--------------------------|-------------------------|--------------------------------------------------|  
|data|DBTYPE_WSTR|10|NULL|NULL|  
|time|DBTYPE_WSTR|8, 10..16|NULL|NULL|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|  
|datetime|DBTYPE_DBTIMESTAMP|16|23|3|  
|datetime2|DBTYPE_WSTR|19,21..27|NULL|NULL|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|NULL|NULL|  
  
#### <a name="columnsinfogetcolumninfo"></a>ColumnsInfo::GetColumnInfo  
 La struttura DBCOLUMNINFO restituisce le informazioni seguenti:  
  
|Tipo di parametro|wType|ulColumnSize|bPrecision|bScale|  
|--------------------|-----------|------------------|----------------|------------|  
|data|DBTYPE_WSTR|10|~0|~0|  
|time(1..7)|DBTYPE_WSTR|8, 10..16|~0|~0|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|  
|datetime|DBTYPE_DBTIMESTAMP|16|23|3|  
|datetime2|DBTYPE_WSTR|19,21..27|~0|~0|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|~0|~0|  
  
### <a name="schema-rowsets"></a>Set di righe dello schema  
 In questa sezione vengono descritti i metadati per parametri, colonne dei risultati e set di righe dello schema per i nuovi tipi di dati. Queste informazioni sono utili è sia un provider client sviluppato utilizzando strumenti precedenti a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
#### <a name="columns-rowset"></a>Set di righe COLUMNS  
 Per i tipi di data/ora vengono restituiti i valori di colonna seguenti:  
  
|Tipo di colonna|DATA_TYPE|CHARACTER_MAXIMUM_LENGTH|CHARACTER_OCTET_LENGTH|DATETIME_PRECISION|  
|-----------------|----------------|--------------------------------|------------------------------|-------------------------|  
|data|DBTYPE_WSTR|10|20|NULL|  
|time|DBTYPE_WSTR|8, 10..16|16,20..32|NULL|  
|smalldatetime|DBTYPE_DBTIMESTAMP|NULL|NULL|0|  
|datetime|DBTYPE_DBTIMESTAMP|NULL|NULL|3|  
|datetime2|DBTYPE_WSTR|19,21..27|38,42..54|NULL|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|52, 56..68|NULL|  
  
#### <a name="procedureparameters-rowset"></a>Set di righe PROCEDURE_PARAMETERS  
 Per i tipi di data/ora vengono restituiti i valori di colonna seguenti:  
  
|Tipo di colonna|DATA_TYPE|CHARACTER_MAXIMUM_LENGTH|CHARACTER_OCTET_LENGTH|TYPE_NAME<br /><br /> LOCAL_TYPE_NAME|  
|-----------------|----------------|--------------------------------|------------------------------|--------------------------------------|  
|data|DBTYPE_WSTR|10|20|data|  
|time|DBTYPE_WSTR|8, 10..16|16,20..32|time|  
|smalldatetime|DBTYPE_DBTIMESTAMP|NULL|NULL|smalldatetime|  
|datetime|DBTYPE_DBTIMESTAMP|NULL|NULL|datetime|  
|datetime2|DBTYPE_WSTR|19,21..27|38,42..54|datetime2|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|52, 56..68|datetimeoffset|  
  
#### <a name="providertypes-rowset"></a>Set di righe PROVIDER_TYPES  
 Per i tipi di data/ora vengono restituite le righe seguenti:  
  
|Type -><br /><br /> Colonna|data|time|smalldatetime|datetime|datetime2|datetimeoffset|  
|--------------------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|TYPE_NAME|data|time|smalldatetime|datetime|datetime2|datetimeoffset|  
|DATA_TYPE|DBTYPE_WSTR|DBTYPE_WSTR|DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMP|DBTYPE_WSTR|DBTYPE_WSTR|  
|COLUMN_SIZE|10|16|16|23|27|34|  
|LITERAL_PREFIX|‘|‘|‘|‘|‘|‘|  
|LITERAL_SUFFIX|‘|‘|‘|‘|‘|‘|  
|CREATE_PARAMS|NULL|NULL|NULL|NULL|NULL|NULL|  
|IS_NULLABLE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|  
|CASE_SENSITIVE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|  
|UNSIGNED_ATTRIBUTE|NULL|NULL|NULL|NULL|NULL|NULL|  
|FIXED_PREC_SCALE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|AUTO_UNIQUE_VALUE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|LOCAL_TYPE_NAME|data|time|smalldatetime|datetime|datetime2|datetimeoffset|  
|MINIMUM_SCALE|NULL|NULL|NULL|NULL|NULL|NULL|  
|MAXIMUM_SCALE|NULL|NULL|NULL|NULL|NULL|NULL|  
|GUID|NULL|NULL|NULL|NULL|NULL|NULL|  
|TYPELIB|NULL|NULL|NULL|NULL|NULL|NULL|  
|VERSION|NULL|NULL|NULL|NULL|NULL|NULL|  
|IS_LONG|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|BEST_MATCH|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_TRUE|VARIANT_FALSE|VARIANT_FALSE|  
|IS_FIXEDLENGTH|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
  
## <a name="down-level-server-behavior"></a>Comportamento dei server legacy  
 Quando si è connessi a un server di una versione precedente a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], qualsiasi tentativo di usare i nuovi nomi di tipo di server (ad esempio, con ICommandWithParameters:: SetParameterInfo o itabledefinition:: CreateTable) comporterà DB_E_BADTYPENAME.  
  
 Se vengono associati nuovi tipi per parametri o risultati senza l'utilizzo di un nome del tipo e il nuovo tipo viene utilizzato per specificare in modo implicito il tipo di server o non è disponibile una conversione valida dal tipo di server al tipo di client, viene restituito DB_E_ERRORSOCCURRED e DBBINDSTATUS_UNSUPPORTED_CONVERSION viene impostato come stato dell'associazione per la funzione di accesso utilizzata in fase di esecuzione.  
  
 Se è disponibile una conversione client supportata dal tipo di buffer al tipo di server per la versione del server nella connessione, è possibile utilizzare tutti i tipi di buffer client. In questo contesto, *tipo server* significa che il tipo specificato da ICommandWithParameters:: SetParameterInfo o implicite dal tipo di buffer se ICommandWithParameters:: SetParameterInfo non è stato chiamato. Di conseguenza, è possibile utilizzare DBTYPE_DBTIME2 e DBTYPE_DBTIMESTAMPOFFSET con i server legacy o quando DataTypeCompatibility=80, se la conversione client a un tipo di server supportato ha esito positivo. Se il tipo di server non è corretto, potrebbe essere segnalato un errore dal server se questo non è in grado di eseguire una conversione implicita al tipo di server effettivo.  
  
## <a name="sspropinitdatatypecompatibility-behavior"></a>Comportamento di SSPROP_INIT_DATATYPECOMPATIBILITY  
 Quando SSPROP_INIT_DATATYPECOMPATIBILITY è impostato su SSPROPVAL_DATATYPECOMPATIBILITY_SQL2000, i tipi di nuovo data/ora e i metadati associati vengono visualizzati ai client come vengono visualizzati per i client legacy, come descritto in [modifiche di copia Bulk per Avanzata data e ora tipi &#40; OLE DB e ODBC &#41; ](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md).  
  
## <a name="comparability-for-irowsetfind"></a>Possibilità di confronto per IRowsetFind  
 Per i nuovi tipi di data/ora sono consentiti tutti gli operatori di confronto, in quanto vengono visualizzati come tipi stringa anziché come tipi di data/ora.  
  
## <a name="see-also"></a>Vedere anche  
 [Data e ora miglioramenti &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
