---
title: MSSQLSERVER_1222 | Microsoft Docs
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
helpviewer_keywords: 1222 (Database Engine error)
ms.assetid: c5b1c2f4-f591-4cc1-aa17-204636a27f29
caps.latest.revision: "20"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 743031212890f81073ac39bb617170cc0e4d218e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver1222"></a>MSSQLSERVER_1222
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|1222|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|LK_TIMEOUT|  
|Testo del messaggio|Timeout della richiesta di blocco.|  
  
## <a name="explanation"></a>Spiegazione  
Una risorsa necessaria viene mantenuta in blocco da un'altra transazione per un periodo superiore al tempo di attesa ammesso dalla query.  
  
## <a name="user-action"></a>Azione dell'utente  
Per risolvere il problema, eseguire le operazioni seguenti:  
  
1.  Se possibile, individuare la transazione che blocca la risorsa necessaria. Usare le viste a gestione dinamica **sys.dm_os_waiting_tasks** e **sys.dm_tran_locks**.  
  
2.  Se la transazione continua a mantenere il blocco, terminarla se appropriato.  
  
3.  Eseguire nuovamente la query.  
  
Se l'errore si verifica spesso, modificare il periodo di timeout del blocco oppure le transazioni all'origine del problema in modo che mantengano il blocco per un periodo di tempo inferiore.  
  
