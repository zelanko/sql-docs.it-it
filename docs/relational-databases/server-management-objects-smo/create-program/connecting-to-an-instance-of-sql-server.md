---
title: Connessione a un'istanza di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, connections
- connections [SMO]
- instances of SQL Server, connections
- SMO [SQL Server], connections
ms.assetid: ad3cf354-b2e3-468b-b986-1232e375fd84
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e2bcbea3415d26de6146609c1493a2c86781bc8b
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: it-IT
ms.lasthandoff: 07/06/2020
ms.locfileid: "86006380"
---
# <a name="connecting-to-an-instance-of-sql-server"></a>Connessione a un'istanza di SQL Server
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  Il primo passaggio di programmazione in un' [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] applicazione SMO (Management Objects) consiste nel creare un'istanza dell' <xref:Microsoft.SqlServer.Management.Smo.Server> oggetto e stabilire la connessione a un'istanza di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 È possibile creare un'istanza dell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Server> e stabilire una connessione all'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in tre modi diversi. Il primo metodo consiste nell'utilizzare una variabile oggetto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> per fornire le informazioni di connessione. Il secondo consiste nel fornire le informazioni di connessione impostando in modo esplicito le proprietà dell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Server>. Il terzo consiste infine nel passare il nome dell'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nel costruttore dell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Server>. 
  
 **Utilizzo di un oggetto ServerConnection**  
  
 Il vantaggio dell'utilizzo della variabile oggetto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> è costituito dal fatto che consente di riutilizzare le informazioni di connessione. Dichiarare una variabile oggetto <xref:Microsoft.SqlServer.Management.Smo.Server>. Dichiarare quindi un oggetto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> e impostare proprietà con le informazioni di connessione, quali il nome dell'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e la modalità di autenticazione. Passare quindi la variabile oggetto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> come parametro al costruttore dell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Server>. Non è consigliabile condividere connessioni tra diversi oggetti server contemporaneamente. Utilizzare il metodo <xref:Microsoft.SqlServer.Management.Common.ServerConnection.Copy%2A> per ottenere una copia delle impostazioni di connessione esistenti.  
  
 **Impostazione esplicita delle proprietà dell'oggetto server**  
  
 In alternativa, è possibile dichiarare la variabile oggetto <xref:Microsoft.SqlServer.Management.Smo.Server> e chiamare il costruttore predefinito. In questo modo, l'oggetto <xref:Microsoft.SqlServer.Management.Smo.Server> tenta di connettersi all'istanza predefinita di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con tutte le impostazioni di connessione predefinite.  
  
 **Definizione del nome dell'istanza di SQL Server nel costruttore dell'oggetto server**  
  
 Dichiarare la variabile oggetto <xref:Microsoft.SqlServer.Management.Smo.Server> e passare il nome dell'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] come parametro di stringa nel costruttore. L'oggetto <xref:Microsoft.SqlServer.Management.Smo.Server> stabilisce una connessione con l'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con le impostazioni di connessione predefinite.  
  
## <a name="connection-pooling"></a>Pool di connessioni  
 Non è in genere necessario chiamare il metodo <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Connect%2A> dell'oggetto <xref:Microsoft.SqlServer.Management.Common.ServerConnection>. SMO stabilirà automaticamente una connessione laddove necessario e rilascerà la connessione al pool di connessioni dopo avere completato l'esecuzione delle operazioni. Quando viene chiamato il metodo <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Connect%2A>, la connessione non viene rilasciata al pool. È necessaria una chiamata esplicita al metodo <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Disconnect%2A> per rilasciare la connessione al pool. È inoltre possibile richiedere una connessione non in pool impostando la proprietà <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.NonPooledConnection%2A> dell'oggetto <xref:Microsoft.SqlServer.Management.Common.ServerConnection>.  
  
## <a name="multithreaded-applications"></a>Applicazioni a thread multipli  
 Per le applicazioni multithreading, in ogni thread è necessario utilizzare un oggetto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> separato.  
  
## <a name="connecting-to-an-instance-of-sql-server-for-rmo"></a>Connessione a un'istanza di SQL Server per RMO  
 RMO (Replication Management Objects) utilizza un metodo leggermente diverso da SMO per connettersi a un server di replica.  
  
 Gli oggetti di programmazione RMO richiedono che venga stabilita una connessione a un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tramite l' <xref:Microsoft.SqlServer.Management.Common.ServerConnection> oggetto implementato dallo spazio dei nomi **Microsoft. SqlServer. Management. Common** . Questa connessione al server viene stabilita indipendentemente da un oggetto di programmazione RMO. La connessione viene quindi passata all'oggetto RMO durante la creazione dell'istanza o tramite l'assegnazione alla proprietà <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> dell'oggetto. In questo modo, un oggetto di programmazione RMO e le istanze dell'oggetto connessione possono essere creati e gestiti separatamente e un singolo oggetto connessione può essere riutilizzato con più oggetti di programmazione RMO. Le regole seguenti sono valide per le connessioni a un server di replica:  
  
-   Tutte le proprietà per la connessione vengono definite per un oggetto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> specificato.  
  
