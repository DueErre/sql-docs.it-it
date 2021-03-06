---
title: Scegliere un algoritmo di crittografia | Microsoft Docs
ms.custom: 
ms.date: 01/08/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: security
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cryptography [SQL Server], algorithms
- encryption [SQL Server], algorithms
- security [SQL Server], encryption
- algorithms [SQL Server encryption]
ms.assetid: 8227028c-a9c9-489d-bd27-fbf8242634ae
caps.latest.revision: "36"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: b0c946ccc0547e3efadf26f78bb66fcdd3feb517
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="choose-an-encryption-algorithm"></a>Scelta di un algoritmo di crittografia
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] La crittografia è una delle molte difese in profondità che gli amministratori possono usare per proteggere un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Gli algoritmi di crittografia definiscono trasformazioni dei dati che non possono essere invertite facilmente dagli utenti non autorizzati. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] consente ad amministratori e sviluppatori di scegliere tra diversi algoritmi, tra cui DES, Triple DES, TRIPLE_DES_3KEY, RC2, RC4, RC4 a 128 bit, DESX, AES a 128 bit, AES a 192 bit e AES a 256 bit.  
  
> [!NOTE]  
>  A partire da [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)], tutti gli algoritmi diversi da AES_128, AES_192 e AES_256 sono deprecati. Per usare algoritmi meno recenti (sconsigliato), è necessario impostare il database sul livello di compatibilità del database 120 o su uno inferiore.  
  
 Nessun algoritmo è ideale in tutte le situazioni e la valutazione dei vantaggi relativi a ogni algoritmo esula dall'ambito della documentazione online di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Sono comunque validi i principi generali seguenti:  
  
-   La crittografia avanzata utilizza in genere una quantità di risorse della CPU maggiore rispetto alla crittografia vulnerabile.  
  
-   Le chiavi lunghe consentono in genere una crittografia più avanzata rispetto a quelle brevi.  
  
-   La crittografia asimmetrica è meno avanzata della crittografia simmetrica che usa la stessa lunghezza di chiave, ma è relativamente lenta.  
  
-   Le crittografie a blocchi con chiavi lunghe sono più avanzate rispetto alle crittografie a flussi.  
  
-   Le password lunghe e complesse sono più avanzate rispetto alle password brevi.  
  
-   Se si crittografano molti dati, è necessario crittografarli tramite una chiave simmetrica e crittografare la chiave simmetrica con una asimmetrica.  
  
-   I dati crittografati non possono essere compressi, ma i dati compressi possono essere crittografati. Se si utilizza la compressione, è necessario comprimere i dati prima di crittografarli.  
  
> [!IMPORTANT]  
>  L'algoritmo RC4 è supportato solo per motivi di compatibilità con le versioni precedenti. È possibile crittografare il nuovo materiale usando RC4 o RC4_128 solo quando il livello di compatibilità del database è 90 o 100. (Non consigliato.) Usare un algoritmo più recente, ad esempio uno degli algoritmi AES. In [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] e versioni successive il materiale crittografato utilizzando RC4 o RC4_128 può essere decrittografato in qualsiasi livello di compatibilità.  
>   
>  L'utilizzo ripetuto della stessa funzione KEY_GUID RC4 o RC4_128 su blocchi di dati diversi produrrà la stessa chiave RC4 perché [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] non fornisce automaticamente un valore salt. L'utilizzo ripetuto della stessa chiave RC4 è un errore noto che comporta una crittografia molto debole. Per questo motivo le parole chiave RC4 e RC4_128 sono deprecate. [!INCLUDE[ssNoteDepFutureDontUse](../../../includes/ssnotedepfuturedontuse-md.md)]  
  
 Per altre informazioni sugli algoritmi e sulla tecnologia di crittografia, vedere [Concetti chiave sulla sicurezza](http://go.microsoft.com/fwlink/?LinkId=62082) nella Guida per gli sviluppatori di .NET Framework in MSDN.  
  
 **Chiarimento relativo agli algoritmi DES:**  
  
-   La crittografia DESX è stata menzionata erroneamente. Le chiavi simmetriche create con ALGORITHM = DESX utilizzano in realtà la crittografia TRIPLE DES con una chiave a 192 bit. L'algoritmo DESX non è disponibile. [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
-   Le chiavi simmetriche create con ALGORITHM = TRIPLE_DES_3KEY utilizzano TRIPLE DES con una chiave a 192 bit.  
  
-   Le chiavi simmetriche create con ALGORITHM = TRIPLE_DES utilizzano TRIPLE DES con una chiave a 128 bit.  
  
## <a name="related-tasks"></a>Attività correlate  
  
|||  
|-|-|  
|Crittografia tramite una chiave simmetrica.|[CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-symmetric-key-transact-sql.md)|  
|Crittografia tramite una chiave asimmetrica.|[CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-asymmetric-key-transact-sql.md)|  
|Crittografia tramite certificato.|[CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../../t-sql/statements/create-certificate-transact-sql.md)|  
|Crittografia dei file di database mediante Transparent Data Encryption.|[Transparent Data Encryption &#40;TDE&#41;](../../../relational-databases/security/encryption/transparent-data-encryption.md)|  
|Come crittografare una colonna di una tabella.|[Crittografia di una colonna di dati](../../../relational-databases/security/encryption/encrypt-a-column-of-data.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Crittografia di SQL Server](../../../relational-databases/security/encryption/sql-server-encryption.md)   
 [Gerarchia di crittografia](../../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
