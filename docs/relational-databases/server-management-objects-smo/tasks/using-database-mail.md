---
title: Tramite posta elettronica Database | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- e-mail [SMO]
- Database Mail [SMO]
- mail [SMO]
ms.assetid: 7605390f-b485-48cc-8d97-e364a066067b
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1c1b91f8c1d8f032516a7b2e04a8533f4b792b3b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68030056"
---
# <a name="using-database-mail"></a>Utilizzo di Posta elettronica database
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  In SMO il sottosistema Posta elettronica database è rappresentato dall'oggetto <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> a cui fa riferimento la proprietà <xref:Microsoft.SqlServer.Management.Smo.Server.Mail%2A>. Tramite l'oggetto <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> SMO, è possibile configurare il sottosistema Posta elettronica database e gestire profili e account di posta elettronica. SMO <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> appartiene l'oggetto di **Server** oggetto, vale a dire che l'ambito degli account di posta elettronica è a livello di server.  
  
## <a name="examples"></a>Esempi  
 Per usare qualsiasi esempio di codice fornito, è necessario scegliere l'ambiente di programmazione, il modello di programmazione e il linguaggio di programmazione per la creazione dell'applicazione. Per altre informazioni, vedere [creare un Visual C&#35; progetto SMO in Visual Studio .NET](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
 Per i programmi che usano [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] posta elettronica Database, è necessario includere il **importazioni** istruzione per qualificare lo spazio dei nomi di posta elettronica. Inserire l'istruzione dopo le altre istruzioni **Imports** , ma prima di qualsiasi dichiarazione nell'applicazione, ad esempio:  
  
 `Imports Microsoft.SqlServer.Management.Smo`  
  
 `Imports Microsoft.SqlServer.Management.Common`  
  
 `Imports Microsoft.SqlServer.Management.Smo.Mail`  
  
## <a name="creating-a-database-mail-account-by-using-visual-basic"></a>Creazione di un account di Posta elettronica database tramite Visual Basic  
 In questo esempio di codice viene illustrato come creare un account di posta elettronica in SMO. Il sistema Posta elettronica database è rappresentato dall'oggetto <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> e la proprietà <xref:Microsoft.SqlServer.Management.Smo.Server.Mail%2A> dell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Server> fa riferimento ad esso. È possibile utilizzare SMO per configurare Posta elettronica database a livello di codice, ma non per inviare o gestire i messaggi di posta elettronica ricevuti.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server()
'Define the Database Mail service with a SqlMail object variable and reference it using the Server Mail property.
Dim sm As SqlMail
sm = srv.Mail
'Define and create a mail account by supplying the Database Mail service, name, description, display name, and email address arguments in the constructor.
Dim a As MailAccount
a = New MailAccount(sm, "AdventureWorks Administrator", "AdventureWorks Automated Mailer", "Mail account for administrative e-mail.", "dba@Adventure-Works.com")
a.Create()
```
  
## <a name="creating-a-database-mail-account-by-using-visual-c"></a>Creazione di un account di Posta elettronica database tramite Visual C#  
 In questo esempio di codice viene illustrato come creare un account di posta elettronica in SMO. Il sistema Posta elettronica database è rappresentato dall'oggetto <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> e la proprietà <xref:Microsoft.SqlServer.Management.Smo.Server.Mail%2A> dell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Server> fa riferimento ad esso. È possibile utilizzare SMO per configurare Posta elettronica database a livello di codice, ma non per inviare o gestire i messaggi di posta elettronica ricevuti.  
  
```csharp  
{  
         //Connect to the local, default instance of SQL Server.  
         Server srv = default(Server);   
           srv = new Server();   
           //Define the Database Mail service with a SqlMail object variable   
           //and reference it using the Server Mail property.   
           SqlMail sm;   
           sm = srv.Mail;   
           //Define and create a mail account by supplying the Database Mail  
           //service, name, description, display name, and email address  
           //arguments in the constructor.   
           MailAccount a = default(MailAccount);   
           a = new MailAccount(sm, "AdventureWorks2012 Administrator", "AdventureWorks2012 Automated Mailer", "Mail account for administrative e-mail.", "dba@Adventure-Works.com");   
           a.Create();    
}  
```  
  
## <a name="creating-a-database-mail-account-by-using-powershell"></a>Creazione di un account di Posta elettronica database tramite PowerShell  
 In questo esempio di codice viene illustrato come creare un account di posta elettronica in SMO. Il sistema Posta elettronica database è rappresentato dall'oggetto <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> e la proprietà <xref:Microsoft.SqlServer.Management.Smo.Server.Mail%2A> dell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Server> fa riferimento ad esso. È possibile utilizzare SMO per configurare Posta elettronica database a livello di codice, ma non per inviare o gestire i messaggi di posta elettronica ricevuti.  
  
  
  
```powershell  
#Connect to the local, default instance of SQL Server.  
  
#Get a server object which corresponds to the default instance  
$srv = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
  
#Define the Database Mail; reference it using the Server Mail property.  
$sm = $srv.Mail  
  
#Define and create a mail account by supplying the Database Mail service,  
#name, description, display name, and email address arguments in the constructor.  
$a = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Mail.MailAccount -argumentlist $sm, `  
"Adventure Works Administrator", "Adventure Works Automated Mailer",`  
 "Mail account for administrative e-mail.", "dba@Adventure-Works.com"  
$a.Create()  
```  
  
  
