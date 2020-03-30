---
title: Uso dei metadati del set di risultati | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5e37529a-30db-48c8-b90a-ae9657d0f6b0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0ed0b1eedcafa1fab59d17f756523fc0fc189200
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "69026118"
---
# <a name="using-result-set-metadata"></a>Uso dei metadati del set di risultati

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Per eseguire una query su un set di risultati e ottenere informazioni sulle colonne in esso contenute, [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] implementa la classe [SQLServerResultSetMetaData](../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md). Questa classe contiene vari metodi che restituiscono informazioni sotto forma di singolo valore.

Per creare un oggetto SQLServerResultSetMetaData, è possibile usare il metodo [getMetaData](../../connect/jdbc/reference/getmetadata-method-sqlserverresultset.md) della classe [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md).

Nell'esempio seguente una connessione aperta al database di esempio [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] viene passata alla funzione, il metodo getMetaData della classe SQLServerResultSet viene usato per restituire un oggetto SQLServerResultSetMetaData, quindi vengono usati vari metodi dell'oggetto SQLServerResultSetMetaData per visualizzare le informazioni sul nome e il tipo di dati delle colonne contenute nel set di risultati.

[!code[JDBC#UsingResultSetMetaData1](../../connect/jdbc/codesnippet/Java/using-result-set-metadata_1.java)]

## <a name="see-also"></a>Vedere anche

[Gestione dei metadati con il driver JDBC](../../connect/jdbc/handling-metadata-with-the-jdbc-driver.md)
