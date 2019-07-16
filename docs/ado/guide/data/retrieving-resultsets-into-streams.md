---
title: Recupero dei set di risultati in flussi | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/20/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- streams [ADO], retrieving query results
- query results into stream [ADO]
- retrieving results into stream [ADO]
ms.assetid: 996c1321-c926-4f57-8297-85c8c20de974
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2f0c76a668c7191467e9f66ba48c486aceea16df
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924341"
---
# <a name="retrieving-resultsets-into-streams"></a>Recupero di set di risultati nei flussi
Invece di ricevere i risultati in tradizionale **Recordset** ADO possa invece di recuperare i risultati della query in un flusso oggetto. L'oggetto ADO **Stream** oggetto (o altri oggetti che supportano il modello COM **IStream** interfaccia, ad esempio ASP **richiesta** e **risposta** oggetti ) può essere utilizzato per contenere questi risultati. È possibile utilizzare questa funzionalità consiste nel recuperare i risultati in formato XML. Con SQL Server, ad esempio, i risultati XML possono essere restituiti in diversi modi, ad esempio usando la clausola FOR XML con una query SQL SELECT o una query XPath.  
  
 Per ricevere i risultati della query in formato flusso anziché in un **Recordset**, è necessario specificare il **adExecuteStream** costante dal **ExecuteOptionEnum** come parametro del **Execute** metodo di un **comando** oggetto. Se il provider supporta questa funzionalità, i risultati verranno restituiti in un flusso al termine dell'esecuzione. Potrebbe essere necessario specificare proprietà aggiuntive specifiche del provider prima che l'esecuzione del codice. Ad esempio, con il Provider Microsoft OLE DB per SQL Server, le proprietà come **Output Stream** nel **proprietà** raccolta del **comando** oggetto deve essere specificato. Per altre informazioni sulle proprietà dinamiche specifiche di SQL Server correlate a questa funzionalità, vedere le proprietà XML-Related nella documentazione Online di SQL Server.  
  
## <a name="for-xml-query-example"></a>AD esempio di Query XML  
 Nell'esempio seguente viene scritto in VBScript al database Northwind:  
  
```html
<!-- BeginRecordAndStreamVBS -->  
<%@ LANGUAGE = VBScript %>  
<%  Option Explicit      %>  
  
<HTML>  
<HEAD>  
<META NAME="GENERATOR" Content="Microsoft Developer Studio"/>  
<META HTTP-EQUIV="Content-Type" content="text/html"; charset="iso-8859-1">  
<TITLE>FOR XML Query Example</TITLE>  
  
<STYLE>  
   BODY  
   {  
      FONT-FAMILY: Tahoma;  
      FONT-SIZE: 8pt;  
      OVERFLOW: auto  
   }  
  
   H3  
   {  
      FONT-FAMILY: Tahoma;  
      FONT-SIZE: 8pt;  
      OVERFLOW: auto  
   }  
</STYLE>  
  
<!-- #include file="adovbs.inc" -->  
<%  
   Response.Write "<H3>Server-side processing</H3>"  
  
   Response.Write "Page Generated @ " & Now() & "<BR/>"  
  
   Dim adoConn  
   Set adoConn = Server.CreateObject("ADODB.Connection")  
  
   Dim sConn  
   sConn = "Provider=SQLOLEDB;Data Source=" & _  
      Request.ServerVariables("SERVER_NAME") & ";" & _  
      Initial Catalog=Northwind;Integrated Security=SSPI;"  
  
   Response.write "Connect String = " & sConn & "<BR/>"  
  
   adoConn.ConnectionString = sConn  
   adoConn.CursorLocation = adUseClient  
  
   adoConn.Open  
  
   Response.write "ADO Version = " & adoConn.Version & "<BR/>"  
   Response.write "adoConn.State = " & adoConn.State & "<BR/>"  
  
   Dim adoCmd  
   Set adoCmd = Server.CreateObject("ADODB.Command")  
   Set adoCmd.ActiveConnection = adoConn  
  
   Dim sQuery  
   sQuery = "<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql'><sql:query>SELECT * FROM PRODUCTS WHERE ProductName='Gumbr Gummibrchen' FOR XML AUTO</sql:query></ROOT>"  
  
   Response.write "Query String = " & sQuery & "<BR/>"  
  
   Dim adoStreamQuery  
   Set adoStreamQuery = Server.CreateObject("ADODB.Stream")  
   adoStreamQuery.Open  
   adoStreamQuery.WriteText sQuery, adWriteChar  
   adoStreamQuery.Position = 0  
  
   adoCmd.CommandStream = adoStreamQuery  
   adoCmd.Dialect = "{5D531CB2-E6Ed-11D2-B252-00C04F681B71}"  
  
   Response.write "Pushing XML to client for processing "  & "<BR/>"  
  
   adoCmd.Properties("Output Stream") = Response  
   Response.write "<XML ID='MyDataIsle'>"  
   adoCmd.Execute , , 1024  
   Response.write "</XML>"  
  
%>  
  
<SCRIPT language="VBScript" For="window" Event="onload">  
   Dim xmlDoc  
   Set xmlDoc = MyDataIsle.XMLDocument  
   xmlDoc.resolveExternals=false  
   xmlDoc.async=false  
  
   If xmlDoc.parseError.Reason <> "" then  
      Msgbox "parseError.Reason = " & xmlDoc.parseError.Reason  
   End If  
  
   Dim root, child  
   Set root = xmlDoc.documentElement  
   For each child in root.childNodes  
      dim OutputXML  
      OutputXML = document.all("log").innerHTML  
      document.all("log").innerHTML = OutputXML & "<LI>" & child.getAttribute("ProductName") & "</LI>"  
   Next  
</SCRIPT>  
  
</HEAD>  
  
<BODY>  
  
   <H3>Client-side processing of XML Document MyDataIsle</H3>  
   <UL id=log>  
   </UL>  
  
</BODY>  
</HTML>  
<!-- EndRecordAndStreamVBS -->  
  
```  
  
 La clausola FOR XML indica a SQL Server per restituire i dati sotto forma di un documento XML.  
  
