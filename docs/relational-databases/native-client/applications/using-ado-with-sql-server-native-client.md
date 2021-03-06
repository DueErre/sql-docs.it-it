---
title: Utilizzo di ADO con SQL Server Native Client | Documenti Microsoft
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client|applications
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client, ADO
- data access [SQL Server Native Client], ADO
- ADO [SQL Server Native Client]
- SQLNCLI, ADO
ms.assetid: 118a7cac-4c0d-44fd-b63e-3d542932d239
caps.latest.revision: "22"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 13978b8eb01fda4b9478111a3bef3e36c76f8e58
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2018
---
# <a name="using-ado-with-sql-server-native-client"></a>Utilizzo di ADO con SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Per sfruttare i vantaggi delle nuove funzionalità introdotte [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] , ad esempio multiple active result set (MARS), le notifiche delle query, tipi definiti dall'utente (UDT) o il nuovo **xml** tipo di dati, le applicazioni esistenti che utilizzano ActiveX Data Objects (ADO) deve utilizzare il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provider OLE DB Native Client come provider di accesso ai dati.  
  
 L'uso del provider OLE DB di [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] Native Client è necessario solo per utilizzare una delle caratteristiche introdotte in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se non si intende utilizzare tali caratteristiche, è possibile continuare a usare il provider di accesso ai dati corrente, generalmente SQLOLEDB. L'uso del provider OLE DB di [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] Native Client è consigliabile se si intende potenziare un'applicazione esistente e si ha l'esigenza di utilizzare le nuove caratteristiche introdotte in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Se si sviluppa una nuova applicazione, è consigliabile valutare l'opportunità di utilizzare ADO.NET e il provider di dati .NET Framework per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] anziché [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client per accedere a tutte le nuove caratteristiche delle ultime versioni di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Per ulteriori informazioni sul provider di dati .NET Framework per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], fare riferimento alla documentazione di .NET Framework SDK per ADO.NET.  
  
 Per consentire l'utilizzo in ADO delle nuove caratteristiche delle ultime versioni di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], al provider OLE DB di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client sono stati apportati alcuni miglioramenti che estendono le caratteristiche principali di OLE DB. Questi miglioramenti consentono alle applicazioni ADO di utilizzare più recente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] funzionalità e di utilizzare due tipi di dati introdotti in [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]: **xml** e **udt**. Questi miglioramenti anche di sfruttare i miglioramenti per il **varchar**, **nvarchar**, e **varbinary** tipi di dati. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client aggiunge la proprietà di inizializzazione SSPROP_INIT_DATATYPECOMPATIBILITY di proprietà DBPROPSET_SQLSERVERDBINIT per l'utilizzo nelle applicazioni ADO in modo che i nuovi tipi di dati sono esposti in modo compatibile con ADO. Inoltre, il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provider OLE DB Native Client definisce anche una nuova parola chiave stringa connessione denominata **DataTypeCompatibility** impostato nella stringa di connessione.  
  
> [!NOTE]  
>  Le applicazioni ADO esistenti possono accedere a valori XML, UDT, nonché di campi binari e di testo valore di grandi dimensioni ed eseguirne l'aggiornamento utilizzando il provider SQLOLEDB. Il nuovo maggiore **varchar (max)**, **nvarchar (max)**, e **varbinary (max)** tipi di dati vengono restituiti come i tipi ADO **adLongVarChar**, **adLongVarWChar** e **adLongVarBinary** rispettivamente. Le colonne XML vengono restituite come **adLongVarChar**, e vengono restituite le colonne di tipo definito dall'utente come **adVarBinary**. Tuttavia, se si utilizza il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provider OLE DB Native Client (SQLNCLI11) anziché SQLOLEDB, è necessario assicurarsi di impostare il **DataTypeCompatibility** (parola chiave) su "80" in modo che i nuovi tipi di dati verranno eseguito il mapping correttamente ai dati ADO tipi.  
  
## <a name="enabling-sql-server-native-client-from-ado"></a>Abilitazione di SQL Server Native Client da ADO  
 Per abilitare l'utilizzo di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, le applicazioni ADO saranno necessario implementare le parole chiave seguenti nelle stringhe di connessione:  
  
-   `Provider=SQLNCLI11`  
  
