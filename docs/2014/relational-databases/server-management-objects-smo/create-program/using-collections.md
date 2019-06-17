---
title: Uso delle raccolte | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQL Server Management Objects, collections
- SMO [SQL Server], collections
- collections [SMO]
ms.assetid: 209eb175-2514-4de1-bc32-b2e6a469d945
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0be31e67be0b80de13a9239b221ca73436a8d6e7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63192128"
---
# <a name="using-collections"></a>Utilizzo delle raccolte
  Una raccolta è un elenco di oggetti costruiti dalla stessa classe di oggetti e che condividono lo stesso oggetto padre. L'oggetto raccolta contiene sempre il nome del tipo di oggetto con il suffisso Collection. Per accedere ad esempio alle colonne di una tabella specificata, utilizzare il tipo di oggetto <xref:Microsoft.SqlServer.Management.Smo.ColumnCollection>. Questo tipo contiene tutti gli oggetti <xref:Microsoft.SqlServer.Management.Smo.Column> che appartengono allo stesso oggetto <xref:Microsoft.SqlServer.Management.Smo.Table>.  
  
 Il [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] `For...Each` istruzione o il [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[csprcs](../../../includes/csprcs-md.md)] `foreach` istruzione può essere utilizzata per scorrere ogni membro della raccolta.  
  
## <a name="examples"></a>Esempi  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="referencing-an-object-by-using-a-collection-in-visual-basic"></a>Riferimento a un oggetto tramite una raccolta in Visual Basic  
 In questo esempio di codice viene illustrato come impostare la proprietà di una colonna mediante le proprietà <xref:Microsoft.SqlServer.Management.Smo.TableViewTableTypeBase.Columns%2A>, <xref:Microsoft.SqlServer.Management.Smo.Database.Tables%2A> e <xref:Microsoft.SqlServer.Management.Smo.Server.Databases%2A>. Queste proprietà rappresentano le raccolte che è possibile utilizzare per identificare un determinato oggetto quando sono utilizzate con un parametro che ne specifica il nome. Il nome e lo schema sono necessari per la proprietà dell'oggetto della raccolta <xref:Microsoft.SqlServer.Management.Smo.Database.Tables%2A>.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBCollections1](SMO How to#SMO_VBCollections1)]  -->  
  
## <a name="referencing-an-object-by-using-a-collection-in-visual-c"></a>Riferimento a un oggetto tramite una raccolta in Visual C#  
 In questo esempio di codice viene illustrato come impostare la proprietà di una colonna mediante le proprietà <xref:Microsoft.SqlServer.Management.Smo.TableViewTableTypeBase.Columns%2A>, <xref:Microsoft.SqlServer.Management.Smo.Database.Tables%2A> e <xref:Microsoft.SqlServer.Management.Smo.Server.Databases%2A>. Queste proprietà rappresentano le raccolte che è possibile utilizzare per identificare un determinato oggetto quando sono utilizzate con un parametro che ne specifica il nome. Il nome e lo schema sono necessari per la proprietà dell'oggetto della raccolta <xref:Microsoft.SqlServer.Management.Smo.Database.Tables%2A>.  
  
```  
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Modify a property using the Databases, Tables, and Columns collections to reference a column.   
srv.Databases("AdventureWorks2012").Tables("Person", "Person").Columns("LastName").Nullable = true;   
//Call the Alter method to make the change on the instance of SQL Server.   
srv.Databases("AdventureWorks2012").Tables("Person", "Person").Columns("LastName").Alter();   
}  
```  
  
## <a name="iterating-through-the-members-of-a-collection-in-visual-basic"></a>Scorrimento dei membri di una raccolta in Visual Basic  
 In questo esempio di codice viene eseguito lo scorrimento della proprietà della raccolta <xref:Microsoft.AnalysisServices.Server.Databases%2A> e vengono visualizzate tutte le connessioni di database all'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBCollections2](SMO How to#SMO_VBCollections2)]  -->  
  
## <a name="iterating-through-the-members-of-a-collection-in-visual-c"></a>Scorrimento dei membri di una raccolta in Visual C#  
 In questo esempio di codice viene eseguito lo scorrimento della proprietà della raccolta <xref:Microsoft.AnalysisServices.Server.Databases%2A> e vengono visualizzate tutte le connessioni di database all'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
```  
//Connect to the local, default instance of SQL Server.   
{   
Server srv = default(Server);   
srv = new Server();   
int count = 0;   
int total = 0;   
//Iterate through the databases and call the GetActiveDBConnectionCount method.   
Database db = default(Database);   
foreach ( db in srv.Databases) {   
  count = srv.GetActiveDBConnectionCount(db.Name);   
  total = total + count;   
  //Display the number of connections for each database.   
  Console.WriteLine(count + " connections on " + db.Name);   
}   
//Display the total number of connections on the instance of SQL Server.   
Console.WriteLine("Total connections =" + total);   
}   
```  
  
  
