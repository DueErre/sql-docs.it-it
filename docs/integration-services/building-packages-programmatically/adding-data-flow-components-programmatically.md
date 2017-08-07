---
title: Aggiunta di componenti flusso di dati a livello di codice | Documenti Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data flow task [Integration Services], components
- components [Integration Services], data flow
- data flow [Integration Services], components
ms.assetid: c06065cf-43e5-4b6b-9824-7309d7f5e35e
caps.latest.revision: 61
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: 8bd642d31e0a6a813b239935f3fb091003b682fc
ms.contentlocale: it-it
ms.lasthandoff: 08/03/2017

---
# <a name="adding-data-flow-components-programmatically"></a>Aggiunta di componenti del flusso di dati a livello di programmazione
  Il primo passaggio per la compilazione di un flusso di dati consiste nell'aggiunta di componenti. È quindi necessario configurarli e connetterli per stabilire il flusso di dati in fase di esecuzione. In questa sezione vengono descritti i passaggi per aggiungere un componente all'attività Flusso di dati, creare la relativa istanza della fase di progettazione e quindi configurarlo. Per informazioni su come connettere i componenti, vedere [connessione dati flusso componenti a livello di codice](../../integration-services/building-packages-programmatically/connecting-data-flow-components-programmatically.md).  
  
## <a name="adding-a-component"></a>Aggiunta di un componente  
 Chiamare il metodo <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaDataCollection100.New%2A> della raccolta <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.MainPipeClass.ComponentMetaDataCollection%2A> per creare un nuovo componente e aggiungerlo all'attività Flusso di dati. Questo metodo restituisce l'interfaccia <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> del componente. Tuttavia, a questo punto, <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> non contiene informazioni specifiche di un determinato componente. Impostare la proprietà <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ComponentClassID%2A> per identificare il tipo di componente. L'attività Flusso di dati utilizza il valore di questa proprietà per creare un'istanza del componente in fase di esecuzione.  
  
 Il valore specificato nella proprietà <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ComponentClassID%2A> può essere il CLSID, il PROGID o la proprietà <xref:Microsoft.SqlServer.Dts.Runtime.PipelineComponentInfo.CreationName%2A> del componente. Il CLSID viene in genere visualizzato nella finestra delle proprietà come valore della proprietà <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ComponentClassID%2A> del componente. Per informazioni su come ottenere questa proprietà e altre proprietà dei componenti disponibili, vedere [individuazione dati flusso componenti a livello di codice](../../integration-services/building-packages-programmatically/discovering-data-flow-components-programmatically.md).  
  
## <a name="adding-a-managed-component"></a>Aggiunta di un componente gestito  
 Non è possibile utilizzare il CLSID o il PROGID per aggiungere uno dei componenti gestiti al flusso di dati, perché questi valori puntano a un wrapper e non al componente stesso. È invece possibile usare il **CreationName** proprietà o **AssemblyQualifiedName** proprietà come illustrato nell'esempio seguente.  
  
 Se si prevede di usare il **AssemblyQualifiedName** proprietà, sarà necessario aggiungere un riferimento nel [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] progetto all'assembly che contiene il componente gestito. Questi assembly non sono elencati nella scheda .NET della finestra di **Aggiungi riferimento** la finestra di dialogo. In genere è necessario cercare e per individuare l'assembly nel **C:\Program Files\Microsoft SQL Server\100\DTS\PipelineComponents** cartella.  
  
 I componenti del flusso di dati gestiti predefiniti includono:  
  
-   Origine [!INCLUDE[vstecado](../../includes/vstecado-md.md)]  
  
-   Origine XML  
  
-   DataReader - destinazione  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Destinazione Compact  
  
-   Componente script  
  
 Nell'esempio di codice seguente sono illustrate entrambe le modalità di aggiunta di componenti gestiti al flusso di dati:  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
