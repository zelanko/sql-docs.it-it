---
title: Utilizzo di XML Schema | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- XML [SMO]
ms.assetid: 9d04de01-efeb-4b2d-8c28-3234bc7ff2f3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f65643152bb069c703fe3a63e58ad669f3d3e322
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62626864"
---
# <a name="using-xml-schemas"></a>Utilizzo di XML Schema
  La programmazione XML in SMO è limitata alla fornitura di tipi di dati XML, spazi dei nomi XML e indicizzazione semplice in colonne di tipi di dati XML.  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] fornisce l'archiviazione nativa per istanze di documento XML. Gli elementi XML Schema consentono di definire tipi di dati XML complessi da utilizzare per convalidare documenti XML allo scopo di assicurare l'integrità dei dati. L'elemento XML Schema è definito nell'oggetto <xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection>.  
  
## <a name="example"></a>Esempio  
 Per usare qualsiasi esempio di codice fornito, è necessario scegliere l'ambiente di programmazione, il modello di programmazione e il linguaggio di programmazione per la creazione dell'applicazione. Per altre informazioni, vedere [creare un progetto Visual Basic SMO in Visual Studio .NET](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) oppure [creare un Visual C#&#35; progetto SMO in Visual Studio .NET](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-an-xml-schema-in-visual-basic"></a>Creazione di un elemento XML Schema in Visual Basic  
 In questo esempio di codice viene illustrato come creare un elemento XML Schema tramite l'oggetto <xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection>. La proprietà <xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection.Text%2A>, che definisce la raccolta di XML Schema, contiene numerose virgolette doppie. Queste ultime vengono sostituite dalla stringa `chr(34)`.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBXMLSchema1](SMO How to#SMO_VBXMLSchema1)]  -->  
  
## <a name="creating-an-xml-schema-in-visual-c"></a>Creazione di un elemento XML Schema in Visual C#  
 In questo esempio di codice viene illustrato come creare un elemento XML Schema tramite l'oggetto <xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection>. La proprietà <xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection.Text%2A>, che definisce la raccolta di XML Schema, contiene numerose virgolette doppie. Queste ultime vengono sostituite dalla stringa `chr(34)`.  
  
```  
{  
            //Connect to the local, default instance of SQL Server.   
            Server srv = default(Server);  
            srv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database db = default(Database);  
            db = srv.Databases["AdventureWorks2012"];  
            //Define an XmlSchemaCollection object by supplying the parent  
            // database and name arguments in the constructor.   
            XmlSchemaCollection xsc = default(XmlSchemaCollection);  
            xsc = new XmlSchemaCollection(db, "MySampleCollection");  
            xsc.Text = "<schema xmlns=" + Strings.Chr(34) + "http://www.w3.org/2001/XMLSchema" + Strings.Chr(34) + " xmlns:ns=" + Strings.Chr(34) + "http://ns" + Strings.Chr(34) + "><element name=" + Strings.Chr(34) + "e" + Strings.Chr(34) + " type=" + Strings.Chr(34) + "dateTime" + Strings.Chr(34) + "/></schema>";  
            //Create the XML schema collection on the instance of SQL Server.   
            xsc.Create();  
        }  
```  
  
## <a name="creating-an-xml-schema-in-powershell"></a>Creazione di un elemento XML Schema in PowerShell  
 In questo esempio di codice viene illustrato come creare un elemento XML Schema tramite l'oggetto <xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection>. La proprietà <xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection.Text%2A>, che definisce la raccolta di XML Schema, contiene numerose virgolette doppie. Queste ultime vengono sostituite dalla stringa `chr(34)`.  
  
```  
#Get a server object which corresponds to the default instance replace LocalMachine with the physical server  
cd \sql\LocalHost  
$srv = get-item default  
  
#Reference the AdventureWorks database.  
$db = $srv.Databases["AdventureWorks2012"]  
  
#Create a new schema collection  
$xsc = New-Object -TypeName Microsoft.SqlServer.Management.SMO.XmlSchemaCollection `  
-argumentlist $db,"MySampleCollection"  
  
#Add the xml  
$dq = '"' # the double quote character  
$xsc.Text = "<schema xmlns=" + $dq + "http://www.w3.org/2001/XMLSchema" + $dq + `  
"  xmlns:ns=" + $dq + "http://ns" + $dq + "><element name=" + $dq + "e" + $dq +`  
 " type=" + $dq + "dateTime" + $dq + "/></schema>"  
  
#Create the XML schema collection on the instance of SQL Server.  
$xsc.Create()  
```  
  
  
