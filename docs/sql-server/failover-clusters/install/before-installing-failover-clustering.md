---
title: Operazioni preliminari all'installazione del clustering di failover | Microsoft Docs
ms.custom: 
ms.date: 08/24/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: failover-clusters
ms.reviewer: 
ms.suite: sql
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- clusters [SQL Server], preinstallation checklist
- installing failover clusters
- failover clustering [SQL Server], preinstallation checklist
ms.assetid: a655225d-8c54-4b30-95fd-31f588167899
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: ad89b5180e55bbbcdde55e2856588ca46695baa1
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/15/2018
---
# <a name="before-installing-failover-clustering"></a>Operazioni preliminari all'installazione del clustering di failover
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Prima di installare un cluster di failover di SQL Server è necessario selezionare l'hardware e il sistema operativo usati per l'esecuzione di SQL Server. È inoltre necessario configurare il clustering di failover di Windows Server (WSFC) ed esaminare le considerazioni relative alla rete, alla sicurezza e agli altri software che verranno eseguiti nel cluster di failover.  
  
 Se un cluster Windows dispone di un'unità disco locale e la stessa lettera di unità viene utilizzata anche in uno o più nodi del cluster come unità condivisa, non sarà possibile installare [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in questa unità.  
  
 Potrebbe inoltre essere necessario rivedere gli argomenti seguenti per ulteriori informazioni su attività, funzionalità e concetti relativi al clustering di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
