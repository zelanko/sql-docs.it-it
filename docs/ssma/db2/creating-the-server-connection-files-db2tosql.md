---
description: Creazione dei file di connessione del server (DB2ToSQL)
title: Creazione dei file di connessione del server (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 07/14/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 685419f6-8606-462c-be12-8bace45bede6
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 754f9002dd5b9e8f9111dce59bc81417c704e40d
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/13/2020
ms.locfileid: "91984917"
---
# <a name="creating-the-server-connection-files-db2tosql"></a>Creazione dei file di connessione del server (DB2ToSQL)

È possibile specificare le informazioni sul server nella sezione server del file script o in un file di connessione server separato. Il parametro della riga di comando per il file di connessione del server è, `-c <serverconnectionfile>` . Se lo stesso ID server è presente nel file di script e nel file di connessione al server, viene considerata la definizione del server nel file di script.

**Esempio: 1**

```xml
<!-- Sample of server connection file commands -->
<db2 name="<source-server-unique-name>">
  <standard-mode>

    <connection-provider value="OleDB Provider" />

    <!-- Defines server manager to connect.
         Available manager attribute values
           • zOs - DB2 for z/OS
           • LUW - DB2 for Linux, Unix and Windows
           • DBi - DB2 for i -->
    <database-manager value="$Db2Manager$" />

    <server-name value="$Db2HostName$" />

    <port value="$Db2Port$" />

    <initial-catalog value="$Db2Instance$" />

    <user-id value="$Db2UserName$" />

    <password value="$Db2Password$"/>

  </standard-mode>
</db2>
```

```xml
<sql-server name="<target-server-unique-name>">
  <sql-server-authentication>

    <server value="<server-name>" />

    <database value="<database-name>" />
  
    <user-id value="<user-name>"/>
  
    <password value="<password>"/>

  </sql-server-authentication>
</sql-server>
```

## <a name="next-step"></a>passaggio successivo

Il passaggio successivo per la gestione della console è [l'esecuzione della console SSMA &#40;DB2ToSQL&#41;](../../ssma/db2/executing-the-ssma-console-db2tosql.md)

## <a name="see-also"></a>Vedere anche

- [Esecuzione della console SSMA](./executing-the-ssma-console-db2tosql.md)