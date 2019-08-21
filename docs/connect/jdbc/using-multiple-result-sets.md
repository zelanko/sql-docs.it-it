---
title: Utilizzo di più set di risultati | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ab6a3cfa-073b-44e9-afca-a8675cfe5fd1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 802ade7a34eb5c5174efc35032587f801ef12179
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 08/14/2019
ms.locfileid: "69026269"
---
# <a name="using-multiple-result-sets"></a>Uso di più set di risultati

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Quando si usano stored procedure inline SQL o di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che restituiscono più set di risultati, in [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] è disponibile il metodo [getResultSet](../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md) nella classe [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) per recuperare ogni set di dati restituito. Quando si esegue un'istruzione che restituisce più set di risultati, è inoltre possibile usare il metodo [execute](../../connect/jdbc/reference/execute-method-sqlserverstatement.md) della classe SQLServerStatement, che restituisce un valore **booleano** che indica se il valore restituito è un set di risultati o un conteggio aggiornamenti.

Se il metodo execute restituisce **true**, l'istruzione eseguita ha restituito uno o più set di risultati. Per accedere al primo set di risultati, chiamare il metodo getResultSet. Per determinare se sono disponibili ulteriori set di risultati, chiamare il metodo [getMoreResults](../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md) che, in caso affermativo, restituisce un valore **booleano** **true**. Se sono disponibili più set di risultati, chiamare di nuovo il metodo getResultSet per visualizzarli. È possibile ripetere la procedura finché non sono stati elaborati tutti i set di risultati. Se il metodo getMoreResults restituisce **false**, non sono presenti altri set di risultati da elaborare.

Se il metodo execute restituisce **false**, l'istruzione eseguita ha restituito un valore di conteggio aggiornamenti che può essere recuperato chiamando il metodo [getUpdateCount](../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md).

> [!NOTE]  
> Per ulteriori informazioni sui conteggi degli aggiornamenti, vedere [utilizzo di un stored procedure con un numero di aggiornamenti](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md).

Nell'esempio seguente una connessione aperta al database di esempio [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] è passata alla funzione e viene costruita un'istruzione SQL che, una volta eseguita, restituisce due set di risultati:

[!code[JDBC#UsingMultipleResultSets1](../../connect/jdbc/codesnippet/Java/using-multiple-result-sets_1.java)]

In questo caso il numero di set di risultati (pari a due) è noto. Tuttavia, il codice è scritto in modo tale che se fosse restituito un numero non noto di set di risultati, come, ad esempio, nelle chiamate a stored procedure, tutti i set verranno comunque elaborati. Per un esempio di chiamata a una stored procedure che restituisce più set di risultati oltre a valori di aggiornamento, vedere [Gestione delle istruzioni complesse](../../connect/jdbc/handling-complex-statements.md).

> [!NOTE]  
> Quando si effettua la chiamata al metodo getMoreResults della classe SQLServerStatement, il set di risultati restituito in precedenza viene chiuso in modo implicito.

## <a name="see-also"></a>Vedere anche

[Uso delle istruzioni con il driver JDBC](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)