|Descrizione argomento|Argomento|  
|-----------------------|-----------|  
|Vengono descritti i concetti relativi al clustering di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e vengono forniti collegamenti ad attività e contenuti associati.|[Istanze del cluster di failover Always On &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)|  
|Vengono descritti i concetti relativi ai criteri di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e vengono forniti collegamenti ad argomenti contenenti informazioni per una configurazione dei criteri di failover appropriata ai requisiti organizzativi.|[Failover Policy for Failover Cluster Instances](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md)|  
|Viene descritto come effettuare la gestione del cluster di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] esistente.|[Gestione e manutenzione dell'istanza del cluster di failover](../../../sql-server/failover-clusters/windows/failover-cluster-instance-administration-and-maintenance.md)|  
|Viene spiegato come installare [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] in un cluster di failover Windows Server.|[Come eseguire il clustering di SQL Server Analysis Services](http://go.microsoft.com/fwlink/p/?LinkId=396548)|  
  
 
  
##  <a name="BestPractices"></a> Procedure consigliate  
  
-   Vedere le [Note sulla versione di [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]](http://go.microsoft.com/fwlink/?LinkId=296445)  
  
-   Installare i prerequisiti software. Prima di eseguire il programma di installazione per installare o effettuare l'aggiornamento a [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], installare i prerequisiti riportati di seguito per ridurre il tempo di installazione. È possibile installare il software necessario in ogni nodo del cluster di failover, quindi riavviare i nodi prima di eseguire il programma di installazione.  
  
    -   Windows PowerShell non viene installato più dal programma di installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Windows PowerShell è un prerequisito per l'installazione dei componenti di [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)][!INCLUDE[ssDE](../../../includes/ssde-md.md)] e [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]. Se Windows PowerShell non è installato nel computer, è possibile abilitarlo seguendo le istruzioni disponibili nella pagina [Windows Management Framework](http://go.microsoft.com/fwlink/?LinkId=186214) .  
  
    -   .NET Framework 3.5 SP1 non viene più installato dal programma di installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], tuttavia può essere richiesto durante l'istallazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in sistemi operativi Windows meno recenti. Per altre informazioni, vedere [Note sulla versione di](http://go.microsoft.com/fwlink/?LinkId=296445) [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
    -   **Pacchetto [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Update:** per evitare il riavvio del computer dovuto all'installazione di .NET Framework 4 durante l'installazione, il programma di installazione di [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] richiede l'installazione di un aggiornamento di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] nel computer.  Se si installa [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] in Windows 7 SP1 o in [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] SP2, tale aggiornamento è incluso. Se si sta eseguendo l'installazione in un sistema operativo Windows precedente, scaricarlo da [Microsoft Update per .NET Framework 4.0 in Windows Vista e Windows Server 2008](http://go.microsoft.com/fwlink/?LinkId=198093).  
  
    -   .NET Framework 4: - il programma di installazione consente di installare .NET Framework 4 in un sistema operativo cluster. Per ridurre il tempo di installazione, è consigliabile installare .NET Framework 4 prima di eseguire il programma di installazione.  
  
    -   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] File di supporto per l'installazione. Questi file possono essere installati eseguendo SqlSupport.msi, disponibile nel supporto di installazione di [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
-   Verificare che il software antivirus non sia installato nel cluster WSFC. Per altre informazioni, vedere l'articolo della [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Knowledge Base, [Il software antivirus che non è a conoscenza del cluster può causare problemi con i servizi Cluster](http://go.microsoft.com/fwlink/?LinkId=116986).  
  
-   Nell'assegnare un nome a un gruppo cluster per l'installazione del cluster di failover, non utilizzare nessuno dei seguenti caratteri nel nome del gruppo cluster:  
  
    -   Operatore minore di (\<)  
  
    -   operatore maggiore di (>)  
  
    -   Virgolette doppie (")  
  
    -   Virgolette singole (')  
  
    -   E commerciale (&)  
  
     Verificare inoltre che i nomi dei gruppi cluster esistenti non contengano caratteri non supportati.  
  
-   Assicurarsi che tutti i nodi del cluster siano configurati in modo identico, inclusi COM+, le lettere di unità del disco e gli utenti nel gruppo degli amministratori.  
  
-   Verificare di aver eliminato il contenuto dei registri eventi di sistema in tutti i nodi e visualizzato di nuovo i registri eventi di sistema. Assicurarsi che i registri siano privi di messaggi di errore prima di continuare.  
  
-   Prima di installare o aggiornare un cluster di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], disabilitare tutte le applicazioni e i servizi che potrebbero utilizzare componenti di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] durante l'installazione, ma lasciare online le risorse disco.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Il programma di installazione configura automaticamente le dipendenza tra il gruppo di cluster di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e i dischi che saranno inclusi nel cluster di failover. Non impostare le dipendenze per i dischi prima dell'installazione.  
  
    -   Durante l'installazione del cluster di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] viene creato l'oggetto computer (account computer Active Directory) per il nome risorsa di rete di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . In un cluster di [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] , l'account del nome del cluster (account del computer del cluster) deve disporre delle autorizzazioni per la creazione di oggetti computer. Per altre informazioni, vedere [Configuring Accounts in Active Directory](http://technet.microsoft.com/library/cc731002\(WS.10\).aspx)(Configurazione di account in Active Directory).  
  
    -   Se si utilizza una condivisione di file SMB come opzione di archiviazione, l'account di configurazione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deve disporre di SeSecurityPrivilege nel file server. A questo scopo, usando la console Criteri di sicurezza locali nel file server, aggiungere l'account per l'installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ai diritti **Gestione file registro di controllo e di protezione** .  
  
##  <a name="Hardware"></a> Verificare la soluzione hardware in uso  
  
-   Se nella soluzione cluster sono inclusi nodi del cluster geograficamente distanti, sarà necessario verificare elementi aggiuntivi, come latenza di rete e supporto per dischi condivisi.  
  
    -   Per altre informazioni su [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] e [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)], vedere [Validating Hardware for a failover cluster](http://go.microsoft.com/fwlink/?LinkId=196817) (Convalida dell'hardware per un cluster di failover) e [Criteri del Servizio Supporto Tecnico Microsoft per cluster di failover di Windows Server 2008](http://go.microsoft.com/fwlink/?LinkId=196818).  
  
-   Verificare che il disco in cui verrà installato [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] non sia compresso o crittografato. Se si tenta di installare [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in un'unità compressa o crittografata, l'installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] non viene completata.  
  
-   Le configurazioni SAN sono supportate anche in [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] e [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] Advanced Server Edition e Datacenter Server Edition. La categoria "Cluster/Multi-cluster Device" di Microsoft Windows Catalog e Hardware Compatibility List indica il set di dispositivi di archiviazione compatibili con SAN che sono stati testati e sono supportati come unità di archiviazione SAN con più cluster WSFC collegati. Eseguire la convalida del cluster dopo aver trovato i componenti certificati.  
  
-   La condivisione file SMB è supportata anche per l'installazione di file di dati. Per altre informazioni, vedere [Tipi di archiviazione per i file di dati](../../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#StorageTypes).  
  
    > [!WARNING]  
    >  Se si utilizza un file server di Windows come archiviazione di condivisione file SMB, l'account di configurazione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deve disporre del privilegio SeSecurityPrivilege nel file server. A questo scopo, usando la console Criteri di sicurezza locali nel file server, aggiungere l'account per l'installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ai diritti **Gestione file registro di controllo e di protezione** .  
    >   
    >  Se si utilizza un'archiviazione di condivisione file SMB diversa dal file server di Windows, consultare il fornitore dell'archiviazione per un'impostazione equivalente sul lato del file server.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] supporta punti di montaggio.  
  
     Un volume montato, o punto di montaggio, consente di utilizzare una singola lettera di unità per fare riferimento a più dischi o volumi. Se la lettera di unità D: fa riferimento a un disco o volume normale, è possibile collegare o "montare" dischi o volumi aggiuntivi sotto la lettera D: senza che per tali dischi o volumi siano necessarie lettere di unità specifiche.  
  
     Considerazioni aggiuntive sui punti di montaggio per il clustering di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:  
  
    -   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] L'installazione richiede che all'unità di base di un'unità montata sia associata una lettera di unità. Per le installazioni di cluster di failover, questa unità di base deve essere un'unità del cluster. In questa versione non sono supportati i GUID del volume.  
  
    -   L'unità di base, a cui è associata la lettera di unità, non può essere condivisa tra le istanze del cluster di failover. Si tratta di una limitazione normale per i cluster di failover, ma non per i server autonomi a istanze multiple.  
  
    -   Le installazioni di tipo cluster di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sono limitate al numero di lettere di unità disponibili. Supponendo di utilizzare solo una lettera di unità per il sistema operativo e che le altre siano disponibili come normali unità cluster o unità cluster con hosting dei punti di montaggio, il limite massimo consentito è di 25 istanze di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per cluster di failover.  
  
        > [!TIP]  
        >  È possibile superare il limite di 25 istanze utilizzando l'opzione per la condivisione file di SMB. Se si utilizza la condivisione file SMB come opzione di archiviazione, è possibile installare fino a 50 istanze del cluster di failover [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
    -   La formattazione di un'unità dopo il montaggio di unità aggiuntive non è supportata.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] solo per l'installazione dei file tempdb. Assicurarsi che il percorso specificato per i file di dati tempdb e di log sia valido su tutti i nodi del cluster. Durante il failover, se le directory tempdb non sono disponibili nel nodo di destinazione del failover, la risorsa di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] non verrà riportata online. Per altre informazioni, vedere [Tipi di archiviazione per i file di dati](../../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#StorageTypes) e [Configurazione Motore di database - Directory dati](http://msdn.microsoft.com/library/9b1fa0fc-623b-479a-afc3-4f13bd850487).  
  
-   Se si distribuisce un cluster di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in componenti con tecnologia iSCSI, è consigliabile adottare precauzioni appropriate. Per altre informazioni, vedere [Supporto per SQL Server sui componenti della tecnologia iSCSI](http://go.microsoft.com/fwlink/?LinkId=116960).  
  
-   Per altre informazioni, vedere [Criteri di supporto di SQL Server per Microsoft Clustering](http://go.microsoft.com/fwlink/?LinkId=116958).  
  
-   Per altre informazioni sulla corretta configurazione dell'unità quorum, vedere [Quorum Drive Configuration Information](http://go.microsoft.com/fwlink/?LinkId=196816)(Informazioni sulla configurazione dell'unità quorum).  
  
-   Per installare un cluster di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] quando i file di installazione di origine di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e il cluster si trovano in domini diversi, copiare i file di installazione nel dominio corrente disponibile nel cluster di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
##  <a name="Security"></a> Esaminare le considerazioni sulla sicurezza  
  
-   Per utilizzare la crittografia, installare il certificato server con il nome DNS completo del cluster WSFC in tutti i nodi del cluster di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . In presenza, ad esempio, di un cluster a due nodi, con nodi denominati "Test1.DomainName.com" e "Test2.DomainName.com", e di un'istanza del cluster di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] denominata "Virtsql", è necessario ottenere un certificato per "Virtsql.DomainName.com" e installarlo nei nodi test1 e test2. È quindi possibile selezionare la casella di controllo **Forza crittografia protocollo** in Gestione configurazione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per configurare il cluster di failover per la crittografia.  
  
    > [!IMPORTANT]  
    >  Non selezionare la casella di controllo **Forza crittografia protocollo** prima di aver installato i certificati in tutti i nodi che fanno parte dell'istanza del cluster di failover.  
  
-   Per le installazioni di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in configurazioni side-by-side con versioni precedenti, nei servizi [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] devono essere utilizzati solo gli account disponibili nel gruppo di dominio globale. Gli account utilizzati dai servizi [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] non devono inoltre essere inclusi nel gruppo Administrators locale. Se queste linee guida non vengono rispettate, potrebbero verificarsi effetti imprevisti a livello di sicurezza.  
  
-   Per creare un cluster di failover è necessario essere un amministratore locale con autorizzazioni per accedere come servizio e agire come parte del sistema operativo in tutti i nodi dell'istanza del cluster di failover.  
  
-   In [!INCLUDE[nextref_longhorn](../../../includes/nextref-longhorn-md.md)]i SID del servizio vengono generati automaticamente per essere utilizzati con i servizi [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] . Per le istanze del cluster di failover di [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] aggiornate da versioni precedenti di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], verranno mantenuti i gruppi di dominio e le configurazioni ACL esistenti.  
  
-   I gruppi di dominio devono trovarsi nello stesso dominio degli account computer. Se ad esempio il computer in cui verrà installato [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] si trova nel dominio SQLSVR, figlio di MYDOMAIN, è necessario specificare un gruppo nel dominio SQLSVR. Nel dominio SQLSVR possono essere contenuti account utente di MYDOMAIN.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Il clustering di failover non può essere installato nelle configurazioni in cui i nodi del cluster sono controller di dominio.  
  
-   Vedere [Considerazioni sulla sicurezza per un'installazione di SQL Server](../../../sql-server/install/security-considerations-for-a-sql-server-installation.md).  
  
-   Per abilitare l'autenticazione Kerberos con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], vedere [Come usare l'autenticazione Kerberos in SQL Server](http://support.microsoft.com/kb/319723) nella [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Knowledge Base.  
  
##  <a name="Network"></a> Esaminare le considerazioni relative alla rete, alla porta e al firewall  
  
-   Verificare di aver disabilitato NetBIOS per tutte le schede di rete private prima di avviare l'installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   È consigliabile non utilizzare il nome di rete e l'indirizzo IP di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per altri scopi, ad esempio la condivisione di file. Per creare una risorsa di condivisione file, utilizzare un nome di rete e un indirizzo IP diversi e univoci per la risorsa.  
  
    > [!IMPORTANT]  
    >  È consigliabile non utilizzare le condivisioni file sulle unità dati, in quanto possono influenzare il comportamento e le prestazioni di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   Anche se in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] vengono supportati sia Named Pipes sia TCP/IP Sockets su TCP/IP all'interno di un cluster, è consigliabile utilizzare TCP/IP Sockets in una configurazione cluster.  
  
-   Si noti che ISA Server non è supportato nel Clustering di Windows e, di conseguenza, neanche nei cluster di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   È necessario che sia in esecuzione il servizio Registro di sistema remoto.  
  
-   È necessario che sia abilitata l'amministrazione remota.  
  
-   Per la porta di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] utilizzare Gestione configurazione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per verificare la configurazione di rete di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] relativa al protocollo TCP/IP per l'istanza che si desidera sbloccare. È necessario abilitare la porta TCP per IPALL se si desidera connettersi a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tramite TCP dopo l'installazione. Per impostazione predefinita, SQL Browser è in ascolto sulla porta UDP 1434.  
  
