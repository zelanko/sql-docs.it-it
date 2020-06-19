---
title: Persistenza degli oggetti personalizzati | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- custom objects [Integration Services], persisting
ms.assetid: 97c19716-6447-4c1c-b277-cc2e6c1e6a6c
author: janinezhang
ms.author: janinez
ms.openlocfilehash: bb6d525235db93e10fcf14b73e80fc9c096d9c9f
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84968701"
---
# <a name="persisting-custom-objects"></a>Persistenza degli oggetti personalizzati
  Non è necessario implementare la persistenza personalizzata per gli oggetti personalizzati creati, purché le relative proprietà utilizzino solo tipi di dati semplici, ad esempio `integer` e `string`. L'implementazione predefinita della persistenza salva i metadati per l'oggetto insieme ai valori di tutte le relative proprietà.  
  
 Se tuttavia l'oggetto include proprietà che utilizzano tipi di dati complessi o se si desidera eseguire un'elaborazione personalizzata sui valori delle proprietà quando vengono caricati e salvati, è possibile implementare l'interfaccia <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentPersist> e i relativi metodi <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentPersist.LoadFromXML%2A> e <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentPersist.SaveToXML%2A>. In questi metodi un frammento XML che contiene le proprietà dell'oggetto e i relativi valori correnti viene caricato dalla definizione XML del pacchetto o salvato in quest'ultima. Il formato di questo frammento XML non è definito; l'unico requisito è che sia XML ben formato.  
  
> [!IMPORTANT]  
>  Quando si implementa la persistenza personalizzata, è necessario rendere persistenti tutte le proprietà dell'oggetto, incluse le proprietà ereditate e quelle personalizzate che sono state aggiunte.  
  
## <a name="example"></a>Esempio  
 Anche se l'esempio di gestione connessione personalizzata SQL Server non richiede la persistenza personalizzata per le tre proprietà di tipo `string`, nel codice seguente è illustrato un esempio del codice personalizzato che sarebbe richiesto per rendere persistenti la gestione connessione e le relative proprietà. La classe che contiene il codice deve implementare l'interfaccia <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentPersist>.  
  
```vb  
Private Const PERSIST_ELEMENT As String = "SqlConnectionManager"  
Private Const PERSIST_SERVER As String = "Server"  
Private Const PERSIST_DATABASE As String = "Database"  
Private Const PERSIST_CONNECTIONSTRING As String = "ConnectionString"  
  
Public Sub LoadFromXML(ByVal node As System.Xml.XmlElement, _  
  ByVal infoEvents As Microsoft.SqlServer.Dts.Runtime.IDTSInfoEvents) _  
  Implements Microsoft.SqlServer.Dts.Runtime.IDTSComponentPersist.LoadFromXML  
  
  Dim propertyNode As XmlNode  
  
  ' Make sure that the correct node is being loaded.  
  If node.Name <> PERSIST_ELEMENT Then  
    Throw New Exception("Persisted element is not of type " & PERSIST_ELEMENT)  
  End If  
  
  ' Load the three properties of the object from XML into variables.  
  For Each propertyNode In node.ChildNodes  
    Select Case propertyNode.Name  
      Case PERSIST_SERVER  
        _serverName = propertyNode.InnerText  
      Case PERSIST_DATABASE  
        _databaseName = propertyNode.InnerText  
      Case PERSIST_CONNECTIONSTRING  
        _connectionString = propertyNode.InnerText  
    End Select  
  Next  
  
End Sub  
  
Public Sub SaveToXML(ByVal doc As System.Xml.XmlDocument, _  
  ByVal infoEvents As Microsoft.SqlServer.Dts.Runtime.IDTSInfoEvents) _  
  Implements Microsoft.SqlServer.Dts.Runtime.IDTSComponentPersist.SaveToXML  
  
  Dim elementRoot As XmlElement  
  Dim propertyNode As XmlNode  
  
  ' Create a new node to persist the object and its properties.  
  elementRoot = doc.CreateElement(String.Empty, PERSIST_ELEMENT, String.Empty)  
  
  ' Save the three properties of the object from variables into XML.  
  propertyNode = doc.CreateNode(XmlNodeType.Element, PERSIST_SERVER, String.Empty)  
  propertyNode.InnerText = _serverName  
  elementRoot.AppendChild(propertyNode)  
  
  propertyNode = doc.CreateNode(XmlNodeType.Element, PERSIST_DATABASE, String.Empty)  
  propertyNode.InnerText = _databaseName  
  elementRoot.AppendChild(propertyNode)  
  
  propertyNode = doc.CreateNode(XmlNodeType.Element, PERSIST_CONNECTIONSTRING, String.Empty)  
  propertyNode.InnerText = _connectionString  
  elementRoot.AppendChild(propertyNode)  
  
  doc.AppendChild(elementRoot)  
  
End Sub  
```  
  
