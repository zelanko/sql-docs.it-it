---
title: Uso di un'istruzione SQL senza parametri | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4b0728bd-059b-4b71-895c-999335bc7427
author: MightyPen
ms.author: genemi
ms.openlocfilehash: da4342b8640e89a0183a3f80889dd27ecfb1a76e
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "69026539"
---
# <a name="using-an-sql-statement-with-no-parameters"></a>Uso di un'istruzione SQL senza parametri

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Per usare i dati di un database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante un'istruzione SQL che non contiene parametri, è possibile usare il metodo [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) della classe [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) per restituire un set di risultati [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) contenente i dati richiesti. A tale scopo, è necessario innanzitutto creare un oggetto SQLServerStatement usando il metodo [createStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md) della classe [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md).

Nell'esempio seguente viene passata alla funzione una connessione aperta al database di esempio di [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)], viene costruita ed eseguita un'istruzione SQL, quindi i risultati vengono letti dal set di risultati.

[!code[JDBC#UsingSQLWithNoParams1](../../connect/jdbc/codesnippet/Java/using-an-sql-statement-w_0_1.java)]

Per altre informazioni sull'uso dei set di risultati, vedere [Gestione dei set di risultati con il driver JDBC](../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md).

## <a name="see-also"></a>Vedere anche

[Uso di istruzioni SQL](../../connect/jdbc/using-statements-with-sql.md)
