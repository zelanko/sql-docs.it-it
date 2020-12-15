---
description: Gestione di utenti, ruoli e account di accesso
title: Gestione di utenti, ruoli e account di accesso
ms.custom: seo-dt-2019
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- logins [SMO]
- roles [SMO]
- users [SMO]
ms.assetid: 74e411fa-74ed-49ec-ab58-68c250f2280e
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 365d9ef4654ad196f8d43de3b491c6d810d169e8
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97475512"
---
# <a name="managing-users-roles-and-logins"></a>Gestione di utenti, ruoli e account di accesso
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  In SMO gli account di accesso sono rappresentati dall'oggetto <xref:Microsoft.SqlServer.Management.Smo.Login>. Quando l'account di accesso è presente in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], può essere aggiunto a un ruolo del server. Il ruolo del server è rappresentato dall'oggetto <xref:Microsoft.SqlServer.Management.Smo.ServerRole>. Il ruolo del database è rappresentato dall'oggetto <xref:Microsoft.SqlServer.Management.Smo.DatabaseRole>, mentre il ruolo dell'applicazione è rappresentato dall'oggetto <xref:Microsoft.SqlServer.Management.Smo.ApplicationRole>.  
  
 I privilegi associati al livello del server sono elencati come proprietà dell'oggetto <xref:Microsoft.SqlServer.Management.Smo.ServerPermission>. I privilegi al livello del server possono essere concessi, negati o revocati da account di accesso singoli.  
  
 Ogni oggetto <xref:Microsoft.SqlServer.Management.Smo.Database> dispone di un oggetto <xref:Microsoft.SqlServer.Management.Smo.UserCollection> che specifica tutti gli utenti del database. Ogni utente è associato a un accesso. Un accesso può essere associato agli utenti di più database. Il metodo <xref:Microsoft.SqlServer.Management.Smo.Login> dell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Login.EnumDatabaseMappings%2A> può essere utilizzato per elencare tutti gli utenti di ogni database associato all'accesso. In alternativa, la proprietà <xref:Microsoft.SqlServer.Management.Smo.User> dell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Login> specifica l'accesso associato all'utente.  
  
 I database [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] dispongono anche di ruoli che specificano un set di privilegi al livello del database che consentono a un utente di eseguire attività specifiche. A differenza dei ruoli del server, i ruoli del database non sono fissi, ma possono essere creati, modificati e rimossi. Privilegi e utenti possono essere assegnati a un ruolo del database per l'amministrazione bulk.  
  
## <a name="example"></a>Esempio  
 Per gli esempi di codice seguenti, è necessario selezionare l'ambiente, il modello e il linguaggio di programmazione per la creazione dell'applicazione. Per altre informazioni, vedere [creare un progetto Visual C&#35; SMO in Visual Studio .NET](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="enumerating-logins-and-associated-users-in-visual-c"></a>Enumerazione di account di accesso e utenti associati in Visual C#  
 A ogni utente di un database è associato un account di accesso. L'account di accesso può essere associato a utenti di più database. Nell'esempio di codice viene illustrato come chiamare il metodo <xref:Microsoft.SqlServer.Management.Smo.Login.EnumDatabaseMappings%2A> dell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Login> per ottenere un elenco di tutti gli utenti del database associati all'accesso. Nell'esempio vengono creati un accesso e un utente nel database di [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] per garantire la presenza di informazioni di mapping da enumerare.  
  
```csharp  
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
  
```powershell  
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
 In questo esempio viene illustrato come gestire ruoli e utenti. Per eseguire questo esempio, sarà necessario fare riferimento agli assembly seguenti:  
  
-   Microsoft.SqlServer.Smo.dll  
  
-   Microsoft.SqlServer.Management.Sdk.Sfc.dll  
  
-   Microsoft.SqlServer.ConnectionInfo.dll  
  
-   Microsoft.SqlServer.SqlEnum.dll  
  
```csharp  
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
  
  
