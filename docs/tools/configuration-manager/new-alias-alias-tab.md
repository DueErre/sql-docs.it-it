---
title: Nuovo Alias (scheda Alias) | Documenti Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: configuration-manager
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 785eb6fb-f67e-449d-b1c8-c38dfbb95ef6
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8a39d7940814839dcda00d45b7dd325a887a3d7b
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/03/2018
---
# <a name="new-alias-alias-tab"></a>Nuovo alias (scheda Alias)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
Un alias rappresenta un nome alternativo che può essere utilizzato per stabilire una connessione. L'alias incapsula gli elementi necessari di una stringa di connessione e li espone con un nome scelto dall'utente. La pagina **Alias** della finestra di dialogo **Nuovo alias** consente di specificare gli elementi della stringa di connessione per un alias. Per modificare la stringa di connessione di un alias esistente, vedere [Proprietà &#60;Alias&#62; &#40;scheda Alias&#41;](../../tools/configuration-manager/alias-properties-alias-tab.md).  
  
 Non è necessario completare tutti i valori nella griglia **Proprietà** . Le combinazioni valide variano a seconda del protocollo selezionato. Per esempi di combinazioni valide, vedere gli argomenti elencati di seguito.  
  
 **Nome alias**  
 Nome o alias che si desidera utilizzare per fare riferimento alla connessione.  
  
 **Nome pipe** / **Numero porta**  
 Elementi aggiuntivi della stringa di connessione. Il nome di questa casella varia a seconda del protocollo selezionato.  
  
 **Protocollo**  
 Protocollo utilizzato per la connessione.  
  
 **Server**  
 Nome dell'istanza di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a cui si esegue la connessione.  
  
## <a name="when-to-use-an-alias"></a>Situazioni in cui utilizzare un alias  
 Per impostazione predefinita, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si connette a un'istanza locale di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante il protocollo **Shared Memory** e a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un altro computer mediante **TCP/IP** o **Named Pipes**. Creare un alias quando si utilizza TCP/IP o Named Pipes e si desidera fornire una stringa di connessione personalizzata o quando si desidera utilizzare un nome diverso da quello del server per la connessione.  
  
### <a name="examples"></a>Esempi  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non è in attesa sulla porta TCP/IP 1433 predefinita, pertanto si desidera creare una stringa di connessione con un numero di porta diverso.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non è in attesa sulla porta named pipe predefinita, pertanto si desidera creare una stringa di connessione con un nome di pipe diverso.  
  
-   Un'applicazione prevede di connettersi a un database nel server denominato `ACCT`, ma tale database è stato consolidato come istanza denominata `ACCT` nel server `CENTRAL`. Non è semplice modificare l'applicazione. Creare un alias denominato `ACCT`, con una stringa di connessione che punta a `CENTRAL\ACCT`.  
  
## <a name="creating-a-valid-connection-string"></a>Creazione di una stringa di connessione valida  
 Per una descrizione ed esempi di combinazioni valide di proprietà di alias, vedere gli argomenti seguenti:  
  
-   [Creazione di una stringa di connessione valida tramite il protocollo Shared Memory](../../tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)  
  
-   [Creazione di una stringa di connessione valida con TCP/IP](../../tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md)  
  
-   [Creazione di una stringa di connessione valida tramite Named pipe](http://msdn.microsoft.com/library/90930ff2-143b-4651-8ae3-297103600e4f)  
  
  
