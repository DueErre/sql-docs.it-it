---
title: MSSQLSERVER_1203 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 1203 (Database Engine error)
ms.assetid: 33a35f00-98c8-46c6-b432-544b326b6117
caps.latest.revision: "14"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 67be895813ef4007a83e4e8388d70b15066922e6
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver1203"></a>MSSQLSERVER_1203
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|1203|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|LK_NOT|  
|Testo del messaggio|Il processo con ID %d ha tentato di sbloccare una risorsa di cui non è proprietario: %.*ls. Ripetere la transazione. L'errore potrebbe essere dovuto a una condizione basata sul tempo. Se il problema persiste, contattare l'amministratore del database.|  
  
## <a name="explanation"></a>Spiegazione  
Questo errore si verifica quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è impegnato in attività diverse dalle normali operazioni di pulizia dei dati temporanei post-elaborazione e tenta di sbloccare una pagina specifica che in realtà è già sbloccata.  
  
### <a name="possible-causes"></a>Possibili cause  
La causa sottostante di questo errore può essere correlata a problemi strutturali nel database interessato. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gestisce l'acquisizione e il rilascio di pagine per mantenere il controllo della concorrenza nell'ambiente multiutente. Per il mantenimento di questo meccanismo vengono utilizzate diverse strutture di blocco interne che identificano la pagina e il tipo di blocco presente. I blocchi vengono acquisiti per consentire l'elaborazione delle pagine interessate e rilasciati al termine dell'elaborazione.  
  
## <a name="user-action"></a>Azione dell'utente  
Eseguire DBCC CHECKDB sul database cui appartiene l'oggetto. Se DBCC CHECKDB non restituisce errori, provare a ristabilire la connessione e a eseguire il comando.  
  
> [!IMPORTANT]  
> Se l'esecuzione di DBCC CHECKDB con una delle clausole REPAIR non consente di correggere il problema relativo all'indice oppure non si è certi dell'effetto prodotto sui dati dall'esecuzione di DBCC CHECKDB con una clausola REPAIR, contattare il personale del supporto tecnico.  
  