using Microsoft.SqlServer.Dts.Pipeline;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Microsoft.SqlServer.Dts.Runtime.Package package = new Microsoft.SqlServer.Dts.Runtime.Package();  
      Executable e = package.Executables.Add("STOCK:PipelineTask");  
      Microsoft.SqlServer.Dts.Runtime.TaskHost thMainPipe = (Microsoft.SqlServer.Dts.Runtime.TaskHost)e;  
      MainPipe dataFlowTask = (MainPipe)thMainPipe.InnerObject;  
  
      // The Application object will be used to obtain the CreationName  
      //  of a PipelineComponentInfo from its PipelineComponentInfos collection.  
      Application app = new Application();  
  
      // Add a first ADO NET source to the data flow.  
      //  The CreationName property requires an Application instance.  
      IDTSComponentMetaData100 component1 = dataFlowTask.ComponentMetaDataCollection.New();  
      component1.Name = "DataReader Source";  
      component1.ComponentClassID = app.PipelineComponentInfos["DataReader Source"].CreationName;  
  
      // Add a second ADO NET source to the data flow.  
      //  The AssemblyQualifiedName property requires a reference to the assembly.  
      IDTSComponentMetaData100 component2 = dataFlowTask.ComponentMetaDataCollection.New();  
      component2.Name = "DataReader Source";  
      component2.ComponentClassID = typeof(Microsoft.SqlServer.Dts.Pipeline.DataReaderSourceAdapter).AssemblyQualifiedName;  
    }  
  }  
}  
  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports Microsoft.SqlServer.Dts.Pipeline  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
  
Module Module1  
  
  Sub Main()  
  
    Dim package As Microsoft.SqlServer.Dts.Runtime.Package = _  
      New Microsoft.SqlServer.Dts.Runtime.Package()  
    Dim e As Executable = package.Executables.Add("STOCK:PipelineTask")  
    Dim thMainPipe As Microsoft.SqlServer.Dts.Runtime.TaskHost = _  
      CType(e, Microsoft.SqlServer.Dts.Runtime.TaskHost)  
    Dim dataFlowTask As MainPipe = CType(thMainPipe.InnerObject, MainPipe)  
  
    ' The Application object will be used to obtain the CreationName  
    '  of a PipelineComponentInfo from its PipelineComponentInfos collection.  
    Dim app As New Application()  
  
    ' Add a first ADO NET source to the data flow.  
    '  The CreationName property requires an Application instance.  
    Dim component1 As IDTSComponentMetaData100 = _  
      dataFlowTask.ComponentMetaDataCollection.New()  
    component1.Name = "DataReader Source"  
    component1.ComponentClassID = app.PipelineComponentInfos("DataReader Source").CreationName  
  
    ' Add a second ADO NET source to the data flow.  
    '  The AssemblyQualifiedName property requires a reference to the assembly.  
    Dim component2 As IDTSComponentMetaData100 = _  
      dataFlowTask.ComponentMetaDataCollection.New()  
    component2.Name = "DataReader Source"  
    component2.ComponentClassID = _  
      GetType(Microsoft.SqlServer.Dts.Pipeline.DataReaderSourceAdapter).AssemblyQualifiedName  
  
  End Sub  
  
