---
title: Usando i metadati del parametro | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: db2c1957-91c6-4989-a07b-9f8be6d2033a
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: e2c0e9f7589f58a1ef3c1cc5ee4026dd9eea5076
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66798571"
---
# <a name="using-parameter-metadata"></a>Utilizzo dei metadati dei parametri

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Per eseguire una query su un oggetto [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) o [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) per recuperare i parametri in esso contenuti, [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] implementa la classe [SQLServerParameterMetaData](../../connect/jdbc/reference/sqlserverparametermetadata-class.md). Questa classe contiene numerosi campi e metodi che restituiscono informazioni in forma di singolo valore.

Per creare un oggetto SQLServerParameterMetaData, è possibile usare la [getParameterMetaData](../../connect/jdbc/reference/getparametermetadata-method-sqlserverpreparedstatement.md) metodi delle classi SQLServerPreparedStatement e SQLServerCallableStatement.

Nell'esempio seguente, una connessione aperta al [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] database di esempio viene passato alla funzione, il metodo getParameterMetaData della classe SQLServerCallableStatement viene utilizzato per restituire un oggetto SQLServerParameterMetaData e quindi vari metodi dell'oggetto SQLServerParameterMetaData vengono utilizzati per visualizzare informazioni sul tipo e la modalità dei parametri che sono contenuti all'interno della routine Uspupdateemployeehireinfo archiviati.

[!code[JDBC#UsingParamMetaData1](../../connect/jdbc/codesnippet/Java/using-parameter-metadata_1.java)]  

> [!NOTE]  
> Esistono alcune limitazioni quando si usa la classe SQLServerParameterMetaData con le istruzioni preparate.
>
> **Con Microsoft JDBC Driver 6.0 (o versioni successive) per SQL Server**: quando si usa SQL Server 2008 o 2008 R2, il driver JDBC supporta le istruzioni SELECT, DELETE, INSERT e UPDATE purché queste istruzioni non contengano sottoquery e/o join.

Le query MERGE  inoltre non sono supportate per la classe SQLServerParameterMetaData quando si utilizza SQL Server 2008 o 2008 R2. Sono supportati per SQL Server 2012 e versioni successive i metadati del parametro con query complesse.

Recupero dei metadati di parametro per le colonne crittografate non sono supportati. **Con Microsoft JDBC Driver 4.1 o 4.2 per SQL Server**: il driver JDBC supporta le istruzioni SELECT, DELETE, INSERT e UPDATE purché queste istruzioni non contengano sottoquery e/o join. MERGE di query non è inoltre supportati per la classe SQLServerParameterMetaData.
