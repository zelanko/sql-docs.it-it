---
title: Gestione di utenti, ruoli e gli account di accesso | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- logins [SMO]
- roles [SMO]
- users [SMO]
ms.assetid: 74e411fa-74ed-49ec-ab58-68c250f2280e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9bac188dcc6eb26c1bca77ec292a096f4eac2f35
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63226183"
---
# <a name="managing-users-roles-and-logins"></a>Gestione di utenti, ruoli e account di accesso
  In SMO gli account di accesso sono rappresentati dall'oggetto <xref:Microsoft.SqlServer.Management.Smo.Login>. Quando l'account di accesso è presente in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], può essere aggiunto a un ruolo del server. Il ruolo del server è rappresentato dall'oggetto <xref:Microsoft.SqlServer.Management.Smo.ServerRole>. Il ruolo del database è rappresentato dall'oggetto <xref:Microsoft.SqlServer.Management.Smo.DatabaseRole>, mentre il ruolo dell'applicazione è rappresentato dall'oggetto <xref:Microsoft.SqlServer.Management.Smo.ApplicationRole>.  
  
 I privilegi associati al livello del server sono elencati come proprietà dell'oggetto <xref:Microsoft.SqlServer.Management.Smo.ServerPermission>. I privilegi al livello del server possono essere concessi, negati o revocati da account di accesso singoli.  
  
 Ogni oggetto <xref:Microsoft.SqlServer.Management.Smo.Database> dispone di un oggetto <xref:Microsoft.SqlServer.Management.Smo.UserCollection> che specifica tutti gli utenti del database. Ogni utente è associato a un accesso. Un accesso può essere associato agli utenti di più database. Il metodo <xref:Microsoft.SqlServer.Management.Smo.Login> dell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Login.EnumDatabaseMappings%2A> può essere utilizzato per elencare tutti gli utenti di ogni database associato all'accesso. In alternativa, la proprietà <xref:Microsoft.SqlServer.Management.Smo.User> dell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Login> specifica l'accesso associato all'utente.  
  
 I database [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] dispongono anche di ruoli che specificano un set di privilegi al livello del database che consentono a un utente di eseguire attività specifiche. A differenza dei ruoli del server, i ruoli del database non sono fissi, ma possono essere creati, modificati e rimossi. Privilegi e utenti possono essere assegnati a un ruolo del database per l'amministrazione bulk.  
  
