---
title: La gestione di problemi di concorrenza di Database negli updategram (SQLXML 4.0) | Documenti Microsoft
ms.custom: 
ms.date: 03/16/2017
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
- <before> block
- low concurrency protection
- database concurrency [SQLXML]
- timestamp column [SQLXML]
- updategrams [SQLXML], database concurrency
- high concurrency protection [SQLXML]
- optimistic concurrency control
- concurrency [SQLXML]
- intermediate concurrency protection [SQLXML]
ms.assetid: d4b908d1-b25b-4ad9-8478-9cd882e8c44e
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1e19d8397d59b4c85d60593c63faa5bc6f0f2ea4
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2018
---
# <a name="handling-database-concurrency-issues-in-updategrams-sqlxml-40"></a>Gestione dei problemi di concorrenza di database negli updategram (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Analogamente ad altri meccanismi di aggiornamento del database, gli updategram devono gestire aggiornamenti simultanei ai dati in un ambiente multiutente. Gli updategram utilizzano il controllo della concorrenza ottimistica, che esegue il confronto dei dati di campo come snapshot per garantire che i dati da aggiornare non siano già stati modificati da un'altra applicazione utente dal momento in cui sono stati letti dal database. Gli updategram includono questi valori di snapshot nel  **\<prima >** blocco degli Updategram. Prima di aggiornare il database, l'updategram controlla i valori specificati nel  **\<prima >** blocco in base ai valori presenti nel database per verificare che l'aggiornamento sia valido.  
  
 Il controllo della concorrenza ottimistica offre tre livelli di protezione in un updategram: basso (nessuno), intermedio ed elevato. È possibile stabilire il livello di protezione necessario specificando l'updategram di conseguenza.  
  
## <a name="lowest-level-of-protection"></a>Livello di protezione più basso  
 Questo livello corrisponde a un aggiornamento nascosto, in cui l'aggiornamento viene elaborato senza riferimento ad altri aggiornamenti eseguiti dall'ultima lettura del database. In tal caso, specificare solo le colonne chiave primaria nel  **\<prima >** blocco per identificare il record e specificare le informazioni aggiornate nel  **\<dopo >** blocco.  
  
 Il nuovo numero di telefono del contatto nell'updategram seguente, ad esempio, è corretto, indipendentemente dal numero di telefono precedente. Si noti come  **\<prima >** blocco specifica solo la colonna chiave primaria (ContactID).  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
<updg:before>  
   <Person.Contact ContactID="1" />  
</updg:before>  
<updg:after>  
   <Person.Contact ContactID="1" Phone="111-111-1111" />  
</updg:after>  
</updg:sync>  
</ROOT>  
```  
  
## <a name="intermediate-level-of-protection"></a>Livello di protezione intermedio  
 In questo livello di protezione l'updategram confronta i valori correnti dei dati aggiornati con i valori nelle colonne del database per verificare che i valori non siano stati modificati da altre transazioni dalla lettura del record da parte della transazione.  
  
 È possibile ottenere questo livello di protezione specificando le colonne chiave primaria e le colonne in cui si siano aggiornando il  **\<prima >** blocco.  
  
 Questo updategram, ad esempio, modifica il valore nella colonna Phone della tabella Person.Contact per il contatto con ContactID 1. Il  **\<prima >** blocco specifica il **Phone** attributo per garantire che il valore dell'attributo corrisponde al valore nella colonna corrispondente nel database prima di applicare il valore aggiornato .  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
<updg:before>  
   <Person.Contact ContactID="1" Phone="398-555-0132" />  
</updg:before>  
<updg:after>  
   <Person.Contact ContactID="1" Phone="111-111-1111" />  
</updg:after>  
</updg:sync>  
</ROOT>  
```  
  
## <a name="high-level-of-protection"></a>Livello di protezione elevato  
 Un livello di protezione elevato garantisce che il record resti inalterato dall'ultima lettura da parte dell'applicazione, ovvero dal momento in cui l'applicazione ha letto il record, che non è stato modificato da alcuna transazione.  
  
 Per ottenere questo livello di protezione elevato contro aggiornamenti simultanei, sono disponibili due metodi:  
  