End Module  
```  
  
## <a name="creating-the-design-time-instance-of-the-component"></a>Creazione dell'istanza della fase di progettazione del componente  
 Chiamare il metodo <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.Instantiate%2A> per creare l'istanza della fase di progettazione del componente identificato dalla proprietà <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ComponentClassID%2A>. Questo metodo restituisce l'oggetto <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapper>, che corrisponde al wrapper gestito per l'interfaccia <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSDesigntimeComponent100>.  
  
 Se possibile, modificare un componente utilizzando i metodi dell'istanza della fase di progettazione anziché modificando direttamente i relativi metadati. Anche se alcuni elementi dei metadati devono essere impostati direttamente, ad esempio le connessioni, in genere non è consigliabile eseguire questa operazione perché in questo modo il componente non è più in grado di monitorare e convalidare le modifiche.  
  
## <a name="assigning-connections"></a>Assegnazione di connessioni  
 Alcuni componenti, ad esempio il componente Origine OLE DB, richiedono una connessione a dati esterni e utilizzano un oggetto <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> esistente nel pacchetto a tale scopo. La proprietà <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeConnectionCollection100.Count%2A> della raccolta <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.RuntimeConnectionCollection%2A> indica il numero di oggetti <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> di runtime richiesti dal componente. Se il conteggio è maggiore di zero, il componente richiede una connessione. Assegnare una gestione connessione dal pacchetto al componente specificando le proprietà <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeConnection100.ConnectionManager%2A> e <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeConnection100.Name%2A> della prima connessione in <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.RuntimeConnectionCollection%2A>. Si noti che il nome della gestione connessione nella raccolta di connessione di run-time deve corrispondere al nome di managerreferenced la connessione dal pacchetto.  
  
## <a name="setting-the-values-of-custom-properties"></a>Impostazione dei valori delle proprietà personalizzate  
 Dopo aver creato l'istanza della fase di progettazione del componente, chiamare il metodo <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapperClass.ProvideComponentProperties%2A>. Questo metodo è simile a un costruttore, in quanto inizializza un componente appena creato definendone le proprietà personalizzate e gli oggetti di input e output. Non chiamare <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapperClass.ProvideComponentProperties%2A> più di una volta su un componente, perché il componente potrebbe reimpostarsi e perdere le modifiche apportate in precedenza ai propri metadati.  
  
 L'oggetto <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.CustomPropertyCollection%2A> del componente contiene una raccolta di oggetti <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100> specifici del componente. A differenza di altri modelli di programmazione, in cui le proprietà di un oggetto sono sempre visibili sullo stesso, i componenti popolano le loro raccolte di proprietà personalizzate solo quando viene chiamato il metodo <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapperClass.ProvideComponentProperties%2A>. Dopo aver chiamato il metodo, utilizzare il metodo <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapperClass.SetComponentProperty%2A> dell'istanza della fase di progettazione del componente per assegnare valori alle relative proprietà personalizzate. Questo metodo accetta una coppia nome/valore che identifica la proprietà personalizzata e fornisce il nuovo valore.  
  
## <a name="initializing-output-columns"></a>Inizializzazione di colonne di output  
 Dopo aver aggiunto un componente all'attività e dopo averlo configurato, inizializzare la raccolta di colonne in <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100> dell'oggetto. Questo passaggio è particolarmente importante per i componenti di origine, ma è possibile che non inizializzi le colonne per i componenti di trasformazione e destinazione, in quanto in genere dipendono dalle colonne che ricevono dai componenti a monte.  
  
 Chiamare il metodo <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapperClass.ReinitializeMetaData%2A> per inizializzare le colonne negli output di un componente di origine. Poiché i componenti non si connettono automaticamente alle origini dati esterne, chiamare il metodo <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapperClass.AcquireConnections%2A> prima di chiamare <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapperClass.ReinitializeMetaData%2A> per fornire al componente l'accesso all'origine dati esterna e la possibilità di popolare le proprie colonne di metadati. Infine, chiamare il metodo <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapperClass.ReleaseConnections%2A> per rilasciare la connessione.  
  
## <a name="next-step"></a>Passaggio successivo  
 Dopo l'aggiunta e configurazione del componente, il passaggio successivo consiste nella creazione di percorsi tra componenti, come illustrato nell'argomento [la creazione di un percorso tra due componenti](../../integration-services/building-packages-programmatically/connecting-data-flow-components-programmatically.md).  
  
## <a name="sample"></a>Esempio  
 Nell'esempio di codice seguente viene aggiunto il componente Origine OLE DB all'attività Flusso di dati, viene creata un'istanza della fase di progettazione del componente e vengono configurate le relative proprietà. Per questo esempio è richiesto un riferimento aggiuntivo all'assembly Microsoft.SqlServer.DTSRuntimeWrap.  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
using Microsoft.SqlServer.Dts.Runtime.Wrapper;  
using Microsoft.SqlServer.Dts.Pipeline;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Runtime.Package package = new Runtime.Package();  
      Executable e = package.Executables.Add("STOCK:PipelineTask");  
      Runtime.TaskHost thMainPipe = e as Runtime.TaskHost;  
      MainPipe dataFlowTask = thMainPipe.InnerObject as MainPipe;  
  
      // Add an OLEDB connection manager to the package.  
      ConnectionManager cm = package.Connections.Add("OLEDB");  
      cm.Name = "OLEDB ConnectionManager";  
      cm.ConnectionString = "Data Source=(local);" +   
        "Initial Catalog=AdventureWorks;Provider=SQLOLEDB.1;" +   
        "Integrated Security=SSPI;"  
  
      // Add an OLE DB source to the data flow.  
      IDTSComponentMetaData100 component =   
        dataFlowTask.ComponentMetaDataCollection.New();  
      component.Name = "OLEDBSource";  
      component.ComponentClassID = "DTSAdapter.OleDbSource.1";  
      // You can also use the CLSID of the component instead of the PROGID.  
      //component.ComponentClassID = "{2C0A8BE5-1EDC-4353-A0EF-B778599C65A0}";  
  
      // Get the design time instance of the component.  
      CManagedComponentWrapper instance = component.Instantiate();  
  
      // Initialize the component  
      instance.ProvideComponentProperties();  
  
      // Specify the connection manager.  
      if (component.RuntimeConnectionCollection.Count > 0)  
      {  
        component.RuntimeConnectionCollection[0].ConnectionManager =   
          DtsConvert.GetExtendedInterface(package.Connections[0]);  
        component.RuntimeConnectionCollection[0].ConnectionManagerID =   
          package.Connections[0].ID;      }  
  
      // Set the custom properties.  
      instance.SetComponentProperty("AccessMode", 2);  
      instance.SetComponentProperty("SqlCommand",   
        "Select * from Production.Product");  
  
      // Reinitialize the metadata.  
      instance.AcquireConnections(null);  
      instance.ReinitializeMetaData();  
      instance.ReleaseConnections();  
  
      // Add other components to the data flow and connect them.  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports Microsoft.SqlServer.Dts.Runtime.Wrapper  
Imports Microsoft.SqlServer.Dts.Pipeline  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
  
Module Module1  
  
  Sub Main()  
  
    Dim package As Microsoft.SqlServer.Dts.Runtime.Package = _  
      New Microsoft.SqlServer.Dts.Runtime.Package()  
    Dim e As Executable = package.Executables.Add("STOCK:PipelineTask")  
    Dim thMainPipe As Microsoft.SqlServer.Dts.Runtime.TaskHost = _  
      CType(e, Microsoft.SqlServer.Dts.Runtime.TaskHost)  
    Dim dataFlowTask As MainPipe = CType(thMainPipe.InnerObject, MainPipe)  
  
    ' Add an OLEDB connection manager to the package.  
    Dim cm As ConnectionManager = package.Connections.Add("OLEDB")  
    cm.Name = "OLEDB ConnectionManager"  
    cm.ConnectionString = "Data Source=(local);" & _  
      "Initial Catalog=AdventureWorks;Provider=SQLOLEDB.1;" & _  
      "Integrated Security=SSPI;"  
  
    ' Add an OLE DB source to the data flow.  
    Dim component As IDTSComponentMetaData100 = _  
      dataFlowTask.ComponentMetaDataCollection.New()  
    component.Name = "OLEDBSource"  
    component.ComponentClassID = "DTSAdapter.OleDbSource.1"  
    ' You can also use the CLSID of the component instead of the PROGID.  
    'component.ComponentClassID = "{2C0A8BE5-1EDC-4353-A0EF-B778599C65A0}";  
  
    ' Get the design time instance of the component.  
    Dim instance As CManagedComponentWrapper = component.Instantiate()  
  
    ' Initialize the component.  
    instance.ProvideComponentProperties()  
  
    ' Specify the connection manager.  
    If component.RuntimeConnectionCollection.Count > 0 Then  
      component.RuntimeConnectionCollection(0).ConnectionManager = _  
        DtsConvert.GetExtendedInterface(package.Connections(0))  
      component.RuntimeConnectionCollection(0).ConnectionManagerID = _  
        package.Connections(0).ID  
    End If  
  
    ' Set the custom properties.  
    instance.SetComponentProperty("AccessMode", 2)  
    instance.SetComponentProperty("SqlCommand", _  
      "Select * from Production.Product")  
  
    ' Reinitialize the metadata.  
    instance.AcquireConnections(vbNull)  
    instance.ReinitializeMetaData()  
    instance.ReleaseConnections()  
  
    ' Add other components to the data flow and connect them.  
  
  End Sub  
  
End Module  
```  
  
## <a name="external-resources"></a>Risorse esterne  
 Post di blog, [Ezapi per SQL Server 2012](http://go.microsoft.com/fwlink/?LinkId=243223), su blogs.msdn.com.  

## <a name="see-also"></a>Vedere anche  
 [La connessione a livello di programmazione di componenti flusso di dati](../../integration-services/building-packages-programmatically/connecting-data-flow-components-programmatically.md)  
  
  