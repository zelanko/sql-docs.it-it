---
title: Eseguire, rieseguire una query ed eliminare i metodi esempio (VBScript) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- Execute method [ADO], VBScript example
- Clear method [ADO], VBScript example
- Requery method [ADO], VBScript example
ms.assetid: 3a7bbf07-2fca-4892-95f4-eec93f2d5e91
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 27a177b6a3d23f20790490e1f16fac2be4ec958f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67918808"
---
# <a name="execute-requery-and-clear-methods-example-vbscript"></a>Eseguire, rieseguire una query ed eliminare i metodi esempio (VBScript)
Questo esempio viene illustrato il **Execute** metodo quando viene eseguito dallo entrambi una [comando](../../../ado/reference/ado-api/command-object-ado.md) oggetto e un [connessione](../../../ado/reference/ado-api/connection-object-ado.md) oggetto. Usa anche il [Requery](../../../ado/reference/ado-api/requery-method.md) metodo per recuperare i dati correnti in un [recordset](../../../ado/reference/ado-api/recordset-object-ado.md)e il [cancellare](../../../ado/reference/ado-api/clear-method-ado.md) metodo per cancellare il contenuto del [errori](../../../ado/reference/ado-api/errors-collection-ado.md)collection. Le procedure ExecuteCommand e PrintOutput sono necessari per eseguire questa procedura.  
  
 Usare l'esempio seguente in una pagina ASP (Active Server). Per visualizzare in questo esempio completamente funzionale, è necessario disporre di dati che si trova in C:\Program Files\Microsoft piattaforma SDK\Samples\DataAccess\Rds\RDSTest\advworks.mdb AdvWorks.mdb (installato con gli esempi SDK) di origine o modificare il percorso nel codice di esempio per riflettono l'effettiva posizione di questo file. Si tratta di un file di database Microsoft Access.  
  
 Usare **trovare** per individuare il file Adovbs. inc e inserirlo nella directory di cui si intende usare. Tagliare e incollare il codice seguente nel blocco note o un altro editor di testo e salvarlo come **ExecuteVBS**. È possibile visualizzare il risultato in qualsiasi browser client.  
  
```  
<!-- BeginExecuteVBS -->  
<%@ Language=VBScript %>  
<% ' use this meta tag instead of ADOVBS.inc%>  
<!-- METADATA TYPE="typelib" uuid="00000205-0000-0010-8000-00AA006D2EA4"  -->  
<HTML>  
<HEAD>  
<META name="VI60_DefaultClientScript"  content=VBScript>  
<META NAME="GENERATOR" Content="Microsoft Visual Studio 6.0">  
<title>ADO Execute Method</title>  
<STYLE>  
<!--  
BODY {  
   font-family: 'Verdana','Arial','Helvetica',sans-serif;  
   BACKGROUND-COLOR:white;  
   COLOR:black;  
    }  
.thead {  
   background-color: #008080;   
   font-family: 'Verdana','Arial','Helvetica',sans-serif;   
   font-size: x-small;  
   color: white;  
   }  
.thead2 {  
   background-color: #800000;   
   font-family: 'Verdana','Arial','Helvetica',sans-serif;   
   font-size: x-small;  
   color: white;  
   }  
.tbody {   
   text-align: center;  
   background-color: #f7efde;  
   font-family: 'Verdana','Arial','Helvetica',sans-serif;   
   font-size: x-small;  
    }  
-->  
</STYLE>  
</HEAD>  
  
<BODY>  
<H3>ADO Execute Method</H3>  
<HR>  
<H4>Recordset Retrieved Using Connection Object</H4>  
<!--- Recordsets retrieved using Execute method of Connection and Command Objects-->  
<%   
     ' connection, command and recordset variables  
    Dim Cnxn, strCnxn  
    Dim rsCustomers, strSQLCustomers  
    Dim Cmd   
    Dim rsProducts, strSQLProducts  
  
    ' create and open connection  
    Set Cnxn = Server.CreateObject("ADODB.Connection")   
    strCnxn="Provider='sqloledb';Data Source=" & _  
            Request.ServerVariables("SERVER_NAME") & ";" & _  
            "Integrated Security='SSPI';Initial Catalog='Northwind';"  
    Cnxn.Open  strCnxn  
    ' create and open recordset  
    Set rsCustomers = Server.CreateObject("ADODB.Recordset")  
    strSQLCustomers = "Customers"  
    rsCustomers.Open strSQLCustomers, Cnxn, adOpenKeyset, adLockOptimistic, adCmdTable  
  
    '1st Recordset using Connection - Execute  
    Set rsCustomers = Cnxn.Execute(strSQLCustomers)   
  
    Set Cmd = Server.CreateObject("ADODB.Command")  
    Cmd.ActiveConnection = Cnxn  
    strSQLProducts = "SELECT * From Products"  
    Cmd.CommandText = strSQLProducts  
  
    '2nd Recordset Cmd - execute   
    Set rsProducts = Cmd.Execute  
    %>  
    <TABLE COLSPAN=8 CELLPADDING=5 BORDER=0 ALIGN=CENTER>  
    <!-- BEGIN column header row for Customer Table-->  
    <TR CLASS=thead>  
      <TH>Company Name</TH>  
      <TH>Contact Name</TH>  
      <TH>City</TH>  
    </TR>  
  
    <!--Display ADO Data from Customer Table-->  
    <%   
    Do While Not rsCustomers.EOF %>  
      <TR CLASS=tbody>  
        <TD>   
        <%= rsCustomers("CompanyName")%>   
        </TD>  
        <TD>  
        <%= rsCustomers("ContactName") %>   
        </TD>  
        <TD>   
        <%= rsCustomers("City")%>   
        </TD>  
      </TR>   
      <%   
    rsCustomers.MoveNext   
    Loop   
    %>  
</TABLE>  
  
<HR>  
<H4>Recordset Retrieved Using Command Object</H4>  
  
<TABLE CELLPADDING=5 BORDER=0 ALIGN=CENTER WIDTH="80%">  
  
<!-- BEGIN column header row for Product List Table-->  
<TR CLASS=thead2>  
  <TH>Product Name</TH>  
  <TH>Unit Price</TH>  
</TR>  
  
<!-- Display ADO Data Product List-->  
<% Do Until rsProducts.EOF %>  
  <TR CLASS=tbody>  
    <TD>  
    <%= rsProducts("ProductName")%>    
    </TD>  
    <TD>   
    <%= rsProducts("UnitPrice")%>   
    </TD>  
<%   
    rsProducts.MoveNext   
    Loop  
  
    ' clean up  
    If rsCustomers.State = adStateOpen then  
        rsCustomers.Close  
    End If  
    If rsProducts.State = adStateOpen then  
        rsProducts.Close  
    End If  
    If Cnxn.State = adStateOpen then  
        Cnxn.Close  
    End If  
    Set Cmd = Nothing  
    Set rsCustomers = Nothing  
    Set rsProducts = Nothing  
    Set Cnxn = Nothing  
%>  
</TABLE>  
  
</BODY>  
</HTML>  
<!-- EndExecuteVBS -->  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo Clear (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [Oggetto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [Oggetto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Oggetto Error](../../../ado/reference/ado-api/error-object.md)   
 [Raccolta di errori (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [Eseguire il metodo (comando ADO)](../../../ado/reference/ado-api/execute-method-ado-command.md)   
 [Eseguire il metodo (connessione ADO)](../../../ado/reference/ado-api/execute-method-ado-connection.md)   
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Metodo Requery](../../../ado/reference/ado-api/requery-method.md)
