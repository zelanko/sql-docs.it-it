---
title: I flussi e persistenza | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- persisted streams [ADO]
- streams [ADO], persistence
ms.assetid: ad5bf52c-fd10-4cfa-bf7d-fcedcaa41eea
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 246d894ff38cc0dd74e96bb0fcbdb7b170b51d53
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66700500"
---
# <a name="streams-and-persistence"></a>Flussi e persistenza
Il [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto [salvare](../../../ado/reference/ado-api/save-method.md) gli archivi di metodo, o *persiste*, un **Recordset** in un file e il [aprire](../../../ado/reference/ado-api/open-method-ado-recordset.md)metodo ripristini il **Recordset** da tale file.  
  
 Con ADO 2.7 o versione successiva, il **salvare** e **Open** metodi possono rendere persistente un **Recordset** a un [Stream](../../../ado/reference/ado-api/stream-object-ado.md) anche l'oggetto. Questa funzionalità è particolarmente utile quando si lavora sul servizio dati remoto (RDS) e le pagine ASP (Active Server).  
  
 Per altre informazioni su come la persistenza può essere usata da solo alle pagine ASP, vedere la documentazione di ASP corrente.  
  
 Di seguito sono proposti alcuni scenari che illustrano come **Stream** oggetti e persistenza possono essere usati.  
  
## <a name="scenario-1"></a>Scenario 1  
 Questo scenario viene salvato un **Recordset** in un file e quindi in un **Stream**. In un altro quindi si apre un flusso persistente **Recordset**.  
  
```  
Dim rs1 As ADODB.Recordset  
Dim rs2 As ADODB.Recordset  
Dim stm As ADODB.Stream  
  
Set rs1 = New ADODB.Recordset  
Set rs2 = New ADODB.Recordset  
Set stm = New ADODB.Stream  
  
rs1.Open   "SELECT * FROM Customers", "Provider=sqloledb;" & _  
        "Data Source=MyServer;Initial Catalog=Northwind;" & _  
        "Integrated Security=SSPI;""", adopenStatic, adLockReadOnly, adCmdText  
rs1.Save "c:\myfolder\mysubfolder\myrs.xml", adPersistXML  
rs1.Save stm, adPersistXML  
rs2.Open stm  
```  
  
## <a name="scenario-2"></a>Scenario 2  
 Questo scenario persiste un **Recordset** in un **Stream** in formato XML. Quindi legge il **Stream** in una stringa che è possibile esaminare, modificare o visualizzare.  
  
```  
Dim rs As ADODB.Recordset  
Dim stm As ADODB.Stream  
Dim strRst As String  
  
Set rs = New ADODB.Recordset  
Set stm = New ADODB.Stream  
  
' Open, save, and close the recordset.   
rs.Open "SELECT * FROM Customers", "Provider=sqloledb;" & _  
        "Data Source=MyServer;Initial Catalog=Northwind;" & _  
        "Integrated Security=SSPI;"""  
rs.Save stm, adPersistXML  
rs.Close  
Set rs = nothing  
  
' Put saved Recordset into a string variable.  
strRst = stm.ReadText(adReadAll)  
  
' Examine, manipulate, or display the XML data.  
...  
```  
  
## <a name="scenario-3"></a>Scenario 3  
 Questo esempio di codice viene illustrato come rendere persistente codice ASP una **Recordset** come XML direttamente per il **risposta** oggetto:  
  
```  
...  
<%  
response.ContentType = "text/xml"  
  
' Create and open a Recordset.  
Set rs = Server.CreateObject("ADODB.Recordset")  
rs.Open "select * from Customers", "Provider=sqloledb;" & _  
        "Data Source=MyServer;Initial Catalog=Northwind;" & _  
        "Integrated Security=SSPI;"""  
  
' Save Recordset directly into output stream.  
rs.Save Response, adPersistXML   
  
' Close Recordset.  
rs.Close  
Set rs = nothing  
%>  
...  
```  
  
## <a name="scenario-4"></a>Scenario 4  
 In questo scenario, il codice ASP scrive il contenuto del **Recordset** in formato ADTG al client. Il [Microsoft Cursor Service per OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) possono usare questi dati per creare un disconnesso **Recordset**.  
  
 Una nuova proprietà di servizi desktop remoto [DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md), [URL](../../../ado/reference/rds-api/url-property-rds.md), punta alla pagina ASP che genera il **Recordset**. Ciò significa che un **Recordset** oggetto può essere ottenuto senza servizi desktop remoto mediante il server-side [DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) oggetto oppure l'utente la scrittura di un oggetto business. Ciò semplifica il modello di programmazione di servizi desktop remoto in modo significativo.  
  
 Sul lato server, nome in codice https://server/directory/recordset.asp:  
  
```  
<%  
Dim rs   
Set rs = Server.CreateObject("ADODB.Recordset")  
rs.Open "select au_fname, au_lname, phone from Authors", ""& _  
        "Provider=sqloledb;Data Source=MyServer;" & _  
        "Initial Catalog=Pubs;Integrated Security=SSPI;"  
response.ContentType = "multipart/mixed"  
rs.Save response, adPersistADTG  
%>  
```  
  
 Codice lato client:  
  
```  
<HTML>  
<HEAD>  
<TITLE>RDS Query Page</TITLE>  
</HEAD>  
<body>  
<CENTER>  
<H1>Remote Data Service 2.5</H1>  
<TABLE DATASRC="#DC1">  
   <TR>   
      <TD><SPAN DATAFLD="au_fname"></SPAN></TD>  
      <TD><SPAN DATAFLD="au_lname"></SPAN></TD>  
      <TD><SPAN DATAFLD="phone"></SPAN></TD>  
   </TR>  
</TABLE>  
<BR>  
  
<OBJECT classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"  
    ID=DC1 HEIGHT=1 WIDTH = 1>  
    <PARAM NAME="URL" VALUE="https://server/directory/recordset.asp">  
</OBJECT>  
  
</SCRIPT>  
</BODY>  
</HTML>  
```  
  
 Gli sviluppatori hanno inoltre la possibilità di usare una **Recordset** oggetto nel client:  
  
```  
...  
function GetRs()   
    {  
    rs = CreateObject("ADODB.Recordset");  
    rs.Open "https://server/directory/recordset.asp"  
    DC1.SourceRecordset = rs;  
    }  
...  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo Open (Recordset ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Record Object (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [Metodo Save](../../../ado/reference/ado-api/save-method.md)
