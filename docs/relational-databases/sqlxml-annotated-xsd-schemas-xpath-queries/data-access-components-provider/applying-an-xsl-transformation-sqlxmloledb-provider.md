---
title: Applicando una trasformazione XSL (SQLXMLOLEDB Provider) | Documenti di Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXMLOLEDB Provider, applying XSL transformations
- applying XSL transformations [SQLXML]
- xsl property
- Base Path property
- XSL Transformations [SQLXML]
ms.assetid: cb5e41ab-dd20-4873-af20-f417bd1bbf6d
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8c9d73330063cf3f051695c5fd25c689bb6c4c10
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68061406"
---
# <a name="applying-an-xsl-transformation-sqlxmloledb-provider"></a>Applicazione di una trasformazione XSL (provider SQLXMLOLEDB)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  In questa applicazione ADO di esempio viene eseguita una query SQL e viene applicata una trasformazione XSL al risultato. Impostando la proprietà ClientSideXML su True applica l'elaborazione del set di righe sul lato client. Il sottolinguaggio del comando è impostato su {5d531cb2-e6ed-11d2-b252-00c04f681b71}, in quanto la query SQL è specificata in un modello e questo sottolinguaggio deve essere specificato per l'esecuzione di un modello. La proprietà xsl specifica il file XSL da utilizzare per applicare la trasformazione. Il valore della proprietà percorso di Base viene utilizzato per cercare il file XSL. Se si specifica un percorso del valore della proprietà xsl, il percorso è relativo al percorso specificato nella proprietà percorso di Base.  
  
 In questo esempio viene illustrato come utilizzare le proprietà specifiche del provider SQLXMLOLEDB seguenti:  
  
-   ClientSideXML  
  
-   xsl  
  
 In questa applicazione ADO di esempio sul lato client, viene eseguito un modello XML costituito da una query SQL nel server.  
  
 Poiché la proprietà ClientSideXML è impostata su True, l'istruzione SELECT senza la clausola FOR XML viene inviato al server. Il server esegue la query e restituisce un set di righe al client. Il client applica quindi la trasformazione FOR XML al set di righe e produce il documento XML.  
  
 La proprietà xsl specificata nell'applicazione. di conseguenza, la trasformazione XSL viene applicata al documento XML generato sul client e il risultato è una tabella a due colonne.  
  
 Per eseguire il comando del modello, è necessario specificare il sottolinguaggio per i modelli XML - {5d531cb2-e6ed-11d2-b252-00c04f681b71}.  
  
> [!NOTE]  
>  Nel codice è necessario specificare il nome dell'istanza di Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nella stringa di connessione. In questo esempio viene inoltre specificato l'utilizzo di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client come provider di dati, che richiede l'installazione di un software client di rete aggiuntivo. Per altre informazioni, vedere [requisiti di sistema per SQL Server Native Client](../../../relational-databases/native-client/system-requirements-for-sql-server-native-client.md).  
  
```  
Option Explicit  
Sub main()  
Dim oTestStream As New ADODB.Stream  
Dim oTestConnection As New ADODB.Connection  
Dim oTestCommand As New ADODB.Command  
oTestConnection.Open "provider=SQLXMLOLEDB.4.0;data provider=SQLNCLI11;data source=SqlServerName;initial catalog=AdventureWorks;Integrated Security=SSPI;"  
Set oTestCommand.ActiveConnection = oTestConnection  
oTestCommand.Properties("ClientSideXML") = True  
oTestCommand.CommandText = _  
        "<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql' >" & _  
       " <sql:query> " & _  
        "   SELECT TOP 25 FirstName, LastName FROM Person.Contact FOR XML AUTO " & _  
        "   </sql:query> " & _  
        " </ROOT> "  
oTestStream.Open  
' You need the dialect if you are executing a template.  
oTestCommand.Dialect = "{5d531cb2-e6ed-11d2-b252-00c04f681b71}"  
oTestCommand.Properties("Output Stream").Value = oTestStream  
oTestCommand.Properties("Base Path").Value = "c:\Schemas\SQLXML4\ExecuteTemplateWithXSL\"  
oTestCommand.Properties("xsl").Value = "myxsl.xsl"  
oTestCommand.Execute , , adExecuteStream  
  
oTestStream.Position = 0  
oTestStream.Charset = "utf-8"  
Debug.Print oTestStream.ReadText(adReadAll)  
End Sub  
Sub Form_Load()  
 main  
End Sub  
```  
  
 Di seguito viene fornito il modello XSL. Il risultato dell'applicazione di questo modello XSL è una tabella a due colonne.  
  
```  
<?xml version='1.0' encoding='UTF-8'?>            
 <xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" version="1.0">   
  
    <xsl:template match = 'Person.Contact'>  
       <TR>  
         <TD><xsl:value-of select = '@FirstName' /></TD>  
         <TD><B><xsl:value-of select = '@LastName' /></B></TD>  
       </TR>  
    </xsl:template>  
    <xsl:template match = '/'>  
      <HTML>  
        <HEAD>  
           <STYLE>th { background-color: #CCCCCC }</STYLE>  
        </HEAD>  
        <BODY>  
         <TABLE border='1' style='width:300;'>  
           <TR><TH colspan='2'>Contacts</TH></TR>  
           <TR>  
              <TH >First name</TH>  
              <TH>Last name</TH>  
           </TR>  
           <xsl:apply-templates select = 'ROOT' />  
         </TABLE>  
        </BODY>  
      </HTML>  
    </xsl:template>  
</xsl:stylesheet>  
```  
  
  