-   Le operazioni di installazione del cluster di failover includono una regola che controlla l'ordine di associazione di rete. Anche se gli ordini di associazione possono sembrare corretti, è possibile che nel sistema siano presenti configurazioni di schede di rete disabilitate o fantasma. Tali configurazioni possono influire sull'ordine di associazione e causare la generazione di un avviso da parte della regola dell'ordine di associazione. Per evitare questa situazione, effettuare i passaggi seguenti per identificare e rimuovere le schede di rete disabilitate:  
  
    1.  Al prompt dei comandi digitare: set devmgr_Show_Nonpersistent_Devices=1.  
  
    2.  Digitare ed eseguire: start Devmgmt.msc.  
  
    3.  Espandere l'elenco di schede di rete. L'elenco dovrebbe contenere solo le schede fisiche. Se una scheda di rete è disabilitata, il programma di installazione segnalerà un errore per la regola dell'ordine di associazione di rete. Tale scheda verrà visualizzata come disabilitata anche in Connessioni di rete nel Pannello di controllo. Verificare che in Impostazioni di rete e nel Pannello di controllo venga visualizzato lo stesso elenco di schede fisiche abilitate indicate in devmgmt.msc.  
  
    4.  Rimuovere le schede di rete disabilitate prima di eseguire il programma di installazione di SQL Server.  
  
    5.  Al termine dell'installazione, tornare in Connessioni di rete nel Pannello di controllo e disabilitare le schede di rete attualmente non in uso.  
  
