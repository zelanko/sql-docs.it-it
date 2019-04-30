---
title: Script | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- dependencies [SMO]
- scripts [SMO]
ms.assetid: 13a35511-3987-426b-a3b7-3b2e83900dc7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f10289e099a0c3b6400b71d972c6f749ffb76ff8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63158788"
---
# <a name="scripting"></a>Scripting
  In SMO la generazione di script è controllata dall'oggetto <xref:Microsoft.SqlServer.Management.Smo.Scripter> e dai relativi oggetti figlio oppure dal metodo `Script` in oggetti singoli. Il <xref:Microsoft.SqlServer.Management.Smo.Scripter> oggetto controlla il mapping da relazioni di dipendenza per gli oggetti in un'istanza di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 La generazione di script avanzata tramite l'oggetto <xref:Microsoft.SqlServer.Management.Smo.Scripter> e i relativi oggetti figlio è un processo a tre fasi:  
  
1.  Individuazione  
  
2.  Generazione dell'elenco  
  
3.  Generazione dello script  
  
 Nella fase di individuazione viene utilizzato l'oggetto <xref:Microsoft.SqlServer.Management.Smo.DependencyWalker>. A partire da un elenco URN di oggetti, il metodo <xref:Microsoft.SqlServer.Management.Smo.DependencyWalker.DiscoverDependencies%2A> dell'oggetto <xref:Microsoft.SqlServer.Management.Smo.DependencyWalker> restituisce un oggetto <xref:Microsoft.SqlServer.Management.Smo.DependencyTree> per gli oggetti presenti nell'elenco URN. Valore Boolean *fParents* parametro viene utilizzato per specificare se i genitori o gli elementi figlio dell'oggetto specificato per essere individuati. In questa fase è possibile modificare l'albero delle dipendenze.  
  
 Nella fase di generazione dell'elenco viene passato l'albero e viene restituito l'elenco risultante. Questo elenco di oggetti è ordinato secondo la generazione di script e può essere modificato.  
  
 Nelle fasi di generazione dell'elenco viene utilizzato il metodo <xref:Microsoft.SqlServer.Management.Smo.DependencyWalker.WalkDependencies%2A> per restituire un oggetto <xref:Microsoft.SqlServer.Management.Smo.DependencyTree>. In questa fase è possibile modificare <xref:Microsoft.SqlServer.Management.Smo.DependencyTree>.  
  
 Nella terza e ultima fase viene generato uno script con l'elenco e le opzioni di generazione script specificate. Il risultato viene restituito come un oggetto di sistema <xref:System.Collections.Specialized.StringCollection>. In questa fase i nomi degli oggetti dipendenti vengono estratti dalla raccolta Elementi dell'oggetto <xref:Microsoft.SqlServer.Management.Smo.DependencyTree> e da proprietà come <xref:Microsoft.SqlServer.Management.Smo.DependencyTree.NumberOfSiblings%2A> e <xref:Microsoft.SqlServer.Management.Smo.DependencyTree.FirstChild%2A>.  
  
