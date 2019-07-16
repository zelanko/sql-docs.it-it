---
title: Creare un transazioni distribuite | Microsoft Docs
ms.custom: ''
ms.date: 05/13/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- MS DTC, performing distributed transactions
- SQL Server Native Client ODBC driver, transactions
- distributed transactions [ODBC]
- transactions [ODBC]
- ODBC, transactions
ms.assetid: 2c17fba0-7a3c-453c-91b7-f801e7b39ccb
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fc61ad955be287faad20289245ca4520efcd4bbd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67913169"
---
# <a name="create-a-distributed-transaction"></a>Creare una transazione distribuita

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

<!--
The following includes .md file is Empty, as of long before 2019/May/13.
/includes/snac-deprecated.md
-->

[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

Una transazione distribuita può essere creata per diversi sistemi di Microsoft SQL in modi diversi.

## <a name="odbc-driver-calls-the-msdtc-for-sql-server-on-premises"></a>Driver ODBC chiama il servizio MSDTC per SQL Server locale

Microsoft Distributed Transaction Coordinator (MSDTC) consente alle applicazioni di estendere o _distribuire_ una transazione tra due o più istanze di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. La transazione distribuita funziona anche quando le due istanze sono ospitate in computer separati.

MSDTC è installato Microsoft SQL Server in locale, ma non è disponibile per il servizio cloud di Microsoft Database SQL di Azure.

MSDTC viene chiamato dal driver SQL Server Native Client per Open Database Connectivity (ODBC), quando il C++ programma gestisce una transazione distribuita. Il driver ODBC di Native Client presenta una gestione transazioni conforme con il Open gruppo Distributed Transaction elaborazione (DTP) XA standard. Questa conformità è necessario MSDTC. In genere, tutti i comandi di gestione delle transazioni vengono inviati tramite il driver ODBC di Native Client. La sequenza è come segue:

1. Il C++ applicazione ODBC di Native Client inizia una transazione chiamando [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md), con la modalità autocommit disabilitata.

2. L'applicazione aggiorna alcuni dati in SQL Server X in computer A.

3. L'applicazione aggiorna alcuni dati in SQL Server Y sul computer B.
    - Se un aggiornamento in SQL Server Y non riesce, vengano eseguito il rollback di tutti gli aggiornamenti non sottoposte a commit in entrambe le istanze di SQL Server.

4. Infine, l'applicazione termina la transazione chiamando [SQLEndTran _(1)_ ](../../../relational-databases/native-client-odbc-api/sqlendtran.md), con l'opzione SQL_COMMIT o SQL_ROLLBACK.

[!INCLUDE[freshInclude](../../../includes/paragraph-content/fresh-note-steps-feedback.md)]

_(1)_  MSDTC può essere richiamato senza ODBC. In tal caso, MSDTC diventa il gestore delle transazioni e l'applicazione non vengono più utilizzati **SQLEndTran**.

### <a name="only-one-distributed-transaction"></a>Solo una transazione distribuita

Si supponga che il C++ applicazione ODBC di Native Client viene inserita in una transazione distribuita. Accanto all'applicazione integra in una seconda transazione distribuita. In questo caso, il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client lascia la transazione distribuita originale e consente di integrare nella transazione distribuita nuova.

Per altre informazioni, vedere [di riferimento per programmatori di DTC](https://docs.microsoft.com/previous-versions/windows/desktop/ms686108\(v=vs.85\)).

## <a name="c-alternative-for-sql-database-in-the-cloud"></a>C#In alternativa per il Database SQL nel cloud

MSDTC non è supportata per il Database SQL di Azure o Azure SQL Data Warehouse.

Tuttavia, è possibile creare una transazione distribuita per Database SQL di facendo in modo che il C# programma di usare la classe .NET [TransactionScope](/dotnet/api/system.transactions.transactionscope).

### <a name="other-programming-languages"></a>Altri linguaggi di programmazione

I seguenti linguaggi di programmazione potrebbero non fornire alcun supporto per le transazioni distribuite con il servizio Database SQL:

- Nativa C++ che utilizzano i driver ODBC
- Server collegato tramite Transact-SQL
- Driver JDBC

## <a name="see-also"></a>Vedere anche

[Esecuzione di transazioni (ODBC)](performing-transactions-in-odbc.md)