##  <a name="OS_Support"></a> Verificare il sistema operativo in uso  
 Assicurarsi che il sistema operativo sia installato correttamente e sia configurato per il supporto del clustering di failover. Nella tabella seguente vengono elencate le edizioni di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e i sistemi operativi in cui sono supportati.  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] edition|[!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] Enterprise|[!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] Datacenter Server|[!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] Enterprise|[!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] Datacenter Server|  
|---------------------------------------|------------------------------------------------|-------------------------------------------------------|----------------------------------------------|-----------------------------------------------------|  
|[!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] Enterprise (64 bit) x64*|Sì|Sì|Sì**|Sì**|  
|[!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] Enterprise (32 bit)|Sì|Sì|||  
|[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] bit) Developer (64|Sì|Sì|Sì**|Sì**|  
|[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] Developer (32 bit)|Sì|Sì|||  
|[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] Standard (64 bit)|Sì|Sì|Sì|Sì|  
|[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] Standard (32 bit)|Sì|Sì|||  
  
 *[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] I cluster non sono supportati nella modalità WOW. inclusi gli aggiornamenti da versioni precedenti di cluster di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] che, in origine, erano stati installati nella modalità WOW. Per tali cluster l'unica opzione di aggiornamento consiste nell'installazione side-by-side della nuova versione e nella successiva migrazione.  
  
 **Supportato per il clustering di failover in più subnet di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
