---
title: SQLSetDescRec | Documenti Microsoft
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-api
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: SQLSetDescRec function
ms.assetid: 203d02a2-aa09-462b-a489-a2cdd6f6023b
caps.latest.revision: "23"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 03db037c6048261681a1f2857be910ebf800c5ad
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/17/2017
---
# <a name="sqlsetdescrec"></a>SQLSetDescRec
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Questo argomento vengono illustrate funzionalità SQLSetDescRec specifico [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
## <a name="sqlsetdescrec-and-table-valued-parameters"></a>SQLSetDescRec e parametri con valori di tabella  
 SQLSetDescRec può essere utilizzato per impostare i campi di descrizione per i parametri con valori di tabella e le colonne di parametri con valori di tabella. Le colonne dei parametri con valori di tabella sono disponibili solo quando il campo di intestazione di descrizione SQL_SOPT_SS_PARAM_FOCUS è impostato sul numero ordinale di un record in cui SQL_DESC_TYPE è impostato su SQL_SS_TABLE. Per ulteriori informazioni su SQL_SOPT_SS_PARAM_FOCUS, vedere [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md).  
  
 Nella tabella seguente viene descritto il mapping tra parametri e campi di descrizione.  
  
|Parametro|Attributo correlato per i tipi di parametro non con valori di tabella, incluse le relative colonne|Attributo correlato per i parametri con valori di tabella|  
|---------------|--------------------------------------------------------------------------------------------------------|----------------------------------------------------|  
|*Tipo*|SQL_DESC_TYPE|SQL_SS_TABLE|  
|*Sottotipo*|Ignorato|Per i record di tipo SQL_DATETIME o SQL_INTERVAL, impostare su SQL_DESC_DATETIME_INTERVAL_CODE.|  
|*Lunghezza*|SQL_DESC_OCTET_LENGTH|Lunghezza del nome del tipo di parametro con valori di tabella. Può essere SQL_NTS, se il nome del tipo è con terminazione Null oppure zero se il nome del tipo di parametro con valori di tabella non è obbligatorio.|  
|*Precisione*|SQL_DESC_PRECISION|SQL_DESC_ARRAY_SIZE|  
|*Scala*|SQL_DESC_SCALE|Non utilizzato. Questo parametro deve essere zero.|  
|*DataPtr*|SQL_DESC_DATA_PTR in APD|SQL_CA_SS_TYPE_NAME<br /><br /> Questo parametro è facoltativo per le chiamate di stored procedure ed è possibile specificare NULL se non è obbligatorio. È necessario specificarlo per istruzioni SQL che non sono chiamate di procedure.<br /><br /> *DataPtr* funge anche da un valore univoco che l'applicazione può utilizzare per identificare il parametro con valori di tabella quando viene utilizzata l'associazione variabile di righe.|  
|*StringLengthPtr*|SQL_DESC_OCTET_LENGTH_PTR|SQL_DESC_OCTET_LENGTH_PTR<br /><br /> Per un parametro con valori di tabella, è il numero di righe da trasferire o SQL_DATA_AT_EXEC.SQL_DATA_AT_EXEC. Questo è un puntatore a un valore che contiene il numero di righe da trasferire con SQLExecDirect.|  
|*IndicatorPtr*|SQL_DESC_INDICATOR_PTR|SQL_DESC_INDICATOR_PTR|  
  
 Per ulteriori informazioni sui parametri con valori di tabella, vedere [parametri con valori di tabella &#40; ODBC &#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlsetdescrec-support-for-enhanced-date-and-time-features"></a>Supporto di SQLSetDescRec per le caratteristiche avanzate di data e ora  
 I valori consentiti per i tipi di data/ora sono i seguenti:  
  
||*Tipo*|*Sottotipo*|*Lunghezza*|*Precisione*|*Scala*|  
|-|------------|---------------|--------------|-----------------|-------------|  
|datetime|SQL_DATETIME|SQL_CODE_TIMESTAMP|4|3|3|  
|smalldatetime|SQL_SQL_DATETIME|SQL_CODE_TIMESTAMP|8|0|0|  
|data|SQL_DATETIME|SQL_CODE_DATE|6|0|0|  
|time|SQL_SS_TIME2|0|10|0..7|0..7|  
|datetime2|SQL_DATETIME|SQL_CODE_TIMESTAMP|16|0..7|0..7|  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET|0|20|0..7|0..7|  
  
 Per ulteriori informazioni, vedere [data e ora miglioramenti &#40; ODBC &#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlsetdescrec-support-for-large-clr-udts"></a>Supporto di SQLSetDescRec per tipi definiti dall'utente CLR di grandi dimensioni  
 **SQLSetDescRec** supporta i tipi CLR grandi dimensioni definito dall'utente (UDT). Per ulteriori informazioni, vedere [Large CLR User-Defined tipi &#40; ODBC &#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Vedere anche  
 [SQLSetDescRec](http://go.microsoft.com/fwlink/?LinkId=80704)   
 [Dettagli di implementazione dell'API ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  