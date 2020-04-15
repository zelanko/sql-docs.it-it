---
title: Creazione di una transazione distribuita Documenti Microsoft
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f21ea9b7146b2907a09688f5189d6d9ae4f3f26a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303701"
---
# <a name="create-a-distributed-transaction"></a>Creare una transazione distribuita

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

<!--
The following includes .md file is Empty, as of long before 2019/May/13.
/includes/snac-deprecated.md
-->


È possibile creare una transazione distribuita per diversi sistemi Microsoft SQL in modi diversi.

## <a name="odbc-driver-calls-the-msdtc-for-sql-server-on-premises"></a>Il driver ODBC chiama MSDTC per SQL Server locale

Microsoft Distributed Transaction Coordinator (MSDTC) consente _distribute_ alle applicazioni di estendere [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]o distribuire una transazione tra due o più istanze di . La transazione distribuita funziona anche quando le due istanze sono ospitate in computer separati.

MSDTC viene installato per Microsoft SQL Server locale, ma non è disponibile per il servizio cloud del database SQL di Azure di Microsoft.MSDTC is installed for Microsoft SQL Server on-premises, but isn't available for Microsoft's Azure SQL Database cloud service.

MSDTC viene chiamato dal driver SQL Server Native Client per Open Database Connectivity (ODBC), quando il programma C . Il driver ODBC Native Client dispone di un gestore delle transazioni compatibile con lo standard XA DTP (Open Group Distributed Transaction Processing). Questa conformità è richiesta da MSDTC. In genere, tutti i comandi di gestione delle transazioni vengono inviati tramite questo driver ODBC Native Client. La sequenza è la seguente:

1. L'applicazione ODBC di C'è Native Client avvia una transazione chiamando [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md), con la modalità autocommit disattivata.

2. L'applicazione aggiorna alcuni dati in SQL Server X nel computer A.

3. L'applicazione aggiorna alcuni dati in SQL Server Y nel computer B.
    - Se si verifica un errore in un aggiornamento in SQL Server Y, viene eseguito il rollback di tutti gli aggiornamenti di cui non è stato eseguito il commit in entrambe le istanze di SQL Server.

4. Infine, l'applicazione termina la transazione chiamando [SQLEndTran _(1)_](../../../relational-databases/native-client-odbc-api/sqlendtran.md), con l'opzione SQL_COMMIT o SQL_ROLLBACK.

_(1)_ MSDTC può essere richiamato senza ODBC. In tal caso, MSDTC diventa il gestore delle transazioni e l'applicazione non utilizza più **SQLEndTran**.

### <a name="only-one-distributed-transaction"></a>Una sola transazione distribuita

Si supponga che l'applicazione ODBC di C, Native Client, sia inserita in una transazione distribuita. Successivamente l'applicazione viene integrata in una seconda transazione distribuita. In questo caso, il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client lascia la transazione distribuita originale e viene incorporato nella nuova transazione distribuita.

Per ulteriori informazioni, vedere [DTC Programmer's Reference](https://docs.microsoft.com/previous-versions/windows/desktop/ms686108\(v=vs.85\)).

## <a name="c-alternative-for-sql-database-in-the-cloud"></a>Alternativa di C ' per il database SQL nel cloud

MSDTC isn't supported for either Azure SQL Database or Azure SQL Data Warehouse.

Tuttavia, è possibile creare una transazione distribuita per il database SQL facendo in modo che il programma in Linguaggio C, utilizzi la classe .NET [System.Transactions.TransactionScope](/dotnet/api/system.transactions.transactionscope).

### <a name="other-programming-languages"></a>Altri linguaggi di programmazione

Gli altri linguaggi di programmazione seguenti potrebbero non fornire alcun supporto per le transazioni distribuite con il servizio di database SQL:The following other programming languages might not provide any support for distributed transactions with the SQL Database service:

- Il codice nativo c'è che utilizza nodi di driver ODBC
- Server collegato con Transact-SQL
- Driver JDBC

## <a name="see-also"></a>Vedere anche

[Esecuzione di transazioni (ODBC)](performing-transactions-in-odbc.md)
