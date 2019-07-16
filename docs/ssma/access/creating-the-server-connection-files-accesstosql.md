---
title: Creazione di file di connessione del Server (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/17/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 829153be-aa8e-4162-87e8-69882feecf19
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 03d622c50a8760bbf1767bc8a4f79e215773695f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006612"
---
# <a name="creating-the-server-connection-files-accesstosql"></a>Creazione del server di file di connessione (AccessToSQL)
Informazioni sul server può essere specificato nella sezione dei server del file di script. Informazioni sul server può anche essere specificati in un file di connessione server separato. Il parametro della riga di comando per il file di connessione del server è `-c <serverconnectionfile>`. Se lo stesso id di server è presente nel file di connessione dello script sia nel server, viene considerata la definizione del server nel file di script.  
  
```xml  
<!--Sample of server connection file commands -->  
<!--Connection to SQL Server-->  
  
<sql-server name="target_3">  
  
  <sql-server-authentication>  
  
    <server value="$TargetServerName$"/>  
  
    <database value="$TargetDB$"/>  
  
    <user-id value="$TargetUserName$"/>  
  
    <password value="$TargetPassword$"/>  
  
    <encrypt value="true"/>  
  
    <trust-server-certificate value="true"/>  
  
  </sql-server-authentication>  
  
</sql-server>  
```  
  
```xml  
<!--Connection to SQL Azure-->  
  
<sql-azure name="target_azure">  
  
  <server value="$TargetAzureServerName$"/>  
  
  <database value="$TargetAzureDB$"/>  
  
  <user-id value="$TargetAzureUserName$"/>  
  
  <password value="$TargetAzurePassword$"/>  
  
</sql-azure>  
```  
  
## <a name="server-connection-file-validation"></a>Convalida del file di connessione server  
L'utente può facilmente convalidare il file di connessione del server in base al file di definizione dello schema **'A2SSConsoleScriptServersSchema.xsd'** disponibile nella cartella "Schemi".  
  
## <a name="next-step"></a>Passaggio successivo  
Il passaggio successivo in costi operativi console consiste [esecuzione della Console SSMA &#40;AccessToSQL&#41;](../../ssma/access/executing-the-ssma-console-accesstosql.md)  
  
## <a name="see-also"></a>Vedere anche  
[Esecuzione della Console SSMA (accesso)](https://msdn.microsoft.com/aa1bf665-8dc0-4259-b36f-46ae67197a43)  
  
