---
title: Usare l'output FOR JSON in SQL Server e nelle app client (SQL Server) | Microsoft Docs
ms.custom: 
ms.date: 06/02/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.component: json
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FOR JSON, using in client apps
- FOR JSON, using in SQL Server
ms.assetid: 302e5397-b499-4ea3-9a7f-c24ccad698eb
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d570ddc6fc2f29a97fa65ccae1c388787d063b27
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/03/2018
---
# <a name="use-for-json-output-in-sql-server-and-in-client-apps-sql-server"></a>Usare l'output FOR JSON in SQL Server e nelle app client (SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Gli esempi seguenti illustrano alcuni modi per usare la clausola **FOR JSON** e il relativo output JSON in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o nelle app client.  
  
## <a name="use-for-json-output-in-sql-server-variables"></a>Usare l'output FOR JSON nelle variabili di SQL Server  
L'output della clausola FOR JSON è di tipo NVARCHAR(MAX), quindi può essere assegnato a qualsiasi variabile, come illustrato nell'esempio seguente.  
  
```sql  
DECLARE @x NVARCHAR(MAX) = (SELECT TOP 10 * FROM Sales.SalesOrderHeader FOR JSON AUTO)  
```  
  
## <a name="use-for-json-output-in-sql-server-user-defined-functions"></a>Usare l'output FOR JSON nelle funzioni SQL Server definite dall'utente  
 È possibile creare funzioni definite dall'utente che formattano i set di risultati come JSON e restituiscono questo output JSON. Nell'esempio seguente viene creata una funzione definita dall'utente che recupera alcune righe di dettaglio di un ordine di vendita e le formatta come matrice JSON.  
  
```sql  
CREATE FUNCTION GetSalesOrderDetails(@salesOrderId int)  
 RETURNS NVARCHAR(MAX)  
AS  
BEGIN  
   RETURN (SELECT UnitPrice, OrderQty  
           FROM Sales.SalesOrderDetail  
           WHERE SalesOrderID = @salesOrderId  
           FOR JSON AUTO)  
END
```  
  
 Questa funzione può essere usata in un batch o in una query, come mostrato nell'esempio seguente.  
  
```sql  
DECLARE @x NVARCHAR(MAX) = dbo.GetSalesOrderDetails(43659)

PRINT dbo.GetSalesOrderDetails(43659)

SELECT TOP 10
  H.*, dbo.GetSalesOrderDetails(H.SalesOrderId) AS Details
FROM Sales.SalesOrderHeader H
```  
  
## <a name="merge-parent-and-child-data-into-a-single-table"></a>Unire dati padre e figlio in una singola tabella  
Nell'esempio seguente ogni set di righe figlio è formattato come matrice JSON. La matrice JSON diventa il valore della colonna Dettagli nella tabella padre.  
  
```sql  
SELECT TOP 10 SalesOrderId, OrderDate,  
      (SELECT TOP 3 UnitPrice, OrderQty  
         FROM Sales.SalesOrderDetail D  
         WHERE H.SalesOrderId = D.SalesOrderID  
         FOR JSON AUTO) AS Details  
INTO SalesOrder  
FROM Sales.SalesOrderHeader H  
```  
  
## <a name="update-the-data-in-json-columns"></a>Aggiornare i dati nelle colonne JSON  
 L'esempio seguente dimostra che è possibile aggiornare il valore di una colonna che contiene testo JSON.  
  
```sql  
UPDATE SalesOrder  
SET Details =  
     (SELECT TOP 1 UnitPrice, OrderQty  
       FROM Sales.SalesOrderDetail D  
       WHERE D.SalesOrderId = SalesOrder.SalesOrderId  
      FOR JSON AUTO 
```  
  
## <a name="use-for-json-output-in-a-c-client-app"></a>Usare l'output FOR JSON in un'app client C#  
 L'esempio seguente mostra come recuperare l'output JSON di una query in un oggetto StringBuilder in un'app client C#. Si supponga che la variabile `queryWithForJson` contenga il testo dell'istruzione SELECT con una clausola FOR JSON.  
  
```csharp  
var queryWithForJson = "SELECT ... FOR JSON";
var conn = new SqlConnection("<connection string>");
var cmd = new SqlCommand(queryWithForJson, conn);
conn.Open();
var jsonResult = new StringBuilder();
var reader = cmd.ExecuteReader();
if (!reader.HasRows)
{
    jsonResult.Append("[]");
}
else
{
    while (reader.Read())
    {
        jsonResult.Append(reader.GetValue(0).ToString());
    }
}
```  

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>Altre informazioni su JSON in SQL Server e nel database SQL di Azure  
  
### <a name="microsoft-blog-posts"></a>Post del blog Microsoft  
  
Per soluzioni specifiche, casi d'uso e indicazioni, vedere questi [post del blog sul supporto JSON integrato](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) in SQL Server e nel database SQL di Azure.  

### <a name="microsoft-videos"></a>Video Microsoft

Per un'introduzione visiva al supporto JSON predefinito in SQL Server e nel database SQL di Azure, vedere i video seguenti:

-   [SQL Server 2016 and JSON Support](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support) (SQL Server 2016 e supporto JSON)

-   [Using JSON in SQL Server 2016 and Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database) (Uso di JSON in SQL Server 2016 e nel database SQL di Azure)

-   [JSON as a bridge between NoSQL and relational worlds](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) (JSON come ponte tra NoSQL e gli ambienti relazionali)
 
## <a name="see-also"></a>Vedere anche  
 [Formattare i risultati delle query in formato JSON con FOR JSON &#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
  
  
