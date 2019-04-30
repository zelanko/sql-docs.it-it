---
title: Creazione di file di connessione del Server (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Server Connection File Creation
- Server Connection File, Server Connection File Validation
ms.assetid: 002f129e-0868-48ad-a4b4-c68b5007e12e
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 8f6eabe706197e8ab2bfb882510b6063bf4e884c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63287684"
---
# <a name="creating-the-server-connection-files-oracletosql"></a>Creazione dei file di connessione del server (OracleToSQL)
Nella sezione dei server del file di script o in un file di connessione server separato, è possibile specificare le informazioni sul server. Il parametro della riga di comando per il file di connessione del server è, `-c <serverconnectionfile>`. Se lo stesso id di server è presente nel file di connessione server sia file di script, viene considerata la definizione del server nel file di script.  
  
**Esempio: 1**  
  
```  
<!--Sample of server connection file commands -->  
  
<oracle name="<source-server-unique-name>">  
  
  <tns-name-mode>  
  
    <connection-provider value="OracleClient"/>  
  
    <service-name value="(DESCRIPTION =(ADDRESS_LIST =(ADDRESS = (PROTOCOL = TCP)(HOST = <host-name>)(PORT = 1521)))(CONNECT_DATA =(SERVICE_NAME = <service-name>)))"/>  
  
    <user-id value="<user-name>"/>  
  
    <password value="<password>"/>  
  
  </tns-name-mode>  
  
</oracle>  
```  
  
```  
<sql-server name="<target-server-unique-name>">  
  
  <sql-server-authentication>  
  
    <server value="<server-name>"/>  
  
    <database value="<database-name>"/>  
  
    <user-id value="<user-name>"/>  
  
    <password value="<password>"/>  
  
    <encrypt value="<true/false>"/>  
  
    <trust-server-certificate value="<true/false>"/>  
  
  </sql-server-authentication>  
  
</sql-server>  
```  
**Esempio: 2**  
  
```  
<!--Sample of server connection file commands -->  
  
<oracle name="<source-server-unique-name>">  
  
  <connection-string-mode>  
  
    <connection-provider value="OleDB Provider"/>  
  
    <custom-connection-string value="Data Source=(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=<host-name>)(PORT=1521))(CONNECT_DATA=(SID=<instance-name>)));User ID=<user-name>;Password=<password>"/>  
  
  </connection-string-mode>  
  
</oracle>  
```  
  
```  
<sql-server name="<target-server-unique-name>">  
  
  <sql-server-authentication>  
  
    <server value="<server-name>"/>  
  
    <database value="<database-name>"/>  
  
    <user-id value="<user-name>"/>  
  
    <password value="<password>"/>  
  
  </sql-server-authentication>  
  
</sql-server>  
```  
  
## <a name="next-step"></a>Passaggio successivo  
Il passaggio successivo in costi operativi console consiste [esecuzione della Console SSMA &#40;OracleToSQL&#41;](../../ssma/oracle/executing-the-ssma-console-oracletosql.md)  
  
## <a name="see-also"></a>Vedere anche  
[Esecuzione della console SSMA](executing-the-ssma-console-oracletosql.md)  
  