## <a name="example"></a>Esempio  
 Per usare qualsiasi esempio di codice fornito, è necessario scegliere l'ambiente di programmazione, il modello di programmazione e il linguaggio di programmazione per la creazione dell'applicazione. Per altre informazioni, vedere [creare un progetto Visual Basic SMO in Visual Studio .NET](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) oppure [creare un Visual C#&#35; progetto SMO in Visual Studio .NET](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
 Per questo esempio di codice è necessaria un'istruzione `Imports` per lo spazio dei nomi System.Collections.Specialized. Inserire questa istruzione con le altre istruzioni Imports prima di qualsiasi dichiarazione nell'applicazione.  
  
```  
Imports Microsoft.SqlServer.Management.Smo  
Imports Microsoft.SqlServer.Management.Common  
Imports System.Collections.Specialized  
```  
  
## <a name="scripting-out-the-dependencies-for-a-database-in-visual-basic"></a>Generazione di script delle dipendenze per un database in Visual Basic  
 In questo esempio di codice viene illustrato come individuare le dipendenze e scorrere l'elenco per visualizzare i risultati.  
  
```  
' compile with:   
' /r:Microsoft.SqlServer.Smo.dll   
' /r:Microsoft.SqlServer.ConnectionInfo.dll   
' /r:Microsoft.SqlServer.Management.Sdk.Sfc.dll   
  
Imports Microsoft.SqlServer.Management.Smo  
Imports Microsoft.SqlServer.Management.Sdk.Sfc  
  
Public Class A  
   Public Shared Sub Main()  
      ' database name  
      Dim dbName As [String] = "AdventureWorksLT2012"   ' database name  
  
      ' Connect to the local, default instance of SQL Server.   
      Dim srv As New Server()  
  
      ' Reference the database.    
      Dim db As Database = srv.Databases(dbName)  
  
      ' Define a Scripter object and set the required scripting options.   
      Dim scrp As New Scripter(srv)  
      scrp.Options.ScriptDrops = False  
      scrp.Options.WithDependencies = True  
      scrp.Options.Indexes = True   ' To include indexes  
      scrp.Options.DriAllConstraints = True   ' to include referential constraints in the script  
  
      ' Iterate through the tables in database and script each one. Display the script.  
      For Each tb As Table In db.Tables  
         ' check if the table is not a system table  
         If tb.IsSystemObject = False Then  
            Console.WriteLine("-- Scripting for table " + tb.Name)  
  
            ' Generating script for table tb  
            Dim sc As System.Collections.Specialized.StringCollection = scrp.Script(New Urn() {tb.Urn})  
            For Each st As String In sc  
               Console.WriteLine(st)  
            Next  
            Console.WriteLine("--")  
         End If  
      Next  
   End Sub  
End Class  
```  
  
## <a name="scripting-out-the-dependencies-for-a-database-in-visual-c"></a>Generazione di script delle dipendenze per un database in Visual C#  
 In questo esempio di codice viene illustrato come individuare le dipendenze e scorrere l'elenco per visualizzare i risultati.  
  
```  
// compile with:   
// /r:Microsoft.SqlServer.Smo.dll   
// /r:Microsoft.SqlServer.ConnectionInfo.dll   
// /r:Microsoft.SqlServer.Management.Sdk.Sfc.dll   
  
using System;  
using Microsoft.SqlServer.Management.Smo;  
using Microsoft.SqlServer.Management.Sdk.Sfc;  
  
public class A {  
   public static void Main() {   
      String dbName = "AdventureWorksLT2012"; // database name  
  
      // Connect to the local, default instance of SQL Server.   
      Server srv = new Server();  
  
      // Reference the database.    
      Database db = srv.Databases[dbName];  
  
      // Define a Scripter object and set the required scripting options.   
      Scripter scrp = new Scripter(srv);  
      scrp.Options.ScriptDrops = false;  
      scrp.Options.WithDependencies = true;  
      scrp.Options.Indexes = true;   // To include indexes  
      scrp.Options.DriAllConstraints = true;   // to include referential constraints in the script  
  
      // Iterate through the tables in database and script each one. Display the script.     
      foreach (Table tb in db.Tables) {   
         // check if the table is not a system table  
         if (tb.IsSystemObject == false) {  
            Console.WriteLine("-- Scripting for table " + tb.Name);  
  
            // Generating script for table tb  
            System.Collections.Specialized.StringCollection sc = scrp.Script(new Urn[]{tb.Urn});  
            foreach (string st in sc) {  
               Console.WriteLine(st);  
            }  
            Console.WriteLine("--");  
         }  
      }   
   }  
}  
```  
  
## <a name="scripting-out-the-dependencies-for-a-database-in-powershell"></a>Generazione di script delle dipendenze per un database in PowerShell  
 In questo esempio di codice viene illustrato come individuare le dipendenze e scorrere l'elenco per visualizzare i risultati.  
  
```  
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\default  
  
# Create a Scripter object and set the required scripting options.  
$scrp = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Scripter -ArgumentList (Get-Item .)  
$scrp.Options.ScriptDrops = $false  
$scrp.Options.WithDependencies = $true  
$scrp.Options.IncludeIfNotExists = $true  
  
# Set the path context to the tables in AdventureWorks2012.  
  
CD Databases\AdventureWorks2012\Tables  
  
foreach ($Item in Get-ChildItem)  
 {    
 $scrp.Script($Item)  
 }  
```  
  
  