## <a name="example"></a>Esempio  
 Per l'esempio di codice seguente, è necessario selezionare l'ambiente, il modello e il linguaggio di programmazione per la creazione dell'applicazione. Per altre informazioni, vedere [creare un progetto Visual Basic SMO in Visual Studio .NET](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) e [creare un Visual C#&#35; progetto SMO in Visual Studio .NET](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="enumerating-logins-and-associated-users-in-visual-basic"></a>Enumerazione di account di accesso e utenti associati in Visual Basic  
 A ogni utente di un database è associato un account di accesso. L'account di accesso può essere associato a utenti di più database. Nell'esempio di codice viene illustrato come chiamare il metodo <xref:Microsoft.SqlServer.Management.Smo.Login.EnumDatabaseMappings%2A> dell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Login> per ottenere un elenco di tutti gli utenti del database associati all'accesso. Nell'esempio vengono creati un accesso e un utente nel database di [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] per garantire la presenza di informazioni di mapping da enumerare.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBLogins1](SMO How to#SMO_VBLogins1)]  -->  
  
## <a name="enumerating-logins-and-associated-users-in-visual-c"></a>Enumerazione di account di accesso e utenti associati in Visual C#  
 A ogni utente di un database è associato un account di accesso. L'account di accesso può essere associato a utenti di più database. Nell'esempio di codice viene illustrato come chiamare il metodo <xref:Microsoft.SqlServer.Management.Smo.Login.EnumDatabaseMappings%2A> dell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Login> per ottenere un elenco di tutti gli utenti del database associati all'accesso. Nell'esempio vengono creati un accesso e un utente nel database di [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] per garantire la presenza di informazioni di mapping da enumerare.  
  
```  
{   
Server srv = new Server();   
//Iterate through each database and display.   
  
foreach ( Database db in srv.Databases) {   
   Console.WriteLine("========");   
   Console.WriteLine("Login Mappings for the database: " + db.Name);   
   Console.WriteLine(" ");   
   //Run the EnumLoginMappings method and return details of database user-login mappings to a DataTable object variable.   
   DataTable d;  
   d = db.EnumLoginMappings();   
   //Display the mapping information.   
   foreach (DataRow r in d.Rows) {   
      foreach (DataColumn c in r.Table.Columns) {   
         Console.WriteLine(c.ColumnName + " = " + r[c]);   
      }   
      Console.WriteLine(" ");   
   }   
}   
}  
```  
  
## <a name="enumerating-logins-and-associated-users-in-powershell"></a>Enumerazione di account di accesso e utenti associati in PowerShell  
 A ogni utente di un database è associato un account di accesso. L'account di accesso può essere associato a utenti di più database. Nell'esempio di codice viene illustrato come chiamare il metodo <xref:Microsoft.SqlServer.Management.Smo.Login.EnumDatabaseMappings%2A> dell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Login> per ottenere un elenco di tutti gli utenti del database associati all'accesso. Nell'esempio vengono creati un accesso e un utente nel database di [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] per garantire la presenza di informazioni di mapping da enumerare.  
  
```  
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\Default\Databases  
  
#Iterate through all databases  
 foreach ($db in Get-ChildItem)  
 {  
 "====="  
 "Login Mappings for the database: "+ $db.Name  
  
 #get the datatable containing the mapping from the smo database oject  
 $dt = $db.EnumLoginMappings()  
  
 #display the results  
 foreach($row in $dt.Rows)  
     {  
        foreach($col in $row.Table.Columns)  
      {  
        $col.ColumnName + "=" + $row[$col]  
       }  
  
     }  
 }  
```  
  
## <a name="managing-roles-and-users"></a>Gestione di ruoli e utenti  
 In questo esempio viene illustrato come gestire ruoli e utenti. Nel primo esempio viene utilizzato C#, nel secondo Visual Basic. Per questi esempi è necessario un riferimento ai seguenti assembly:  
  
-   Microsoft.SqlServer.Smo.dll  
  
-   Microsoft.SqlServer.Management.Sdk.Sfc.dll  
  
-   Microsoft.SqlServer.ConnectionInfo.dll  
  
-   Microsoft.SqlServer.SqlEnum.dll  
  
```  
using Microsoft.SqlServer.Management.Smo;  
using System;  
  
public class A {  
   public static void Main() {  
      Server svr = new Server();  
      Database db = new Database(svr, "TESTDB");  
      db.Create();  
  
      // Creating Logins  
      Login login = new Login(svr, "Login1");  
      login.LoginType = LoginType.SqlLogin;  
      login.Create("password@1");  
  
      Login login2 = new Login(svr, "Login2");  
      login2.LoginType = LoginType.SqlLogin;  
      login2.Create("password@1");  
  
      // Creating Users in the database for the logins created  
      User user1 = new User(db, "User1");  
      user1.Login = "Login1";  
      user1.Create();  
  
      User user2 = new User(db, "User2");  
      user2.Login = "Login2";  
      user2.Create();  
  
      // Creating database permission Sets  
      DatabasePermissionSet dbPermSet = new DatabasePermissionSet(DatabasePermission.AlterAnySchema);  
      dbPermSet.Add(DatabasePermission.AlterAnyUser);  
  
      DatabasePermissionSet dbPermSet2 = new DatabasePermissionSet(DatabasePermission.CreateType);  
      dbPermSet2.Add(DatabasePermission.CreateSchema);  
      dbPermSet2.Add(DatabasePermission.CreateTable);  
  
      // Creating Database roles  
      DatabaseRole role1 = new DatabaseRole(db, "Role1");  
      role1.Create();  
  
      DatabaseRole role2 = new DatabaseRole(db, "Role2");  
      role2.Create();  
  
      // Granting Database Permission Sets to Roles  
      db.Grant(dbPermSet, role1.Name);  
      db.Grant(dbPermSet2, role2.Name);  
  
      // Adding members (Users / Roles) to Role  
      role1.AddMember("User1");  
  
      role2.AddMember("User2");  
  
      // Role1 becomes a member of Role2  
      role2.AddMember("Role1");  
  
      // Enumerating through explicit permissions granted to Role1  
      // enumerates all database permissions for the Grantee  
      DatabasePermissionInfo[] dbPermsRole1 = db.EnumDatabasePermissions("Role1");     
      foreach (DatabasePermissionInfo dbp in dbPermsRole1) {  
         Console.WriteLine(dbp.Grantee + " has " + dbp.PermissionType.ToString() + " permission.");  
      }  
      Console.WriteLine(" ");  
   }  
}  
```  
  
 Versione Visual Basic:  
  
```  
Imports Microsoft.SqlServer.Management.Smo  
  
Public Class A  
   Public Shared Sub Main()  
      Dim svr As New Server()  
      Dim db As New Database(svr, "TESTDB")  
      db.Create()  
  
      ' Creating Logins  
      Dim login As New Login(svr, "Login1")  
      login.LoginType = LoginType.SqlLogin  
      login.Create("password@1")  
  
      Dim login2 As New Login(svr, "Login2")  
      login2.LoginType = LoginType.SqlLogin  
      login2.Create("password@1")  
  
      ' Creating Users in the database for the logins created  
      Dim user1 As New User(db, "User1")  
      user1.Login = "Login1"  
      user1.Create()  
  
      Dim user2 As New User(db, "User2")  
      user2.Login = "Login2"  
      user2.Create()  
  
      ' Creating database permission Sets  
      Dim dbPermSet As New DatabasePermissionSet(DatabasePermission.AlterAnySchema)  
      dbPermSet.Add(DatabasePermission.AlterAnyUser)  
  
      Dim dbPermSet2 As New DatabasePermissionSet(DatabasePermission.CreateType)  
      dbPermSet2.Add(DatabasePermission.CreateSchema)  
      dbPermSet2.Add(DatabasePermission.CreateTable)  
  
      ' Creating Database roles  
      Dim role1 As New DatabaseRole(db, "Role1")  
      role1.Create()  
  
      Dim role2 As New DatabaseRole(db, "Role2")  
      role2.Create()  
  
      ' Granting Database Permission Sets to Roles  
      db.Grant(dbPermSet, role1.Name)  
      db.Grant(dbPermSet2, role2.Name)  
  
      ' Adding members (Users / Roles) to Role  
      role1.AddMember("User1")  
  
      role2.AddMember("User2")  
  
      ' Role1 becomes a member of Role2  
      role2.AddMember("Role1")  
  
      ' Enumerating through explicit permissions granted to Role1  
      ' enumerates all database permissions for the Grantee  
      Dim dbPermsRole1 As DatabasePermissionInfo() = db.EnumDatabasePermissions("Role1")  
      For Each dbp As DatabasePermissionInfo In dbPermsRole1  
         Console.WriteLine(dbp.Grantee + " has " & dbp.PermissionType.ToString() & " permission.")  
      Next  
      Console.WriteLine(" ")  
   End Sub  
End Class  
```  
  
  
