---
title: "Accesso alla funzionalità SQLXML nell'ambiente .NET | Documenti Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- Managed Classes [SQLXML], accessing SQLXML functionality
- SQLXML Managed Classes, accessing SQLXML functionality
- DiffGrams [SQLXML], accessing SQLXML functionality
- .NET Framework [SQLXML], accessing SQLXML functionality
ms.assetid: 74744535-2945-414d-9a5b-7e8cc363953a
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 408a93509ff703b843dac572269fdc8a30825bd7
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2018
---
# <a name="accessing-sqlxml-functionality-in-the-net-environment"></a>Accesso alla funzionalità SQLXML nell'ambiente .NET
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Questo esempio mostra:  
  
-   Come usare [!INCLUDE[msCoName](../../../includes/msconame-md.md)] classi gestite SQLXML (Microsoft.Data.SqlXml) per accedere a Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nel [!INCLUDE[msCoName](../../../includes/msconame-md.md)] ambiente .NET Framework.  
  
-   Come i DiffGram generati nell'ambiente .NET Framework possono applicare aggiornamenti dei dati alle tabelle di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 In questa applicazione viene eseguita una query XPath su uno schema XSD. L'esecuzione della query XPath restituisce un documento XML costituito da dati di contatto (**FirstName**, **LastName**). L'applicazione carica il documento XML nel set di dati nell'ambiente .NET Framework. I dati nel set di dati vengono modificati: il nome del contatto viene modificato in "Susan" per il primo contatto nel set di dati. Il DiffGram viene generato dal set di dati e l'aggiornamento specificato nel DiffGram (la modifica nel nome del dipendente) viene quindi applicato alla tabella Person.Contact.  
  
> [!NOTE]  
>  Nel codice è necessario specificare il nome dell'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nella stringa di connessione.  
  
```  
using System;  
using System.Data;  
using Microsoft.Data.SqlXml;  
using System.IO;  
class Test  
{  
   static string ConnString = "Provider=SQLOLEDB;Server=SqlServerName;database=AdventureWorks;Integrated Security=SSPI;";  
   public static int testParams()  
   {  
      DataRow row;  
      SqlXmlAdapter ad;  
      //need a memory stream to hold diff gram temporarily  
      MemoryStream ms = new MemoryStream();  
      SqlXmlCommand cmd = new SqlXmlCommand(ConnString);  
      cmd.RootTag = "ROOT";  
      cmd.CommandText = "Con";  
      cmd.CommandType = SqlXmlCommandType.XPath;  
      cmd.SchemaPath = "MySchema.xml";  
      //load data set  
      DataSet ds = new DataSet();  
      ad = new SqlXmlAdapter(cmd);  
      ad.Fill(ds);  
      row = ds.Tables["Con"].Rows[0];  
      row["FName"] = "Susan";  
      ad.Update(ds);  
      return 0;  
   }  
   public static int Main(String[] args)  
   {  
      testParams();  
      return 0;  
   }  
}  
```  
  
 **Per testare l'esempio:**  
  
 Per testare questo esempio, è necessario che nel computer sia installato [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework.  
  
1.  Salvare questo schema XSD (MySchema.xml) in una cartella:  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
      <xsd:element name="Con" sql:relation="Person.Contact" >  
       <xsd:complexType>  
         <xsd:sequence>  
            <xsd:element name="FName"    
                         sql:field="FirstName"   
                         type="xsd:string" />   
            <xsd:element name="LName"    
                         sql:field="LastName"    
                         type="xsd:string" />  
         </xsd:sequence>  
         <xsd:attribute name="ContactID" type="xsd:integer" />  
        </xsd:complexType>  
      </xsd:element>  
    </xsd:schema>  
    ```  
  
2.  Salvare il codice C# (DocSample.cs) fornito in questo esempio nella stessa cartella nella quale viene archiviato lo schema. Se si archiviano i file in un'altra cartella, sarà necessario modificare il codice e specificare il percorso di directory appropriato per lo schema di mapping.  
  
3.  Compilare il codice. Per compilare il codice al prompt dei comandi, utilizzare:  
  
    ```  
    csc /reference:Microsoft.Data.SqlXML.dll DocSample.cs  
    ```  
  
     Viene creato un file eseguibile (DocSample.exe).  
  
 Al prompt dei comandi eseguire DocSample.exe.  
  
  
