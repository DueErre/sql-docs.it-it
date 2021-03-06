---
title: Valori restituiti SQLGetInfo per dBASE | Documenti Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], DBasedriver
- desktop database drivers [ODBC], DBasedriver
- SQLGetInfo function [ODBC], dBASE Driver
- DBase driver [ODBC], SQLGetInfo
- ODBC desktop database drivers [ODBC], DBasedriver
ms.assetid: af64753c-c758-4b68-954b-2c84e3bbd93f
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dab32294edbe982817a03cc81c33d6623ff973ab
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/15/2018
---
# <a name="sqlgetinfo-returned-values-for-dbase"></a>Valori restituiti SQLGetInfo per dBASE
La tabella seguente elenca il linguaggio C# defines per il *fInfoType* argomento e i corrispondenti valori restituiti da **SQLGetInfo**. Queste informazioni possono essere recuperate passando il linguaggio C elencato #defines a **SQLGetInfo** nel *fInfoType* argomento. Per ulteriori informazioni sui valori restituiti da **SQLGetInfo**, vedere il *riferimento per programmatori ODBC*.  
  
> [!NOTE]  
>  Dove **SQLGetInfo** restituisce una maschera a 32 bit, una barra verticale (&#124;) rappresenta un'operazione OR.  
  
|InfoType|Valore restituito|  
|--------------|--------------------|  
|SQL_ACCESSIBLE_PROCEDURES|"N"|  
|SQL_ACCESSIBLE_TABLES|"Y"|  
|SQL_ACTIVE_ENVIRONMENTS|0|  
|SQL_AGGREGATE_FUNCTIONS|Tutti i set|  
|SQL_ALTER_DOMAIN|0|  
|SQL_ALTER_TABLE|Più valori|  
|SQL_ASYNC_MODE|0|  
|SQL_BATCH_ROW_COUNT|0|  
|SQL_BATCH_SUPPORT|0|  
|SQL_BOOKMARK_PERSISTENCE|Più valori|  
|SQL_CATALOG_LOCATION|SQL_QL_START|  
|SQL_CATALOG_NAME|"Y"|  
|SQL_CATALOG_NAME_SEPARATOR|"\\"|  
|SQL_CATALOG_TERM|"Directory"|  
|SQL_CATALOG_USAGE|Più valori|  
|SQL_COLLATION_SEQ|""|  
|SQL_COLUMN_ALIAS|"Y"|  
|SQL_CONCAT_NULL_BEHAVIOR|SQL_CB_NON_NULL|  
|SQL_CONVERT_BIGINT|0|  
|SQL_CONVERT_BINARY|Più valori|  
|SQL_CONVERT_BIT|0|  
|SQL_CONVERT_CHAR|Più valori|  
|SQL_CONVERT_DATE|Più valori|  
|SQL_CONVERT_DECIMAL|0|  
|SQL_CONVERT_DOUBLE|Più valori|  
|SQL_CONVERT_FLOAT|Più valori|  
|SQL_CONVERT_FUNCTIONS|SQL_FN_CVT_CONVERT|  
|SQL_CONVERT_INTEGER|Più valori|  
|SQL_CONVERT_LONGVARBINARY|Più valori|  
|SQL_CONVERT_LONGVARCHAR|Più valori|  
|SQL_CONVERT_NUMERIC|Più valori|  
|SQL_CONVERT_REAL|Più valori|  
|SQL_CONVERT_SMALLINT|Più valori|  
|SQL_CONVERT_TIME|Più valori|  
|SQL_CONVERT_TIMESTAMP|Più valori|  
|SQL_CONVERT_TINYINT|Più valori|  
|SQL_CONVERT_VARBINARY|Più valori|  
|SQL_CONVERT_VARCHAR|Più valori|  
|SQL_CORRELATION_NAME|SQL_CN_ANY|  
|SQL_CREATE_ASSERTION|0|  
|SQL_CREATE_CHARACTER_SET|0|  
|SQL_CREATE_COLLATION|0|  
|SQL_CREATE_DOMAIN|0|  
|SQL_CREATE_SCHEMA|0|  
|SQL_CREATE_TABLE|SQL_CT_CREATE_TABLE|  
|SQL_CREATE_TRANSLATION|0|  
|SQL_CREATE_VIEW|0|  
|SQL_CURSOR_COMMIT_BEHAVIOR|SQL_CB_CLOSE|  
|SQL_CURSOR_ROLLBACK_BEHAVIOR|SQL_CB_CLOSE|  
|SQL_CURSOR_SENSITIVITY|SQL_UNSPECIFIED|  
|SQL_DATA_SOURCE_NAME|DSN da ODBC, o "" Se viene utilizzata la parola chiave DRIVER in ODBC|  
|SQL_DATA_SOURCE_READ_ONLY|"N" (seconda sull'origine dati).|  
|SQL_DATABASE_NAME|Directory del database corrente|  
|SQL_DATETIME_LITERALS|0|  
|SQL_DBMS_NAME|"DBASE"|  
|SQL_DBMS_VER|Più valori|  
|SQL_DDL_INDEX|Più valori|  
|SQL_DEFAULT_TXN_ISOLATION|0|  
|SQL_DESCRIBE_PARAMETER|0|  
|SQL_DRIVER_HDBC|Gestito da Gestione Driver.|  
|SQL_DRIVER_HENV|Gestito da Gestione Driver.|  
|SQL_DRIVER_HLIB|Gestito da Gestione Driver.|  
|SQL_DRIVER_HSTMT|Gestito da Gestione Driver.|  
|SQL_DRIVER_NAME|"OdbcJt32.dll"|  
|SQL_DRIVER_ODBC_VER|"3.51.0000"|  
|SQL_DRIVER_VER|"4.00.*nnnn*" ( *nnnn*  specifica la data di compilazione)|  
|SQL_DROP_ASSERTION|0|  
|SQL_DROP_CHARACTER_SET|0|  
|SQL_DROP_COLLATION|0|  
|SQL_DROP_DOMAIN|0|  
|SQL_DROP_SCHEMA|0|  
|SQL_DROP_TABLE|SQL_DT_DROP_TABLE|  
|SQL_DROP_TRANSLATION|0|  
|SQL_DROP_VIEW|SQL_DV_DROP_VIEW|  
|SQL_EXPRESSIONS_IN_ORDERBY|"Y"|  
|SQL_FILE_USAGE|SQL_FILE_TABLE|  
|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1|SQL_CA1_NEXT|  
|SQL_GETDATA_EXTENSIONS|Più valori|  
|SQL_GROUP_BY|SQL_GB_GROUP_BY_CONTAINS_SELECT|  
|SQL_IDENTIFIER_CASE|SQL_IC_UPPER (il qualificatore viene restituito in caratteri maiuscoli e minuscoli in modo che Windows NT può individuare la directory.)|  
|SQL_IDENTIFIER_QUOTE_CHAR|"'" (virgolette inverse)|  
|SQL_KEYWORDS|Più valori|  
|SQL_LIKE_ESCAPE_CLAUSE|"N"|  
|SQL_MAX_BINARY_LITERAL_LEN|255|  
|SQL_MAX_CATALOG_NAME_LEN|66|  
|SQL_MAX_CHAR_LITERAL_LEN|254|  
|SQL_MAX_COLUMN_NAME_LEN|10|  
|SQL_MAX_COLUMNS_IN_GROUP_BY|10|  
|SQL_MAX_COLUMNS_IN_INDEX|0 (limite sconosciuto o non applicabile)|  
|SQL_MAX_COLUMNS_IN_ORDER_BY|10|  
|SQL_MAX_COLUMNS_IN_SELECT|255|  
|SQL_MAX_COLUMNS_IN_TABLE|255|  
|SQL_MAX_CONCURRENT_ACTIVITIES|0|  
|SQL_MAX_CURSOR_NAME_LEN|64|  
|SQL_MAX_DRIVER_CONNECTIONS|64|  
|SQL_MAX_INDEX_SIZE|220|  
|SQL_MAX_PROCEDURE_NAME_LEN|0|  
|SQL_MAX_ROW_SIZE|4.000|  
|SQL_MAX_ROW_SIZE_INCLUDES_LONG|"N"|  
|SQL_MAX_SCHEMA_NAME_LEN|0|  
|SQL_MAX_STATEMENT_LEN|65000|  
|SQL_MAX_TABLE_NAME_LEN|12|  
|SQL_MAX_TABLES_IN_SELECT|16|  
|SQL_MAX_USER_NAME_LEN|0|  
|SQL_MULT_RESULT_SETS|"N"|  
|SQL_MULTIPLE_ACTIVE_TXN|"Y"|  
|SQL_NEED_LONG_DATA_LEN|"N"|  
|SQL_NON_NULLABLE_COLUMNS|SQL_NNC_NON_NULL|  
|SQL_NULL_COLLATION|SQL_NC_LOW|  
|SQL_NUMERIC_FUNCTIONS|Più valori|  
|SQL_ODBC_SAG_CLI_ CONFORMANCE|SQL_OSCC_COMPLIANT|  
|SQL_ODBC_SQL_INTEGRITY|"N"|  
|SQL_ODBC_VER|Da Gestione Driver|  
|SQL_OJ_CAPABILITIES|Più valori|  
|SQL_ORDER_BY_COLUMNS_IN_SELECT|"N"|  
|SQL_OUTER_JOINS|"Y"|  
|SQL_PROCEDURE_TERM|""|  
|SQL_PROCEDURES|"N"|  
|SQL_QUOTED_IDENTIFIER_CASE|SQL_IC_MIXED|  
|SQL_ROW_UPDATES|"N"|  
|SQL_SCHEMA_TERM|""|  
|SQL_SCHEMA_USAGE|0|  
|SQL_SCROLL_OPTIONS|Più valori|  
|SQL_SEARCH_PATTERN_ESCAPE|"\\"|  
|SQL_SERVER_NAME|"DBASE"|  
|SQL_SPECIAL_CHARACTERS|"~`@#$%^&*_-+=\\}{"';:?/><,.!'[]&#124;"|  
|SQL_STRING_FUNCTIONS|Più valori|  
|SQL_SUBQUERIES|Più valori|  
|SQL_SYSTEM_FUNCTIONS|0|  
|SQL_TABLE_TERM|"TABLE"|  
|SQL_TIMEDATE_ADD_INTERVALS|0|  
|SQL_TIMEDATE_DIFF_INTERVALS|0|  
|SQL_TIMEDATE_FUNCTIONS|Più valori|  
|SQL_TXN_CAPABLE|SQL_TC_NONE|  
|SQL_TXN_ISOLATION_OPTION|0|  
|SQL_UNION|Più valori|  
|SQL_USER_NAME|""|