### <a name="for-xml-syntax"></a>Per informazioni sulla sintassi XML  
  
```syntax
FOR XML [RAW|AUTO|EXPLICIT]  
```  
  
 PER XML RAW genera elementi riga generico con valori di colonna come attributi. FOR XML AUTO utilizza l'euristica per generare una struttura gerarchica con i nomi di elementi in base ai nomi di tabella. FOR XML EXPLICIT genera una tabella universale con relazioni completamente descritte dai metadati.  
  
 L'istruzione SQL SELECT FOR XML di esempio seguente:  
  
```sql
SELECT * FROM PRODUCTS ORDER BY PRODUCTNAME FOR XML AUTO  
```  
  
 Il comando può essere specificato in una stringa come illustrato in precedenza, assegnato a **CommandText**, o sotto forma di una query del modello XML assegnata a **CommandStream**. Per altre informazioni sulle query modello XML, vedere [comando flussi](../../../ado/guide/data/command-streams.md) in ADO o flussi di utilizzo per l'Input di comando nella documentazione Online di SQL Server.  
  
 Come una query del modello XML, la query FOR XML viene visualizzato come segue:  
  
```xml
<sql:query> SELECT * FROM PRODUCTS ORDER BY PRODUCTNAME FOR XML AUTO </sql:query>  
```  
  
 Questo esempio viene specificato l'ASP **risposta** dell'oggetto per il **Output Stream** proprietà:  
  
```vb
adoCmd.Properties("Output Stream") = Response  
```  
  
 A questo punto, specificare **adExecuteStream** del parametro **Execute**. In questo esempio esegue il wrapping di flusso nei tag XML per creare un'isola di dati XML:  
  
```vb
Response.write "<XML ID=MyDataIsle>"  
adoCmd.Execute , , adExecuteStream  
Response.write "</XML>"  
```  
  
### <a name="remarks"></a>Note  
 A questo punto, XML è stato trasmesso al browser del client ed è pronto per essere visualizzato. Questa operazione viene eseguita utilizzando VBScript lato client per associare il documento XML a un'istanza del DOM e scorrimento in ciclo tra ogni nodo figlio per creare un elenco di prodotti in formato HTML.
