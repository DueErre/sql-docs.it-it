---
title: 'Esclusione di elementi dello Schema dal documento XML utilizzando sql: il mapping | Documenti Microsoft'
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- element does not map [SQLXML]
- annotated XSD schemas, excluding schema elements
- mapped annotation
- table mapping [SQLXML], excluding schema elements
- sql:mapped
- excluding schema elements
- element mapping [SQLXML], excluding schema elements
- column mapping [SQLXML]
- XSD schemas [SQLXML], excluding schema elements
- attribute mapping [SQLXML], excluding schema elements
- table/view mapping [SQLXML], excluding schema elements
ms.assetid: 7d2649dd-0038-4a2c-b16d-f80f7c306966
caps.latest.revision: "26"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 660fe866db09675916d90cdf8130b2b99980b2ec
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/17/2017
---
# <a name="excluding-schema-elements-from-the-xml-document-using-sqlmapped"></a>Esclusione di elementi dello Schema dal documento XML utilizzando sql: il mapping
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]Ogni elemento e attributo nello schema XSD viene mappato a una tabella o vista di database e una colonna a causa del mapping predefinito. Se si desidera creare un elemento nello schema XSD che non è mappato ad alcuna tabella di database (vista) o una colonna e che non viene visualizzata nel codice XML, è possibile specificare il **sql: il mapping** annotazione.  
  
 Il **sql: il mapping** annotazione è particolarmente utile se lo schema non può essere modificato o se lo schema viene utilizzato per convalidare XML da altre origini pur contenendo dati non archiviati nel database. Il **sql: il mapping** annotazione è diverso da **sql: costante è** in quanto gli attributi e gli elementi non mappati non vengono visualizzati nel documento XML.  
  
 Il **sql: il mapping** annotazione accetta un valore booleano (0 = false, 1 = true). I valori possibili sono 0, 1, true e false.  
  
## <a name="examples"></a>Esempi  
 Per creare esempi reali utilizzando gli esempi seguenti, è necessario soddisfare alcuni requisiti. Per ulteriori informazioni, vedere [requisiti per esecuzione esempi SQLXML](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-specifying-the-sqlmapped-annotation"></a>A. Specifica dell'annotazione sql:mapped  
 Si supponga di disporre di uno schema XSD di un'altra origine. Questo schema XSD è costituito un  **\<Person. Contact >** elemento con **ContactID**, **FirstName**, **LastName**, e **HomeAddress** attributi.  
  
 Per eseguire il mapping di questo schema XSD alla tabella Person. Contact nel database AdventureWorks, **sql: mappato** viene specificata per il **HomeAddress** attributo perché la tabella Employees non archivia la home page indirizzi dei dipendenti. Di conseguenza, questo attributo non viene mappato al database e non viene restituito nel documento XML risultante quando viene specificata una query XPath sullo schema di mapping.  
  
 Per il resto dello schema viene eseguito il mapping predefinito. Il  **\<Person. Contact >** elemento viene mappato alla tabella Person. Contact e tutti gli attributi vengono mappati alle colonne con lo stesso nome nella tabella Person. Contact.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Person.Contact">  
    <xsd:complexType>  
      <xsd:attribute name="ContactID"   type="xsd:string"/>  
      <xsd:attribute name="FirstName"    type="xsd:string" />  
      <xsd:attribute name="LastName"     type="xsd:string" />  
      <xsd:attribute name="HomeAddress" type="xsd:string"   
                     sql:mapped="false" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Per testare una query Xpath di esempio sullo schema  
  
1.  Copiare il codice dello schema precedente e incollarlo in un file di testo. Salvare il file con il nome sql-mapped.xml.  
  
2.  Copiare il modello seguente e incollarlo in un file di testo. Salvare il file con il nome sql-mappedT.xml nella stessa directory in cui è stato salvato il file sql-mapped.xml.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="sql-mapped.xml">  
            /Person.Contact[@ContactID < 10]  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     Il percorso di directory specificato per lo schema di mapping (MySchema.xml) è relativo alla directory in cui è salvato il modello. È possibile specificare anche un percorso assoluto, ad esempio:  
  
    ```  
    mapping-schema="C:\MyDir\sql-mapped.xml"  
    ```  
  
3.  Creare e utilizzare lo script di test SQLXML 4.0 (Sqlxml4test.vbs) per eseguire il modello.  
  
     Per ulteriori informazioni, vedere [utilizzando ADO per eseguire query SQLXML](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Set di risultati:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Person.Contact ContactID="1" FirstName="Gustavo" LastName="Achong" />   
  <Person.Contact ContactID="2" FirstName="Catherine" LastName="Abel" />   
  <Person.Contact ContactID="3" FirstName="Kim" LastName="Abercrombie" />   
  <Person.Contact ContactID="4" FirstName="Humberto" LastName="Acevedo" />   
  <Person.Contact ContactID="5" FirstName="Pilar" LastName="Ackerman" />   
  <Person.Contact ContactID="6" FirstName="Frances" LastName="Adams" />   
  <Person.Contact ContactID="7" FirstName="Margaret" LastName="Smith" />   
  <Person.Contact ContactID="8" FirstName="Carla" LastName="Adams" />   
  <Person.Contact ContactID="9" FirstName="Jay" LastName="Adams" />   
</ROOT>  
```  
  
 Si noti che il ContactID, FirstName e LastName sono presenti, ma in quanto lo schema di mapping specifica il valore 0 per il **sql: il mapping** attributo.  
  
## <a name="see-also"></a>Vedere anche  
 [Mapping predefinito di attributi ed elementi XSD a tabelle e colonne &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)  
  
  