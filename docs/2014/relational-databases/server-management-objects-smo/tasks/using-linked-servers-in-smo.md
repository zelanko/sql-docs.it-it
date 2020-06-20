---
title: Utilizzo di server collegati in SMO | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- linked servers [SQL Server], SMO
ms.assetid: 0ea8837b-2596-4df1-b065-3bb717c9f22c
author: stevestein
ms.author: sstein
ms.openlocfilehash: 67bb9f002356e94f2546527aacae13b56768930d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85003533"
---
# <a name="using-linked-servers-in-smo"></a>Utilizzo di server collegati in SMO
  Un server collegato rappresenta un'origine dati OLE DB in un server remoto. Le origini dati OLE DB remote vengono collegate all'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tramite l'oggetto <xref:Microsoft.SqlServer.Management.Smo.LinkedServer>.  
  
 I server di database remoti possono essere collegati all'istanza corrente di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tramite un provider OLE DB. In SMO i server collegati sono rappresentati dall'oggetto <xref:Microsoft.SqlServer.Management.Smo.LinkedServer>. La proprietà <xref:Microsoft.SqlServer.Management.Smo.LinkedServer.LinkedServerLogins%2A> fa riferimento a una raccolta di oggetti <xref:Microsoft.SqlServer.Management.Smo.LinkedServerLogin> in cui sono archiviate le credenziali di accesso necessarie per stabilire una connessione con il server collegato.  
  
## <a name="ole-db-providers"></a>Provider OLE DB  
 In SMO i provider OLE DB installati sono rappresentati da una raccolta di oggetti <xref:Microsoft.SqlServer.Management.Smo.OleDbProviderSettings>.  
  
## <a name="example"></a>Esempio  
 Per l'esempio di codice seguente, è necessario selezionare l'ambiente, il modello e il linguaggio di programmazione per la creazione dell'applicazione. Per ulteriori informazioni, vedere la pagina relativa alla [creazione di un progetto Visual Basic SMO in Visual Studio .NET](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) e alla [creazione di un progetto Visual C&#35; SMO in Visual Studio .NET](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-a-link-to-an-ole-db-provider-server-in-visual-basic"></a>Creazione di un collegamento a un server del provider OLE DB in Visual Basic  
 Nell'esempio di codice viene illustrato come creare un collegamento a un'origine dati [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] OLE DB eterogenea tramite l'oggetto <xref:Microsoft.SqlServer.Management.Smo.LinkedServer>. Specificando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] come nome del prodotto, è possibile accedere ai dati nel server collegato utilizzando il [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provider OLE DB client, che è il provider OLE DB ufficiale per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBLinkedServers1](SMO How to#SMO_VBLinkedServers1)]  -->  
  
## <a name="creating-a-link-to-an-ole-db-provider-server-in-visual-c"></a>Creazione di un collegamento a un server del provider OLE DB in Visual C#  
 Nell'esempio di codice viene illustrato come creare un collegamento a un'origine dati [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] OLE DB eterogenea tramite l'oggetto <xref:Microsoft.SqlServer.Management.Smo.LinkedServer>. Specificando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] come nome di prodotto, è possibile accedere ai dati nel server collegato tramite il provider OLE DB di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Client, ovvero il provider OLE DB ufficiale per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
```csharp
//Connect to the local, default instance of SQL Server.   
{   
   Server srv = new Server();   
   //Create a linked server.   
   LinkedServer lsrv = default(LinkedServer);   
   lsrv = new LinkedServer(srv, "OLEDBSRV");   
   //When the product name is SQL Server the remaining properties are   
   //not required to be set.   
   lsrv.ProductName = "SQL Server";   
   lsrv.Create();   
}   
```  
  
## <a name="creating-a-link-to-an-ole-db-provider-server-in-powershell"></a>Creazione di un collegamento a un server del provider OLE DB in PowerShell  
 Nell'esempio di codice viene illustrato come creare un collegamento a un'origine dati [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] OLE DB eterogenea tramite l'oggetto <xref:Microsoft.SqlServer.Management.Smo.LinkedServer>. Specificando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] come nome di prodotto, è possibile accedere ai dati nel server collegato tramite il provider OLE DB di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Client, ovvero il provider OLE DB ufficiale per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
```powershell
#Get a server object which corresponds to the default instance  
$svr = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
  
#Create a linked server object which corresponds to an OLEDB type of SQL server product  
$lsvr = New-Object -TypeName Microsoft.SqlServer.Management.SMO.LinkedServer -ArgumentList $svr,"OLEDBSRV"  
  
#When the product name is SQL Server the remaining properties are not required to be set.
$lsvr.ProductName = "SQL Server"
  
#Create the Database Object  
$lsvr.Create()
```  
