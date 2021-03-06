---
title: Database di ALTER DATABASE Mirroring (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 08/17/2017
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
dev_langs:
- TSQL
helpviewer_keywords:
- witness [SQL Server], establishing
- manual failover [SQL Server]
- ALTER DATABASE statement, database mirroring
- database mirroring [SQL Server], Transact-SQL
ms.assetid: 27a032ef-1cf6-4959-8e67-03d28c4b3465
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 54396925abb0e8eb2d6006ffdd4048551792d6db
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2018
---
# <a name="alter-database-transact-sql-database-mirroring"></a>ALTER DATABASE (Transact-SQL) Database Mirroring 
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Utilizzare [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] invece.  
  
 Controlla il mirroring del database per un database. I valori specificati per le opzioni di mirroring del database vengono applicati a entrambe le copie del database e alla sessione di mirroring del database nella sua globalità. Un solo \<database_mirroring_option > è consentito per l'istruzione ALTER DATABASE.  
  
> [!NOTE]  
>  È consigliabile configurare il mirroring del database durante le fasce orarie di minore attività, dato che la configurazione può influire sulle prestazioni.  
  
 Per le opzioni di ALTER DATABASE, vedere [ALTER DATABASE &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql.md). Per le opzioni di ALTER DATABASE SET, vedere [opzioni ALTER DATABASE SET &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
ALTER DATABASE database_name   
SET { <partner_option> | <witness_option> }  
  <partner_option> ::=  
    PARTNER { = 'partner_server'   
            | FAILOVER   
            | FORCE_SERVICE_ALLOW_DATA_LOSS  
            | OFF  
            | RESUME   
            | SAFETY { FULL | OFF }  
            | SUSPEND   
            | TIMEOUT integer  
            }  
  <witness_option> ::=  
    WITNESS { = 'witness_server'   
            | OFF   
            }  
  
```  
  
## <a name="arguments"></a>Argomenti  
  
> [!IMPORTANT]  
>  È possibile che un comando SET PARTNER o SET WITNESS venga completato correttamente al momento dell'immissione, ma non riesca in un secondo momento.  
  
> [!NOTE]  
>  Le opzioni di mirroring ALTER DATABASE non sono disponibili per un database indipendente.  
  
 *database_name*  
 Nome del database da modificare.  
  
 PARTNER \<partner_option >  
 Controlla le proprietà del database che definiscono i partner di failover di una sessione di mirroring del database e il relativo comportamento. Alcune opzioni SET PARTNER possono essere impostate indifferentemente in uno dei partner. Altre sono supportate solo nel server principale o nel server mirror. Per ulteriori informazioni, vedere le descrizioni seguenti delle singole opzioni PARTNER. La clausola SET PARTNER influisce su entrambe le copie del database, indipendentemente dal partner in cui viene specificata.  
  
 Per eseguire un'istruzione SET PARTNER, l'opzione STATE degli endpoint di entrambi i partner deve essere impostata su STARTED. Si noti, inoltre, che l'opzione ROLE dell'endpoint di mirroring del database di ogni istanza del server partner deve essere impostata su PARTNER o su ALL. Per informazioni su come specificare un endpoint, vedere [creare un Database Mirroring Endpoint per l'autenticazione Windows &#40; Transact-SQL &#41; ](../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md). Per informazioni sul ruolo e sullo stato dell'endpoint di mirroring del database per un'istanza del server, utilizzare l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] seguente in tale istanza:  
  
```  
SELECT role_desc, state_desc FROM sys.database_mirroring_endpoints  
```  
  
 **\<partner_option> ::=**  
  
> [!NOTE]  
>  Un solo \<partner_option > è consentito per ogni clausola SET PARTNER.  
  
 **'** *partner_server* **'**  
 Specifica l'indirizzo di rete del server di un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che fungerà da partner di failover in una nuova sessione di mirroring del database. Ogni sessione deve includere due partner, uno avviato come server principale e l'altro come server mirror. È consigliabile che tali partner si trovino in computer diversi.  
  
 Questa opzione viene specificata una sola volta per sessione in ogni partner. Avviare una sessione di mirroring del database richiede due ALTER DATABASE *database* SET PARTNER **='***partner_server***'** istruzioni. L'ordine con cui vengono specificate è significativo. In primo luogo, connettersi al server mirror e specificare l'istanza del server principale come *partner_server* (SET PARTNER **='***principal_server***'**). In secondo luogo, connettersi al server principale e specificare l'istanza del server mirror come *partner_server* (SET PARTNER **='***mirror_server***'**); verrà avviato un database sessione tra i due partner di mirroring. Per ulteriori informazioni, vedere [Impostazione del mirroring del database &#40;SQL Server&#41;](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md).  
  
 Il valore di *partner_server* è un indirizzo di rete. La sintassi è la seguente:  
  
 TCP **://***\<indirizzo-sistema >***: * * *\<porta >*  
  
 dove  
  
-   *\<indirizzo-sistema >* è una stringa, ad esempio un nome di sistema, un nome di dominio completo o un indirizzo IP, che identifichi univocamente il sistema di computer di destinazione.  
  
-   *\<porta >* è un numero di porta associato all'endpoint del mirroring dell'istanza del server partner.  
  
 Per altre informazioni, vedere [Specificare un indirizzo di rete del server &#40;Mirroring del database&#41;](../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md).  
  
 Nell'esempio seguente viene illustrato il SET PARTNER **='***partner_server***'** clausola:  
  
```  
'TCP://MYSERVER.mydomain.Adventure-Works.com:7777'  
```  
  
> [!IMPORTANT]  
>  Se una sessione viene configurata tramite l'istruzione ALTER DATABASE anziché con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], per la sessione viene specificato per impostazione predefinita il livello di protezione completo delle transazioni (opzione SAFETY impostata su FULL) e tale sessione viene eseguita in modalità a protezione elevata senza failover automatico. Per consentire il failover automatico, configurare un server di controllo del mirroring. Per l'esecuzione in modalità a prestazioni elevate, disattivare la protezione delle transazioni (opzione SAFETY impostata su OFF).  
  
 FAILOVER  
 Esegue manualmente il failover del server principale nel server mirror. È possibile specificare l'opzione FAILOVER solo nel server principale. Questa opzione è valida solo con l'impostazione FULL per SAFETY (impostazione predefinita).  
  
 L'opzione di FAILOVER richiede **master** come contesto di database.  
  
 FORCE_SERVICE_ALLOW_DATA_LOSS  
 Forza il servizio di database nel database mirror in seguito a errori del server principale con il database in stato non sincronizzato o in stato sincronizzato, quando il failover automatico non si verifica.  
  
 È consigliabile forzare il servizio solo se il server principale non è più in esecuzione. In caso contrario, alcuni client potrebbero continuare ad accedere al database principale originale anziché al nuovo database principale.  
  
 FORCE_SERVICE_ALLOW_DATA_LOSS è disponibile solo nel server mirror ed esclusivamente quando sono valide tutte le condizioni seguenti:  
  
-   Il server principale non è disponibile.  
  
-   L'opzione WITNESS è impostata su OFF o il server di controllo del mirroring è connesso al server mirror.  
  
 Forzare il servizio solo se il rischio di perdita parziale dei dati è accettabile al fine di ripristinare immediatamente il database.  
  
 Quando si forza il servizio, la sessione viene sospesa mantenendo temporaneamente tutti i dati nel database principale originale. Dopo che il server principale originale viene attivato ed è in grado di comunicare con il nuovo server principale, l'amministratore del database può ripristinare il servizio. Alla ripresa della sessione, tutti i record di log non inviati e gli aggiornamenti corrispondenti vengono persi.  
  
 OFF  
 Rimuove una sessione di mirroring del database e rimuove il mirroring dal database. È possibile specificare l'opzione OFF in qualsiasi partner. Per informazioni sull'impatto della rimozione del mirroring, vedere [rimozione del mirroring del Database &#40; SQL Server &#41; ](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md).  
  
 RESUME  
 Riprende una sessione di mirroring del database sospesa. È possibile specificare l'opzione RESUME solo nel server principale.  
  
 SAFETY { FULL | OFF }  
 Imposta il livello di protezione delle transazioni. È possibile specificare l'opzione SAFETY solo nel server principale.  
  
 Il valore predefinito è FULL. Con la protezione completa, il sessione di mirroring del database viene eseguito in modo sincrono (in *modalità a sicurezza elevata*). Se la protezione è impostata su OFF, il sessione di mirroring del database viene eseguito in modo asincrono (in *modalità a prestazioni elevate*).  
  
 Il comportamento della modalità a protezione elevata dipende in parte dal server di controllo del mirroring, come indicato di seguito:  
  
-   Se la protezione è impostata su FULL e per la sessione è impostato un server di controllo del mirroring, la sessione viene eseguita in modalità a protezione elevata con failover automatico. Quando il server principale non è più disponibile, viene eseguito il failover automatico della sessione se il database è sincronizzato e se l'istanza del server mirror e il server di controllo del mirroring sono ancora connessi tra loro, ovvero se dispongono di un quorum. Per altre informazioni, vedere [Quorum: Impatto di un server di controllo del mirroring sulla disponibilità del database &#40;mirroring del database&#41;](../../database-engine/database-mirroring/quorum-how-a-witness-affects-database-availability-database-mirroring.md).  
  
     Se per la sessione è impostato un server di controllo del mirroring ma quest'ultimo è disconnesso, in caso di interruzione del server mirror il server principale si arresta.  
  
-   Se la protezione è impostata su FULL e il server di controllo del mirroring è impostato su OFF, la sessione viene eseguita in modalità a protezione elevata senza failover automatico. Un eventuale arresto dell'istanza del server mirror non influisce sul server principale. Se l'istanza del server principale si arresta, è possibile forzare il servizio nell'istanza del server mirror, con una possibile perdita di dati.  
  
 Se l'opzione SAFETY è impostata su OFF, la sessione viene eseguita in modalità a prestazioni elevate, in cui non sono supportati né il failover automatico né quello manuale. I problemi del server mirror, tuttavia, non influiscono sul server principale. Se l'istanza del server principale si arresta e l'opzione WITNESS è impostata su OFF o il server di controllo del mirroring è connesso al server mirror, è possibile, se necessario, forzare il servizio nell'istanza del server mirror, con una possibile perdita di dati. Per ulteriori informazioni sulla forzatura del servizio, vedere "FORCE_SERVICE_ALLOW_DATA_LOSS" più indietro in questa sezione.  
  
> [!IMPORTANT]  
>  La modalità a prestazioni elevate non prevede l'utilizzo di un server di controllo del mirroring. Ogni volta che l'opzione SAFETY viene impostata su OFF, è tuttavia consigliabile verificare che l'opzione WITNESS sia impostata su OFF.  
  
 SUSPEND  
 Sospende una sessione di mirroring del database.  
  
 È possibile specificare l'opzione SUSPEND in qualsiasi partner.  
  
 TIMEOUT *integer*  
 Specifica il periodo di timeout in secondi. Il periodo di timeout indica l'intervallo di attesa massimo rispettato dall'istanza del server per la ricezione di un messaggio PING da un'altra istanza nella sessione di mirroring, prima che l'altra istanza venga considerata disconnessa.  
  
 È possibile specificare l'opzione TIMEOUT solo nel server principale. Se non si specifica questa opzione, il periodo di timeout predefinito è di 10 secondi. Se si specifica un valore maggiore o uguale a 5, il periodo di timeout viene impostato sul numero di secondi specificato. Se si specifica un valore di timeout compreso tra 0 e 4 secondi, l'intervallo viene impostato automaticamente su 5 secondi.  
  
> [!IMPORTANT]  
>  È consigliabile usare un periodo di timeout di almeno 10 secondi. Con un valore inferiore a 10 secondi, può verificarsi un sovraccarico del sistema, con perdita di PING e generazione di falsi errori.  
  
 Per altre informazioni, vedere [Possibili errori durante il mirroring del database](../../database-engine/database-mirroring/possible-failures-during-database-mirroring.md).  
  
 Controllo del mirroring \<witness_option >  
 Controlla le proprietà del database che definiscono un server di controllo del mirroring del database. La clausola SET WITNESS influisce su entrambe le copie del database, ma è possibile specificare SET WITNESS solo nel server principale. Se un server di controllo è impostato per una sessione, il quorum è necessario per rendere disponibile il database, indipendentemente dall'impostazione della sicurezza; Per ulteriori informazioni, vedere [Quorum: come un server di controllo influisce sulla disponibilità del Database &#40; mirroring del Database &#41;](../../database-engine/database-mirroring/quorum-how-a-witness-affects-database-availability-database-mirroring.md).  
  
 È consigliabile che il server di controllo del mirroring e i partner di failover si trovino in computer diversi. Per informazioni su controllo del mirroring, vedere [di controllo del Mirroring del Database](../../database-engine/database-mirroring/database-mirroring-witness.md).  
  
 Per eseguire un'istruzione SET WITNESS, l'opzione STATE degli endpoint deve essere impostata su STARTED sia nell'istanza del server principale che nell'istanza del server di controllo del mirroring. Si noti, inoltre, che l'opzione ROLE dell'endpoint di mirroring del database di un'istanza del server di controllo del mirroring deve essere impostata su WITNESS o su ALL. Per informazioni su come specificare un endpoint, vedere [Endpoint del Mirroring del Database &#40; SQL Server &#41; ](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md).  
  
 Per informazioni sul ruolo e sullo stato dell'endpoint di mirroring del database per un'istanza del server, utilizzare l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] seguente in tale istanza:  
  
```  
SELECT role_desc, state_desc FROM sys.database_mirroring_endpoints  
```  
  
> [!NOTE]  
>  Non è possibile impostare le proprietà del database nel server di controllo del mirroring.  
  
 **\<witness_option> ::=**  
  
> [!NOTE]  
>  Un solo \<witness_option > è consentito per ogni clausola SET WITNESS.  
  
 **'** *witness_server* **'**  
 Specifica un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] da utilizzare come server di controllo del mirroring per una sessione di mirroring del database. È possibile specificare istruzioni SET WITNESS solo nel server principale.  
  
 In un SET WITNESS **='***witness_server***'** istruzione, la sintassi di *witness_server* è uguale alla sintassi di *partner_server*.  
  
 OFF  
 Rimuove il server di controllo del mirroring da una sessione di mirroring del database. L'impostazione del server di controllo del mirroring su OFF disabilita il failover automatico. Se per il database l'opzione SAFETY è impostata su FULL e il server di controllo del mirroring è impostato su OFF, in caso di errore nel server mirror, il server principale rende il database non disponibile.  
  
## <a name="remarks"></a>Osservazioni  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-creating-a-database-mirroring-session-with-a-witness"></a>A. Creazione di una sessione di mirroring del database con un server di controllo del mirroring  
 Per configurare il mirroring del database con un server di controllo del mirroring, è necessario configurare la sicurezza e preparare il database mirror, nonché utilizzare l'istruzione ALTER DATABASE per l'impostazione dei partner. Per un esempio del processo di installazione completa, vedere [impostazione mirroring del Database &#40; SQL Server &#41; ](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md).  
  
### <a name="b-manually-failing-over-a-database-mirroring-session"></a>B. Failover manuale di una sessione di mirroring del database  
 È possibile avviare il failover manuale da qualsiasi partner di mirroring del database. Prima di eseguire il failover, è necessario verificare che il server che si ritiene essere il server principale corrente, sia effettivamente il server principale. Nel caso del database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)], ad esempio, eseguire la query seguente nell'istanza del server che si ritiene essere il server principale corrente:  
  
```  
SELECT db.name, m.mirroring_role_desc   
FROM sys.database_mirroring m   
JOIN sys.databases db  
ON db.database_id = m.database_id  
WHERE db.name = N'AdventureWorks2012';   
GO  
```  
  
 Se l'istanza del server in oggetto è effettivamente il server principale, il valore di `mirroring_role_desc` è `Principal`. Se questa istanza del server fosse invece il server mirror, l'istruzione `SELECT` restituirebbe `Mirror`.  
  
 Nell'esempio seguente si presuppone che il server sia il server principale corrente.  
  
1.  Eseguire il failover manuale nel partner di mirroring del database:  
  
    ```  
    ALTER DATABASE AdventureWorks2012 SET PARTNER FAILOVER;  
    GO  
    ```  
  
2.  Per verificare i risultati del failover nel nuovo server mirror, eseguire la query seguente:  
  
    ```  
    SELECT db.name, m.mirroring_role_desc   
    FROM sys.database_mirroring m   
    JOIN sys.databases db  
    ON db.database_id = m.database_id  
    WHERE db.name = N'AdventureWorks2012';   
    GO  
    ```  
  
     Il valore corrente di `mirroring_role_desc` è ora `Mirror`.  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [sys.database_mirroring_witnesses &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)  
  
  
