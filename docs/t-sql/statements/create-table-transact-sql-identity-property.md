---
title: "IDENTITY (proprietà) (Transact-SQL) | Documenti Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- IDENTITY_TSQL
- IDENTITY
dev_langs:
- TSQL
helpviewer_keywords:
- IDENTITY property
- columns [SQL Server], creating
- identity columns [SQL Server], IDENTITY property
- autonumbers, identity numbers
ms.assetid: 8429134f-c821-4033-a07c-f782a48d501c
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: c8ed5f2b2dd8daaf244f9e12ea17a69ff489ae3b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="create-table-transact-sql-identity-property"></a>CREARE una tabella (Transact-SQL) IDENTITY (proprietà)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

  Crea una colonna Identity in una tabella. Questa proprietà viene utilizzata con le istruzioni CREATE TABLE e ALTER TABLE di [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
> [!NOTE]  
>  La proprietà IDENTITY è diversa da SQL-DMO **identità** proprietà che espone la proprietà identity di riga di una colonna.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
IDENTITY [ (seed , increment) ]  
```  
  
## <a name="arguments"></a>Argomenti  
 *valore di inizializzazione*  
 Valore usato per la prima riga caricata nella tabella.  
  
 *incremento*  
 Valore incrementale aggiunto al valore Identity della riga caricata in precedenza.  
  
 È necessario specificare sia il valore di inizializzazione che l'incremento oppure nessuno dei due valori. In questo secondo caso, il valore predefinito è (1,1).  
  
## <a name="remarks"></a>Osservazioni  
 Le colonne Identity possono essere usate per la generazione di valori di chiave. Tramite la proprietà Identity in una colonna viene garantito quanto riportato di seguito:  
  
-   Ogni nuovo valore viene generato in base all'incremento e al valore di inizializzazione correnti.  
  
-   Ogni nuovo valore per una transazione specifica è diverso da altre transazioni simultanee nella tabella.  
  
 Tramite la proprietà Identity in una colonna non viene garantito quanto riportato di seguito:  
  
-   **L'univocità del valore** : deve essere implementata tramite un **chiave primaria** o **UNIQUE** vincolo o **UNIQUE** indice.  
  
-   **Valori consecutivi in una transazione** : non è garantita che una transazione di inserimento di più righe per ottenere valori consecutivi per le righe, poiché potrebbero verificarsi altri inserimenti simultanei nella tabella. Se i valori devono essere consecutivi, la transazione deve utilizzare un blocco esclusivo sulla tabella o utilizzare il **SERIALIZABLE** livello di isolamento.  
  
-   **Valori consecutivi dopo il riavvio del server o altri errori** –[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] potrebbe memorizzare nella cache di valori identity per motivi di prestazioni e alcuni dei valori assegnati possono essere persi durante un riavvio del server o errore di database. Questo può comportare dei gap nel valore Identity al momento dell'inserimento. Se i gap non sono accettabili, l'applicazione dovrà usare un meccanismo specifico per generare i valori chiave. Usando un generatore di sequenza con la **NOCACHE** opzione possibile limitare i gap a transazioni che non sono mai eseguito il commit.  
  
-   **Riutilizzo di valori** : per una determinata proprietà identity con valore di inizializzazione/incremento specifico, l'identità di valori non vengono riutilizzati dal motore di. Se una particolare istruzione INSERT non riesce o se viene eseguito il rollback di quest'ultima, i valori Identity usati vengono persi e non saranno generati di nuovo. Questa condizione può comportare dei gap quando vengono generati i successivi valori Identity.  
  
 Queste restrizioni fanno parte della progettazione per migliorare le prestazioni e perché sono accettabili in molte situazioni comuni. Se non è possibile usare valori Identity a causa di queste restrizioni, creare una tabella separata contenente un valore corrente e gestire l'accesso all'assegnazione di numeri e tabelle con l'applicazione.  
  
 Se una tabella che include una colonna Identity viene pubblicata per la replica, la colonna Identity deve essere gestita in modo adeguato per il tipo di replica usato. Per altre informazioni, vedere [Replicare colonne Identity](../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
 Ogni tabella può includere una sola colonna Identity.  
  
 Nelle tabelle ottimizzate per la memoria il valore di inizializzazione e l'incremento devono essere impostati su 1,1. Impostare il valore di inizializzazione o incremento su un valore diverso da 1 comporta l'errore seguente: l'utilizzo di inizializzazione e incremento valori diversi rispetto a 1 non è supportato con le tabelle con ottimizzazione per la memoria.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-using-the-identity-property-with-create-table"></a>A. Uso della proprietà IDENTITY con CREATE TABLE  
 Nell'esempio seguente viene creata una nuova tabella tramite la proprietà `IDENTITY` per un numero di identificazione a incremento automatico.  
  
```  
USE AdventureWorks2012;  
  
IF OBJECT_ID ('dbo.new_employees', 'U') IS NOT NULL  
   DROP TABLE new_employees;  
GO  
CREATE TABLE new_employees  
(  
 id_num int IDENTITY(1,1),  
 fname varchar (20),  
 minit char(1),  
 lname varchar(30)  
);  
  
INSERT new_employees  
   (fname, minit, lname)  
VALUES  
   ('Karin', 'F', 'Josephs');  
  
INSERT new_employees  
   (fname, minit, lname)  
VALUES  
   ('Pirkko', 'O', 'Koskitalo');  
```  
  
### <a name="b-using-generic-syntax-for-finding-gaps-in-identity-values"></a>B. Uso della sintassi generica per individuare interruzioni nella sequenza di valori Identity  
 Nell'esempio seguente viene illustrato l'uso di una sintassi generica per individuare le interruzioni nella sequenza di valori Identity create in seguito alla rimozione di dati.  
  
> [!NOTE]  
>  La prima parte del seguente script [!INCLUDE[tsql](../../includes/tsql-md.md)] è riportata solo a scopo illustrativo. È possibile eseguire lo script [!INCLUDE[tsql](../../includes/tsql-md.md)] a partire dal commento `-- Create the img table`.  
  
```  
-- Here is the generic syntax for finding identity value gaps in data.  
-- The illustrative example starts here.  
SET IDENTITY_INSERT tablename ON;  
DECLARE @minidentval column_type;  
DECLARE @maxidentval column_type;  
DECLARE @nextidentval column_type;  
SELECT @minidentval = MIN($IDENTITY), @maxidentval = MAX($IDENTITY)  
    FROM tablename  
IF @minidentval = IDENT_SEED('tablename')  
   SELECT @nextidentval = MIN($IDENTITY) + IDENT_INCR('tablename')  
   FROM tablename t1  
   WHERE $IDENTITY BETWEEN IDENT_SEED('tablename') AND   
      @maxidentval AND  
      NOT EXISTS (SELECT * FROM tablename t2  
         WHERE t2.$IDENTITY = t1.$IDENTITY +   
            IDENT_INCR('tablename'))  
ELSE  
   SELECT @nextidentval = IDENT_SEED('tablename');  
SET IDENTITY_INSERT tablename OFF;  
-- Here is an example to find gaps in the actual data.  
-- The table is called img and has two columns: the first column   
-- called id_num, which is an increasing identification number, and the   
-- second column called company_name.  
-- This is the end of the illustration example.  
  
-- Create the img table.  
-- If the img table already exists, drop it.  
-- Create the img table.  
IF OBJECT_ID ('dbo.img', 'U') IS NOT NULL  
   DROP TABLE img;  
GO  
CREATE TABLE img (id_num int IDENTITY(1,1), company_name sysname);  
INSERT img(company_name) VALUES ('New Moon Books');  
INSERT img(company_name) VALUES ('Lucerne Publishing');  
-- SET IDENTITY_INSERT ON and use in img table.  
SET IDENTITY_INSERT img ON;  
  
DECLARE @minidentval smallint;  
DECLARE @nextidentval smallint;  
SELECT @minidentval = MIN($IDENTITY) FROM img  
 IF @minidentval = IDENT_SEED('img')  
    SELECT @nextidentval = MIN($IDENTITY) + IDENT_INCR('img')  
    FROM img t1  
    WHERE $IDENTITY BETWEEN IDENT_SEED('img') AND 32766 AND  
      NOT    EXISTS (SELECT * FROM img t2  
          WHERE t2.$IDENTITY = t1.$IDENTITY + IDENT_INCR('img'))  
 ELSE  
    SELECT @nextidentval = IDENT_SEED('img');  
SET IDENTITY_INSERT img OFF;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [DBCC CHECKIDENT &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md)   
 [IDENT_INCR &#40; Transact-SQL &#41;](../../t-sql/functions/ident-incr-transact-sql.md)   
 [@@IDENTITY &#40;Transact-SQL&#41;](../../t-sql/functions/identity-transact-sql.md)   
 [IDENTITÀ &#40; Funzione &#41; &#40; Transact-SQL &#41;](../../t-sql/functions/identity-function-transact-sql.md)   
 [IDENT_SEED &#40; Transact-SQL &#41;](../../t-sql/functions/ident-seed-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [SET IDENTITY_INSERT &#40; Transact-SQL &#41;](../../t-sql/statements/set-identity-insert-transact-sql.md)   
 [Replicare colonne Identity](../../relational-databases/replication/publish/replicate-identity-columns.md)  
  
  
