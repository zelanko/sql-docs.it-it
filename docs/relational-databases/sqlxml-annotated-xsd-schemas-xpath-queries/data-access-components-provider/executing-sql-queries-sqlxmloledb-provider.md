---
title: Esecuzione di query SQL (provider SQLXMLOLEDB)
description: Informazioni su come usare le proprietà radice ClientSideXML e XML del provider SQLXMLOLEDB durante l'esecuzione di una query SQL sul lato client.
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- queries [SQLXML], SQLXMLOLEDB Provider
- xml root property [SQLXML]
- SQLXMLOLEDB Provider, executing SQL queries
- SQL queries [SQLXML]
ms.assetid: 50334cf5-9c87-4c00-9beb-e08577c4fa82
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a54a5cc0612a1740be9c6884bcc65c25b16b3fa3
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97467162"
---
# <a name="executing-sql-queries-sqlxmloledb-provider"></a>Esecuzione di query SQL (provider SQLXMLOLEDB)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  In questo esempio viene illustrato l'utilizzo delle proprietà specifiche del provider SQLXMLOLEDB seguenti:  
  
-   ClientSideXML  
  
-   xml root  
  
 In questa applicazione di esempio ADO sul lato client viene eseguita una query SQL semplice sul client. Poiché la proprietà ClientSideXML è impostata su true, l'istruzione SELECT senza la clausola FOR XML viene inviata al server. Il server esegue la query e restituisce un set di righe al client. Il client applica quindi la trasformazione FOR XML al set di righe e produce un documento XML.  
  
 La proprietà radice XML fornisce il singolo elemento radice di primo livello per il documento XML generato.  
  
> [!NOTE]  
>  Nel codice è necessario specificare il nome dell'istanza di Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nella stringa di connessione. In questo esempio viene inoltre specificato l'utilizzo di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (SQLNCLI11) per il provider di dati che richiede l'installazione di un software client di rete aggiuntivo. Per ulteriori informazioni, vedere [requisiti di sistema per SQL Server Native Client](../../../relational-databases/native-client/system-requirements-for-sql-server-native-client.md).  
  
```  
Option Explicit  
Sub main()  
Dim oTestStream As New ADODB.Stream  
Dim oTestConnection As New ADODB.Connection  
Dim oTestCommand As New ADODB.Command  
  
oTestConnection.Open "provider=SQLXMLOLEDB.4.0;data provider=SQLNCLI11;data source=SqlServerName;initial catalog=AdventureWorks;Integrated Security=SSPI ;"  
oTestCommand.ActiveConnection = oTestConnection  
oTestCommand.Properties("ClientSideXML") = True  
oTestCommand.CommandText = "SELECT TOP 10 FirstName, LastName FROM Person.Contact FOR XML AUTO"  
oTestStream.Open  
oTestCommand.Properties("Output Stream").Value = oTestStream  
oTestCommand.Properties("xml root") = "root"  
oTestCommand.Execute , , adExecuteStream  
  
oTestStream.Position = 0  
oTestStream.Charset = "utf-8"  
Debug.Print oTestStream.ReadText(adReadAll)  
End Sub  
Sub Form_Load()  
 main  
End Sub  
```  
  
  
