---
title: ALTER EVENT SESSION (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 08/07/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER EVENT SESSION
- ALTER_EVENT_SESSION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- event sessions [SQL Server]
- extended events [SQL Server], Transact-SQL
- ALTER EVENT SESSION statement
ms.assetid: da006ac9-f914-4995-a2fb-25b5d971cd90
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 593be40520403888b5ad2584515820f1935bb270
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="alter-event-session-transact-sql"></a>ALTER EVENT SESSION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Consente di avviare o arrestare una sessione eventi oppure di modificare la configurazione di una sessione eventi.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
ALTER EVENT SESSION event_session_name  
ON SERVER  
{  
    [ [ {  <add_drop_event> [ ,...n] }     
       | { <add_drop_event_target> [ ,...n ] } ]   
    [ WITH ( <event_session_options> [ ,...n ] ) ]  
    ]  
    | [ STATE = { START | STOP } ]  
}  
  
<add_drop_event>::=  
{  
    [ ADD EVENT <event_specifier>   
         [ ( {   
                 [ SET { event_customizable_attribute = <value> [ ,...n ] } ]  
                 [ ACTION ( { [event_module_guid].event_package_name.action_name [ ,...n ] } ) ]  
                 [ WHERE <predicate_expression> ]  
        } ) ]  
   ]   
   | DROP EVENT <event_specifier> }  
  
<event_specifier> ::=  
{  
[event_module_guid].event_package_name.event_name  
}  
  
<predicate_expression> ::=   
{  
    [ NOT ] <predicate_factor> | {( <predicate_expression> ) }   
    [ { AND | OR } [ NOT ] { <predicate_factor> | ( <predicate_expression> ) } ]   
    [ ,...n ]  
}  
  
<predicate_factor>::=   
{  
    <predicate_leaf> | ( <predicate_expression> )  
}  
  
<predicate_leaf>::=  
{  
      <predicate_source_declaration> { = | < > | ! = | > | > = | < | < = } <value>   
    | [event_module_guid].event_package_name.predicate_compare_name ( <predicate_source_declaration>, <value> )   
}  
  
<predicate_source_declaration>::=   
{  
    event_field_name | ( [event_module_guid].event_package_name.predicate_source_name )  
}  
  
<value>::=   
{  
    number | 'string'  
}  
  
<add_drop_event_target>::=  
{  
    ADD TARGET <event_target_specifier>  
        [ ( SET { target_parameter_name = <value> [ ,...n] } ) ]  
    | DROP TARGET <event_target_specifier>  
}  
  
<event_target_specifier>::=  
{  
    [event_module_guid].event_package_name.target_name  
}  
  
<event_session_options>::=  
{  
    [    MAX_MEMORY = size [ KB | MB] ]  
    [ [,] EVENT_RETENTION_MODE = { ALLOW_SINGLE_EVENT_LOSS | ALLOW_MULTIPLE_EVENT_LOSS | NO_EVENT_LOSS } ]  
    [ [,] MAX_DISPATCH_LATENCY = { seconds SECONDS | INFINITE } ]  
    [ [,] MAX_EVENT_SIZE = size [ KB | MB ] ]  
    [ [,] MEMORY_PARTITION_MODE = { NONE | PER_NODE | PER_CPU } ]  
    [ [,] TRACK_CAUSALITY = { ON | OFF } ]  
    [ [,] STARTUP_STATE = { ON | OFF } ]  
}  
```  
  
## <a name="arguments"></a>Argomenti  
  
|||  
|-|-|  
|Nome|Definizione|  
|*event_session_name*|Nome di una sessione dell'evento esistente.|  
|STATO = INIZIO &#124; ARRESTA|Avvia o arresta la sessione dell'evento. Questo argomento è valido solo quando ALTER EVENT SESSION è applicato a un oggetto della sessione dell'evento.|  
|Aggiungi evento \<event_specifier >|Associa l'evento identificato da \<event_specifier > con la sessione dell'evento.|
|[*event_module_guid*]*. event_package_name.event_name*|Nome di un evento in un pacchetto dell'evento dove:<br /><br /> -   *event_module_guid* è il GUID per il modulo che contiene l'evento.<br />-   *event_package_name* è il pacchetto che contiene l'oggetto azione.<br />-   *EVENT_NAME* è l'oggetto evento.<br /><br /> Gli eventi vengono visualizzati nella vista sys.dm_xe_objects come object_type "event".|  
|SET { *event_customizable_attribute*= \<valore > [,... *n*] }|Specifica gli attributi personalizzabili per l'evento. Gli attributi personalizzabili vengono visualizzati nella vista sys.dm xe_object_columns come column_type 'customizable' e object_name = *event_name*.|  
|AZIONE ({[*event_module_guid*]*. event_package_name.action_name* [ **,**... *n*] } )|Azione da associare alla sessione dell'evento, dove:<br /><br /> -   *event_module_guid* è il GUID per il modulo che contiene l'evento.<br />-   *event_package_name* è il pacchetto che contiene l'oggetto azione.<br />-   *nome_azione* è l'oggetto azione.<br /><br /> Le azioni vengono visualizzate nella vista sys.dm_xe_objects come object_type "action".|  
|DOVE \<predicate_expression >|Indica l'espressione del predicato utilizzata per determinare se un evento deve essere elaborato. Se \<predicate_expression > è true, l'evento viene elaborato ulteriormente dalle azioni e destinazioni della sessione. Se \<predicate_expression > è false, l'evento viene rimosso dalla sessione prima di essere elaborato dalle azioni e destinazioni per la sessione. Le espressioni del predicato possono essere composte da un massimo di 3000 caratteri, pertanto gli argomenti di tipo stringa risultano limitati.|
|*event_field_name*|Nome del campo relativo all'evento che consente di identificare l'origine del predicato.|  
|[event_module_guid].event_package_name.predicate_source_name|Nome dell'origine del predicato globale dove:<br /><br /> -   *event_module_guid* è il GUID per il modulo che contiene l'evento.<br />-   *event_package_name* è il pacchetto che contiene l'oggetto del predicato.<br />-   *predicate_source_name* è definito nella vista sys.dm xe_objects come object_type "pred_source".|  
|[*event_module_guid*]. *event_package_name*. *predicate_compare_name*|Nome dell'oggetto del predicato da associare all'evento, dove:<br /><br /> -   *event_module_guid* è il GUID per il modulo che contiene l'evento.<br />-   *event_package_name* è il pacchetto che contiene l'oggetto del predicato.<br />-   *predicate_compare_name* è un'origine globale definita nella vista sys.dm xe_objects come object_type "pred_compare".|  
|DROP EVENT \<event_specifier >|Elimina l'evento identificato da  *\<event_specifier >*. \<event_specifier > deve essere valido nella sessione dell'evento.|  
|Aggiungi destinazione \<event_target_specifier >|Associa la destinazione identificata da \<event_target_specifier > con la sessione dell'evento.|
|[*event_module_guid*]. *event_package_name*. *target_name*|Nome di una destinazione nella sessione dell'evento dove:<br /><br /> -   *event_module_guid* è il GUID per il modulo che contiene l'evento.<br />-   *event_package_name* è il pacchetto che contiene l'oggetto azione.<br />-   *target_name* è l'azione. Le azioni vengono visualizzate nella vista sys.dm_xe_objects come object_type "target".|  
|SET { *target_parameter_name*= \<valore > [,... *n*] }|Imposta un parametro di destinazione. I parametri di destinazione vengono visualizzati nella vista sys.dm xe_object_columns come column_type 'customizable' e object_name = *target_name*.<br /><br /> **NOTA** Se si utilizza il buffer circolare come destinazione, si consiglia di impostare il parametro di destinazione max_memory su 2048 kilobyte (KB) per evitare il possibile troncamento dei dati dell'output XML. Per ulteriori informazioni sull'utilizzo di diversi tipi di destinazione, vedere [SQL Server Extended Events Targets](http://msdn.microsoft.com/library/e281684c-40d1-4cf9-a0d4-7ea1ecffa384).|  
|OBIETTIVO di rilascio \<event_target_specifier >|Elimina la destinazione identificata da \<event_target_specifier >. \<event_target_specifier > deve essere valido nella sessione dell'evento.|  
|EVENT_RETENTION_MODE = { **ALLOW_SINGLE_EVENT_LOSS** &#124; ALLOW_MULTIPLE_EVENT_LOSS &#124; NO_EVENT_LOSS}|Specifica la modalità di memorizzazione dell'evento da utilizzare per la gestione della perdita di eventi.<br /><br /> **ALLOW_SINGLE_EVENT_LOSS**<br /> Un evento può essere perso dalla sessione. Un evento singolo viene eliminato solo quando tutti i buffer dell'evento sono pieni. La perdita di un singolo evento i buffer sono pieni garantisce un livello accettabile delle prestazioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], riducendo al minimo il rischio di perdita dei dati nel flusso di eventi elaborati.<br /><br /> ALLOW_MULTIPLE_EVENT_LOSS<br /> È possibile che vengano persi i buffer dell'evento pieni contenenti più eventi. Il numero di eventi persi dipende dalla dimensione della memoria allocata alla sessione, dalla partizione della memoria e dalla dimensione degli eventi nel buffer. Questa opzione riduce al minimo l'impatto sulle prestazioni dei server quando i buffer degli eventi vengono riempiti rapidamente, ma numerosi eventi della sessione possono andare persi.<br /><br /> NO_EVENT_LOSS<br /> Non è consentita alcuna perdita di eventi. Questa opzione assicura che tutti gli eventi generati vengano mantenuti. L'utilizzo di questa opzione forza tutte le attività che attivano eventi ad aspettare fino a che lo spazio è disponibile in un buffer degli eventi. Questo può condurre a problemi di prestazione mentre la sessione dell'evento è attiva. Le connessioni utente potrebbero bloccarsi in attesa che gli eventi vengano scaricati dal buffer.|  
|MAX_DISPATCH_LATENCY = { *secondi* secondi &#124; **Infinito** }|Specifica il tempo necessario all'esecuzione del buffer degli eventi nella memoria prima che vengano resi disponibili nelle destinazioni della sessione. Il valore di latenza minimo è 1 secondo. È tuttavia possibile utilizzare il valore 0 per specificare una latenza infinita. Per impostazione predefinita, questo valore è impostato su 30 secondi.<br /><br /> *secondi* secondi<br /> Tempo di attesa, espresso in secondi, prima che venga avviato lo scaricamento dei buffer alle destinazioni. *secondi* è un numero intero.<br /><br /> **INFINITO**<br /> Scarica i buffer nelle destinazioni solo quando i buffer sono pieni o alla chiusura della sessione dell'evento.<br /><br /> **NOTA** MAX_DISPATCH_LATENCY = 0 SECONDS è equivalente a MAX_DISPATCH_LATENCY = INFINITE.|  
|MAX_EVENT_SIZE =*dimensioni* [KB &#124; **MB** ]|Specifica la dimensione massima consentita per gli eventi. MAX_EVENT_SIZE deve essere impostato solo per consentire singoli eventi di dimensioni superiori a quelle di MAX_MEMORY. L'impostazione su un valore inferiore a quello di MAX_MEMORY genera un errore. *dimensioni* è un numero intero e può essere espresso in kilobyte (KB) o un valore di megabyte (MB). Se *dimensioni* è specificato in kilobyte, la dimensione minima consentita è di 64 KB. Quando viene impostato MAX_EVENT_SIZE, due buffer di *dimensioni* vengono creati, oltre a MAX_MEMORY. Ciò significa che la memoria totale utilizzata per la memorizzazione degli eventi nel buffer è MAX_MEMORY + 2 * MAX_EVENT_SIZE.|  
|MEMORY_PARTITION_MODE = { **NONE** &#124; PER_NODE &#124; PER_CPU}|Specifica la posizione di creazione dei buffer dell'evento.<br /><br /> **NONE**<br /> Nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene creato un unico set di buffer.<br /><br /> Per ogni nodo, viene creato un set di buffer per ogni nodo NUMA.<br /><br /> Per ogni CPU - viene creato un set di buffer per ogni CPU.|  
|TRACK_CAUSALITY = {ON &#124; **OFF** }|Specifica se viene tenuta traccia della causalità. Se abilitato, la causalità consente la correlazione di eventi correlati in diverse connessioni server.|  
|STARTUP_STATE = {ON &#124; **OFF** }|Specifica se avviare automaticamente questa sessione dell'evento all'avvio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Se STARTUP_STATE = ON, la sessione dell'evento verrà avviato solo se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene arrestato e riavviato.<br /><br /> IN = evento di sessione viene avviata all'avvio.<br /><br /> **DISATTIVARE** = evento di sessione non è stata avviata all'avvio.|  
  
## <a name="remarks"></a>Osservazioni  
 Non è possibile utilizzare gli argomenti ADD e DROP nella stessa istruzione.  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione ALTER ANY EVENT SESSION.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene avviata una sessione dell'evento, vengono ottenute alcune statistiche della sessione attiva e infine vengono aggiunti due eventi alla sessione esistente.  
  
```  
-- Start the event session  
ALTER EVENT SESSION test_session  
ON SERVER  
STATE = start;  
GO  
-- Obtain live session statistics   
SELECT * FROM sys.dm_xe_sessions;  
SELECT * FROM sys.dm_xe_session_events;  
GO  
  
-- Add new events to the session  
ALTER EVENT SESSION test_session ON SERVER  
ADD EVENT sqlserver.database_transaction_begin,  
ADD EVENT sqlserver.database_transaction_end;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-session-transact-sql.md)   
 [DROP EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-event-session-transact-sql.md)   
 [Destinazioni degli eventi estesi di SQL Server](http://msdn.microsoft.com/library/e281684c-40d1-4cf9-a0d4-7ea1ecffa384)   
 [server_event_sessions &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-server-event-sessions-transact-sql.md)   
 [Sys.dm xe_objects &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-objects-transact-sql.md)   
 [sys.dm_xe_object_columns &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-object-columns-transact-sql.md)  
  
  
