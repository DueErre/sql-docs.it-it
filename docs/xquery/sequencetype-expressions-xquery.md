---
title: Espressioni SequenceType (XQuery) | Documenti Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: xquery
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- SequenceType expressions
- instance of operator [XQuery]
- expressions [XQuery], SequenceType
- cast as operator
ms.assetid: ad3573da-d820-4d1c-81c4-a83c4640ce22
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3fa5ebb01c50823b5fe329063d9fc63023ce2478
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/09/2018
---
# <a name="sequencetype-expressions-xquery"></a>Espressioni SequenceType (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  In XQuery un valore è sempre una sequenza. Il tipo del valore viene definito tipo di sequenza. Il tipo di sequenza può essere utilizzato un **istanza** espressione XQuery. La sintassi SequenceType descritta nella specifica XQuery viene utilizzata quando è necessario fare riferimento a un tipo in un'espressione XQuery.  
  
 Il nome di tipo atomico utilizzabile anche nel **sottoposto a cast come** espressione XQuery. In [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], **istanza** e **sottoposto a cast come** espressioni XQuery in tipi sono parzialmente supportate.  
  
## <a name="instance-of-operator"></a>Operatore instance of  
 Il **istanza** operatore può essere utilizzato per determinare il tipo dinamico, o in fase di esecuzione, il valore dell'espressione specificata. Esempio:  
  
```  
  
Expression instance of SequenceType[Occurrence indicator]  
```  
  
 Si noti che il `instance of` (operatore), il `Occurrence indicator`, specifica la cardinalità, numero di elementi nella sequenza risultante. Se non viene specificato, si presuppone una cardinalità 1. In [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], il punto interrogativo (**?)**  indicatore di occorrenza è supportata. Il **?** indicatore di occorrenza indica che `Expression` può restituire zero o un elemento. Se il **?** viene specificato l'indicatore di occorrenza, `instance of` restituisce True quando il `Expression` tipo corrisponde al valore specificato `SequenceType`, indipendentemente dal fatto che `Expression` restituisce un singleton o una sequenza vuota.  
  
 Se il **?** indicatore di occorrenza non viene specificato, `sequence of` restituisce True solo quando il `Expression` digitare corrispondenze di `Type` specificato e `Expression` restituisce un singleton.  
  
 **Nota** il simbolo di segno più (**+**) e l'asterisco (**\***) indicatori di occorrenza non sono supportati in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 Nell'esempio seguente viene illustrato l'utilizzo del**istanza** operatore XQuery.  
  
### <a name="example-a"></a>Esempio A  
 Nell'esempio seguente viene creato un **xml** variabile di tipo e specifica una query su di essa. L'espressione di query specifica un operatore `instance of` per determinare se il tipo dinamico del valore restituito dal primo operando corrisponde al tipo specificato nel secondo operando.  
  
 La query seguente restituisce True, perché il valore 125 è un'istanza del tipo specificato, **xs: integer**:  
  
```  
declare @x xml  
set @x=''  
select @x.query('125 instance of xs:integer')  
go  
```  
  
 La query seguente restituisce True, poiché il valore restituito dall'espressione /a[1] nel primo operando è un elemento:  
  
```  
declare @x xml  
set @x='<a>1</a>'  
select @x.query('/a[1] instance of element()')  
go  
```  
  
 Allo stesso modo, `instance of` restituisce True nella query seguente poiché il tipo di valore dell'espressione nella prima espressione è un attributo:  
  
```  
declare @x xml  
set @x='<a attr1="x">1</a>'  
select @x.query('/a[1]/@attr1 instance of attribute()')  
go  
```  
  
 Nell'esempio seguente, l'espressione `data(/a[1]` restituisce un valore atomico tipizzato come xdt:untypedAtomic. Tramite l'operatore `instance of` viene pertanto restituito True.  
  
