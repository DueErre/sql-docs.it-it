---
title: Modifica di un Assembly | Documenti Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- assemblies [CLR integration], modifying
- permissions [CLR integration]
- altering assemblies
- ALTER ASSEMBLY statement
ms.assetid: 9e765fbd-f339-473c-8537-22f478e79696
caps.latest.revision: "14"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f279c3f1e1315ea44cdb75918b471c8fdd22ee01
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/17/2017
---
# <a name="altering-an-assembly"></a>Modifica di un assembly
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Gli assembly che sono stati registrati in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] può essere aggiornato da una versione più recente tramite l'istruzione ALTER ASSEMBLY. Per aggiornare un assembly, utilizzare l'istruzione ALTER ASSEMBLY con la sintassi seguente:  
  
```  
ALTER ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
```  
  
 ALTER ASSEMBLY non interrompe i processi in esecuzione che utilizzano l'assembly. L'esecuzione di tali processi continua con l'assembly non modificato. Non è possibile utilizzare ALTER ASSEMBLY per modificare le firme di funzioni, funzioni di aggregazione, stored procedure e trigger di CLR (Common Language Runtime). Nuovi metodi pubblici possono essere aggiunti all'assembly, i metodi privati possono essere modificati nel modo desiderato e i metodi pubblici possono essere modificati a condizione di non modificare le firme o gli attributi. Non è possibile modificare tramite ALTER ASSEMBLY i campi contenuti in un tipo definito dall'utente con serializzazione nativa, inclusi i membri dei dati o le classi base. Tutte le altre modifiche non sono supportate. Per ulteriori informazioni, vedere [ALTER ASSEMBLY &#40; Transact-SQL &#41; ](../../../t-sql/statements/alter-assembly-transact-sql.md).  
  
## <a name="changing-the-permission-set-of-an-assembly"></a>Modifica del set di autorizzazioni di un assembly  
 Il set di autorizzazioni di un assembly può essere anch'esso modificato utilizzando l'istruzione ALTER ASSEMBLY. L'istruzione seguente modifica il set di autorizzazioni dell'assembly SQLCLRTest **EXTERNAL_ACCESS**.  
  
```  
ALTER ASSEMBLY SQLCLRTest  
WITH PERMISSION_SET = EXTERNAL_ACCESS   
```  
  
 Se il set di autorizzazioni di un assembly viene modificato da **provvisoria** a **EXTERNAL_ACCESS** o **UNSAFE**, una chiave asimmetrica e l'account di accesso corrispondente con  **EXTERNAL ACCESS ASSEMBLY** autorizzazione o **ASSEMBLY UNSAFE** è necessario creare l'autorizzazione per l'assembly. Per altre informazioni, vedere [Creating an Assembly](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md).  
  
## <a name="adding-the-source-code-of-an-assembly"></a>Aggiunta del codice sorgente di un assembly.  
 La clausola ADD FILE nella sintassi ALTER ASSEMBLY non è presente in CREATE ASSEMBLY. È possibile utilizzarla per aggiungere codice sorgente o altri file associati a un assembly. I file vengono copiati dai percorsi originali e vengono archiviati nelle tabelle di sistema del database. In questo modo il codice sorgente o gli altri file saranno sempre disponibili nel caso in cui sia necessario ricreare o documentare la versione corrente del tipo definito dall'utente (UDT).  
  
 L'istruzione seguente aggiunge il codice sorgente della classe Point.cs per il tipo definito dall'utente Point. Il testo contenuto nel file Point.cs viene copiato e archiviato nel database con il nome "PointSource".  
  
 `ALTER ASSEMBLY Point`  
  
 `ADD FILE FROM 'C:\Projects\Point\Point.cs' AS PointSource`  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione degli assembly di integrazione CLR](../../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md)   
 [Creazione di un Assembly](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)   
 [Eliminazione di un Assembly](../../../relational-databases/clr-integration/assemblies/dropping-an-assembly.md)   
 [ALTER ASSEMBLY &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-assembly-transact-sql.md)  
  
  