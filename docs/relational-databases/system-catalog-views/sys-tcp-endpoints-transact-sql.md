---
title: Sys. tcp_endpoints (Transact-SQL) | Documenti Microsoft
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.tcp_endpoints
- sys.tcp_endpoints_TSQL
- tcp_endpoints
- tcp_endpoints_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.tcp_endpoints catalog view
ms.assetid: 43cc3afa-cced-4463-8e97-fbfdaf2e4fa8
caps.latest.revision: "28"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2be15d96b5ab7274688c34303ccf1603064dce9d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="systcpendpoints-transact-sql"></a>sys.tcp_endpoints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una riga per ogni endpoint TCP nel sistema. Gli endpoint che sono descritti **Sys. tcp_endpoints** forniscono un oggetto per concedere e revocare il privilegio di connessione. Le informazioni visualizzate relative alle porte e agli indirizzi IP non vengono utilizzate per configurare i protocolli e potrebbero non corrispondere alla configurazione effettiva del protocollo. Per visualizzare e configurare i protocolli, utilizzare Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|**< colonne ereditate >**||Eredita le colonne da [Endpoints](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md).|  
|**port**|int|Numero della porta su cui è in attesa l'endpoint. Non ammette i valori Null.|  
|**is_dynamic_port**|bit|1 = Il numero della porta è stato assegnato dinamicamente.<br /><br /> Non ammette i valori Null.|  
|**indirizzo_IP**|**nvarchar(45)**|Indirizzo IP del listener specificato dalla clausola LISTENER_IP. Ammette i valori Null.|  
  
## <a name="remarks"></a>Osservazioni  
 Eseguire la query seguente per raccogliere informazioni sugli endpoint e sulle connessioni. Gli endpoint senza connessioni correnti o TCP verranno visualizzati con valori NULL. Aggiungere il **in** clausola `WHERE des.session_id = @@SPID` per restituire informazioni sulla connessione corrente.  
  
```  
SELECT des.login_name, des.host_name, program_name,  dec.net_transport, des.login_time,   
e.name AS endpoint_name, e.protocol_desc, e.state_desc, e.is_admin_endpoint,   
t.port, t.is_dynamic_port, dec.local_net_address, dec.local_tcp_port   
FROM sys.endpoints AS e  
LEFT JOIN sys.tcp_endpoints AS t  
   ON e.endpoint_id = t.endpoint_id  
LEFT JOIN sys.dm_exec_sessions AS des  
   ON e.endpoint_id = des.endpoint_id  
LEFT JOIN sys.dm_exec_connections AS dec  
   ON des.session_id = dec.session_id;  
```  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Viste del catalogo degli endpoint &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)  
  
  
