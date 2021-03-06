---
title: Annotazione di dataset tipizzati
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-ado
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
ms.assetid: f82aaa62-321e-4c8a-b51b-9d1114700170
caps.latest.revision: "6"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: dotnet
ms.openlocfilehash: cc09f3f9b43b70b7f9b302d7a9d75428b5a0e6c7
ms.sourcegitcommit: ed26cfef4e18f6d93ab822d8c29f902cff3519d1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/17/2018
---
# <a name="annotating-typed-datasets"></a>Annotazione di dataset tipizzati
Le annotazioni consentono di modificare i nomi degli elementi nel <xref:System.Data.DataSet> tipizzato senza modificare lo schema sottostante. Modifica i nomi degli elementi dello schema sottostante causerebbe l'oggetto tipizzato **DataSet** fare riferimento a oggetti che non esiste nell'origine dati, nonché perderebbe un riferimento per gli oggetti presenti nell'origine dati.  
  
 Utilizzo delle annotazioni, è possibile personalizzare i nomi degli oggetti in tipizzato **DataSet** con nomi più significativi, rendendo più leggibili codice e tipizzato **DataSet** più semplice per i client da utilizzare, lasciando schema sottostante intatto. Ad esempio, il seguente elemento di schema per il **clienti** tabella del **Northwind** database comporta la un **DataRow** il nome dell'oggetto  **CustomersRow** e <xref:System.Data.DataRowCollection> denominato **clienti**.  
  
```xml  
<xs:element name="Customers">  
  <xs:complexType>  
    <xs:sequence>  
      <xs:element name="CustomerID" type="xs:string" minOccurs="0" />  
    </xs:sequence>  
  </xs:complexType>  
</xs:element>  
```  
  
 A **DataRowCollection** nome di **clienti** è significativo nel codice client, ma un **DataRow** nome di **CustomersRow** è fuorviante perché si tratta di un singolo oggetto. In comune scenari, l'oggetto potrebbe essere indicato anche senza il **riga** identificatore e invece potrebbe essere semplicemente considerato come un **cliente** oggetto. La soluzione consiste nell'annotare lo schema e identificare nuovi nomi per il **DataRow** e **DataRowCollection** oggetti. Di seguito viene riportata una versione annotata dello schema precedente.  
  
```xml  
<xs:element name="Customers" codegen:typedName="Customer" codegen:typedPlural="Customers">  
  <xs:complexType>  
    <xs:sequence>  
      <xs:element name="CustomerID" type="xs:string" minOccurs="0" />  
    </xs:sequence>  
  </xs:complexType>  
</xs:element>  
```  
  
 Specifica un **typedName** valore **cliente** comporterà un **DataRow** il nome dell'oggetto **cliente**. Specifica un **typedPlural** valore **clienti** mantiene il **DataRowCollection** nome di **clienti**.  
  
 Nella seguente tabella sono indicate le annotazioni disponibili.  
  
|Annotazione|Descrizione|  
|----------------|-----------------|  
|**typedName**|Nome dell'oggetto.|  
|**typedPlural**|Nome della raccolta di oggetti.|  
|**typedParent**|Nome dell'oggetto quando si fa riferimento a tale oggetto in una relazione padre.|  
|**typedChildren**|Nome del metodo per la restituzione di oggetti da una relazione figlio.|  
|**nullValue**|Il valore se il valore sottostante è **DBNull**. Vedere la tabella seguente per **nullValue** annotazioni. Il valore predefinito è **throw**.|  
  
 Nella tabella seguente vengono illustrati i valori che possono essere specificati per il **nullValue** annotazione.  
  
|Valore nullValue|Descrizione|  
|---------------------|-----------------|  
|*Valore di sostituzione*|Specifica il valore da restituire. È necessario che il valore restituito corrisponda al tipo dell'elemento. Usare ad esempio `nullValue="0"` per restituire 0 per i campi integer null.|  
|**_throw**|Generazione di un'eccezione. Questa è l'impostazione predefinita.|  
|**_null**|Consente di restituire un riferimento null o di generare un'eccezione se viene rilevato un tipo primitivo.|  
|**_empty**|Per le stringhe, restituire **Empty**, in caso contrario, restituire un oggetto creato da un costruttore vuoto. Se viene rilevato un tipo primitivo, consente di generare un'eccezione.|  
  
 Nella tabella seguente mostra i valori predefiniti per gli oggetti in una classe tipizzata **DataSet** e le annotazioni disponibili.  
  