##  <a name="MultiSubnet"></a> Considerazioni aggiuntive per le configurazioni di più subnet  
 Nelle sezioni seguenti si descrivono i requisiti da ricordare in caso di installazione di un cluster di failover su più subnet di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Una configurazione di più subnet comporta clustering attraverso più subnet, pertanto comporta utilizzando più indirizzi IP e viene modificata nelle dipendenze della risorsa indirizzo IP.  
  
### <a name="includessnoversionincludesssnoversion-mdmd-edition-and-operating-system-considerations"></a>[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Considerazioni sul sistema operativo e sull'edizione  
  
-   Per informazioni sulle edizioni di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] che supportano in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cluster di failover in più subnet, vedere [Funzionalità supportate dalle edizioni di SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
-   Per creare un cluster di failover su più subnet di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , è necessario innanzitutto creare il cluster di failover multisito di [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] in più subnet.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Il cluster di failover dipende dal cluster di failover di Windows Server per assicurarsi che le condizioni della dipendenza IP siano valide se si verifica un failover.  
  
-   [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] richiede che tutti i server del cluster si trovino nello stesso dominio di Active Directory. Pertanto, nel cluster di failover su più subnet di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] viene richiesto che tutti i nodi del cluster si trovino nello stesso dominio Active Directory anche se sono presenti in subnet diverse.  
  