-   `DataTypeCompatibility=80`  
  
 Per ulteriori informazioni su ADO parole chiave supportate in stringhe di connessione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, vedere [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 Ecco un esempio di creazione di una stringa di connessione ADO pienamente abilitata per funzionare con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, inclusa l'abilitazione della funzionalità di MARS:  
  
```  
Dim con As New ADODB.Connection  
  
con.ConnectionString = "Provider=SQLNCLI11;" _  
         & "Server=(local);" _  
         & "Database=AdventureWorks;" _   
         & "Integrated Security=SSPI;" _  
         & "DataTypeCompatibility=80;" _  
         & "MARS Connection=True;"  
con.Open  
```  
  
## <a name="examples"></a>Esempi  
 Nelle sezioni seguenti vengono forniscono esempi di come è possibile utilizzare ADO con il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provider OLE DB Native Client.  
  
### <a name="retrieving-xml-column-data"></a>Recupero dei dati delle colonne XML  
 In questo esempio viene utilizzato un recordset per recuperare e visualizzare i dati da una colonna XML nel [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **AdventureWorks** database di esempio.  
  
```  
Dim con As New ADODB.Connection  
Dim rst As New ADODB.Recordset  
Dim sXMLResult As String  
  
con.ConnectionString = "Provider=SQLNCLI11;" _  
         & "Server=(local);" _  
         & "Database=AdventureWorks;" _   
         & "Integrated Security=SSPI;" _   
         & "DataTypeCompatibility=80;"  
  
con.Open  
  
' Get the xml data as a recordset.  
Set rst.ActiveConnection = con  
rst.Source = "SELECT AdditionalContactInfo FROM Person.Contact " _  
   & "WHERE AdditionalContactInfo IS NOT NULL"  
rst.Open  
  
' Display the data in the recordset.  
While (Not rst.EOF)  
   sXMLResult = rst.Fields("AdditionalContactInfo").Value  
   Debug.Print (sXMLResult)  
   rst.MoveNext  
End While  
  
con.Close  
Set con = Nothing  
```  
  
> [!NOTE]  
>  L'applicazione di filtri al recordset non è supportata con le colonne XML. Se si prova ad applicare i filtri, viene generato un errore.  
  
### <a name="retrieving-udt-column-data"></a>Recupero dei dati delle colonne con tipo definito dall'utente  
 In questo esempio, un **comando** oggetto viene usato per eseguire una query SQL che restituisce un tipo definito dall'utente, i dati di tipo definito dall'utente vengono aggiornati e quindi i nuovi dati viene inseriti nel database. In questo esempio si presuppone che il **punto** tipo definito dall'utente è già stato registrato nel database.  
  
```  
Dim con As New ADODB.Connection  
Dim cmd As New ADODB.Command  
Dim rst As New ADODB.Recordset  
Dim strOldUDT As String  
Dim strNewUDT As String  
Dim aryTempUDT() As String  
Dim strTempID As String  
Dim i As Integer  
  
con.ConnectionString = "Provider=SQLNCLI11;" _  
         & "Server=(local);" _  
         & "Database=AdventureWorks;" _   
         & "Integrated Security=SSPI;" _  
         & "DataTypeCompatibility=80;"  
  
con.Open  
  
' Get the UDT value.  
Set cmd.ActiveConnection = con  
cmd.CommandText = "SELECT ID, Pnt FROM dbo.Points.ToString()"  
Set rst = cmd.Execute  
strTempID = rst.Fields(0).Value  
strOldUDT = rst.Fields(1).Value  
  
' Do something with the UDT by adding i to each point.  
arytempUDT = Split(strOldUDT, ",")  
i = 3  
strNewUDT = LTrim(Str(Int(aryTempUDT(0)) + i)) + "," + _  
   LTrim(Str(Int(aryTempUDT(1)) + i))  
  
' Insert the new value back into the database.  
cmd.CommandText = "UPDATE dbo.Points SET Pnt = '" + strNewUDT + _  
   "' WHERE ID = '" + strTempID + "'"  
cmd.Execute  
  
con.Close  
Set con = Nothing  
```  
  
### <a name="enabling-and-using-mars"></a>Abilitazione e utilizzo di MARS  
 In questo esempio viene costruita la stringa di connessione per abilitare MARS mediante il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provider OLE DB Native Client e quindi due oggetti recordset vengono creati da eseguire utilizzando la stessa connessione.  
  
```  
Dim con As New ADODB.Connection  
  
con.ConnectionString = "Provider=SQLNCLI11;" _  
         & "Server=(local);" _  
         & "Database=AdventureWorks;" _   
         & "Integrated Security=SSPI;" _  
         & "DataTypeCompatibility=80;" _  
         & "MARS Connection=True;"  
con.Open  
  
Dim recordset1 As New ADODB.Recordset  
Dim recordset2 As New ADODB.Recordset  
  
Dim recordsaffected As Integer  
Set recordset1 =  con.Execute("SELECT * FROM Table1", recordsaffected, adCmdText)  
Set recordset2 =  con.Execute("SELECT * FROM Table2", recordsaffected, adCmdText)  
  
con.Close  
Set con = Nothing  
```  
  
 Nelle versioni precedenti del provider OLE DB questo codice determinerebbe la creazione di una connessione implicita alla seconda esecuzione, in quanto per una sola connessione sarebbe possibile aprire un solo set attivo di risultati. Poiché la connessione implicita non sarebbe inserita nel pool di connessioni OLE DB, questa situazione provocherebbe overhead aggiuntivo. Con la funzionalità MARS esposto dal [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provider OLE DB Native Client, si ottengono più risultati attivi in un'unica connessione.  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di applicazioni con SQL Server Native Client](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
