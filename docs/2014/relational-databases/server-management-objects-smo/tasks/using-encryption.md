---
title: Uso della crittografia | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- database master key [SMO]
- cryptography [SMO]
- cryptography [SQL Server], SMO
- encryption keys [SMO]
- encryption [SQL Server], SMO
- encryption [SMO]
- certificates [SMO]
- service master key [SMO]
ms.assetid: 405e0ed7-50a9-430e-a343-471f54b4af76
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 233f5bc9decf5e8246f2aba6836ec5ecb650283b
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/22/2019
ms.locfileid: "72781852"
---
# <a name="using-encryption"></a>Uso della crittografia
  In SMO la chiave master del servizio è rappresentata dall'oggetto <xref:Microsoft.SqlServer.Management.Smo.ServiceMasterKey>. A questo oggetto fa riferimento la proprietà <xref:Microsoft.SqlServer.Management.Smo.Server.ServiceMasterKey%2A> dell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Server>. La chiave può essere rigenerata tramite il metodo <xref:Microsoft.SqlServer.Management.Smo.ServiceMasterKey.Regenerate%2A>.  
  
 La chiave master del database è rappresentata dall'oggetto <xref:Microsoft.SqlServer.Management.Smo.MasterKey>. La proprietà <xref:Microsoft.SqlServer.Management.Smo.MasterKey.IsEncryptedByServer%2A> indica se la chiave master del database viene crittografata o meno tramite la chiave master del servizio. La copia crittografata nel database master viene aggiornata automaticamente ogni volta che viene modificata la chiave master del database.  
  
 È possibile eliminare la crittografia della chiave del servizio utilizzando il metodo <xref:Microsoft.SqlServer.Management.Smo.MasterKey.DropServiceKeyEncryption%2A> e crittografare la chiave master del database con una password. In questo caso sarà necessario aprire in modo esplicito la chiave master del database prima di accedere a chiavi private protette dalla chiave master.  
  
 Quando un database viene allegato a un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], è necessario fornire la password per la chiave master del database oppure eseguire il metodo <xref:Microsoft.SqlServer.Management.Smo.MasterKey.AddServiceKeyEncryption%2A> per eseguire una copia non crittografata della chiave master del database disponibile per la crittografia con la chiave master del servizio. Si consiglia di eseguire questo passaggio per evitare la necessità di aprire in modo esplicito la chiave master del database.  
  
 Il metodo <xref:Microsoft.SqlServer.Management.Smo.MasterKey.Regenerate%2A> rigenera la chiave master del database. In seguito alla rigenerazione della chiave master del database, tutte le chiavi crittografate con tale chiave vengono decrittografate e successivamente crittografate con la nuova chiave master del database. Il metodo <xref:Microsoft.SqlServer.Management.Smo.MasterKey.DropServiceKeyEncryption%2A> rimuove l'impostazione per la crittografia della chiave master del database tramite la chiave master del servizio. <xref:Microsoft.SqlServer.Management.Smo.MasterKey.AddServiceKeyEncryption%2A> con una copia della chiave master viene crittografata utilizzando la chiave master del servizio e archiviata sia nel database corrente che nel database master.  
  
 In SMO i certificati sono rappresentati dall'oggetto <xref:Microsoft.SqlServer.Management.Smo.Certificate>. L'oggetto <xref:Microsoft.SqlServer.Management.Smo.Certificate> dispone di proprietà che specificano la chiave pubblica, il nome dell'oggetto, il periodo di validità e le informazioni sull'autorità emittente. L'autorizzazione per l'accesso al certificato è controllata tramite i metodi `Grant`, `Revoke` e `Deny`.  
  
## <a name="example"></a>Esempio  
 Per l'esempio di codice seguente, è necessario selezionare l'ambiente, il modello e il linguaggio di programmazione per la creazione dell'applicazione. Per ulteriori informazioni, vedere la pagina relativa alla [creazione di un progetto Visual Basic SMO in Visual Studio .NET](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) e alla [creazione di un progetto Visual C&#35; SMO in Visual Studio .NET](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="adding-a-certificate-in-visual-basic"></a>Aggiunta di un certificato in Visual Basic  
 Nell'esempio di codice viene creato un certificato semplice con una password di crittografia. A differenza di altri oggetti, il metodo <xref:Microsoft.SqlServer.Management.Smo.Certificate.Create%2A> dispone di diversi overload. L'overload utilizzato nell'esempio crea un nuovo certificato con una password di crittografia.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBCertificate1](SMO How to#SMO_VBCertificate1)]  -->  
  
## <a name="adding-a-certificate-in-visual-c"></a>Aggiunta di un certificato in Visual C#  
 Nell'esempio di codice viene creato un certificato semplice con una password di crittografia. A differenza di altri oggetti, il metodo <xref:Microsoft.SqlServer.Management.Smo.Certificate.Create%2A> dispone di diversi overload. L'overload utilizzato nell'esempio crea un nuovo certificato con una password di crittografia.  
  
```csharp
{  
            //Connect to the local, default instance of SQL Server.   
            {  
                Server srv = new Server();  
  
                //Reference the AdventureWorks2012 database.   
                Database db = srv.Databases["AdventureWorks2012"];  
  
                //Define a Certificate object variable by supplying the parent database and name in the constructor.   
                Certificate c = new Certificate(db, "Test_Certificate");  
  
                //Set the start date, expiry date, and description.   
                System.DateTime dt;  
                DateTime.TryParse("January 01, 2010", out dt);  
                c.StartDate = dt;  
                DateTime.TryParse("January 01, 2015", out dt);  
                c.ExpirationDate = dt;  
                c.Subject = "This is a test certificate.";  
                //Create the certificate on the instance of SQL Server by supplying the certificate password argument.   
                c.Create("pGFD4bb925DGvbd2439587y");  
            }  
        }   
```  
  
## <a name="adding-a-certificate-in-powershell"></a>Aggiunta di un certificato in PowerShell  
 Nell'esempio di codice viene creato un certificato semplice con una password di crittografia. A differenza di altri oggetti, il metodo <xref:Microsoft.SqlServer.Management.Smo.Certificate.Create%2A> dispone di diversi overload. L'overload utilizzato nell'esempio crea un nuovo certificato con una password di crittografia.  
  
```powershell
# Set the path context to the local, default instance of SQL Server and get a reference to AdventureWorks2012  
CD \sql\localhost\default\databases  
$db = get-item AdventureWorks2012  
  
#Create a certificate
$c = New-Object -TypeName Microsoft.SqlServer.Management.Smo.Certificate -ArgumentList $db, "Test_Certificate"  
$c.StartDate = "January 01, 2010"  
$c.Subject = "This is a test certificate."  
$c.ExpirationDate = "January 01, 2015"  
  
#Create the certificate on the instance of SQL Server by supplying the certificate password argument.  
$c.Create("pGFD4bb925DGvbd2439587y")
```  
  
## <a name="see-also"></a>Vedere anche  
 [Uso delle chiavi di crittografia](using-encryption.md)  
