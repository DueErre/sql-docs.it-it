---
title: I membri di SQLServerXAResource | Documenti Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a069bf2c-1b70-4817-b084-a508445de799
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7e61b22a719ea74b1097a50f811a4e1bde85db54
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/18/2017
---
# <a name="sqlserverxaresource-members"></a>Membri di SQLServerXAResource
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Le tabelle seguenti elencano i membri esposti dal [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) classe.  
  
## <a name="constructors"></a>Costruttori  
 nessuna.  
  
## <a name="fields"></a>Campi  
  
|Nome|Description|  
|----------|-----------------|  
|[SSTRANSTIGHTLYCPLD](../../../connect/jdbc/reference/sstranstightlycpld-field-sqlserverxaresource.md)|Utilizzato per consentire le transazioni XA "a regime di controllo stretto ("tightly-coupled")" che dispongono di diversi ID di transazione dei rami XA (XID), ma dello stesso ID di transazione globale (GTRID).|  
  
## <a name="inherited-fields"></a>Campi ereditati  
  
|Classe ereditata da:|Metodi|  
|---------------------------|-------------|  
|javax.transaction.xa.XAResource|TMENDRSCAN, TMFAIL, TMJOIN, TMNOFLAGS, TMONEPHASE, TMRESUME, TMSTARTRSCAN, TMSUCCESS, TMSUSPEND, XA_OK, XA_RDONLY|  
  
## <a name="methods"></a>Metodi  
  
|Nome|Description|  
|----------|-----------------|  
|[commit](../../../connect/jdbc/reference/commit-method-sqlserverxaresource.md)|Esegue il commit della transazione globale specificata dall'oggetto Xid specificato.|  
|[fine](../../../connect/jdbc/reference/end-method-sqlserverxaresource.md)|Termina il lavoro eseguito per conto di un ramo di transazione.|  
|[dimenticare](../../../connect/jdbc/reference/forget-method-sqlserverxaresource.md)|Indica allo strumento di gestione delle risorse di dimenticare un ramo di transazione completato euristicamente.|  
|[getTransactionTimeout](../../../connect/jdbc/reference/gettransactiontimeout-method-sqlserverxaresource.md)|Ottiene il valore di timeout della transazione corrente impostato per questo [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) oggetto.|  
|[isSameRM](../../../connect/jdbc/reference/issamerm-method-sqlserverxaresource.md)|Determina se l'istanza di gestione risorse rappresentata dall'oggetto di destinazione corrisponde all'istanza del gestore di risorse rappresentata dall'oggetto fornito XAResource.|  
|[preparare](../../../connect/jdbc/reference/prepare-method-sqlserverxaresource.md)|Richieste di Prepara il gestore delle risorse per un commit della transazione specificata dall'oggetto Xid specificato.|  
|[recuperare](../../../connect/jdbc/reference/recover-method-sqlserverxaresource.md)|Ottiene un elenco di rami di transazioni preparati da uno strumento di gestione delle risorse.|  
|[rollback](../../../connect/jdbc/reference/rollback-method-sqlserverxaresource.md)|Richiede che il lavoro di rollback dello strumento di gestione delle risorse venga eseguito per conto di un ramo di transazione.|  
|[setTransactionTimeout](../../../connect/jdbc/reference/settransactiontimeout-method-sqlserverxaresource.md)|Imposta il valore di timeout della transazione corrente per questo [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) oggetto.|  
|[inizio](../../../connect/jdbc/reference/start-method-sqlserverxaresource.md)|Avvia il lavoro per conto di un ramo di transazione specificato nell'oggetto Xid.|  
  
## <a name="inherited-methods"></a>Metodi ereditati  
  
|Classe ereditata da:|Metodi|  
|---------------------------|-------------|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
  
## <a name="see-also"></a>Vedere anche  
 [Classe SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
