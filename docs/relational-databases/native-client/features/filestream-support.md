---
title: Supporto FILESTREAM | Documenti Microsoft
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: native-client|features
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- FILESTREAM [SQL Server], SQL Server Native Client
- SQL Server Native Client [FILESTREAM support]
ms.assetid: 1ad3400d-7fcd-40c9-87ae-f5afc61e0374
caps.latest.revision: "21"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3ca2ec81cacec47dba4247f8c1c61ad2cf5d3d92
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2018
---
# <a name="filestream-support"></a>Supporto FILESTREAM
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  FILESTREAM consente di archiviare e accedere a valori binari di grandi dimensioni mediante [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o accesso diretto al file system di Windows. Un valore binario di grandi dimensioni è un valore superiore a 2 gigabyte (GB). Per ulteriori informazioni sul supporto FILESTREAM avanzato, vedere [FILESTREAM &#40; SQL Server &#41; ](../../../relational-databases/blob/filestream-sql-server.md).  
  
 Quando viene aperta una connessione al database, **@@TEXTSIZE**  verrà impostato su -1 ("unlimited"), per impostazione predefinita.  
  
 È anche possibile accedere alle colonne FILESTREAM e aggiornarle utilizzando l'API del file system di Windows.  
  
 Per altre informazioni, vedere gli argomenti seguenti:  
  
-   [Supporto FILESTREAM &#40; OLE DB &#41;](../../../relational-databases/native-client/ole-db/filestream-support-ole-db.md)  
  
-   [Supporto FILESTREAM &#40; ODBC &#41;](../../../relational-databases/native-client/odbc/filestream-support-odbc.md)  
  
-   [Accesso ai dati FILESTREAM con OpenSqlFilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)  
  
## <a name="querying-for-filestream-columns"></a>Esecuzione di una query sulle colonne FILESTREAM  
 I set di righe degli schemi in OLE DB non indicano se una colonna è di tipo FILESTREAM. ITableDefinition in OLE DB non può essere utilizzato per creare una colonna FILESTREAM.  
  
 Funzioni di catalogo, ad esempio SQLColumns di ODBC non indicano se una colonna è una colonna FILESTREAM.  
  
 Per creare colonne FILESTREAM o per rilevare le colonne esistenti sono colonne FILESTREAM, è possibile utilizzare il **is_filestream** colonna il [Columns](../../../relational-databases/system-catalog-views/sys-columns-transact-sql.md) vista del catalogo.  
  
 Di seguito è riportato un esempio:  
  
```  
-- Create a table with a FILESTREAM column.  
CREATE TABLE Bob_01 (GuidCol1 uniqueidentifier ROWGUIDCOL NOT NULL UNIQUE DEFAULT NEWID(), IntCol2 int, varbinaryCol3 varbinary(max) FILESTREAM);  
  
-- Find FILESTREAM columns.  
SELECT name FROM sys.columns WHERE is_filestream=1;  
  
-- Determine whether a column is a FILESTREAM column.  
SELECT is_filestream FROM sys.columns WHERE name = 'varbinaryCol3' AND object_id IN (SELECT object_id FROM sys.tables WHERE name='Bob_01');  
```  
  
## <a name="down-level-compatibility"></a>Compatibilità con le versioni precedenti  
 Se il client è stato compilato utilizzando la versione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client inclusa in [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], e l'applicazione si connette a [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], **varbinary (max)** comportamento sarà compatibile con [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Questo significa che i dati restituiti avranno come dimensione massima 2 GB. Per valori di dimensioni superiori a 2 GB, si verificherà il troncamento e verrà restituito un avviso di "stringa dati troncamento a destra".  
  
 Quando la compatibilità con il tipo di dati è impostata su 80, il comportamento client sarà coerente con il comportamento del client legacy.  
  
 Per i client che utilizzano SQLOLEDB o altri provider rilasciati prima di [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] versione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, **varbinary (max)** verrà eseguito il mapping all'immagine.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzionalità di SQL Server Native Client](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
