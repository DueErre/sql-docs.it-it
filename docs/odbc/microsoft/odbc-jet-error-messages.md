---
title: I messaggi di errore di Jet ODBC | Documenti Microsoft
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
helpviewer_keywords: error messages (ODBC driver for oracle)
ms.assetid: f8d2a8f2-0316-42c4-bc34-5367661634ae
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 206ebbdc1dd8a121f3c41f95cd305de6f4ef3d10
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/21/2017
---
# <a name="odbc-jet-error-messages"></a>I messaggi di errore di Jet ODBC
Per gli errori che si verificano nell'origine dati, il driver ODBC restituisce un messaggio di errore restituito dal File di libreria ODBC. Per gli errori che si verificano in Gestione Driver o il driver ODBC, il driver di restituisce un messaggio di errore in base al testo è associato il valore SQLSTATE.  
  
 Messaggi di errore presentano il formato seguente:  
  
```  
[vendor][ODBC-component][data-source]message-text  
```  
  
 I prefissi tra parentesi quadre ([]) identificano la posizione dell'errore. Quando l'errore si verifica in Gestione Driver *origine dati* non è consentito. Quando si verifica l'errore nell'origine dati, il [*fornitore*] e [*componente ODBC*] i prefissi di identificano il fornitore e il nome del componente che ha ricevuto l'errore dall'origine dati ODBC.  
  
 Nella tabella seguente mostra i messaggi di errore restituiti da Gestione Driver e driver ISAM:  
  
|Messaggio di errore|Posizione dell'errore|  
|-------------------|--------------------|  
|[Microsoft] [Gestione Driver ODBC] *-testo del messaggio*|Gestione driver (Odbc32.dll)|  
|[Microsoft] [ODBC *nome driver*]*-testo del messaggio*|Driver ISAM (vedere Driver ISAM)|
