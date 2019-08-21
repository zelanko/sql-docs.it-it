---
title: Uso dei metadati dei parametri | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: db2c1957-91c6-4989-a07b-9f8be6d2033a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 80ff8cebcc4141e8363c25f83821cb4924e6c46a
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 08/14/2019
ms.locfileid: "69026080"
---
# <a name="using-parameter-metadata"></a>Uso dei metadati dei parametri

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Per eseguire una query su un oggetto [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) o [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) per recuperare i parametri in esso contenuti, [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] implementa la classe [SQLServerParameterMetaData](../../connect/jdbc/reference/sqlserverparametermetadata-class.md). Questa classe contiene numerosi campi e metodi che restituiscono informazioni in forma di singolo valore.

Per creare un oggetto SQLServerParameterMetaData, è possibile usare i metodi [getParameterMetaData](../../connect/jdbc/reference/getparametermetadata-method-sqlserverpreparedstatement.md) delle classi SQLServerPreparedStatement e SQLServerCallableStatement.

Nell'esempio seguente viene passata alla funzione una connessione aperta [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] al database di esempio, viene usato il metodo getParameterMetaData della classe SQLServerCallableStatement per restituire un oggetto SQLServerParameterMetaData e quindi varie i metodi dell'oggetto SQLServerParameterMetaData vengono utilizzati per visualizzare le informazioni sul tipo e sulla modalità dei parametri contenuti all'interno del stored procedure HumanResources. uspUpdateEmployeeHireInfo.

[!code[JDBC#UsingParamMetaData1](../../connect/jdbc/codesnippet/Java/using-parameter-metadata_1.java)]  

> [!NOTE]  
> Esistono alcune limitazioni quando si usa la classe SQLServerParameterMetaData con le istruzioni preparate.
>
> **Con Microsoft JDBC Driver 6.0 (o versioni successive) per SQL Server**: quando si usa SQL Server 2008 o 2008 R2, il driver JDBC supporta le istruzioni SELECT, DELETE, INSERT e UPDATE purché queste istruzioni non contengano sottoquery e/o join.

Le query MERGE  inoltre non sono supportate per la classe SQLServerParameterMetaData quando si utilizza SQL Server 2008 o 2008 R2. Sono supportati per SQL Server 2012 e versioni successive i metadati del parametro con query complesse.

Il recupero dei metadati del parametro per le colonne crittografate non è supportato. **Con Microsoft JDBC Driver 4.1 o 4.2 per SQL Server**: il driver JDBC supporta le istruzioni SELECT, DELETE, INSERT e UPDATE purché queste istruzioni non contengano sottoquery e/o join. Anche le query di MERGE non sono supportate per la classe SQLServerParameterMetaData.
