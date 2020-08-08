---
title: Creazione dei file di connessione del server (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/17/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 829153be-aa8e-4162-87e8-69882feecf19
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: b74cf86e6a68653a2047aebefc7ca86ab6868475
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2020
ms.locfileid: "87933982"
---
# <a name="creating-the-server-connection-files-accesstosql"></a>Creazione dei file di connessione del server (AccessToSQL)
È possibile specificare le informazioni sul server nella sezione server del file script. Le informazioni sul server possono inoltre essere specificate in un file di connessione server separato. Il parametro della riga di comando per il file di connessione del server è `-c <serverconnectionfile>` . Se lo stesso ID server è presente in entrambi i file di connessione script e server, viene considerata la definizione del server nel file di script.  
  
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
  
