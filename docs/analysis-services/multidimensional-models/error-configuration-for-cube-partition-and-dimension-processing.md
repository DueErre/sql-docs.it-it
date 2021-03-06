---
title: Configurazione errori per cubi, partizioni e l'elaborazione della dimensione | Documenti Microsoft
ms.custom: 
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.sqlserverstudio.cubeproperties.errorconfiguration.f1
- sql13.asvs.sqlserverstudio.partitionproperties.errorconfiguration.f1
- sql13.asvs.sqlserverstudio.dimensionproperties.errorconfiguration.f1
ms.assetid: 3f442645-790d-4dc8-b60a-709c98022aae
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 9dcbefced6fd34dd5fa69537733d7820b0130f4d
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/15/2018
---
# <a name="error-configuration-for-cube-partition-and-dimension-processing"></a>Configurazione errori per cubi, partizioni e l'elaborazione della dimensione
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
Con le proprietà di configurazione degli errori in oggetti dimensione, cubi o partizioni viene determinata la modalità di risposta del server in caso di errori di integrità dei dati durante l'elaborazione. L'attivazione di errori di questo tipo è in genere dovuta a chiavi duplicate, chiavi mancanti e valori Null in una colonna chiave e, anche se il record che causa l'errore non viene aggiunto al database, è possibile impostare le proprietà con cui vengono determinate le operazioni successive. Per impostazione predefinita, l'elaborazione viene arrestata. Tuttavia, durante lo sviluppo di un cubo, è possibile che l'elaborazione continui quando si verificano degli errori, in modo da poter testare i comportamenti del cubo con i dati importati, anche se incompleti.  
  
 In questo argomento sono contenute le sezioni seguenti:  
  