-   Ogni connessione a un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deve disporre del relativo oggetto <xref:Microsoft.SqlServer.Management.Common.ServerConnection>.  
  
-   Tutte le informazioni di autenticazione che consentono di stabilire la connessione e accedere correttamente al server vengono fornite nell'oggetto <xref:Microsoft.SqlServer.Management.Common.ServerConnection>.  
  
-   Per impostazione predefinita, le connessioni vengono stabilite tramite l'autenticazione di Microsoft Windows. Per utilizzare l'autenticazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], la proprietà <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.LoginSecure%2A> deve essere impostata su False e <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.Login%2A> e <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.Password%2A> devono essere impostate su un account di accesso e una password di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] validi. Le credenziali di sicurezza devono essere sempre archiviate e gestite in modo protetto, e fornite in fase di esecuzione laddove possibile.  
  
-   Il metodo <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Connect%2A> deve essere chiamato prima di passare la connessione a qualsiasi oggetto di programmazione RMO.  
  
## <a name="examples"></a>Esempi  
Per usare qualsiasi esempio di codice fornito, è necessario scegliere l'ambiente di programmazione, il modello di programmazione e il linguaggio di programmazione per la creazione dell'applicazione. Per altre informazioni, vedere [creare un progetto Visual C&#35; SMO in Visual Studio .NET](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="connecting-to-the-local-instance-of-sql-server-by-using-windows-authentication-in-visual-basic"></a>Connessione all'istanza locale di SQL Server tramite l'autenticazione di Windows in Visual Basic  
 La connessione all'istanza locale di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] non richiede molto codice, ma si basa al contrario sulle impostazioni predefinite per il metodo di autenticazione e per il server. La prima operazione che richiede il recupero di dati comporterà la creazione di una connessione.  
 
Questo esempio è Visual Basic codice .NET che si connette all'istanza locale di SQL Server usando l'autenticazione di Windows. 

```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'The connection is established when a property is requested.
Console.WriteLine(srv.Information.Version)
'The connection is automatically disconnected when the Server variable goes out of scope.
```
  
## <a name="connecting-to-the-local-instance-of-sql-server-by-using-windows-authentication-in-visual-c"></a>Connessione all'istanza locale di SQL Server tramite l'autenticazione di Windows in Visual C#  
 La connessione all'istanza locale di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] non richiede molto codice, ma si basa al contrario sulle impostazioni predefinite per il metodo di autenticazione e per il server. La prima operazione che richiede il recupero di dati comporterà la creazione di una connessione.  
  
 Questo esempio include il codice Visual C# .NET per la connessione all'istanza locale di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tramite l'autenticazione di Windows.  
  
```csharp  
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//The connection is established when a property is requested.   
Console.WriteLine(srv.Information.Version);   
}   
//The connection is automatically disconnected when the Server variable goes out of scope.  
```  
  
## <a name="connecting-to-a-remote-instance-of-sql-server-by-using-windows-authentication-in-visual-basic"></a>Connessione a un'istanza remota di SQL Server tramite l'autenticazione di Windows in Visual Basic  
 Quando ci si connette a un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tramite l'autenticazione di Windows, non è necessario specificare il tipo di autenticazione. L'autenticazione di Windows rappresenta l'impostazione predefinita.  
  
 Questo esempio è [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] codice .NET che si connette all'istanza remota di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tramite l'autenticazione di Windows. La variabile di stringa *strServer* contiene il nome dell'istanza remota.  
  
```VBNET   
'Connect to a remote instance of SQL Server.
Dim srv As Server
'The strServer string variable contains the name of a remote instance of SQL Server.
srv = New Server(strServer)
'The actual connection is made when a property is retrieved. 
Console.WriteLine(srv.Information.Version)
'The connection is automatically disconnected when the Server variable goes out of scope.
```
  
## <a name="connecting-to-a-remote-instance-of-sql-server-by-using-windows-authentication-in-visual-c"></a>Connessione a un'istanza remota di SQL Server tramite l'autenticazione di Windows in Visual C#  
 Quando ci si connette a un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tramite l'autenticazione di Windows, non è necessario specificare il tipo di autenticazione. L'autenticazione di Windows rappresenta l'impostazione predefinita.  
  
 Questo esempio include il codice Visual C# .NET per la connessione all'istanza remota di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tramite l'autenticazione di Windows. La variabile di stringa *strServer* contiene il nome dell'istanza remota.  
  
```csharp  
{   
//Connect to a remote instance of SQL Server.   
Server srv;   
//The strServer string variable contains the name of a remote instance of SQL Server.   
srv = new Server(strServer);   
//The actual connection is made when a property is retrieved.   
Console.WriteLine(srv.Information.Version);   
}   
//The connection is automatically disconnected when the Server variable goes out of scope.  
```  
  
## <a name="connecting-to-an-instance-of-sql-server-by-using-sql-server-authentication-in-visual-basic"></a>Connessione a un'istanza di SQL Server tramite l'autenticazione di SQL Server in Visual Basic  
 Quando ci si connette a un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tramite l'autenticazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], è necessario specificare il tipo di autenticazione. In questo esempio viene illustrato il metodo alternativo per dichiarare una variabile oggetto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> che consente il riutilizzo delle informazioni di connessione.  
  
 L'esempio è il [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] codice .NET che illustra come connettersi a remote e *mentre oggetto vPassword* contengono l'accesso e la password.  
  
```VBNET  
' compile with:   
' /r:Microsoft.SqlServer.Smo.dll  
' /r:Microsoft.SqlServer.ConnectionInfo.dll  
' /r:Microsoft.SqlServer.Management.Sdk.Sfc.dll   
  
Imports Microsoft.SqlServer.Management.Smo  
Imports Microsoft.SqlServer.Management.Common  
  
Public Class A  
   Public Shared Sub Main()  
      Dim sqlServerLogin As [String] = "user_id"  
      Dim password As [String] = "pwd"  
      Dim instanceName As [String] = "instance_name"  
      Dim remoteSvrName As [String] = "remote_server_name"  
  
      ' Connecting to an instance of SQL Server using SQL Server Authentication  
      Dim srv1 As New Server()   ' connects to default instance  
      srv1.ConnectionContext.LoginSecure = False   ' set to true for Windows Authentication  
      srv1.ConnectionContext.Login = sqlServerLogin  
      srv1.ConnectionContext.Password = password  
      Console.WriteLine(srv1.Information.Version)   ' connection is established  
  
      ' Connecting to a named instance of SQL Server with SQL Server Authentication using ServerConnection  
      Dim srvConn As New ServerConnection()  
      srvConn.ServerInstance = ".\" & instanceName   ' connects to named instance  
      srvConn.LoginSecure = False   ' set to true for Windows Authentication  
      srvConn.Login = sqlServerLogin  
      srvConn.Password = password  
      Dim srv2 As New Server(srvConn)  
      Console.WriteLine(srv2.Information.Version)   ' connection is established  
  
      ' For remote connection, remote server name / ServerInstance needs to be specified  
      Dim srvConn2 As New ServerConnection(remoteSvrName)  
      srvConn2.LoginSecure = False  
      srvConn2.Login = sqlServerLogin  
      srvConn2.Password = password  
      Dim srv3 As New Server(srvConn2)  
      Console.WriteLine(srv3.Information.Version)   ' connection is established  
   End Sub  
End Class  
```  
  
## <a name="connecting-to-an-instance-of-sql-server-by-using-sql-server-authentication-in-visual-c"></a>Connessione a un'istanza di SQL Server tramite l'autenticazione di SQL Server in Visual C#  
 Quando ci si connette a un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tramite l'autenticazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], è necessario specificare il tipo di autenticazione. In questo esempio viene illustrato il metodo alternativo per dichiarare una variabile oggetto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> che consente il riutilizzo delle informazioni di connessione.  
  
 L'esempio è il codice Visual C# .NET che illustra come connettersi a remote e *mentre oggetto vPassword* contengono l'accesso e la password.  
  
```csharp  
// compile with:   
// /r:Microsoft.SqlServer.Smo.dll  
// /r:Microsoft.SqlServer.ConnectionInfo.dll  
// /r:Microsoft.SqlServer.Management.Sdk.Sfc.dll   
  
using System;  
using Microsoft.SqlServer.Management.Smo;  
using Microsoft.SqlServer.Management.Common;  
  
public class A {  
   public static void Main() {   
      String sqlServerLogin = "user_id";  
      String password = "pwd";  
      String instanceName = "instance_name";  
      String remoteSvrName = "remote_server_name";  
  
      // Connecting to an instance of SQL Server using SQL Server Authentication  
      Server srv1 = new Server();   // connects to default instance  
      srv1.ConnectionContext.LoginSecure = false;   // set to true for Windows Authentication  
      srv1.ConnectionContext.Login = sqlServerLogin;  
      srv1.ConnectionContext.Password = password;  
      Console.WriteLine(srv1.Information.Version);   // connection is established  
  
      // Connecting to a named instance of SQL Server with SQL Server Authentication using ServerConnection  
      ServerConnection srvConn = new ServerConnection();  
      srvConn.ServerInstance = @".\" + instanceName;   // connects to named instance  
      srvConn.LoginSecure = false;   // set to true for Windows Authentication  
      srvConn.Login = sqlServerLogin;  
      srvConn.Password = password;  
      Server srv2 = new Server(srvConn);  
      Console.WriteLine(srv2.Information.Version);   // connection is established  
  
      // For remote connection, remote server name / ServerInstance needs to be specified  
      ServerConnection srvConn2 = new ServerConnection(remoteSvrName);  
      srvConn2.LoginSecure = false;  
      srvConn2.Login = sqlServerLogin;  
      srvConn2.Password = password;  
      Server srv3 = new Server(srvConn2);  
      Console.WriteLine(srv3.Information.Version);   // connection is established  
   }  
}  
```  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.SqlServer.Management.Smo.Server>   
 <xref:Microsoft.SqlServer.Management.Common.ServerConnection>  
  
  