```  
declare @x xml  
set @x='<a>1</a>'  
select @x.query('data(/a[1]) instance of xdt:untypedAtomic')  
go  
```  
  
 Nella query seguente, l'espressione `data(/a[1]/@attrA` restituisce un valore atomico non tipizzato. Tramite l'operatore `instance of` viene pertanto restituito True.  
  
```  
declare @x xml  
set @x='<a attrA="X">1</a>'  
select @x.query('data(/a[1]/@attrA) instance of xdt:untypedAtomic')  
go  
```  
  
### <a name="example-b"></a>Esempio B  
 In questo esempio viene eseguita una query su una colonna XML tipizzata del database di esempio AdventureWorks. La raccolta di XML Schema associata alla colonna sulla quale viene eseguita la query fornisce le informazioni di tipizzazione.  
  
 Nell'espressione, **data ()** restituisce il valore tipizzato dell'attributo ProductModelID, il cui tipo è xs: String in base allo schema associato alla colonna. Tramite l'operatore `instance of` viene pertanto restituito True.  
  
```  
SELECT CatalogDescription.query('  
   declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
   data(/PD:ProductDescription[1]/@ProductModelID) instance of xs:string  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 Per altre informazioni, vedere [Confrontare dati XML tipizzati con dati XML non tipizzati](../relational-databases/xml/compare-typed-xml-to-untyped-xml.md).  
  
 La seguente query usetheBoolean `instance of` espressione per determinare se l'attributo LocationID è di tipo xs: integer:  
  
```  
SELECT Instructions.query('  
   declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   /AWMI:root[1]/AWMI:Location[1]/@LocationID instance of attribute(LocationID,xs:integer)  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 La query seguente viene specificata sulla colonna XML tipizzata CatalogDescription. Le informazioni di tipizzazione sono fornite dalla raccolta di XML Schema associata alla colonna.  
  
 Nella query viene utilizzato il test `element(ElementName, ElementType?)` nell'espressione `instance of` per verificare che tramite `/PD:ProductDescription[1]` venga restituito un nodo di elemento con un nome e un tipo specifici.  
  
```  
SELECT CatalogDescription.query('  
     declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     /PD:ProductDescription[1] instance of element(PD:ProductDescription, PD:ProductDescription?)  
    ') as Result  
FROM  Production.ProductModel  
where ProductModelID=19  
```  
  
 La query restituisce True.  
  
### <a name="example-c"></a>Esempio C  
 Quando si utilizzano i tipi unione, l'espressione `instance of` in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] presenta una limitazione. In particolare, quando un elemento o un attributo è di un tipo unione, è possibile che `instance of` non riesca a determinare il tipo esatto. Di conseguenza, una query restituirà False, a meno che i tipi atomici utilizzati in SequenceType siano l'elemento padre di livello più alto del tipo effettivo dell'espressione nella gerarchia simpleType, ovvero che i tipi atomici specificati in SequenceType siano figli diretti di anySimpleType. Per informazioni sulla gerarchia dei tipi, vedere [le regole di cast di tipo in XQuery](../xquery/type-casting-rules-in-xquery.md).  
  
 La prossima query esegue le operazioni seguenti:  
  
-   Crea a una raccolta di XML Schema contenente la definizione di un tipo unione, ad esempio un tipo integer o stringa.  
  
-   Dichiarare una classe tipizzata **xml** variabile tramite la raccolta di XML schema.  
  
-   Assegna un'istanza XML di esempio alla variabile.  
  
-   Esegue una query sulla variabile per illustrare il funzionamento di `instance of` quando è applicato a un tipo unione.  
  
 Query:  
  
```  
CREATE XML SCHEMA COLLECTION MyTestSchema AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema" targetNamespace="http://ns" xmlns:ns="http://ns">  
<simpleType name="MyUnionType">  
<union memberTypes="integer string"/>  
</simpleType>  
<element name="TestElement" type="ns:MyUnionType"/>  
</schema>'  
Go  
```  
  
 La query seguente restituisce False, perché il SequenceType specificato nell'espressione `instance of` non è l'elemento padre di livello più alto del tipo effettivo dell'espressione specificata. Il valore dell'elemento <`TestElement`> è infatti un tipo integer. L'elemento padre di livello più alto è xs:decimal, ma non è specificato come secondo operando dell'operatore `instance of`.  
  
```  
SET QUOTED_IDENTIFIER ON  
DECLARE @var XML(MyTestSchema)  
  
SET @var = '<TestElement xmlns="http://ns">123</TestElement>'  
  
SELECT @var.query('declare namespace ns="http://ns"   
   data(/ns:TestElement[1]) instance of xs:integer')  
go  
```  
  
 Poiché l'elemento padre di livello più alto di xs:integer è xs:decimal, se viene modificata specificando xs:decimal come SequenceType la query restituirà True.  
  
```  
SET QUOTED_IDENTIFIER ON  
DECLARE @var XML(MyTestSchema)  
SET @var = '<TestElement xmlns="http://ns">123</TestElement>'  
SELECT @var.query('declare namespace ns="http://ns"     
   data(/ns:TestElement[1]) instance of xs:decimal')  
go  
```  
  
### <a name="example-d"></a>Esempio D  
 In questo esempio, prima di tutto creare una raccolta di XML schema e utilizzarla per tipizzare una **xml** variabile. L'oggetto tipizzato **xml** variabile viene quindi eseguita una query per illustrare il `instance of` funzionalità.  
  
 La raccolta di XML Schema seguente definisce il tipo semplice myType e un elemento, <`root`> di tipo myType:  
  
```  
drop xml schema collection SC  
go  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema" targetNamespace="myNS" xmlns:ns="myNS"  
xmlns:s="http://schemas.microsoft.com/sqlserver/2004/sqltypes">  
      <import namespace="http://schemas.microsoft.com/sqlserver/2004/sqltypes"/>  
      <simpleType name="myType">  
           <restriction base="s:varchar">  
                  <maxLength value="20"/>  
            </restriction>  
      </simpleType>  
      <element name="root" type="ns:myType"/>  
</schema>'  
Go  
```  
  
 Creare un oggetto tipizzato **xml** variabile ed eseguire una query:  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root xmlns="myNS">My data</root>'  
SELECT @var.query('declare namespace sqltypes = "http://schemas.microsoft.com/sqlserver/2004/sqltypes";  
declare namespace ns="myNS";   
   data(/ns:root[1]) instance of ns:myType')  
go  
```  
  
 Poiché il tipo myType deriva per restrizione da un tipo varchar definito nello schema sqltypes, anche `instance of` restituirà True.  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root xmlns="myNS">My data</root>'  
SELECT @var.query('declare namespace sqltypes = "http://schemas.microsoft.com/sqlserver/2004/sqltypes";  
declare namespace ns="myNS";   
data(/ns:root[1]) instance of sqltypes:varchar?')  
go  
```  
  
### <a name="example-e"></a>Esempio E  
 Nell'esempio seguente, l'espressione recupera uno dei valori dell'attributo IDREFS e utilizza `instance of` per determinare se il valore sia di tipo IDREF. Nell'esempio vengono eseguite le operazioni seguenti:  
  
-   Crea una raccolta XML schema in cui il <`Customer`> elemento ha un **OrderList** attributo di tipo IDREFS e <`Order`> elemento ha un **OrderID** attributo di tipo ID.  
  
-   Crea un oggetto tipizzato **xml** variabile e assegna un codice XML di esempio istanza.  
  
-   Specifica una query sulla variabile. L'espressione della query recupera il valore di ID del primo ordine dall'attributo OrderList di tipo IDREFS del primo elemento <`Customer`>. Il valore recuperato è di tipo IDREF. L'operatore `instance of` pertanto restituisce True.  
  
```  
create xml schema collection SC as  
'<schema xmlns="http://www.w3.org/2001/XMLSchema" xmlns:Customers="Customers" targetNamespace="Customers">  
            <element name="Customers" type="Customers:CustomersType"/>  
            <complexType name="CustomersType">  
                        <sequence>  
                            <element name="Customer" type="Customers:CustomerType" minOccurs="0" maxOccurs="unbounded" />  
                        </sequence>  
            </complexType>  
             <complexType name="OrderType">  
                <sequence minOccurs="0" maxOccurs="unbounded">  
                            <choice>  
                                <element name="OrderValue" type="integer" minOccurs="0" maxOccurs="unbounded"/>  
                            </choice>  
                </sequence>                                             
                <attribute name="OrderID" type="ID" />  
            </complexType>  
  
            <complexType name="CustomerType">  
                <sequence minOccurs="0" maxOccurs="unbounded">  
                            <choice>  
                                <element name="spouse" type="string" minOccurs="0" maxOccurs="unbounded"/>  
                                <element name="Order" type="Customers:OrderType" minOccurs="0" maxOccurs="unbounded"/>  
                            </choice>  
                </sequence>                                             
                <attribute name="CustomerID" type="string" />  
                <attribute name="OrderList" type="IDREFS" />  
            </complexType>  
 </schema>'  
go  
declare @x xml(SC)  
set @x='<CustOrders:Customers xmlns:CustOrders="Customers">  
                <Customer CustomerID="C1" OrderList="OrderA OrderB"  >  
                              <spouse>Jenny</spouse>  
                                <Order OrderID="OrderA"><OrderValue>11</OrderValue></Order>  
                                <Order OrderID="OrderB"><OrderValue>22</OrderValue></Order>  
  
                </Customer>  
                <Customer CustomerID="C2" OrderList="OrderC OrderD" >  
                                <spouse>John</spouse>  
                                <Order OrderID="OrderC"><OrderValue>33</OrderValue></Order>  
                                <Order OrderID="OrderD"><OrderValue>44</OrderValue></Order>  
  
                        </Customer>  
                <Customer CustomerID="C3"  OrderList="OrderE OrderF" >  
                                <spouse>Jane</spouse>  
                                <Order OrderID="OrderE"><OrderValue>55</OrderValue></Order>  
                                <Order OrderID="OrderF"><OrderValue>55</OrderValue></Order>  
                </Customer>  
                <Customer CustomerID="C4"  OrderList="OrderG"  >  
                                <spouse>Tim</spouse>  
                                <Order OrderID="OrderG"><OrderValue>66</OrderValue></Order>  
                        </Customer>  
                <Customer CustomerID="C5"  >  
                </Customer>  
                <Customer CustomerID="C6" >  
                </Customer>  
                <Customer CustomerID="C7"  >  
                </Customer>  
</CustOrders:Customers>'  
  
select @x.query(' declare namespace CustOrders="Customers";   
 data(CustOrders:Customers/Customer[1]/@OrderList)[1] instance of xs:IDREF ? ') as XML_result  
```  
  
### <a name="implementation-limitations"></a>Limitazioni di implementazione  
 Limitazioni:  
  
-   Il **schema-element()** e **schema-attribute()** tipi di sequenza non sono supportati per il confronto di `instance of` operatore.  
  
-   Le sequenze complete, ad esempio `(1,2) instance of xs:integer*`, non sono supportate.  
  
-   Quando si utilizza una forma del **element()** tipo che specifica un nome di tipo, ad esempio di sequenza `element(ElementName, TypeName)`, il tipo deve essere qualificato con un punto interrogativo (?). Ad esempio, `element(Title, xs:string?)` indica che l'elemento potrebbe essere null. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]non supporta il rilevamento di runtime del **xsi: nil** proprietà utilizzando `instance of`.  
  
-   Se il valore in `Expression` viene da un elemento o un attributo tipizzato come unione, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] può identificare solo il tipo primitivo dal quale deriva il tipo di valore, non il tipo derivato. Ad esempio, se si specifica un tipo statico (xs:integer | xs:string) per <`e1`>, la query seguente restituirà False.  
  
    ```  
    data(<e1>123</e1>) instance of xs:integer  
    ```  
  
     `data(<e1>123</e1>) instance of xs:decimal` tuttavia restituirà True.  
  
-   Per il **//Processing-Instruction ()** e **document-node()** tipi di sequenza sono consentiti solo forme senza argomenti. Ad esempio, `processing-instruction()` è consentito, ma `processing-instruction('abc')` non è consentito.  
  
## <a name="cast-as-operator"></a>Operatore cast as  
 Il **sottoposto a cast come** espressione può essere utilizzata per convertire un valore di un tipo di dati specifico. Esempio:  
  
```  
  
Expression cast as  AtomicType?  
```  
  
 In [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], dopo `AtomicType` è necessario il punto interrogativo (?). Ad esempio, come illustrato nella query seguente, `"2" cast as xs:integer?` converte il valore stringa in un intero:  
  
```  
declare @x xml  
set @x=''  
select @x.query('"2" cast as xs:integer?')  
```  
  
 Nella query seguente, **data ()** restituisce il valore tipizzato dell'attributo ProductModelID, un tipo stringa. Il `cast as`operatore converte il valore in xs: integer.  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS PD)  
SELECT CatalogDescription.query('  
   data(/PD:ProductDescription[1]/@ProductModelID) cast as xs:integer?  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 L'utilizzo esplicito di **data ()** non è necessario in questa query. L'espressione `cast as` esegue l'atomizzazione implicita sull'espressione di input.  
  
### <a name="constructor-functions"></a>Funzioni costruttore  
 È possibile utilizzare le funzioni costruttore del tipo atomico. Ad esempio, anziché utilizzare il `cast as` operatore `"2" cast as xs:integer?`, è possibile utilizzare il **xs:integer()** funzione del costruttore, come nell'esempio seguente:  
  
```  
declare @x xml  
set @x=''  
select @x.query('xs:integer("2")')  
```  
  
 L'esempio seguente restituisce un valore xs:date uguale a 2000-01-01Z.  
  
```  
declare @x xml  
set @x=''  
select @x.query('xs:date("2000-01-01Z")')  
```  
  
 È inoltre possibile utilizzare i costruttori per i tipi atomici definiti dall'utente. Ad esempio, se la raccolta di XML schema è associato il tipo di dati XML definisce un tipo semplice, un **myType()** costruttore può essere utilizzato per restituire un valore di quel tipo.  
  
#### <a name="implementation-limitations"></a>Limitazioni di implementazione  
  
-   Le espressioni XQuery **typeswitch**, **eseguire il casting**, e **trattare** non sono supportati.  
  
-   **sottoposto a cast come** richiede un punto interrogativo (?) Dopo il tipo atomico.  
  
-   **xs: QName** non è supportato come un cast del tipo. Utilizzare **expanded-QName-** invece.  
  
-   **xs: date**, **xs: Time**, e **xs: DateTime** richiedono un fuso orario, indicata da una Z.  
  
     La query seguente ha esito negativo, perché il fuso orario non è specificato.  
  
    ```  
    DECLARE @var XML  
    SET @var = ''  
    SELECT @var.query(' <a>{xs:date("2002-05-25")}</a>')  
    go  
    ```  
  
     Aggiungendo l'indicatore di fuso orario Z al valore, la query riesce.  
  
    ```  
    DECLARE @var XML  
    SET @var = ''  
    SELECT @var.query(' <a>{xs:date("2002-05-25Z")}</a>')  
    go  
    ```  
  
     Risultato:  
  
    ```  
    <a>2002-05-25Z</a>  
    ```  
  
## <a name="see-also"></a>Vedere anche  
 [Espressioni XQuery](../xquery/xquery-expressions.md)   
 [Tipo di sistema &#40; XQuery &#41;](../xquery/type-system-xquery.md)  
  
  