-   [Ordine di esecuzione](#bkmk_exec)  
  
-   [Comportamenti predefiniti](#bkmk_default)  
  
-   [Proprietà di configurazione degli errori](#bkmk_props)  
  
-   [Posizione in cui impostare le proprietà di configurazione degli errori](#bkmk_tools)  
  
-   [Chiavi mancanti (KeyNotFound)](#bkmk_missing)  
  
-   [Chiavi esterne Null in una tabella dei fatti (KeyNotFound)](#bkmk_nullfact)  
  
-   [Chiavi Null in una dimensione](#bkmk_nulldim)  
  
-   [Chiavi duplicate che generano relazioni incoerenti (KeyDuplicate)](#bkmk_dupe)  
  
-   [Modifica del limite errori o della relativa azione](#bkmk_limit)  
  
-   [Impostazione del percorso del log degli errori](#bkmk_log)  
  
-   [Passaggio successivo](#bkmk_next)  
  
##  <a name="bkmk_exec"></a> Ordine di esecuzione  
 Le regole **NullProcessing** vengono eseguite dal server sempre prima delle regole **ErrorConfiguration** per ogni record. Questo aspetto è importante per capire il motivo per cui con le proprietà di elaborazione dei valori Null mediante le quali questi ultimi vengono convertiti in zeri possono essere introdotti successivamente errori di chiave duplicata quando in due o più record degli errori è presente uno zero in una colonna chiave.  
  
##  <a name="bkmk_default"></a> Comportamenti predefiniti  
 Per impostazione predefinita, l'elaborazione viene arrestata al primo errore che implica una colonna chiave. Questo comportamento viene controllato da un limite errori tramite cui viene specificato zero come numero di errori consentiti e dalla direttiva Arresta elaborazione con cui viene indicato al server di arrestare l'elaborazione quando il limite errori viene raggiunto.  
  
 I record che attivano un errore, a causa di valori Null o mancanti o duplicati, vengono convertiti in membri sconosciuti o rimossi. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] non verranno importati i dati che violano i relativi vincoli di integrità.  
  
-   La conversione in membro sconosciuto si verifica per impostazione predefinita, a causa dell'impostazione **ConvertToUnknown** per **KeyErrorAction**. I record allocati al membro sconosciuto vengono messi in quarantena nel database come prova di un problema che potrebbe essere opportuno esaminare al termine dell'elaborazione.  
  
     I membri sconosciuti vengono esclusi dai carichi di lavoro di query, ma saranno visibili in alcune applicazioni client se l'opzione **UnknownMember** è impostata su **Visibile**.  
  
     Se si desidera tenere traccia del numero di valori Null convertiti in membri sconosciuti, è possibile modificare la proprietà **NullKeyConvertedToUnknown** per segnalare questi errori nel log o nella finestra di elaborazione.  
  
-   L'eliminazione si verifica quando la proprietà **KeyErrorAction** viene impostata manualmente su **DiscardRecord**.  
  
 Tramite le proprietà di configurazione degli errori è possibile determinare la modalità di risposta del server in caso di errore. Le opzioni prevedono l'arresto immediato dell'elaborazione, la continuazione dell'elaborazione ma l'arresto della registrazione oppure la continuazione dell'elaborazione e della registrazione degli errori. Le impostazioni predefinite variano in base alla gravità dell'errore.  
  
 Con il conteggio errori si tiene traccia del numero di errori che si verificano. Quando si imposta un limite superiore, la risposta del server cambia al raggiungimento del limite in questione. Per impostazione predefinita, l'elaborazione viene arrestata dal server dopo aver raggiunto il limite. Il limite predefinito è 0, che causa l'arresto dell'elaborazione al primo errore conteggiato.  
  
 Gli errori con impatto elevato, ad esempio una chiave mancante o un valore Null in un campo chiave, devono essere risolti rapidamente. Per impostazione predefinita, questi errori sono conformi ai comportamenti del server **ReportAndContinue** , dove tramite quest'ultimo viene rilevato l'errore, che viene poi aggiunto al conteggio errori, e viene quindi continuata l'elaborazione, ad eccezione di quando il limite errori è zero; in tal caso l'elaborazione viene arrestata immediatamente.  
  
 Altri errori vengono generati ma non conteggiati o registrati per impostazione predefinita: si tratta dell'impostazione **IgnoreError** , perché l'errore non necessariamente genera un problema di integrità dei dati.  
  
 I conteggi errori sono interessati dalle impostazioni di elaborazione dei valori Null. Per gli attributi della dimensione, le opzioni di elaborazione dei valori Null determinano la modalità di risposta del server in caso di valori Null. Per impostazione predefinita, i valori Null in una colonna numerica vengono convertiti in zeri, mentre i valori Null in una colonna stringa vengono elaborati come stringhe vuote. È possibile ignorare le proprietà **NullProcessing** per rilevare i valori Null prima della trasformazione in errori **KeyNotFound** o **KeyDuplicate** . Per informazioni dettagliate, vedere [Chiavi Null in una dimensione](#bkmk_nulldim) .  
  
 Gli errori vengono registrati nella finestra di dialogo di elaborazione ma non vengono salvati. È possibile specificare un nome del file del log degli errori di chiave per raccogliere gli errori in un file di testo.  
  
##  <a name="bkmk_props"></a> Proprietà di configurazione degli errori  
 Sono disponibili nove proprietà di configurazione degli errori. Cinque vengono utilizzate per determinare la risposta del server quando si verifica un errore specifico. Le altre quattro vengono definite a livello di ambito dei carichi di lavoro di configurazione degli errori, ad esempio il numero di errori da consentire, le operazioni da eseguire quando questo limite viene raggiunto e se raccogliere gli errori in un file di log.  
  
 **Risposta del server a errori specifici**  
  
|Proprietà|Valore predefinito|Altri valori|  
|--------------|-------------|------------------|  
|**CalculationError**<br /><br /> Si verifica durante l'inizializzazione della configurazione degli errori.|**IgnoreError** non registra né conteggia l'errore; l'elaborazione continua finché il conteggio errori è al di sotto del limite massimo.|**ReportAndContinue** registra e conteggia l'errore.<br /><br /> **ReportAndStop** segnala l'errore e arresta immediatamente l'elaborazione, indipendentemente dal limite errori.|  
|**KeyNotFound**<br /><br /> Si verifica quando una chiave esterna in una tabella dei fatti non dispone di una chiave primaria corrispondente in una tabella delle dimensioni correlata, ad esempio una tabella dei fatti relativa alle vendite con un record con un ID prodotto che non esiste nella tabella delle dimensioni del prodotto. Questo errore può verificarsi durante l'elaborazione di partizioni o di dimensioni con schema snowflake.|**ReportAndContinue** registra e conteggia l'errore.|**ReportAndStop** segnala l'errore e arresta immediatamente l'elaborazione, indipendentemente dal limite errori.<br /><br /> **IgnoreError** non registra né conteggia l'errore; l'elaborazione continua finché il conteggio errori è al di sotto del limite massimo. I record che attivano questo errore vengono convertiti in membri sconosciuti per impostazione predefinita, tuttavia, in alternativa, è possibile modificare la proprietà **KeyErrorAction** per rimuoverli.|  
|**KeyDuplicate**<br /><br /> Si verifica in caso di chiavi di attributo duplicate in una dimensione. Nella maggior parte dei casi, è accettabile disporre di chiavi di attributo duplicate, ma con questo errore l'utente viene informato della presenza di duplicati in modo da poter verificare eventuali difetti di progettazione della dimensione che potrebbero generare relazioni incoerenti tra gli attributi.|**IgnoreError** non registra né conteggia l'errore; l'elaborazione continua finché il conteggio errori è al di sotto del limite massimo.|**ReportAndContinue** registra e conteggia l'errore.<br /><br /> **ReportAndStop** segnala l'errore e arresta immediatamente l'elaborazione, indipendentemente dal limite errori.|  
|**NullKeyNotAllowed**<br /><br /> Si verifica quando **NullProcessing** = **Errore** è impostato su un attributo della dimensione o in caso di valori Null in una colonna chiave dell'attributo usata per identificare in modo univoco un membro.|**ReportAndContinue** registra e conteggia l'errore.|**ReportAndStop** segnala l'errore e arresta immediatamente l'elaborazione, indipendentemente dal limite errori.<br /><br /> **IgnoreError** non registra né conteggia l'errore; l'elaborazione continua finché il conteggio errori è al di sotto del limite massimo. I record che attivano questo errore vengono convertiti in membri sconosciuti per impostazione predefinita, tuttavia, in alternativa, è possibile impostare la proprietà **KeyErrorAction** per rimuoverli.|  
|**NullKeyConvertedToUnknown**<br /><br /> Si verifica quando i valori Null vengono convertiti successivamente in membri sconosciuti. L'impostazione di **NullProcessing** = **ConvertToUnknown** in un attributo della dimensione comporterà l'attivazione di questo errore.|**IgnoreError** non registra né conteggia l'errore; l'elaborazione continua finché il conteggio errori è al di sotto del limite massimo.|Se si considera questo errore come messaggio informativo, mantenere l'impostazione predefinita. In caso contrario, è possibile scegliere **ReportAndContinue** per segnalare l'errore nella finestra di elaborazione e conteggiarlo per il relativo limite.<br /><br /> **ReportAndStop** segnala l'errore e arresta immediatamente l'elaborazione, indipendentemente dal limite errori.|  
  
 **Proprietà generali**  
  
|**Proprietà**|**Valori**|  
|------------------|----------------|  
|**KeyErrorAction**|Si tratta dell'azione eseguita dal server in caso di errore **KeyNotFound** . Le risposte valide all'errore prevedono **ConvertToUnknown** o **DiscardRecord**.|  
|**KeyErrorLogFile**|Si tratta di un nome di file definito dall'utente che deve avere un'estensione di file log ed essere posizionato in una cartella in cui l'account del servizio dispone delle autorizzazioni di lettura-scrittura. Il file di log conterrà solo gli errori generati durante l'elaborazione. Se sono necessarie informazioni più dettagliate, usare utilità Traccia eventi.|  
|**KeyErrorLimit**|Numero massimo di errori di integrità dei dati che il server consentirà prima di interrompere l'elaborazione. Un valore pari a 1 indica che non vi sono limiti. L'impostazione predefinita è 0, che indica l'arresto dell'elaborazione dopo il primo errore. È inoltre possibile impostare come valore un numero intero.|  
|**KeyErrorLimitAction**|Si tratta dell'azione eseguita dal server quando viene raggiunto il limite superiore del numero di errori di chiave. Con **Arresta elaborazione**, l'elaborazione termina immediatamente. Con **Arresta registrazione**, l'elaborazione continua ma gli errori non vengono più segnalati né conteggiati.|  
  
##  <a name="bkmk_tools"></a> Posizione in cui impostare le proprietà di configurazione degli errori  
 Utilizzare le pagine delle proprietà in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] al termine della distribuzione del database o nel progetto di modello in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. In entrambi gli strumenti sono disponibili le stesse proprietà. È inoltre possibile impostare le proprietà di configurazione degli errori nel file msmdrsrv.ini per modificare le impostazioni predefinite del server per la configurazione degli errori e nei comandi **Batch** e **Process** se l'elaborazione viene eseguita come operazione controllata da script.  
  
 È possibile impostare la configurazione degli errori in qualsiasi oggetto che può essere elaborato come operazione autonoma.  
  
#### <a name="sql-server-management-studio"></a>SQL Server Management Studio  
  
1.  In Esplora oggetti fare clic con il pulsante destro del mouse sulle **proprietà** di uno di questi oggetti: dimensione, cubo o partizione.  
  
2.  In Proprietà fare clic su **Configurazione errori**.  
  
#### <a name="sql-server-data-tools"></a>SQL Server Data Tools  
  
1.  In Esplora soluzioni fare doppio clic su una dimensione o un cubo. Viene visualizzato**ErrorConfiguration** in Proprietà nel riquadro sottostante.  
  
2.  In alternativa, solo per una singola dimensione, fare clic con il pulsante destro del mouse sulla dimensione in Esplora soluzioni, selezionare **Elabora**, quindi scegliere **Cambia impostazioni** nella finestra di dialogo di elaborazione della dimensione. Le opzioni di configurazione degli errori vengono visualizzate nella scheda Errori chiave dimensione.  
  
##  <a name="bkmk_missing"></a> Chiavi mancanti (KeyNotFound)  
 I record con un valore di chiave mancante non possono essere aggiunti al database, neanche quando gli errori vengono ignorati o non vi è un limite errori.  
  
 Tramite il server viene generato l'errore **KeyNotFound** durante l'elaborazione della partizione, quando in un record della tabella dei fatti è contenuto un valore di chiave esterna, ma la chiave esterna non dispone di record corrispondenti in una tabella delle dimensioni correlata. Questo errore si verifica inoltre durante l'elaborazione di tabelle delle dimensioni correlate o con schema snowflake, in cui tramite un record in una dimensione viene specificata una chiave esterna che non esiste nella dimensione correlata.  
  
 Quando si verifica un errore **KeyNotFound** , il record errato viene allocato al membro sconosciuto. Questo comportamento viene controllato tramite **l'azione della chiave**, impostata su **ConvertToUnknown**, in modo che sia possibile visualizzare i record allocati per un controllo ulteriore.  
  
##  <a name="bkmk_nullfact"></a> Chiavi esterne Null in una tabella dei fatti (KeyNotFound)  
 Per impostazione predefinita, un valore Null in una colonna chiave esterna di una tabella dei fatti viene convertito in zero. Se zero non è un valore di chiave esterna valido, l'errore **KeyNotFound** verrà registrato e verrà conteggiato per il limite errori che corrisponde a zero per impostazione predefinita.  
  
 Per consentire la continuazione dell'elaborazione, è possibile gestire il valore Null prima che venga convertito e controllato per la presenza di eventuali errori. A tale scopo, impostare **NullProcessing** su **Errore**.  
  
#### <a name="set-nullprocessing-property-on-a-measure"></a>Impostazione della proprietà NullProcessing in una misura  
  
1.  In Esplora soluzioni in SQL Server Data Tools fare doppio clic sul cubo per aprirlo in Progettazione cubi.  
  
2.  Fare clic con il pulsante destro del mouse su una misura nel riquadro Misure e scegliere **Proprietà**.  
  
3.  In Proprietà espandere **Origine** per visualizzare la proprietà **NullProcessing** . È impostata su **Automatica** per impostazione predefinita che, per gli elementi OLAP, consente di convertire i valori Null in zeri per i campi contenenti dati numerici.  
  
4.  Impostare il valore su **Errore** per escludere tutti i record con valore Null, evitando la conversione di un valore Null in uno numerico (zero). Questa modifica consente di evitare errori di chiave duplicata correlati a più record con zero nella colonna chiave, nonché errori **KeyNotFound** quando una chiave esterna con valore zero non dispone di chiavi primarie equivalenti in una tabella delle dimensioni correlata.  
  
##  <a name="bkmk_nulldim"></a> Chiavi Null in una dimensione  
 Per continuare l'elaborazione in caso di valori Null in chiavi esterne in una dimensione con schema snowflake, gestire i valori Null impostando in primo luogo **NullProcessing** su **KeyColumn** dell'attributo della dimensione. In questo modo i record vengono rimossi o convertiti prima che si possa verificare l'errore **KeyNotFound** .  
  
 Sono disponibili due opzioni per la gestione di valori Null nell'attributo della dimensione:  
  
-   Impostare **NullProcessing**=**UnknownMember** per allocare i record con valori Null al membro sconosciuto. Verrà generato l'errore **NullKeyConvertedToUnknown** , che viene ignorato per impostazione predefinita.  
  
-   Impostare **NullProcessing**=**Errore** per escludere i record con valori Null. Verrà generato l'errore **NullKeyNotAllowed** , che viene registrato e conteggiato per il limite di errori di chiave. È possibile impostare la proprietà di configurazione degli errori in **Chiave Null non consentita** su **IgnoreError** per consentire la continuazione dell'elaborazione.  
  
 I valori Null possono rappresentare un problema per i campi non chiave, in quanto le query MDX restituiscono risultati diversi a seconda se Null viene interpretato come valore pari a zero o vuoto. Per questo motivo, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fornisce opzioni di elaborazione dei valori Null che consentono di predefinire il comportamento di conversione desiderato. Per informazioni dettagliate, vedere [Definizione delle proprietà UnknownMember e NullProcessing](../../analysis-services/lesson-4-7-defining-the-unknown-member-and-null-processing-properties.md) e <xref:Microsoft.AnalysisServices.NullProcessing> .  
  
#### <a name="set-nullprocessing-property-on-a-dimension-attribute"></a>Impostazione della proprietà NullProcessing in un attributo della dimensione  
  
1.  In Esplora soluzioni in SQL Server Data Tools fare doppio clic sulla dimensione per aprirla in Progettazione dimensioni.  
  
2.  Fare clic con il pulsante destro del mouse su un attributo nel riquadro Attributi e scegliere **Proprietà**.  
  
3.  In Proprietà espandere **KeyColumns** per visualizzare la proprietà **NullProcessing** . È impostata su **Automatica** per impostazione predefinita; in altre parole i valori Null vengono convertiti in zeri per i campi contenenti dati numerici. Impostare il valore su **Errore** o su **UnknownMember**.  
  
     Con questa modifica vengono rimosse le condizioni sottostanti tramite cui viene attivato **KeyNotFound** rimuovendo o convertendo il record prima che venga verificata la presenza di errori.  
  
     A seconda della configurazione degli errori, una di queste azioni può generare un errore che viene segnalato e conteggiato. Potrebbe essere necessario modificare le proprietà aggiuntive, ad esempio impostando **KeyNotFound** su **ReportAndContinue** o **KeyErrorLimit** su un valore diverso da zero, per consentire la continuazione dell'elaborazione quando questi errori vengono segnalati e conteggiati.  
  
##  <a name="bkmk_dupe"></a> Chiavi duplicate che generano relazioni incoerenti (KeyDuplicate)  
 Per impostazione predefinita, la presenza di una chiave duplicata non determina l'arresto dell'elaborazione, ma l'errore viene ignorato e il record duplicato viene escluso dal database.  
  
 Per modificare questo comportamento, impostare **KeyDuplicate** su **ReportAndContinue** o **ReportAndStop** per segnalare l'errore. È quindi possibile esaminare l'errore per determinare potenziali difetti nella progettazione delle dimensioni.  
  
##  <a name="bkmk_limit"></a> Modifica del limite errori o della relativa azione  
 È possibile aumentare il limite errori per consentire più errori durante l'elaborazione. Non sono disponibili informazioni aggiuntive per l'aumento del limite errori; il valore appropriato dipenderà dallo scenario. I limiti errori vengono specificati come **KeyErrorLimit** nelle proprietà **ErrorConfiguration** properties nelle proprietà [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]oppure come **Numero di errori** nelle proprietà the Error Configuration tab for properties of dimensions, cubes, or measure groups nelle proprietà [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 Una volta raggiunto il limite errori, è possibile specificare l'arresto dell'elaborazione o della registrazione. Ad esempio si supponga di impostare l'azione su **StopLogging** in un limite errori pari a 100. Al 101esimo errore, l'elaborazione continua ma gli errori non vengono più registrati né conteggiati. Le azioni di limite di errore vengono specificate come **KeyErrorLimitAction** nelle proprietà **ErrorConfiguration** in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]oppure come **Azione in caso di errore** nella scheda Configurazione errori per le proprietà relative a dimensioni, cubi o gruppi di misure in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
##  <a name="bkmk_log"></a> Impostazione del percorso del log degli errori  
 È possibile specificare un file per archiviare i messaggi di errore correlati alla chiave che vengono segnalati durante l'elaborazione. Per impostazione predefinita, gli errori sono visibili durante l'elaborazione interattiva nella finestra di elaborazione e vengono quindi rimossi quando si chiude la finestra o la sessione. Nel log saranno contenute solo le informazioni sull'errore correlate alle chiavi, identici agli errori visualizzati nelle finestre di dialogo di elaborazione.  
  
 Gli errori verranno registrati in un file di testo che deve avere log come estensione di file. Il file sarà vuoto a meno che non si verifichino degli errori. Per impostazione predefinita, un file verrà creato nella cartella DATA. È possibile specificare un'altra cartella finché tramite l'account del servizio Analysis Services è possibile scrivere in questa posizione.  
  
##  <a name="bkmk_next"></a> Passaggio successivo  
 Stabilire se gli errori determineranno l'arresto dell'elaborazione o verranno ignorati. Si tenga presente che solo l'errore viene ignorato. Il record che ha causato l'errore non viene ignorato; viene rimosso o convertito in membro sconosciuto. I record che violano le regole di integrità dei dati non vengono mai aggiunti al database. Per impostazione predefinita, l'elaborazione viene arrestata al primo errore, ma è possibile modificare questo comportamento aumentando il limite errori. Nello sviluppo del cubo, può essere utile ridurre le regole di configurazione degli errori, consentendo la continuazione dell'elaborazione, in modo che vi siano dati con cui eseguire il test.  
  
 Decidere se modificare i comportamenti di elaborazione dei valori Null predefiniti. Per impostazione predefinita, i valori Null in una colonna stringa vengono elaborati come valori vuoti, mentre i valori Null in una colonna numerica vengono elaborati come valori pari a zero. Per istruzioni sull'impostazione dell'elaborazione di valori Null in un attributo, vedere [Definizione delle proprietà UnknownMember e NullProcessing](../../analysis-services/lesson-4-7-defining-the-unknown-member-and-null-processing-properties.md) .  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà dei log](../../analysis-services/server-properties/log-properties.md)   
 [Che definisce il membro sconosciuto e le proprietà di elaborazione dei valori Null](../../analysis-services/lesson-4-7-defining-the-unknown-member-and-null-processing-properties.md)  
  
  
