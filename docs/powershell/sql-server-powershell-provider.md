---
title: Provider PowerShell per SQL Server | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: powershell
ms.service: 
ms.component: powershell
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- PowerShell [SQL Server], provider
- PowerShell [SQL Server], SQL Server PowerShell Provider
- Providers [PowerShell]
- SMO [SQL Server], PowerShell
- PowerShell [SQL Server], SMO
- SQL Server Management Objects, PowerShell
ms.assetid: b97acc43-fcd2-4ae5-b218-e183bab916f9
caps.latest.revision: "61"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 25efe8ce2a9ee4bd0af52a04e6f2d09f47a60396
ms.sourcegitcommit: 779f3398e4e3f4c626d81ae8cedad153bee69540
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/16/2018
---
# <a name="sql-server-powershell-provider"></a>Provider PowerShell per SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Il provider [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per Windows PowerShell espone la gerarchia degli oggetti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in percorsi simili ai percorsi del file system. È possibile usare i percorsi per trovare un oggetto e, successivamente, usare i metodi dei modelli SMO ( [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Management Objects) per eseguire azioni sugli oggetti.  
  
> [!NOTE]
> Esistono due moduli SQL Server PowerShell: **SqlServer** e **SQLPS**. Il modulo **SQLPS** è incluso nell'installazione di SQL Server (per la compatibilità con le versioni precedenti), ma non viene più aggiornato. Il modulo PowerShell più aggiornato è il modulo **SqlServer**. Il modulo **SqlServer** contiene versioni aggiornate dei cmdlet di **SQLPS** e include anche nuovi cmdlet per il supporto delle funzionalità SQL più recenti.  
> Le versioni precedenti del modulo **SqlServer** *erano* incluse con SQL Server Management Studio (SSMS), ma solo con le versioni 16.x di SQL Server Management Studio. Per usare PowerShell con SSMS 17.0 e versioni successive, è necessario installare il modulo **SqlServer** da PowerShell Gallery.
> Per installare il modulo **SqlServer**, vedere [Installare il modulo PowerShell SqlServer](download-sql-server-ps-module.md).


## <a name="benefits-of-the-sql-server-powershell-provider"></a>Vantaggi del provider PowerShell per SQL Server  
 Attraverso i percorsi implementati dal provider di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] è possibile verificare facilmente e in modo interattivo tutti gli oggetti in un'istanza di SQL Server. È possibile spostarsi tra i percorsi utilizzando alias di Windows PowerShell simili ai comandi normalmente utilizzati per spostarsi tra i percorsi del file system.  
  
