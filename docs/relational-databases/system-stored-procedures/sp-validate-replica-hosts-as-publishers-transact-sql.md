---
title: sp_validate_replica_hosts_as_publishers (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_validate_replica_hosts_as_publishers_TSQL
- sp_validate_replica_hosts_as_publishers
helpviewer_keywords: sp_validate_replica_hosts_as_publishers
ms.assetid: 45001fc9-2dbd-463c-af1d-aa8982d8c813
caps.latest.revision: "11"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2f4cd7135f5773300e1d95291c778463cece6a85
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="spvalidatereplicahostsaspublishers-transact-sql"></a>sp_validate_replica_hosts_as_publishers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  **sp_validate_replica_hosts_as_publishers** è un'estensione di **sp_validate_redirected_publisher** che consente tutte le repliche secondarie, piuttosto che solo la replica primaria corrente, da convalidare. **sp_validate_replicat_hosts_as_publisher** convalida un'intera sempre nella topologia di replica. **sp_validate_replica_hosts_as_publishers** deve essere eseguita direttamente nel server di distribuzione tramite una sessione desktop remoto per evitare un errore di sicurezza a doppio hop (21892).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_validate_replica_hosts_as_publishers   
    [ @original_publisher = ] 'original_publisher',  
    [ @publisher_db = ] 'database_name',   
    [ @redirected_publisher = ] 'new_publisher' output  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@original_publisher**  =] **'***original_publisher***'**  
 Il nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che ha pubblicato in origine il database. *original_publisher* è **sysname**, non prevede alcun valore predefinito.  
  
 [  **@publisher_db**  =] **'***publisher_db***'**  
 Il nome del database da pubblicare. *publisher_db* è **sysname**, non prevede alcun valore predefinito.  
  
 [  **@redirected_publisher**  =] **'***redirected_publisher***'**  
 La destinazione di reindirizzamento quando **sp_redirect_publisher** è stato chiamato per l'originale server di pubblicazione/database pubblicato coppia. *redirected_publisher* è **sysname**, non prevede alcun valore predefinito.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="result-sets"></a>Set di risultati  
 nessuna.  
  
## <a name="remarks"></a>Osservazioni  
 Se non esiste alcuna voce per il server di pubblicazione e il database di pubblicazione, **sp_validate_redirected_publisher** restituisce null per il parametro di output  *@redirected_publisher* . In caso contrario, viene restituito il server di pubblicazione reindirizzato associato, sia in caso di esito positivo che di esito negativo.  
  
 Se la convalida ha esito positivo, **sp_validate_redirected_publisher** restituisce un'indicazione di esito positivo.  
  
 Se la convalida non riesce, vengono generati gli errori appropriati.  **sp_validate_redirected_publisher** rende durante un tentativo per la generazione di tutti i problemi e non solo il primo.  
  
> [!NOTE]  
>  **sp_validate_replica_hosts_as_publishers** avrà esito negativo e verrà visualizzato il messaggio di errore seguente durante la convalida degli host della replica secondaria che non consentono l'accesso in lettura o richiedono che venga specificata la finalità di lettura.  
>   
>  Msg 21899, Livello 11, Stato 1, Procedura **sp_hadr_verify_subscribers_at_publisher**, Riga 109  
>   
>  La query sul server di pubblicazione reindirizzato 'MyReplicaHostName' per determinare la presenza di voci sysserver per i sottoscrittori del server di pubblicazione originale 'MyOriginalPublisher' non è riuscita restituendo l'errore '976', messaggio di errore 'Errore 976, Livello 14, Stato 1, Messaggio: Il database di destinazione, 'MyPublishedDB', partecipa a un gruppo di disponibilità e non è attualmente accessibile per le query. Lo spostamento dei dati è sospeso o la replica di disponibilità non è abilitata per l'accesso in lettura. Per consentire l'accesso in sola lettura a questo e ad altri database nel gruppo di disponibilità, abilitare l'accesso in lettura a una o più repliche di disponibilità secondarie nel gruppo.  Per altre informazioni, vedere l'istruzione **ALTER AVAILABILITY GROUP** nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
>   
>  Sono stati rilevati uno o più errori di convalida del server di pubblicazione per l'host della replica 'MyReplicaHostName'.  
  
## <a name="permissions"></a>Permissions  
 Chiamante deve essere un membro del **sysadmin** ruolo predefinito del server, il **db_owner** ruolo predefinito del database per il database di distribuzione o un membro di un elenco di accesso per una pubblicazione definita associato al database di pubblicazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure per la replica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sp_get_redirected_publisher &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-get-redirected-publisher-transact-sql.md)   
 [sp_redirect_publisher &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-redirect-publisher-transact-sql.md)   
 [sp_validate_redirected_publisher &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-validate-redirected-publisher-transact-sql.md)  
  
  
