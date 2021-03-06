---
title: PHP Driver per SQL Server Support for LocalDB | Documenti Microsoft
ms.custom: 
ms.date: 02/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: sql
ms.prod_service: drivers
ms.component: php
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d315ad6a-0d50-4093-80c2-2f11217237c2
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4dcf9e36eb3928bc606053bdfda441520155864a
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/21/2017
---
# <a name="php-driver-for-sql-server-support-for-localdb"></a>PHP Driver for SQL Server Support for LocalDB (Driver PHP per il supporto SQL Server per LocalDB)

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

A partire da [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)], una versione leggera di [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], chiamata LocalDB, sarà disponibile. In questo argomento viene discussa la modalità di connessione a un database in un'istanza del database locale.

## <a name="remarks"></a>Osservazioni

Per ulteriori informazioni su LocalDB, ad esempio come installarlo e configurare l'istanza di LocalDB, vedere il [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] argomento della documentazione Online in [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] Express LocalDB.

Riepilogando, il database locale consente di:

-   Utilizzare **sqllocaldb.exe è** per individuare il nome dell'istanza predefinita.

-   Utilizzare il **AttachDBFilename** parola chiave di stringa di connessione per specificare quale file di database il server deve essere connesso. Quando si utilizza **AttachDBFilename**, se non si specifica il nome del database con il **Database** parola chiave di stringa di connessione, verrà rimosso dal database dell'istanza del database locale quando l'applicazione chiude.

-   Specificare un'istanza di LocalDB nella stringa di connessione. Di seguito è ad esempio, una stringa di connessione di esempio SQLSRV:

    ```php
    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array( 'Database'=>'myData'));

    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array('AttachDBFileName'=>'c:\\myData.MDF','Database'=>'myData'));

    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array('AttachDBFileName'=>'c:\\myData.MDF'));
    ```

    Di seguito è una stringa di connessione di esempio PDO_SQLSRV:  

    ```php
    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'Database=myData', NULL, NULL);

    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'AttachDBFileName=c:\\myData.MDF;Database=myData ',
        NULL, NULL);

    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'AttachDBFileName=c:\\myData.MDF', NULL, NULL);  
    ```

Se necessario, è possibile creare un'istanza del database locale con sqllocaldb.exe. È possibile utilizzare anche sqlcmd.exe per aggiungere e modificare i database in un'istanza del database locale. Ad esempio, `sqlcmd -S (localdb)\v11.0`. (Quando si esegue IIS, è necessario eseguire con l'account corretto per ottenere gli stessi risultati quando si esegue la riga di comando; vedere [con LocalDB con IIS completo, parte 2: la proprietà dell'istanza](http://blogs.msdn.com/b/sqlexpress/archive/2011/12/09/using-localdb-with-full-iis-part-2-instance-ownership.aspx) per ulteriori informazioni.)

Esempio le stringhe di connessione con il driver SQLSRV che si connettono a un database in un database locale denominato istanza chiamata myInstance sono i seguenti:

```php
$conn = sqlsrv_connect( '(localdb)\\myInstance',
    array( 'Database'=>'myData'));
```

Di seguito sono stringhe di connessione esempio Usa il driver PDO_SQLSRV che si connettono a un database in un database locale di istanza chiamata myInstance denominato:  
  
```php
$conn = new PDO( 'sqlsrv:server=(localdb)\\myInstance;'
    . 'database=myData', NULL, NULL);
```

È possibile scaricare LocalDB dal [pagina feature pack di SQL Server 2012](http://go.microsoft.com/fwlink/?LinkID=236805), o dal [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] Express edition. Se si usa sqlcmd.exe per modificare i dati nell'istanza di LocalDB, sarà necessario sqlcmd da [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)], che è possibile ottenere dal download nell'utilità della riga di comando di [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] pagina Feature Pack.

## <a name="see-also"></a>Vedere anche

[Connessione al server](../../connect/php/connecting-to-the-server.md)
