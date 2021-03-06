---
title: Applicazioni personalizzate | Documenti Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- interoperability [ODBC], custom applications
- custom applications [ODBC]
- interoperability [ODBC], levels
ms.assetid: f28178d9-ecd6-4e8c-9644-9bb624999dcb
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0bac0656a0e0de15d216b73b76285d1ddede6e74
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/21/2017
---
# <a name="custom-applications"></a>Applicazioni personalizzate
Applicazioni personalizzate in genere eseguono un'attività specifica per i pochi DBMS. Ad esempio, un'applicazione può recuperare i dati da un singolo DBMS e generare un report oppure è possibile trasferire dati tra diversi DBMS. Ciò che queste applicazioni hanno in comune è che questi DBMS sono noti prima che l'applicazione viene scritta e sono in genere modificata durante il ciclo di vita dell'applicazione.  
  
 L'applicazione personalizzata richiede pertanto senza alcuna interoperabilità. Lo sviluppatore di applicazioni è possibile scegliere un driver singolo per ogni sistema DBMS e il codice direttamente per i driver. L'applicazione in modo sicuro può contenere codice specifico del driver per sfruttare le funzionalità del driver e può anche effettuare chiamate al database API native l'utilizzo delle funzionalità non supportate da ODBC.  
  
 Il problema di interoperabilità principali della maggior parte delle applicazioni personalizzata è se il DBMS di destinazione verrà modificato in futuro. In caso affermativo, questo processo può essere semplificato scrivendo codice più interoperabile con cui iniziare. Tuttavia, tale modifica del DBMS è rara e in genere comporta l'uso di una grande quantità di lavoro. Per questo motivo, gli sviluppatori di applicazioni personalizzate scegliere raramente aumentare l'interoperabilità a scapito della funzionalità. in genere scelti per modificare tale funzionalità quando vengono modificate DBMS.
