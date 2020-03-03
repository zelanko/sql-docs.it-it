---
title: Scaricare Microsoft JDBC Driver per SQL Server
description: Scaricare Microsoft JDBC Driver per SQL Server per sviluppare applicazioni Java che si connettono a SQL Server.
ms.date: 02/26/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 451181b8-11e6-4d01-b547-9ac5aada8238
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6576ed155e57fbd69757065c440382efa4adba5e
ms.sourcegitcommit: 6ee40a2411a635daeec83fa473d8a19e5ae64662
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/28/2020
ms.locfileid: "77903498"
---
# <a name="download-microsoft-jdbc-driver-for-sql-server"></a>Scaricare Microsoft JDBC Driver per SQL Server

Questo articolo include collegamenti per il download di Microsoft JDBC Driver per SQL Server. Questo driver consente di sviluppare applicazioni Java che si connettono a SQL Server.  

## <a name="available-downloads-of-jdbc-driver-for-sql-server"></a>Download disponibili del driver JDBC per SQL Server

Usare i collegamenti nella tabella seguente per scaricare la versione più recente di Microsoft JDBC Driver per SQL Server corrispondente all'ambiente Java Runtime Environment (JRE) in uso:

| Versione | Data di rilascio | Versioni Java |
|---|---|---|
| [Microsoft JDBC Driver 8.2](https://go.microsoft.com/fwlink/?linkid=2116870) | 26/2/2020 | JRE 8, 11, 13 |
| [Microsoft JDBC Driver 7.4](https://go.microsoft.com/fwlink/?linkid=2099962) | 1/8/2019 | JRE 8, 11, 12 |
| [Microsoft JDBC Driver 7.2](https://go.microsoft.com/fwlink/?linkid=2063159) | 17/4/2019 | JRE 8, 11 |
| [Microsoft JDBC Driver 7.0](https://go.microsoft.com/fwlink/?linkid=2005972) | 31/7/2018 | JRE 8, 10 |
| [Microsoft JDBC Driver 6.4](https://go.microsoft.com/fwlink/?linkid=868290)  | 26/3/2018 | JRE 7, 8, 9 |
| [Microsoft JDBC Driver 6.2](https://go.microsoft.com/fwlink/?linkid=852460) | 12/2/2018 | JRE 7, 8 |
| [Microsoft JDBC Driver 6.0](https://go.microsoft.com/fwlink/?LinkId=245496) | 27/2/2018 | JRE 7, 8 |
| [Microsoft JDBC Driver 4.2](https://go.microsoft.com/fwlink/?linkid=841534) | 26/2/2018 | JRE 7, 8 |

Quando si Scarica il driver sono presenti più file JAR. Il nome del file JAR indica la versione di Java supportata. Per altre informazioni su ogni versione, vedere le [Note sulla versione](release-notes-for-the-jdbc-driver.md) e i [Requisiti di sistema](system-requirements-for-the-jdbc-driver.md).

## <a name="using-the-jdbc-driver-with-maven-central"></a>Uso del driver JDBC con Maven Central

Il driver JDBC può essere aggiunto a un progetto Maven aggiungendolo come dipendenza nel file POM.xml con il codice seguente:

```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>8.2.1.jre11</version>
</dependency>
```  

## <a name="unsupported-drivers"></a>Driver non supportati

Le versioni non supportate dei driver non sono disponibili per il download in questo contesto. Il supporto per la connettività Java è in continuo miglioramento, Di conseguenza, è consigliabile usare la versione più recente di Microsoft JDBC Driver.  
  
## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su Microsoft JDBC Driver per SQL Server, vedere [Panoramica del driver JDBC](overview-of-the-jdbc-driver.md) e il [repository GitHub del driver JDBC](https://github.com/microsoft/mssql-jdbc/blob/dev/README.md).
