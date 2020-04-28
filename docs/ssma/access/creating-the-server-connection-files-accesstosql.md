---
title: Creazione dei file di connessione del server (AccessToSQL) | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68006612"
---
# <a name="creating-the-server-connection-files-accesstosql"></a>Creazione dei file di connessione del server (AccessToSQL)
È possibile specificare le informazioni sul server nella sezione server del file script. Le informazioni sul server possono inoltre essere specificate in un file di connessione server separato. Il parametro della riga di comando per il file di `-c <serverconnectionfile>`connessione del server è. Se lo stesso ID server è presente in entrambi i file di connessione script e server, viene considerata la definizione del server nel file di script.  
  
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
  
## <a name="server-connection-file-validation"></a>Convalida file di connessione server  
L'utente può convalidare facilmente il file di connessione del server con il file di definizione dello schema **' A2SSConsoleScriptServersSchema. xsd '** disponibile nella cartella ' schemi '.  
  
## <a name="next-step"></a>Passaggio successivo  
Il passaggio successivo per la gestione della console è [l'esecuzione della console SSMA &#40;AccessToSQL&#41;](../../ssma/access/executing-the-ssma-console-accesstosql.md)  
  
## <a name="see-also"></a>Vedere anche  
[Esecuzione della console SSMA (accesso)](https://msdn.microsoft.com/aa1bf665-8dc0-4259-b36f-46ae67197a43)  
  
