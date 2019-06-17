---
title: Disconnessione da un'istanza di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, disconnecting
- SMO [SQL Server], disconnecting
- instances of SQL Server, disconnecting
- disconnecting [SMO]
ms.assetid: 4ca7f7eb-6b3f-4c73-ac63-88afa8570b61
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7783fa93912c305403cc34ad6e52668123d164ed
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63192070"
---
# <a name="disconnecting-from-an-instance-of-sql-server"></a>Disconnessione da un'istanza di SQL Server
  Non è richiesta la chiusura e la disconnessione manuale degli oggetti SMO ( [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects). Le connessioni vengono aperte e chiuse in base alle necessità.  
  
## <a name="connection-pooling"></a>Pool di connessioni  
 Quando viene chiamato il metodo <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Connect%2A>, la connessione non viene rilasciata automaticamente. Per rilasciare la connessione nel pool di connessioni, è necessario che il metodo <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Disconnect%2A> venga richiamato in modo esplicito. È inoltre possibile richiedere una connessione non in pool. Per eseguire questa operazione, impostare la proprietà <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.NonPooledConnection%2A> della proprietà <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> che fa riferimento all'oggetto <xref:Microsoft.SqlServer.Management.Common.ServerConnection>.  
  
## <a name="disconnecting-from-an-instance-of-sql-server-for-rmo"></a>Disconnessione da un'istanza di SQL Server per RMO  
 La chiusura delle connessioni al server quando si programma con RMO funziona in modo leggermente diverso da SMO.  
  
 Perché la connessione al server per un oggetto RMO viene mantenuta per la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> dell'oggetto, questo oggetto viene anche usato durante la disconnessione da un'istanza di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] quando si programma tramite RMO. Per chiudere una connessione tramite l'oggetto <xref:Microsoft.SqlServer.Management.Common.ServerConnection>, chiamare il metodo <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Disconnect%2A> dell'oggetto RMO. Dopo che è stata chiusa la connessione, gli oggetti RMO non possono essere utilizzati.  
  
## <a name="example"></a>Esempio  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="closing-and-disconnecting-an-smo-object-in-visual-basic"></a>Chiusura e disconnessione di un oggetto SMO in Visual Basic  
 In questo esempio di codice viene illustrato come richiedere una connessione non in pool impostando la proprietà <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.NonPooledConnection%2A> della proprietà dell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A>.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VB4](SMO How to#SMO_VB4)]  -->  
  
## <a name="closing-and-disconnecting-an-smo-object-in-visual-c"></a>Chiusura e disconnessione di un oggetto SMO in Visual C#  
 In questo esempio di codice viene illustrato come richiedere una connessione non in pool impostando la proprietà <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.NonPooledConnection%2A> della proprietà dell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A>.  
  
```  
{   
Server srv;   
srv = new Server();   
//Disable automatic disconnection.   
srv.ConnectionContext.AutoDisconnectMode = AutoDisconnectMode.NoAutoDisconnect;   
//Connect to the local, default instance of SQL Server.   
srv.ConnectionContext.Connect();   
//The actual connection is made when a property is retrieved.   
Console.WriteLine(srv.Information.Version);   
//Disconnect explicitly.   
srv.ConnectionContext.Disconnect();  
}  
```  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.SqlServer.Management.Smo.Server>   
 <xref:Microsoft.SqlServer.Management.Common.ServerConnection>  
  
  
