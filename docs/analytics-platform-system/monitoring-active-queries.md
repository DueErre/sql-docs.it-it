---
title: Monitoraggio delle query attive (SQL Server PDW)
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/13/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bb73f790-0537-414b-8dc2-f1eb69b92362
caps.latest.revision: "7"
ms.openlocfilehash: b2975ef92cb3af808ea5698f1980af3f9d0996d1
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/17/2017
---
# <a name="monitoring-active-queries"></a>Monitoraggio delle query attive
In questo argomento viene illustrato come utilizzare la Console di amministrazione e le viste di sistema di SQL Server PDW per il monitoraggio delle query attive. Vedere [monitorare il dispositivo tramite la Console di amministrazione](monitor-the-appliance-by-using-the-admin-console.md) e [viste di sistema](tsql-system-views.md) per informazioni su questi strumenti.  
  
## <a name="prerequisites"></a>Prerequisiti  
Indipendentemente dal metodo utilizzato per il monitoraggio delle query attive, l'accesso deve disporre delle autorizzazioni descritte in "Utilizzo tutti della Console di amministrazione" in [Grant-autorizzazioni per utilizzare la Console di amministrazione](grant-permissions.md#grant-permissions-to-use-the-admin-console).  
  
## <a name="PermsAdminConsole"></a>Monitoraggio di query attive  
Sia la Console di amministrazione e le viste di sistema di SQL Server PDW sono utilizzabile per il monitoraggio delle query attive. Seguire le istruzioni seguenti.  
  
### <a name="to-monitor-active-queries-by-using-the-admin-console"></a>Per il monitoraggio delle query attive tramite la Console di amministrazione  
  
1.  Accedere a una Console di amministrazione. Vedere [monitorare il dispositivo tramite la Console di amministrazione](monitor-the-appliance-by-using-the-admin-console.md) per le istruzioni.  
  
2.  Nel menu in alto, fare clic su **query**. Verrà visualizzata una tabella con le informazioni di base sulle query più recente nel dispositivo, inclusi l'account di accesso che ha inviato la query, l'ora di inizio e fine per la query e lo stato corrente della query.  
  
3.  Per visualizzare il comando di query, posizionare il puntatore del mouse su ID di query nella colonna a sinistra per la riga.  
  
    Per visualizzare che ulteriori informazioni dettagliate per una determinata query, scegliere l'ID di query. Verranno visualizzate informazioni tra cui la query completa e il piano di query con informazioni sullo stato per ogni passaggio dell'esecuzione di query. Se sono stati restituiti errori, è anche possibile visualizzare informazioni dettagliate sugli errori. <!-- MISSING LINKS See [Understanding Query Plans &#40;SQL Server PDW&#41;](../sqlpdw/understanding-query-plans-sql-server-pdw.md) for information on how to interpret the query plan information available in the Admin Console.  -->
  
### <a name="to-monitor-active-queries-by-using-the-system-views"></a>Per il monitoraggio delle query attive tramite le viste di sistema  
La vista di sistema principale utilizzata per monitorare le query è [sys.dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md). Utilizzare questa vista di sistema per trovare il `request_id` per una query active o recente, in base al testo della query.  
  
Ad esempio, la query seguente trova i `request_id` corrente e `status` per qualsiasi query che seleziona tutte le colonne di `memberAddresses` tabella.  
  
```sql  
SELECT request_id, command, status   
FROM sys.dm_pdw_exec_requests   
WHERE command   
LIKE ‘%SELECT * FROM db1..memberAddresses%’;  
```  
  
Dopo il `request_id` è stata identificata per una query, utilizzare le altre informazioni presenti il `dm_pdw_exec_requests` per scoprire l'elaborazione della query di tabella oppure utilizzare [sys.dm_pdw_request_steps](../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md) per visualizzare lo stato della query singole passaggi per l'esecuzione della query.  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  