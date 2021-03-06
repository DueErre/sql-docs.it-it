---
title: Scrittura di istruzioni Transact-SQL internazionali | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: collations
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- writing international statements
- Transact-SQL international considerations
- international considerations [SQL Server], Transact-SQL
- Database Engine international considerations [SQL Server], Transact-SQL
- statements [SQL Server], international
- database international considerations [SQL Server], Transact-SQL
- dates [SQL Server], international considerations
ms.assetid: f0b10fee-27f7-45fe-aece-ccc3f63bdcdb
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f6d2e5bf9dbfe8d4c40cde744ca49dcda0c1d029
ms.sourcegitcommit: 9d0467265e052b925547aafaca51e5a5e93b7e38
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/02/2018
---
# <a name="write-international-transact-sql-statements"></a>Scrittura di istruzioni Transact-SQL internazionali
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Le linee guida seguenti consentono di aumentare il grado di portabilità tra lingue diverse, nonché il supporto di più lingue, per i database e le applicazioni di database che utilizzano istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
-   Sostituire tutte le occorrenze dei tipi di dati **char**, **varchar**e **text** con **nchar**, **nvarchar**e **nvarchar(max)**. In questo modo non si verificano problemi a livello di conversione della tabella codici. Per altre informazioni, vedere [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md).  
  
-   Quando si eseguono confronti e operazioni con mesi o giorni della settimana, utilizzare le parti numeriche della data anziché le stringhe di nomi. I nomi dei mesi e dei giorni della settimana restituiti variano a seconda dell'impostazione della lingua. Ad esempio, DATENAME (MONTH,GETDATE()) restituisce May quando la lingua è impostata sull'inglese (Stati Uniti) Mai se è impostato il tedesco e mai se è impostato il francese. Specificare pertanto una funzione quale DATEPART che utilizza il numero anziché il nome del mese. Utilizzare i nomi DATEPART quando si compilano i set di risultati da visualizzare all'utente, in quanto le stringhe di nomi sono più significative delle parti numeriche. Non creare tuttavia il codice di logica che dipende dai nomi visualizzati di una lingua specifica.  
  
-   Quando si specificano le date nei confronti o nell'input di istruzioni INSERT e UPDATE, utilizzare costanti che vengono interpretate nello stesso modo indipendentemente dall'impostazione della lingua:  
  
    -   Le applicazioni ADO, OLE DB e ODBC devono utilizzare le clausole di escape seguenti relative a timestamp, data e ora:  
  
         **{ ts'**aaaa**-***mm***-***gg**hh***:***mm***:***ss*[**.***fff*] **'}** ad esempio: **{ ts'**1998**-**09**-**24 10**:**02**:**20**' }**  
  
         **{ d'** *aaaa* **-** *mm* **-** *gg* **'}** ad esempio: **{ d'**1998**-**09**-**24**'}**  
  
         **{ t'** *hh* **:** *mm* **:** *ss* **'}** ad esempio: **{ t'**10:02:20**'}**  
  
    -   Nelle applicazioni che utilizzano altre API, oppure script, stored procedure e trigger di [!INCLUDE[tsql](../../includes/tsql-md.md)] , è necessario utilizzare le stringhe numeriche non separate, Ad esempio, *aaaammgg* come 19980924.  
  
    -   Nelle applicazioni che usano altre API oppure script, stored procedure e trigger di [!INCLUDE[tsql](../../includes/tsql-md.md)] è anche possibile usare l'istruzione CONVERT con un parametro di stile esplicito per tutte le conversioni tra i tipi di dati **time**, **date**, **smalldate**, **datetime**, **datetime2**e **datetimeoffset** e i tipi di dati stringa di caratteri. L'istruzione seguente viene interpretata nello stesso modo indipendentemente dalle impostazioni di connessione della lingua o del formato della data:  
  
        ```  
        SELECT *  
        FROM AdventureWorks2012.Sales.SalesOrderHeader  
        WHERE OrderDate = CONVERT(DATETIME, '20060719', 101)  
        ```  
  
         Per altre informazioni, vedere [CAST and CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md).  
  
  
