---
title: MSSQLSERVER_1462 | Microsoft Docs
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
helpviewer_keywords: 1462 (Database Engine error)
ms.assetid: 680e9c1c-a9d6-4765-b601-956d0a83324c
caps.latest.revision: "12"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9465f1c9eef03f1fc1ffa0070cc960cfa05bc657
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver1462"></a>MSSQLSERVER_1462
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|1462|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|DBM_DISABLED_DUE_TO_FAILED_REDO|  
|Testo del messaggio|Mirroring del database disabilitato a causa di un'operazione di rollforward non riuscita. Impossibile riprendere.|  
  
## <a name="explanation"></a>Spiegazione  
Il mirroring del database non è riuscito a eseguire un'operazione di rollforward di un record di log nel mirror.  
  
### <a name="possible-causes"></a>Possibili cause  
La causa più probabile è che un'operazione di aggiunta file è stata completata nel database principale ma non è stata eseguita nel database mirror perché i nomi file o le strutture di directory del server principale e del server mirror sono diverse.  
  
## <a name="user-action"></a>Azione dell'utente  
Esaminare il log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per individuare la causa dell'errore. Provare a eliminare la causa del problema e a riprendere il mirroring nel database.  
  
## <a name="see-also"></a>Vedere anche  
[Risolvere i problemi relativi alla configurazione del mirroring del database &#40;SQL Server&#41;](~/database-engine/database-mirroring/troubleshoot-database-mirroring-configuration-sql-server.md)  
  