|Oggetto/Metodo/Evento|Default|Annotazione|  
|---------------------------|-------------|----------------|  
|**DataTable**|TableNameDataTable|typedPlural|  
|**DataTable** metodi|NewTableNameRow<br /><br /> AddTableNameRow<br /><br /> DeleteTableNameRow|typedName|  
|**DataRowCollection**|TableName|typedPlural|  
|**DataRow**|TableNameRow|typedName|  
|**DataColumn**|DataTable.ColumnNameColumn<br /><br /> DataRow.ColumnName|typedName|  
|**Property**|PropertyName|typedName|  
|**Figlio** della funzione di accesso|GetChildTableNameRows|typedChildren|  
|**Padre** della funzione di accesso|TableNameRow|typedParent|  
|**Set di dati** eventi|TableNameRowChangeEvent<br /><br /> TableNameRowChangeEventHandler|typedName|  
  
 Utilizzare tipizzati **DataSet** annotazioni, è necessario includere il seguente **xmlns** riferimento nello schema XML Schema definition language (XSD). (Per creare un file xsd dalle tabelle di database, vedere <xref:System.Data.DataSet.WriteXmlSchema%2A> o [uso di dataset in Visual Studio](http://msdn.microsoft.com/library/8bw9ksd6.aspx)).  
  
```  
xmlns:codegen="urn:schemas-microsoft-com:xml-msprop"  
```  
  
 Di seguito è riportato un esempio di schema con annotazioni che espone il **clienti** tabella il **Northwind** database con una relazione con il **ordini** tabella inclusa.  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<xs:schema id="CustomerDataSet"   
      xmlns:codegen="urn:schemas-microsoft-com:xml-msprop"  
      xmlns=""   
      xmlns:xs="http://www.w3.org/2001/XMLSchema"   
      xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
  <xs:element name="CustomerDataSet" msdata:IsDataSet="true">  
    <xs:complexType>  
      <xs:choice maxOccurs="unbounded">  
        <xs:element name="Customers" codegen:typedName="Customer" codegen:typedPlural="Customers">  
          <xs:complexType>  
            <xs:sequence>  
              <xs:element name="CustomerID"  
codegen:typedName="CustomerID" type="xs:string" minOccurs="0" />  
              <xs:element name="CompanyName"  
codegen:typedName="CompanyName" type="xs:string" minOccurs="0" />  
              <xs:element name="Phone" codegen:typedName="Phone" codegen:nullValue="" type="xs:string" minOccurs="0" />  
            </xs:sequence>  
          </xs:complexType>  
        </xs:element>  
        <xs:element name="Orders" codegen:typedName="Order" codegen:typedPlural="Orders">  
          <xs:complexType>  
            <xs:sequence>  
              <xs:element name="OrderID" codegen:typedName="OrderID"  
type="xs:int" minOccurs="0" />  
              <xs:element name="CustomerID"  
codegen:typedName="CustomerID"                  codegen:nullValue="" type="xs:string" minOccurs="0" />  
              <xs:element name="EmployeeID"  
codegen:typedName="EmployeeID" codegen:nullValue="0"   
type="xs:int" minOccurs="0" />  
              <xs:element name="OrderAdapter"  
codegen:typedName="OrderAdapter" codegen:nullValue="1980-01-01T00:00:00"   
type="xs:dateTime" minOccurs="0" />  
            </xs:sequence>  
          </xs:complexType>  
        </xs:element>  
      </xs:choice>  
    </xs:complexType>  
    <xs:unique name="Constraint1">  
      <xs:selector xpath=".//Customers" />  
      <xs:field xpath="CustomerID" />  
    </xs:unique>  
    <xs:keyref name="CustOrders" refer="Constraint1"  
codegen:typedParent="Customer" codegen:typedChildren="GetOrders">  
      <xs:selector xpath=".//Orders" />  
      <xs:field xpath="CustomerID" />  
    </xs:keyref>  
  </xs:element>  
</xs:schema>  
```  
  
 L'esempio di codice seguente viene utilizzato un oggetto fortemente tipizzato **DataSet** creato dallo schema di esempio. Viene utilizzato uno <xref:System.Data.SqlClient.SqlDataAdapter> per popolare il **clienti** tabella e un altro <xref:System.Data.SqlClient.SqlDataAdapter> per popolare il **ordini** tabella. L'oggetto fortemente tipizzato **DataSet** definisce il **DataRelations**.  
  
```vb  
' Assumes a valid SqlConnection object named connection.  
Dim customerAdapter As SqlDataAdapter = New SqlDataAdapter( _  
    "SELECT CustomerID, CompanyName, Phone FROM Customers", &  
    connection)  
Dim orderAdapter As SqlDataAdapter = New SqlDataAdapter( _  
    "SELECT OrderID, CustomerID, EmployeeID, OrderAdapter FROM Orders", &  
    connection)  
  
' Populate a strongly typed DataSet.  
connection.Open()  
Dim customers As CustomerDataSet = New CustomerDataSet()  
customerAdapter.Fill(customers, "Customers")  
orderAdapter.Fill(customers, "Orders")  
connection.Close()  
  
' Add a strongly typed event.  
AddHandler customers.Customers.CustomerChanged, &  
    New CustomerDataSet.CustomerChangeEventHandler( _  
    AddressOf OnCustomerChanged)  
  
' Add a strongly typed DataRow.  
Dim newCustomer As CustomerDataSet.Customer = _  
    customers.Customers.NewCustomeromer()  
newCustomer.CustomerID = "NEW01"  
newCustomer.CompanyName = "My New Company"  
customers.Customers.AddCustomer(newCustomer)  
  
' Navigate the child relation.  
Dim customer As CustomerDataSet.Customer  
Dim order As CustomerDataSet.Order  
  
For Each customer In customers.Customers  
  Console.WriteLine(customer.CustomerID)  
  For Each order In customer.GetOrders()  
    Console.WriteLine(vbTab & order.OrderID)  
  Next  
Next  
  
Private Shared Sub OnCustomerChanged( _  
    sender As Object, e As CustomerDataSet.CustomerChangeEvent)  
  
End Sub  
```  
  
```csharp  
// Assumes a valid SqlConnection object named connection.  
SqlDataAdapter customerAdapter = new SqlDataAdapter(  
    "SELECT CustomerID, CompanyName, Phone FROM Customers",  
    connection);  
SqlDataAdapter orderAdapter = new SqlDataAdapter(  
    "SELECT OrderID, CustomerID, EmployeeID, OrderAdapter FROM Orders",   
    connection);  
  
// Populate a strongly typed DataSet.  
connection.Open();  
CustomerDataSet customers = new CustomerDataSet();  
customerAdapter.Fill(customers, "Customers");  
orderAdapter.Fill(customers, "Orders");  
connection.Close();  
  
// Add a strongly typed event.  
customers.Customers.CustomerChanged += new   
  CustomerDataSet.CustomerChangeEventHandler(OnCustomerChanged);  
  
// Add a strongly typed DataRow.  
CustomerDataSet.Customer newCustomer =   
    customers.Customers.NewCustomeromer();  
newCustomer.CustomerID = "NEW01";  
newCustomer.CompanyName = "My New Company";  
customers.Customers.AddCustomer(newCustomer);  
  
// Navigate the child relation.  
foreach(CustomerDataSet.Customer customer in customers.Customers)  
{  
  Console.WriteLine(customer.CustomerID);  
  foreach(CustomerDataSet.Order order in customer.GetOrders())  
    Console.WriteLine("\t" + order.OrderID);  
}  
  
protected static void OnCustomerChanged(object sender, CustomerDataSet.CustomerChangeEvent e)  
    {  
  
    }  
```  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Data.DataColumnCollection>  
 <xref:System.Data.DataSet>  
 [Set di dati tipizzati](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/typed-datasets.md)  
 [Oggetti DataSet, DataTable e DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)  
 [Provider gestiti ADO.NET e Centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)
