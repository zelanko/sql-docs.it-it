---
title: Uso dei metadati del database | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8b048371-e912-4ed1-afd7-436978f48888
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fce2bf9d72136b303ee3bc974f3aede313233a82
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 08/14/2019
ms.locfileid: "69026423"
---
# <a name="using-database-metadata"></a>Uso dei metadati del database

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Per eseguire una query su un database e ottenere informazioni sugli oggetti supportati, [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] implementa la classe [SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md). Questa classe contiene vari metodi che restituiscono informazioni sotto forma di singolo valore o come set di risultati.

Per creare un oggetto SQLServerDatabaseMetaData, è possibile usare il metodo [getMetaData](../../connect/jdbc/reference/getmetadata-method-sqlserverconnection.md) della classe [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) per ottenere informazioni sul database a cui è connesso.

Nell'esempio seguente viene passata alla funzione una connessione aperta [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] al database di esempio, viene usato il metodo getMetaData della classe SQLServerConnection per restituire un oggetto SQLServerDatabaseMetaData e quindi vari metodi di L'oggetto SQLServerDatabaseMetaData viene utilizzato per visualizzare informazioni sul driver, sulla versione del driver, sul nome del database e sulla versione del database.

[!code[JDBC#UsingDBMetaData1](../../connect/jdbc/codesnippet/Java/using-database-metadata_1.java)]

## <a name="see-also"></a>Vedere anche

[Gestione dei metadati con il driver JDBC](../../connect/jdbc/handling-metadata-with-the-jdbc-driver.md)
