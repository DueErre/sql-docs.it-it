---
title: sp_create_removable (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_create_removable
- sp_create_removable_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_create_removable
ms.assetid: 06e36ae5-f70d-4a26-9a7f-ee4b9360b355
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e7b5a66828c1ee49734e720137d3a0ededc0098e
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/03/2018
---
# <a name="spcreateremovable-transact-sql"></a>sp_create_removable (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Viene creato un database su supporti rimovibili. Vengono creati tre o più file, uno per le tabelle del catalogo di sistema, uno per il log delle transazioni e uno o più per le tabelle di dati, quindi viene inserito il database in questi file.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] È consigliabile utilizzare [CREATE DATABASE](../../t-sql/statements/create-database-sql-server-transact-sql.md) invece.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_create_removable   
   [ @dbname = ] 'dbname',   
   [ @syslogical= ] 'syslogical',   
   [ @sysphysical = ] 'sysphysical',   
   [ @syssize = ] syssize,   
   [ @loglogical = ] 'loglogical',   
   [ @logphysical = ] 'logphysical',   
   [ @logsize = ] logsize,   
   [ @datalogical1 = ] 'datalogical1',   
   [ @dataphysical1 = ] 'dataphysical1',   
   [ @datasize1 = ] datasize1 ,   
   [ @datalogical16 = ] 'datalogical16',   
   [ @dataphysical16 = ] 'dataphysical16',   
   [ @datasize16 = ] datasize16 ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [ **@dbname=** ] **'***dbname***'**  
 Nome del database da creare per utilizzarlo nei supporti rimovibili. *dbname* è **sysname**.  
  
 [ **@syslogical=** ] **'***syslogical***'**  
 Nome logico del file contenente le tabelle del catalogo di sistema. *syslogical* è **sysname**.  
  
 [  **@sysphysical=** ] **'***sysphysical***'**  
 Nome fisico. In esso è incluso un percorso completo del file contenente le tabelle del catalogo di sistema. *sysphysical* è **nvarchar (260)**.  
  
 [ **@syssize=** ] *syssize*  
 Dimensione in megabyte del file contenente le tabelle del catalogo di sistema. *syssize* è **int**. Il valore minimo *syssize* è 1.  
  
 [ **@loglogical=** ] **'***loglogical***'**  
 Nome logico del file contenente il log delle transazioni. *loglogical* è **sysname**.  
  
 [  **@logphysical=** ] **'***logphysical***'**  
 Nome fisico. In esso è incluso un percorso completo del file contenente il log delle transazioni. *logphysical* è **nvarchar (260)**.  
  
 [  **@logsize=** ] *logsize*  
 Dimensioni in megabyte del file contenente il log delle transazioni. *LogSize* è **int**. Il valore minimo *logsize* è 1.  
  
 [  **@datalogical1=** ] **'***datalogical***'**  
 Nome logico di un file contenente le tabelle di dati. *datalogical* è **sysname**.  
  
 Il numero dei file di dati è compreso tra 1 e 16. Vengono in genere creati più file di dati quando si prevede che il database sia di grandi dimensioni e debba essere pertanto suddiviso su più dischi.  
  
 [  **@dataphysical1=** ] **'***dataphysical***'**  
 Nome fisico. In esso è incluso un percorso completo di un file contenente le tabelle di dati. *dataphysical* è **nvarchar (260)**.  
  
 [  **@datasize1=** ] **'***datasize***'**  
 Dimensioni in megabyte di un file contenente le tabelle di dati. *DataSize* è **int**. Il valore minimo *datasize* è 1.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
 Nessuno  
  
## <a name="remarks"></a>Osservazioni  
 Utilizzare questa stored procedure se si desidera creare una copia del database su un supporto rimovibile, ad esempio un CD, e distribuire il database ad altri utenti.  
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'autorizzazione CREATE DATABASE, CREATE ANY DATABASE o ALTER ANY DATABASE.  
  
 Per mantenere il controllo sull'utilizzo del disco per un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], l'autorizzazione per la creazione dei database è in genere limitata a pochi account di accesso.  
  
### <a name="permissions-on-data-and-log-files"></a>Autorizzazioni per i file di dati e di log  
 Ogni volta che si eseguono determinate operazioni in un database, vengono impostate le autorizzazioni corrispondenti per i relativi file di dati e di log. Con le autorizzazioni è possibile evitare che vengano accidentalmente alterati i file che si trovano in una directory con autorizzazioni aperte.  
  
|Operazione nel database|Autorizzazioni impostate per i file|  
|---------------------------|------------------------------|  
|Modifica per l'aggiunta di un nuovo file|Data creazione|  
|Esecuzione del backup|Collegamento|  
|Ripristino|Scollegamento|  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non dati del set di file di log e le autorizzazioni.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente il database `inventory` viene creato come database rimovibile.  
  
```  
EXEC sp_create_removable 'inventory',   
   'invsys',  
   'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\invsys.mdf'  
, 2,   
   'invlog',  
   'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\invlog.ldf', 4,  
   'invdata',  
   'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\invdata.ndf',   
10;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Collegamento e scollegamento di un database &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [sp_certify_removable &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-certify-removable-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [sp_dbremove &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbremove-transact-sql.md)   
 [sp_detach_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)   
 [sp_helpfile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpfile-transact-sql.md)   
 [sp_helpfilegroup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpfilegroup-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
