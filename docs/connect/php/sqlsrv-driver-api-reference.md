---
title: Riferimento all'API del Driver SQLSRV | Documenti Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0b55da26-ddeb-4e89-872a-91e0aba57103
caps.latest.revision: "42"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 48d43c13a850e057d675d3abaaec612bc51723e1
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/18/2017
---
# <a name="sqlsrv-driver-api-reference"></a>Riferimento all'API del driver SQLSRV
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Il nome dell'API per il driver SQLSRV nei [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] è **sqlsrv**. Tutti **sqlsrv** funzioni iniziano con **sqlsrv _** e sono seguiti da un verbo o un sostantivo. Quelle seguite da un verbo eseguono un'azione e quelle seguite da un sostantivo restituiscono un tipo di metadati.  
  
## <a name="in-this-section"></a>Argomenti della sezione  
Il driver SQLSRV contiene le funzioni seguenti:  
  
|Funzione|Description|  
|------------|---------------|  
|[sqlsrv_begin_transaction](../../connect/php/sqlsrv-begin-transaction.md)|Avvio di una transazione.|  
|[sqlsrv_cancel](../../connect/php/sqlsrv-cancel.md)|Annulla un'istruzione. Elimina eventuali risultati in sospeso per l'istruzione.|  
|[sqlsrv_client_info](../../connect/php/sqlsrv-client-info.md)|Fornisce informazioni sul client.|  
|[sqlsrv_close](../../connect/php/sqlsrv-close.md)|Chiude una connessione. Libera tutte le risorse associate alla connessione.|  
|[sqlsrv_commit](../../connect/php/sqlsrv-commit.md)|Esegue il commit di una transazione.|  
|[sqlsrv_configure](../../connect/php/sqlsrv-configure.md)|Modifica la gestione degli errori e le configurazioni di registrazione.|  
|[sqlsrv_connect](../../connect/php/sqlsrv-connect.md)|Crea e apre una connessione.|  
|[sqlsrv_errors](../../connect/php/sqlsrv-errors.md)|Restituisce informazioni sull'errore e/o sull'avviso relativo all'ultima operazione.|  
|[sqlsrv_execute](../../connect/php/sqlsrv-execute.md)|Esegue un'istruzione preparata.|  
|[sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md)|Rende la riga di dati successiva disponibile per la lettura.|  
|[sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md)|Recupera la riga di dati successiva come matrice indicizzata numericamente, matrice associativa o entrambe.|  
|[sqlsrv_fetch_object](../../connect/php/sqlsrv-fetch-object.md)|Recupera la riga di dati successiva come oggetto.|  
|[sqlsrv_field_metadata](../../connect/php/sqlsrv-field-metadata.md)|Restituisce i metadati del campo.|  
|[sqlsrv_free_stmt](../../connect/php/sqlsrv-free-stmt.md)|Chiude un'istruzione. Libera tutte le risorse associate all'istruzione.|  
|[sqlsrv_get_config](../../connect/php/sqlsrv-get-config.md)|Restituisce il valore dell'impostazione di configurazione specificata.|  
|[sqlsrv_get_field](../../connect/php/sqlsrv-get-field.md)|Recupera un campo nella riga corrente in base all'indice. È possibile specificare il tipo PHP restituito.|  
|[sqlsrv_has_rows](../../connect/php/sqlsrv-has-rows.md)|Rileva se il set di risultati include una o più righe.|  
|[sqlsrv_next_result](../../connect/php/sqlsrv-next-result.md)|Rende il risultato successivo disponibile per l'elaborazione.|  
|[sqlsrv_num_rows](../../connect/php/sqlsrv-num-rows.md)|Visualizza il numero di righe di un set di risultati.|  
|[sqlsrv_num_fields](../../connect/php/sqlsrv-num-fields.md)|Recupera il numero di campi in un set di risultati attivo.|  
|[sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)|Prepara una query Transact-SQL senza eseguirla. Associa in modo implicito i parametri.|  
|[sqlsrv_query](../../connect/php/sqlsrv-query.md)|Prepara ed esegue una query Transact-SQL.|  
|[sqlsrv_rollback](../../connect/php/sqlsrv-rollback.md)|Esegue il rollback di una transazione.|  
|[sqlsrv_rows_affected](../../connect/php/sqlsrv-rows-affected.md)|Restituisce il numero di righe modificate.|  
|[sqlsrv_send_stream_data](../../connect/php/sqlsrv-send-stream-data.md)|Invia fino a otto kilobyte (8 KB) di dati al server con ogni chiamata alla funzione.|  
|[sqlsrv_server_info](../../connect/php/sqlsrv-server-info.md)|Fornisce informazioni sul server.|  
  
## <a name="reference"></a>Riferimento  
[Manuale PHP](http://go.microsoft.com/fwlink/?LinkId=105500)  
  
## <a name="see-also"></a>Vedere anche  
[Panoramica del Driver SQL PHP](../../connect/php/overview-of-the-php-sql-driver.md)
[costanti &#40; Driver Microsoft per PHP per SQL Server &#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  
[Guida di programmazione per il driver SQL PHP](../../connect/php/programming-guide-for-php-sql-driver.md)
[Introduzione al driver SQL PHP](../../connect/php/getting-started-with-the-php-sql-driver.md)
  