```csharp  
private const string PERSIST_ELEMENT = "SqlConnectionManager";  
private const string PERSIST_SERVER = "Server";  
private const string PERSIST_DATABASE = "Database";  
private const string PERSIST_CONNECTIONSTRING = "ConnectionString";  
  
public void LoadFromXML(System.Xml.XmlElement node,  
  Microsoft.SqlServer.Dts.Runtime.IDTSInfoEvents infoEvents)  
{  
  
  // Make sure that the correct node is being loaded.  
  if (node.Name != PERSIST_ELEMENT)  
  {  
    throw new Exception("Persisted element is not of type " + PERSIST_ELEMENT);  
  }  
  
  // Save the three properties of the object from variables into XML.  
  foreach (XmlNode propertyNode in node.ChildNodes)  
  {  
    switch (propertyNode.Name)  
    {  
      case PERSIST_SERVER:  
        _serverName = propertyNode.InnerText;  
        break;  
      case PERSIST_DATABASE:  
        _databaseName = propertyNode.InnerText;  
        break;  
      case PERSIST_CONNECTIONSTRING:  
        _connectionString = propertyNode.InnerText;  
        break;  
    }  
  }  
  
}  
  
public void SaveToXML(System.Xml.XmlDocument doc,  
  Microsoft.SqlServer.Dts.Runtime.IDTSInfoEvents infoEvents)  
{  
  
  XmlElement elementRoot;  
  XmlNode propertyNode;  
  
  // Create a new node to persist the object and its properties.  
  elementRoot = doc.CreateElement(String.Empty, PERSIST_ELEMENT, String.Empty);  
  
  // Save the three properties of the object from variables into XML.  
  propertyNode = doc.CreateNode(XmlNodeType.Element, PERSIST_SERVER, String.Empty);  
  propertyNode.InnerText = _serverName;  
  elementRoot.AppendChild(propertyNode);  
  
  propertyNode = doc.CreateNode(XmlNodeType.Element, PERSIST_DATABASE, String.Empty);  
  propertyNode.InnerText = _databaseName;  
  elementRoot.AppendChild(propertyNode);  
  
  propertyNode = doc.CreateNode(XmlNodeType.Element, PERSIST_CONNECTIONSTRING, String.Empty);  
  propertyNode.InnerText = _connectionString;  
  elementRoot.AppendChild(propertyNode);  
  
  doc.AppendChild(elementRoot);  
  
}  
```  
  
![Integration Services icona (piccola)](../media/dts-16.gif "Icona di Integration Services (piccola)")  **rimane aggiornata con Integration Services**<br /> Per i download, gli articoli, gli esempi e i video Microsoft più recenti, oltre alle soluzioni selezionate dalla community, visitare la pagina [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] sul sito MSDN:<br /><br /> [Visitare la pagina relativa a Integration Services su MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Per ricevere una notifica automatica su questi aggiornamenti, sottoscrivere i feed RSS disponibili nella pagina.  
  
## <a name="see-also"></a>Vedere anche  
 [Sviluppo di oggetti personalizzati per Integration Services](developing-custom-objects-for-integration-services.md)   
 [Compilazione, distribuzione e debug di oggetti personalizzati](building-deploying-and-debugging-custom-objects.md)  
  
  
