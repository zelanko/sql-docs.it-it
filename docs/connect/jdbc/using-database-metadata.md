---
title: Usando i metadati del Database | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8b048371-e912-4ed1-afd7-436978f48888
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 0bad06da093edd83b7df2e1c10f2b68bdca7a210
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66798671"
---
# <a name="using-database-metadata"></a>Utilizzo dei metadati del database

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Per eseguire una query su un database e ottenere informazioni sugli oggetti supportati, [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] implementa la classe [SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md). Questa classe contiene vari metodi che restituiscono informazioni sotto forma di singolo valore o come set di risultati.

Per creare un oggetto SQLServerDatabaseMetaData, è possibile usare il metodo [getMetaData](../../connect/jdbc/reference/getmetadata-method-sqlserverconnection.md) della classe [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) per ottenere informazioni sul database a cui è connesso.

Nell'esempio seguente, una connessione aperta al [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] database di esempio viene passato alla funzione, viene usato il metodo getMetaData della classe SQLServerConnection per restituire un oggetto SQLServerDatabaseMetadata e quindi vari metodi del Oggetto SQLServerDatabaseMetaData consentono di visualizzare informazioni su driver, versione del driver, nome del database e versione del database.

[!code[JDBC#UsingDBMetaData1](../../connect/jdbc/codesnippet/Java/using-database-metadata_1.java)]

## <a name="see-also"></a>Vedere anche

[Gestione dei metadati con il driver JDBC](../../connect/jdbc/handling-metadata-with-the-jdbc-driver.md)
