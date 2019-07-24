---
title: Utilizzo dei metadati del set di risultati | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5e37529a-30db-48c8-b90a-ae9657d0f6b0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 86e41f52ed8296c46cfd7b167407b10fc9f0b285
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68005946"
---
# <a name="using-result-set-metadata"></a>Utilizzo dei metadati del set di risultati

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Per eseguire una query su un set di risultati e ottenere informazioni sulle colonne in esso contenute, [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] implementa la classe [SQLServerResultSetMetaData](../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md). Questa classe contiene vari metodi che restituiscono informazioni sotto forma di singolo valore.

Per creare un oggetto SQLServerResultSetMetaData, è possibile usare il metodo [getMetaData](../../connect/jdbc/reference/getmetadata-method-sqlserverresultset.md) della classe [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) .

Nell'esempio seguente viene passata alla funzione una connessione aperta [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] al database di esempio, viene usato il metodo getMetaData della classe SQLServerResultSet per restituire un oggetto SQLServerResultSetMetaData e quindi vari metodi di L'oggetto SQLServerResultSetMetaData viene utilizzato per visualizzare informazioni sul nome e sul tipo di dati delle colonne contenute nel set di risultati.

[!code[JDBC#UsingResultSetMetaData1](../../connect/jdbc/codesnippet/Java/using-result-set-metadata_1.java)]

## <a name="see-also"></a>Vedere anche

[Gestione dei metadati con il driver JDBC](../../connect/jdbc/handling-metadata-with-the-jdbc-driver.md)