-   Specificare le altre colonne nella tabella di  **\<prima >** blocco.  
  
     Se si specificano colonne aggiuntive nel  **\<prima >** blocco, l'updategram confronta i valori specificati per queste colonne con i valori contenuti nel database prima di applicare l'aggiornamento. Se una o più delle colonne dei record è stata modificata dal momento in cui la transazione ha letto il record, l'updategram non esegue l'aggiornamento.  
  
     Ad esempio, l'updategram seguente aggiorna il nome, ma specifica colonne aggiuntive (StartTime, EndTime) nei  **\<prima >** blocco, per richiedere un livello più elevato di protezione contro simultanee aggiornamenti.  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
    <updg:sync >  
    <updg:before>  
       <HumanResources.Shift ShiftID="1"   
                 Name="Day"   
                 StartTime="1900-01-01 07:00:00.000"   
                 EndTime="1900-01-01 15:00:00.000" />  
    </updg:before>  
    <updg:after>  
       <HumanResources.Shift Name="Morning" />  
    </updg:after>  
    </updg:sync>  
    </ROOT>  
    ```  
  
     In questo esempio specifica il livello di protezione più elevato specificando tutti i valori di colonna per il record di  **\<prima >** blocco.  
  
-   Specificare la colonna timestamp, se disponibile, nel  **\<prima >** blocco.  
  
     Anziché specificare tutte le colonne dei record nel  **\<prima**> blocco, è possibile solo specificare la colonna timestamp (se la tabella contiene una) insieme alle colonne chiave primarie nel  **\<prima >** blocco. Il database aggiorna la colonna timestamp a un valore univoco dopo ogni aggiornamento del record. In questo caso, l'updategram confronta il valore del timestamp con il valore corrispondente nel database. Il valore del timestamp archiviato nel database è un valore binary. Di conseguenza, la colonna timestamp deve essere specificata nello schema come **dt:type="bin.hex"**, **dt:type="bin.base64"**, o **SQL: DataType = "timestamp"**. (È possibile specificare il **xml** tipo di dati o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipo di dati.)  
  
#### <a name="to-test-the-updategram"></a>Per testare l'updategram  
  
1.  Creare la tabella nel **tempdb** database:  
  
    ```  
    USE tempdb  
    CREATE TABLE Customer (  
                 CustomerID  varchar(5),  
                 ContactName varchar(20),  
                 LastUpdated timestamp)  
    ```  
  
2.  Aggiungere il record di esempio seguente:  
  
    ```  
    INSERT INTO Customer (CustomerID, ContactName) VALUES   
                         ('C1', 'Andrew Fuller')  
    ```  
  
3.  Copiare lo schema XSD seguente e incollarlo in Blocco note. Salvarlo come file ConcurrencySampleSchema.xml:  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
      <xsd:element name="Customer" sql:relation="Customer" >  
       <xsd:complexType>  
            <xsd:attribute name="CustomerID"    
                           sql:field="CustomerID"   
                           type="xsd:string" />   
  
            <xsd:attribute name="ContactName"    
                           sql:field="ContactName"   
                           type="xsd:string" />  
  
            <xsd:attribute name="LastUpdated"   
                           sql:field="LastUpdated"   
                           type="xsd:hexBinary"   
                 sql:datatype="timestamp" />  
  
        </xsd:complexType>  
      </xsd:element>  
    </xsd:schema>  
    ```  
  
4.  Copiare il codice dell'updategram seguente in Blocco note e salvarlo come ConcurrencySampleTemplate.xml nella stessa directory in cui è stato salvato lo schema creato nel passaggio precedente. Si noti che il valore del timestamp indicato di seguito per LastUpdated differirà nella tabella Customer di esempio. Copiare pertanto il valore effettivo di LastUpdated dalla tabella e incollarlo nell'updategram.  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
    <updg:sync mapping-schema="SampleSchema.xml" >  
    <updg:before>  
       <Customer CustomerID="C1"   
                 LastUpdated = "0x00000000000007D1" />  
    </updg:before>  
    <updg:after>  
       <Customer ContactName="Robert King" />  
    </updg:after>  
    </updg:sync>  
    </ROOT>  
    ```  
  
5.  Creare e utilizzare lo script di test SQLXML 4.0 (Sqlxml4test.vbs) per eseguire il modello.  
  
     Per ulteriori informazioni, vedere [utilizzando ADO per eseguire query di SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Di seguito viene indicato lo schema XDR equivalente:  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"  
        xmlns:dt="urn:schemas-microsoft-com:datatypes"  
        xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
<ElementType name="Customer" sql:relation="Customer" >  
    <AttributeType name="CustomerID" />  
    <AttributeType name="ContactName" />  
    <AttributeType name="LastUpdated"  dt:type="bin.hex"   
                                       sql:datatype="timestamp" />  
    <attribute type="CustomerID" />  
    <attribute type="ContactName" />  
    <attribute type="LastUpdated" />  
</ElementType>  
</Schema>  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Considerazioni sulla sicurezza di updategram &#40; SQLXML 4.0 &#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
