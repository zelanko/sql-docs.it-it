---
title: Tramite un'istruzione SQL con parametri | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3202b88f-ce13-44dd-982c-c6a3b0260378
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 2c2647b4737268a1550bd9e45deb9557ecc0f81d
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66790132"
---
# <a name="using-an-sql-statement-with-parameters"></a>Utilizzo di istruzioni SQL con parametri

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Per elaborare i dati di un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando un'istruzione SQL contenente parametri IN, è possibile usare il metodo [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverpreparedstatement.md) della classe [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) per restituire un [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) contenente i dati richiesti. A tale scopo, è necessario innanzitutto creare un oggetto SQLServerPreparedStatement usando il metodo [prepareStatement](../../connect/jdbc/reference/preparestatement-method-sqlserverconnection.md) della classe [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md).

Quando si costruisce l'istruzione SQL, i parametri IN sono specificati utilizzando il carattere ? (punto interrogativo), il quale funge da segnaposto per i valori dei parametri che verranno successivamente passati all'istruzione SQL. Per specificare un valore per un parametro, è possibile usare uno dei metodi setter della classe SQLServerPreparedStatement. Il metodo Set da utilizzare dipende dal tipo di dati del valore che si desidera passare all'istruzione SQL.

Quando si passa un valore al metodo Set, è necessario specificare non solo il valore effettivo da utilizzare nell'istruzione SQL, ma anche la posizione ordinale del parametro nell'istruzione stessa. Ad esempio, se l'istruzione SQL contiene un singolo parametro, il valore ordinale sarà 1. Se l'istruzione contiene due parametri, il primo valore ordinale sarà 1 e il secondo sarà 2.

Nell'esempio seguente una connessione aperta al database di esempio [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] viene passata alla funzione e un'istruzione SQL preparata viene costruita ed eseguita con un singolo valore del parametro di stringa. I risultati vengono quindi letti dal set di risultati.

[!code[JDBC#UsingSQLWithParams1](../../connect/jdbc/codesnippet/Java/using-an-sql-statement-w_1_1.java)]

## <a name="see-also"></a>Vedere anche

[Uso di istruzioni con SQL](../../connect/jdbc/using-statements-with-sql.md)