## <a name="the-sql-server-powershell-hierarchy"></a>Gerarchia di SQL Server PowerShell  
 Nei prodotti in cui i dati o i modelli a oggetti possono essere rappresentati in una gerarchia, per esporre le gerarchie vengono utilizzati i provider Windows PowerShell. La gerarchia viene esposta utilizzando una struttura di unità e percorsi simile a quelle utilizzate dal file system di Windows.  
  
 Ciascun provider Windows PowerShell implementa una o più unità. Ciascuna unità è il nodo radice di una gerarchia di oggetti correlati. Il provider [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] implementa un'unità SQLSERVER:. Nel provider viene inoltre definito un set di cartelle primarie per l'unità SQLSERVER:. Ogni cartella e le relative sottocartelle rappresentano il set di oggetti a cui è possibile accedere usando un modello SMO ( [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Management Objects). Quando si seleziona una sottocartella in un percorso che inizia con una di queste cartelle principali, è possibile utilizzare i metodi del modello a oggetti associato per eseguire azioni sull'oggetto rappresentato dal nodo. Le cartelle di Windows PowerShell implementate dal provider [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] sono elencate nella tabella seguente:  
  
|Cartella|Spazio dei nomi del modello a oggetti di SQL Server|Oggetti|  
|------------|---------------------------------------|-------------|  
|SQLSERVER:\SQL|<xref:Microsoft.SqlServer.Management.Smo><br /><br /> <xref:Microsoft.SqlServer.Management.Smo.Agent><br /><br /> <xref:Microsoft.SqlServer.Management.Smo.Broker><br /><br /> <xref:Microsoft.SqlServer.Management.Smo.Mail>|Oggetti di database, come tabelle, viste e stored procedure.|  
|SQLSERVER:\SQLPolicy|<xref:Microsoft.SqlServer.Management.Dmf><br /><br /> <xref:Microsoft.SqlServer.Management.Facets>|Oggetti di gestione basata sui criteri, come criteri e facet.|  
|SQLSERVER:\SQLRegistration|<xref:Microsoft.SqlServer.Management.RegisteredServers><br /><br /> <xref:Microsoft.SqlServer.Management.Smo.RegSvrEnum>|Oggetti server registrati, come gruppi di server e server registrati.|  
|SQLSERVER:\Utility|<xref:Microsoft.SqlServer.Management.Utility>|Oggetti utilità, ad esempio le istanze gestite del [!INCLUDE[ssDE](../includes/ssde-md.md)].|  
|SQLSERVER:\DAC|<xref:Microsoft.SqlServer.Management.DAC>|Oggetti applicazione del livello dati, ad esempio pacchetti DAC e operazioni quali l'implementazione di DAC.|  
|SQLSERVER:\DataCollection|<xref:Microsoft.SqlServer.Management.Collector>|Oggetti dell'agente di raccolta dati, ad esempio set di raccolta e archivi di configurazione.|  
|SQLSERVER:\IntegrationServices|<xref:Microsoft.SqlServer.Management.IntegrationServices>|[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] oggetti come progetti, pacchetti e ambienti.|  
|SQLSERVER:\SQLAS|<xref:Microsoft.AnalysisServices>|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] oggetti come cubi, aggregazioni e dimensioni.|  
  
 È ad esempio possibile utilizzare la cartella SQLSERVER:\SQL per iniziare percorsi che possono rappresentare qualsiasi oggetto supportato dal modello a oggetti SMO. La parte iniziale di un percorso SQLSERVER:\SQL è SQLSERVER:\SQL\\*NomeComputer*\\*NomeIstanza*. I nodi che seguono il nome dell'istanza possono essere raccolte di oggetti, come *Database* o *Viste*, e nomi di oggetti, ad esempio AdventureWorks2012. Gli schemi non sono rappresentati come classi di oggetti. Quando si specifica il nodo per un oggetto di livello principale in uno schema, ad esempio una tabella o una vista, è necessario specificare il nome dell'oggetto nel formato *NomeSchema.NomeOggetto*.  
  
 L'esempio seguente illustra il percorso della tabella Vendor nello schema Purchasing del database AdventureWorks2012 in un'istanza predefinita del [!INCLUDE[ssDE](../includes/ssde-md.md)] nel computer locale:  
  
```  
SQLSERVER:\SQL\localhost\DEFAULT\Databases\AdventureWorks2012\Tables\Purchasing.Vendor  
```  
  
 Per altre informazioni sulla gerarchia del modello a oggetti SMO, vedere [Diagramma del modello a oggetti SMO](../relational-databases/server-management-objects-smo/smo-object-model-diagram.md).  
  
 I nodi delle raccolte in un percorso sono associati a una classe di raccolte nel modello a oggetti associato. I nodi dei nomi di oggetti sono associati a una classe di oggetti nel modello a oggetti associato, come indicato nella tabella seguente:  
  
|Percorso|Classe SMO|  
|----------|---------------|  
|SQLSERVER:\SQL\MyComputer\DEFAULT\Databases|<xref:Microsoft.SqlServer.Management.Smo.DatabaseCollection>|  
|SQLSERVER:\SQL\MyComputer\DEFAULT\Databases\AdventureWorks2012|<xref:Microsoft.SqlServer.Management.Smo.Database>|  
  
## <a name="sql-server-provider-tasks"></a>Attività del provider di SQL Server  
  
|Descrizione dell'attività|Articolo|  
|----------------------|-----------|  
|Viene descritto come utilizzare i cmdlet di Windows PowerShell per spostarsi tra i nodi all'interno di un percorso e, a ogni nodo, ottenere un elenco degli oggetti in corrispondenza di quel nodo.|[Spostarsi all'interno dei percorsi di SQL Server PowerShell](navigate-sql-server-powershell-paths.md)|  
|Viene descritto come utilizzare i metodi e le proprietà SMO per eseguire report e attività sull'oggetto rappresentato da un nodo in un percorso. Viene inoltre descritto come ottenere un elenco dei metodi e delle proprietà SMO per quel nodo.|[Utilizzo di percorsi di SQL Server PowerShell](work-with-sql-server-powershell-paths.md)|  
|Viene descritto come convertire un Uniform Resource Name SMO (URN) in un percorso del provider SQL Server.|[Conversione di URN in percorsi di provider di SQL Server](https://docs.microsoft.com/powershell/module/sqlserver/Convert-UrnToPath)|  
|Viene descritto come stabilire connessioni con autenticazione di SQL Server tramite il provider di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Per impostazione predefinita, il provider utilizza connessioni di autenticazione di Windows stabilite mediante le credenziali dell'account di Windows che esegue il processo di Windows PowerShell.|[Gestire l'autenticazione nel motore di database PowerShell](manage-authentication-in-database-engine-powershell.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  