#### <a name="ip-address-and-ip-address-resource-dependencies"></a>L'indirizzo IP e la dipendenze della risorsa indirizzo IP  
  
1.  La dipendenze della risorsa indirizzo IP è impostata su OR in una configurazione di più subnet. Per altre informazioni, vedere [Creare un nuovo cluster di failover di SQL Server &#40;programma di installazione&#41;](../../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md).  
  
2.  Le dipendenze AND-OR miste dell'indirizzo IP non sono supportate. Ad esempio, \<IP1> AND \<IP2> OR \<IP3> non è supportato.  
  
3.  L'utilizzo di più indirizzi IP per subnet non è supportato.  
  
     Se si decide di utilizzare più indirizzi IP configurati per la stessa subnet, durante l'avvio di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] potrebbero verificarsi errori di connessione client.  
  
#### <a name="related-content"></a>Contenuto correlato  
 Per altre informazioni sul failover multisito di [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] , vedere [Windows Server 2008 R2 Failover Clustering Site](http://technet.microsoft.com/library/ff182338\(v=WS.10\).aspx) (Sito di clustering di failover di Windows Server 2008 R2) e [Design for a Clustered Service or Application in a Multi-Site Failover Cluster](http://go.microsoft.com/fwlink/?LinkId=177873)(Progetto per un servizio o un'applicazione cluster in un cluster di failover multisito).  
  
##  <a name="WSFC"></a> Configurare il cluster di failover di Windows Server  
  
-   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Cluster Service (WSFC) deve essere configurato in almeno un nodo del cluster di server. È inoltre necessario eseguire [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Enterprise, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Business Intelligence o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Standard in combinazione con WSFC. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Enterprise Edition supporta i cluster di failover con un massimo di 16 nodi. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Business Intelligence e [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Standard supportano i cluster di failover con due nodi.  
  
-   Tramite la DLL della risorsa per il servizio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] vengono esportate due funzioni utilizzate da Gestione cluster WSFC per verificare la disponibilità della risorsa di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Per altre informazioni, vedere [Criteri di failover per istanze del cluster di failover](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md).  
  
-   È necessario che WSFC sia in grado di verificare l'esecuzione dell'istanza del cluster di failover mediante il controllo IsAlive. A tale scopo, è necessario che venga stabilita una connessione trusted. Per impostazione predefinita, l'account che esegue il servizio cluster non è configurato come amministratore sui nodi del cluster e il gruppo BUILTIN\Administrators non dispone delle autorizzazioni per accedere a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Tali impostazioni cambiano solo se vengono modificate le autorizzazioni sui nodi del cluster.  
  
-   Configurare Domain Name Service (DNS) e Windows Internet Name Service (WINS). Un server DNS o WINS deve essere in esecuzione nell'ambiente in cui sarà installato il cluster di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Il programma di installazione richiede la registrazione al servizio DDNS del riferimento virtuale all'interfaccia IP di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . La configurazione del server DNS deve consentire ai nodi del cluster di registrare in modo dinamico la mappa di un indirizzo IP online sul nome di rete. Se non è possibile completare la registrazione dinamica, l'installazione non riesce e viene eseguito il rollback. Per altre informazioni, vedere [questo articolo della Knowledge Base](http://support.microsoft.com/kb/947048)  
  
##  <a name="MSDTC"></a> Installare [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Distributed Transaction Coordinator  
 Prima di installare [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in un cluster di failover determinare se è necessario creare la risorsa cluster [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Distributed Transaction Coordinator (MSDTC). Se si installa solo il [!INCLUDE[ssDE](../../../includes/ssde-md.md)], la risorsa cluster MSDTC non sarà necessaria. Se si installano il [!INCLUDE[ssDE](../../../includes/ssde-md.md)] , SSIS e i componenti workstation oppure si utilizzano transazioni distribuite, è necessario installare MSDTC. MSDTC non è necessario per le istanze solo di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
 In [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] e [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)]è possibile installare più istanze di MSDTC in un singolo cluster di failover. La prima istanza di MSDTC installata sarà l'istanza predefinita del cluster di MSDTC. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] si avvale di un'istanza di MSDTC installata nel gruppo di risorse cluster locale di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando automaticamente l'istanza di MSDTC. Tuttavia, è possibile eseguire il mapping delle singole applicazioni a qualsiasi istanza di MSDTC nel cluster.  
  
 Le regole seguenti vengono applicate per un'istanza di MSDTC che deve essere scelta da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:  
  
-   Utilizzare MSDTC installato nel gruppo locale oppure  
  
-   Utilizzare l'istanza di cui è stato eseguito il mapping di MSDTC oppure  
  
-   Utilizzare l'istanza predefinita del cluster di MSDTC oppure  
  
-   Utilizzare l'istanza installata del computer locale di MSDTC  
  
> [!IMPORTANT]  
>  Se l'istanza di MSDTC installata nel gruppo cluster locale di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ha esito negativo, in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] non viene effettuato automaticamente il tentativo di utilizzare l'istanza cluster predefinita o l'istanza del computer locale di MSDTC. Sarebbe necessario rimuovere completamente l'istanza con errori di MSDTC dal gruppo di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per utilizzare un'altra istanza di MSDTC. Analogamente, se si crea un mapping per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e l'istanza di cui è stato eseguito il mapping di MSDTC ha esito negativo, anche le transazioni distribuite non riusciranno. Se si desidera che in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] venga utilizzata un'istanza diversa di MSDTC, è necessario aggiungere un'istanza di MSDTC al gruppo cluster locale di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o eliminare il mapping.  
  
### <a name="configure-includemsconameincludesmsconame-mdmd-distributed-transaction-coordinator"></a>Configurare [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Distributed Transaction Coordinator  
 Dopo l'installazione del sistema operativo e la configurazione del cluster è necessario configurare MSDTC per il funzionamento in un cluster, utilizzando Amministrazione cluster. Se non si configura MSDTC per il clustering, l'installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] non verrà bloccata, ma una configurazione non corretta di MSDTC può influire sulla funzionalità dell'applicazione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Vedere anche  
 [Requisiti hardware e software per l'installazione di SQL Server 2016](../../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)   
 [Parametri di controllo di Controllo configurazione sistema](../../../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md)   
 [Gestione e manutenzione dell'istanza del cluster di failover](../../../sql-server/failover-clusters/windows/failover-cluster-instance-administration-and-maintenance.md)  
  
  

