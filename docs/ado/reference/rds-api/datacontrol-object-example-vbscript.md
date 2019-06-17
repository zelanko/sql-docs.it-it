---
title: Esempio di oggetto DataControl (VBScript) | Microsoft Docs
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
- DataControl object [ADO], VBScript example
ms.assetid: 4f306a51-d5a4-4785-b426-487639cda164
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 385b111c39e05a8ff975545a2fb90e5a9460e033
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66697373"
---
# <a name="datacontrol-object-example-vbscript"></a>Esempio di oggetto DataControl (VBScript)
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Il codice seguente viene illustrato come impostare il [Servizi Desktop remoto. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) parametri in fase di progettazione di tempo e associarle a un controllo con supporto dati. Tagliare e incollare questo codice tra il \<Body > e \</Body > tag in HTML un normale del documento e denominarlo **DataControlDesignVBS**. Lo script identificherà il server.  
  
```  
<!-- BeginDataControlDesignVBS -->  
<%@ Language=VBScript %>  
<HTML>  
<HEAD>  
<META name="VI60_DefaultClientScript"  content=VBScript>  
<META NAME="GENERATOR" Content="Microsoft Visual Studio 6.0">  
<title>RDS DataControl</title>  
  
    <%' local style sheet used for display%>  
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
<H2>RDS API Code Examples</H2>  
<HR>  
<H3>Remote Data Service</H3>  
<TABLE DATASRC=#RDS>  
<TBODY>  
   <TR>  
      <TD><SPAN DATAFLD="FirstName"></SPAN></TD>  
      <TD><SPAN DATAFLD="LastName"></SPAN></TD>  
   </TR>  
</TBODY>  
</TABLE>  
<!-- Remote Data Service with Parameters set at Design Time -->  
  
<OBJECT classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"  
   ID=RDS>  
   <PARAM NAME="SQL" VALUE="Select * from Employees for browse">  
   <PARAM NAME="SERVER" VALUE="https://<%=Request.ServerVariables("SERVER_NAME")%>">  
   <PARAM NAME="CONNECT" VALUE="Provider='sqloledb';Integrated Security='SSPI';Initial Catalog='Northwind'">  
</OBJECT>  
  
</BODY>  
</HTML>  
<!-- EndDataControlDesignVBS -->  
```  
  
 Nell'esempio seguente viene illustrato come impostare i parametri necessari di **Servizi Desktop remoto. DataControl** in fase di esecuzione. Per testare questo esempio, tagliare e incollare questo codice tra il \<Body > e \</Body > tag in HTML un normale del documento e denominarlo **DataControlRuntimeVBS**. Lo script identificherà il server.  
  
```  
<!-- BeginDataControlRuntimeVBS -->  
<%@ Language=VBScript %>  
<html>  
<head>  
    <meta name="VI60_DefaultClientScript"  content=VBScript>  
    <meta name="GENERATOR" content="Microsoft Visual Studio 6.0">  
    <title>Data Control Object Example (VBScript)</title>  
  
    <%' local style sheet used for display%>  
<style>  
<!--  
body {  
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
</style>  
</head>  
  
<body>  
<h1>Data Control Object Example (VBScript)</h1>  
  
<H2>RDS API Code Examples</H2>  
<HR>  
<H3>Remote Data Service Run Time</H3>  
  
<TABLE DATASRC=#RDS>  
<TBODY>  
  <TR>  
    <TD><SPAN DATAFLD="au_lname"></SPAN></TD>  
    <TD><SPAN DATAFLD="au_fname"></SPAN></TD>  
  </TR>  
</TBODY>  
</TABLE>  
<% ' RDS.DataControl with no parameters set at design time %>  
<OBJECT classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID=RDS HEIGHT=1 WIDTH=1></OBJECT>  
  
<FORM name="frmInput">  
<HR>  
<Input Size="70" Name="txtServer" Value="https://<%=Request.ServerVariables("SERVER_NAME")%>"><BR>  
<Input Size="100" Name="txtConnect" Value="Provider='sqloledb';Data Source=<%=Request.ServerVariables("SERVER_NAME")%>;Initial Catalog='Pubs';Integrated Security='SSPI';">  
<BR>  
<Input Size="70" Name="txtSQL" Value="Select * from Authors">  
<HR>  
<INPUT TYPE="BUTTON" NAME="Run" VALUE="Run"><BR>  
<H4>Show grid with these values or change them to see data from another ODBC data source on your server</H4>  
</FORM>  
  
<Script Language="VBScript">  
  
' Set parameters of RDS.DataControl at Run Time  
Sub Run_OnClick  
  
   RDS.Server = document.frmInput.txtServer.Value  
   RDS.Connect = document.frmInput.txtConnect.Value  
   RDS.SQL = document.frmInput.txtSQL.Value  
  
   RDS.Refresh  
  
End Sub  
  
</Script>  
  
</body>  
</html>  
<!-- EndDataControlRuntimeVBS -->  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetto DataControl (Servizi Desktop remoto)](../../../ado/reference/rds-api/datacontrol-object-rds.md)


