---
title: sp_dbmmonitorchangealert (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2016
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
- sp_dbmmonitorchangealert_TSQL
- sp_dbmmonitorchangealert
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dbmmonitorchangealert
- database mirroring [SQL Server], monitoring
ms.assetid: 1b29f82b-9cf8-4539-8d5c-9a1024db8a50
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 41132fa5fd69036e9bc504628cd353d809d6a0bf
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/03/2018
---
# <a name="spdbmmonitorchangealert-transact-sql"></a>sp_dbmmonitorchangealert (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aggiunge o modifica la soglia di avviso per una misurazione delle prestazioni di mirroring specificata.  

  
 
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_dbmmonitorchangealert database_name   
    , alert_id   
    , alert_threshold   
    , enabled   
```  
  
## <a name="arguments"></a>Argomenti  
 *database_name*  
 Specifica il database per cui aggiungere o modificare il valore soglia degli avvisi specificato.  
  
 *alert_id*  
 Valore intero che identifica l'avviso da aggiungere o modificare. Specificare uno dei valori seguenti:  
  
|Valore|Misurazione delle prestazioni|Valore soglia avvisi|  
|-----------|------------------------|-----------------------|  
|1|Transazione non inviata meno recente|Specifica la quantità di transazioni, espressa in minuti, che può accumularsi nella coda di invio prima che venga generato un avviso nell'istanza del server principale. Questo avviso consente di quantificare il rischio potenziale di perdita dei dati in termini di tempo ed è particolarmente rilevante per la modalità a prestazioni elevate. L'avviso risulta tuttavia utile anche per la modalità a sicurezza elevata quando il mirroring viene sospeso in seguito alla disconnessione dei partner.|  
|2|Log non inviato|Specifica la quantità di log non inviati, espressa in kilobyte (KB), che può accumularsi prima che venga generato un avviso nell'istanza del server principale. Questo avviso consente di quantificare il rischio potenziale di perdita dei dati in termini di KB ed è particolarmente rilevante per la modalità a prestazioni elevate. L'avviso risulta tuttavia utile anche per la modalità a sicurezza elevata quando il mirroring viene sospeso in seguito alla disconnessione dei partner.|  
|3|Log non ripristinato|Specifica la quantità di log non ripristinati, espressa in kilobyte (KB), che può accumularsi prima che venga generato un avviso nell'istanza del server mirror. Questo avviso consente di misurare il tempo di failover. Il*tempo di failover* corrisponde essenzialmente al tempo necessario al server mirror precedente per eseguire il rollforward di tutti i log rimanenti nella propria coda di rollforward, più un breve tempo aggiuntivo.|  
|4|Overhead commit mirror|Specifica il ritardo medio per transazione, espresso in millisecondi, che è consentito prima che venga generato un avviso nell'istanza del server principale. Questo ritardo rappresenta la quantità di overhead generato mentre l'istanza del server principale è in attesa che l'istanza del server mirror scriva il record di log della transazione nella coda di rollforward. Questo valore è rilevante solo nella modalità a sicurezza elevata.|  
|5|Periodo di memorizzazione|Metadati che controllano per quanto tempo vengono conservate le righe della tabella dello stato di mirroring del database.|  
  
 Per informazioni sugli ID degli eventi corrispondenti agli avvisi, vedere [le soglie di avviso di utilizzo e avvisi sulle metriche delle prestazioni di Mirroring &#40; SQL Server &#41; ](../../database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md).  
  
 *alert_threshold*  
 Valore soglia per l'avviso. Se quando si aggiorna lo stato di mirroring viene restituito un valore che supera tale soglia, viene immessa una voce nel registro eventi di Windows. Questo valore è espresso in kilobyte, minuti o millisecondi, a seconda della metrica delle prestazioni.  
  
> [!NOTE]  
>  Per visualizzare i valori correnti, eseguire il [sp_dbmmonitorresults](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md) stored procedure.  
  
 *enabled*  
 Specifica se l'avviso è abilitato.  
  
 0 = L'avviso è disabilitato.  
  
 1 = L'avviso è abilitato.  
  
> [!NOTE]  
>  Il periodo di memorizzazione è sempre abilitato.  
  
## <a name="return-code-values"></a>Valori restituiti  
 Nessuno  
  
## <a name="result-sets"></a>Set di risultati  
 Nessuno  
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'appartenenza al ruolo predefinito del server **sysadmin** .  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono impostati i valori soglia per ogni metrica delle prestazioni e il periodo di memorizzazione per il database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]. Nella tabella seguente vengono riportati i valori utilizzati nell'esempio.  
  
|*alert_id*|Misurazione delle prestazioni|Valore soglia avvisi|Specifica se l'avviso è abilitato.|  
|-----------------|------------------------|-----------------------|-----------------------------|  
|1|Transazione non inviata meno recente|30 minuti|Sì|  
|2|Log non inviato|10.000 KB|Sì|  
|3|Log non ripristinato|10.000 KB|Sì|  
|4|Overhead commit mirror|1.000 millisecondi|no|  
|5|Periodo di memorizzazione|8 ore|Sì|  
  
```  
EXEC sp_dbmmonitorchangealert AdventureWorks2012, 1, 30, 1 ;  
EXEC sp_dbmmonitorchangealert AdventureWorks2012, 2, 10000, 1 ;  
EXEC sp_dbmmonitorchangealert AdventureWorks2012, 3, 10000, 1 ;  
EXEC sp_dbmmonitorchangealert AdventureWorks2012, 4, 1000, 0 ;  
EXEC sp_dbmmonitorchangealert AdventureWorks2012, 5, 8, 1 ;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Monitoraggio del mirroring del database &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [sp_dbmmonitorhelpalert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpalert-transact-sql.md)   
 [sp_dbmmonitordropalert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitordropalert-transact-sql.md)  
  
  
