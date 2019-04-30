---
title: Gestione degli eventi SMO | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- events [SMO]
- SQL Server Management Objects, events
- SMO [SQL Server], events
- events [SMO], about events
ms.assetid: b4f120dd-ba78-46ff-99c5-e47effac8544
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d0d309103880a369a88952e19b252fc15693fdd4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63191930"
---
# <a name="handling-smo-events"></a>Gestione degli eventi SMO
  Vi sono tipi di eventi del server che possono essere sottoscritti tramite un gestore di eventi e l'oggetto <xref:Microsoft.SqlServer.Management.Common.ServerConnection>.  
  
 Molte delle classi di istanze in SMO ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects) possono attivare eventi quando si verificano determinate azioni nel server.  
  
 Questi eventi possono essere gestiti a livello di codice configurando un gestore evento e sottoscrivendo gli eventi associati. Questo tipo di gestione degli eventi è temporanea perché quando viene chiuso il programma client SMO vengono rimosse tutte le sottoscrizioni.  
  
## <a name="connectioncontext-event-handling"></a>Gestione degli eventi ConnectionContext  
 L'oggetto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> supporta diversi tipi di evento. La proprietà dell'evento deve essere impostata su un'istanza di un gestore evento appropriato e l'oggetto gestore evento deve essere definito come una funzione protetta che gestisce l'evento.  
  
## <a name="event-subscription"></a>Sottoscrizione di eventi  
 Per gestire gli eventi è necessario scrivere una classe del gestore evento, crearne un'istanza, assegnare il gestore evento all'oggetto padre e infine effettuare la sottoscrizione all'evento.  
  
 Per gestire gli eventi, è necessario scrivere una classe del gestore evento. La classe del gestore evento può contenere più di una funzione del gestore evento e deve essere installata per poter gestire gli eventi. Le funzioni del gestore evento ricevono informazioni sull'evento dal *ServerEventNotificatificationArgs* parametro che può essere usato per segnalare informazioni sull'evento.  
  
 Sono elencati i tipi di eventi di database e server che possono essere gestiti nel <xref:Microsoft.SqlServer.Management.Smo.DatabaseEventSet> classi e <xref:Microsoft.SqlServer.Management.Smo.ServerEventSet>classe.  
  
## <a name="example"></a>Esempio  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="registering-event-handlers-and-subscribing-to-event-handling-in-visual-basic"></a>Registrazione di gestori di eventi e sottoscrizione della gestione degli eventi in Visual Basic  
 In questo esempio di codice viene illustrato come configurare il gestore dell'evento e come effettuare la sottoscrizione degli eventi del database.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBEvents1](SMO How to#SMO_VBEvents1)]  -->  
  
## <a name="registering-event-handlers-and-subscribing-to-event-handling-in-visual-c"></a>Registrazione di gestori di eventi e sottoscrizione della gestione degli eventi in Visual C#  
 In questo esempio di codice viene illustrato come configurare il gestore dell'evento e come effettuare la sottoscrizione degli eventi del database.  
  
```  
//Create an event handler subroutine that runs when a table is created.   
private void MyCreateEventHandler(object sender, ServerEventArgs e)   
{   
Console.WriteLine("A table has just been added to the AdventureWorks2012 database.");   
}   
//Create an event handler subroutine that runs when a table is deleted.   
private void MyDropEventHandler(object sender, ServerEventArgs e)   
{   
Console.WriteLine("A table has just been dropped from the AdventureWorks2012 database.");   
}   
public void Main()   
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Reference the AdventureWorks2012 database.   
Database db;   
db = srv.Databases("AdventureWorks2012");   
//Create a database event set that contains the CreateTable event only.   
DatabaseEventSet databaseCreateEventSet = new DatabaseEventSet();   
databaseCreateEventSet.CreateTable = true;   
//Create a server event handler and set it to the first event handler subroutine.   
ServerEventHandler serverCreateEventHandler;   
serverCreateEventHandler = new ServerEventHandler(MyCreateEventHandler);   
//Subscribe to the first server event handler when a CreateTable event occurs.   
db.Events.SubscribeToEvents(databaseCreateEventSet, serverCreateEventHandler);   
    //Create a database event set that contains the DropTable event only.   
DatabaseEventSet databaseDropEventSet = new DatabaseEventSet();   
databaseDropEventSet.DropTable = true;   
//Create a server event handler and set it to the second event handler subroutine.   
ServerEventHandler serverDropEventHandler;   
serverDropEventHandler = new ServerEventHandler(MyDropEventHandler);   
//Subscribe to the second server event handler when a DropTable event occurs.   
db.Events.SubscribeToEvents(databaseDropEventSet, serverDropEventHandler);   
//Start event handling.   
db.Events.StartEvents();   
//Create a table on the database.   
Table tb;   
tb = new Table(db, "Test_Table");   
Column mycol1;   
mycol1 = new Column(tb, "Name", DataType.NChar(50));   
mycol1.Collation = "Latin1_General_CI_AS";   
mycol1.Nullable = true;   
tb.Columns.Add(mycol1);   
tb.Create();   
//Remove the table.   
tb.Drop();   
//Wait until the events have occured.   
int x;   
int y;   
for (x = 1; x <= 1000000000; x++) {   
    y = x * 2;   
}   
//Stop event handling.   
db.Events.StopEvents();   
}  
```  
  
  
