---
title: Preparazione all'implementazione di un'estensione per l'elaborazione dati | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: extensions
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- interfaces [Reporting Services]
- data processing extensions [Reporting Services], implementing
ms.assetid: 698817e4-33da-4eb5-9407-4103e1c35247
caps.latest.revision: "36"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 424e36f6be32da0aafb6981e923f66aed7c22139
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2018
---
# <a name="preparing-to-implement-a-data-processing-extension"></a>Preparazione all'implementazione di un'estensione per l'elaborazione dati
  Prima di implementare l'estensione per l'elaborazione dati di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], è necessario definire le interfacce da implementare. È possibile fornire implementazioni specifiche dell'estensione dell'intero set di interfacce oppure è possibile incentrare l'implementazione semplicemente su un subset, ad esempio le interfacce <xref:Microsoft.ReportingServices.DataProcessing.IDataReader> e <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand> in cui i client interagirebbero principalmente con un set di risultati come un oggetto **DataReader** e in cui l'estensione per l'elaborazione dati di [!INCLUDE[ssRS](../../../includes/ssrs-md.md)] verrebbe usata come collegamento tra il set di risultati e l'origine dati.  
  
 È possibile implementare le estensioni per l'elaborazione dati scegliendo tra le due modalità seguenti:  
  
-   Le classi dell'estensione per l'elaborazione dati possono implementare le interfacce del provider di dati [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] e, facoltativamente, le interfacce dell'estensione per l'elaborazione dati estese offerte da [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
-   Le classi dell'estensione per l'elaborazione dati possono implementare le interfacce dell'estensione per l'elaborazione dati fornite da [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] e, facoltativamente, le interfacce dell'estensione per l'elaborazione dati estese.  
  
 Se l'estensione per l'elaborazione dati di [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] non supporterà una proprietà o un metodo specifico, implementare la proprietà o il metodo come elemento senza operazioni. Se un client prevede un comportamento specifico, generare un'eccezione **NotSupportedException**.  
  
> [!NOTE]  
>  Un'implementazione senza operazioni di una proprietà o di un metodo si applica solo alle proprietà e ai metodi delle interfacce che si sceglie di implementare. Le interfacce facoltative che si sceglie di non implementare devono essere omesse dall'assembly di estensioni per l'elaborazione dati. Per ulteriori informazioni sul fatto che un'interfaccia sia obbligatoria o facoltativa, vedere la tabella più avanti in questa sezione.  
  
## <a name="required-extension-functionality"></a>Funzionalità obbligatorie delle estensioni  
 Ogni estensione per l'elaborazione dati di [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] deve fornire le funzionalità seguenti:  
  
-   Aprire una connessione a un'origine dati.  
  
-   Analizzare una query e restituire un elenco di nomi di campo per il set di risultati.  
  
-   Eseguire una query sull'origine dati e restituire un set di righe.  
  
-   Passare parametri a valore singolo alla query.  
  
-   Scorrere le righe nel set di righe e recuperare i dati.  
  
 Ogni estensione per l'elaborazione dati può essere estesa per includere le funzionalità seguenti:  
  
-   Analizzare una query e restituire un elenco di nomi di parametri utilizzati nella query.  
  
-   Analizzare una query e restituire l'elenco di campi in base ai quali è raggruppata la query.  
  
-   Analizzare una query e restituire l'elenco di campi in base ai quali è ordinata la query.  
  
-   Fornire un nome utente e una password per la connessione all'origine dati indipendenti dalla stringa di connessione.  
  
-   Scorrere le righe nel set di righe e recuperare i metadati ausiliari relativi ai valori.  
  
-   Aggregare i dati nel server.  
  
## <a name="available-extension-interfaces"></a>Interfacce dell'estensione disponibili  
 Nella tabella seguente sono descritte le interfacce disponibili e viene indicato se l'implementazione è obbligatoria o facoltativa.  
  
|Interfaccia|Description|Implementazione|  
|---------------|-----------------|--------------------|  
|IDbConnection|Rappresenta una sessione univoca con un'origine dati. Nel caso di un sistema di database client/server, la sessione può essere equivalente a una connessione di rete al server.|Obbligatorio|  
|IDbConnectionExtension|Rappresenta proprietà di connessione aggiuntive che possono essere implementate dalle estensioni per l'elaborazione dati di [!INCLUDE[ssRS](../../../includes/ssrs-md.md)] per quanto riguarda sicurezza e autenticazione.|Facoltativo|  
|IDbTransaction|Rappresenta una transazione locale.|Obbligatorio|  
|IDbTransactionExtension|Rappresenta proprietà aggiuntive della transazione che possono essere implementate dalle estensioni per l'elaborazione dati di [!INCLUDE[ssRS](../../../includes/ssrs-md.md)].|Facoltativo|  
|IDbCommand|Rappresenta una query o un comando utilizzato per la connessione a un'origine dati.|Obbligatorio|  
|IDbCommandAnalysis|Rappresenta informazioni aggiuntive sul comando per l'analisi di una query e la restituzione di un elenco di nomi di parametri utilizzati nella query.|Facoltativo|  
|IDataParameter|Rappresenta una coppia nome/valore o un parametro passato a un comando o a una query.|Obbligatorio|  
|IDataParameterCollection|Rappresenta una raccolta di tutti i parametri relativi a un comando o a una query.|Obbligatorio|  
|IDataReader|Fornisce un metodo per leggere un flusso di dati forward-only di sola lettura dall'origine dati.|Obbligatorio|  
|IDataReaderExtension|Fornisce un metodo per leggere uno o più flussi forward-only di set di risultati, ottenuti eseguendo un comando in un'origine dati. Questa interfaccia fornisce supporto aggiuntivo per le aggregazioni di campi.|Facoltativo|  
|IExtension|Fornisce la classe di base per un'estensione per l'elaborazione dati di [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. Consente inoltre a un implementatore di includere un nome localizzato per l'estensione e di passare le impostazioni di configurazione dal file di configurazione all'estensione.|Obbligatorio|  
  
 Le interfacce dell'estensione per l'elaborazione dati sono identiche a un subset delle proprietà, dei metodi e delle interfacce del provider di dati [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)], quando possibile. Per ulteriori informazioni sull'implementazione di un provider di dati [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] completo, vedere l'argomento relativo all'implementazione di un provider di dati nella documentazione di [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] Software Development Kit (SDK).  
  
## <a name="see-also"></a>Vedere anche  
 [Estensioni di Reporting Services](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Implementazione di un'estensione per l'elaborazione dati](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Libreria di estensioni di Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
