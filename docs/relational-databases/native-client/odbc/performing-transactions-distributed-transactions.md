---
title: Creazione di transazioni distribuite | Microsoft Docs
description: Le applicazioni possono utilizzare MSDTC per estendere o distribuire una transazione tra più istanze di SQL Server. Una classe .NET può inoltre distribuire una transazione.
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
ms.openlocfilehash: 2f7a98b35483103059600086c37294c5acb56ad0
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84950417"
---
# <a name="create-a-distributed-transaction"></a>Creazione di una transazione distribuita

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

<!--
The following includes .md file is Empty, as of long before 2019/May/13.
/includes/snac-deprecated.md
-->


Una transazione distribuita può essere creata per diversi sistemi Microsoft SQL in modi diversi.

## <a name="odbc-driver-calls-the-msdtc-for-sql-server-on-premises"></a>Il driver ODBC chiama MSDTC per SQL Server locale

Microsoft Distributed Transaction Coordinator (MSDTC) consente alle applicazioni di estendere o _distribuire_ una transazione tra due o più istanze di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . La transazione distribuita funziona anche quando le due istanze sono ospitate in computer distinti.

MSDTC viene installato per Microsoft SQL Server in locale, ma non è disponibile per il servizio cloud del database SQL di Microsoft Azure.

MSDTC viene chiamato dal driver SQL Server Native Client per Open Database Connectivity (ODBC), quando il programma C++ gestisce una transazione distribuita. Il driver ODBC di Native client dispone di una gestione transazioni conforme allo standard Open Group Distributed Transaction Processing (DTP) XA. Questa conformità è richiesta da MSDTC. In genere, tutti i comandi di gestione delle transazioni vengono inviati tramite questo driver ODBC di Native Client. La sequenza è la seguente:

1. L'applicazione ODBC C++ native client avvia una transazione chiamando [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md), con la modalità autocommit disabilitata.

2. L'applicazione aggiorna alcuni dati in SQL Server X nel computer A.

3. L'applicazione aggiorna alcuni dati in SQL Server Y sul computer B.
    - Se un aggiornamento in SQL Server Y ha esito negativo, viene eseguito il rollback di tutti gli aggiornamenti non sottoposti a commit in entrambe le istanze di SQL Server.

4. Infine, l'applicazione termina la transazione chiamando [SQLEndTran _(1)_](../../../relational-databases/native-client-odbc-api/sqlendtran.md), con l'opzione SQL_COMMIT o SQL_ROLLBACK.

_(1)_ MSDTC può essere richiamato senza ODBC. In tal caso, MSDTC diventa la gestione transazioni e l'applicazione non utilizza più **SQLEndTran**.

### <a name="only-one-distributed-transaction"></a>Una sola transazione distribuita

Si supponga che l'applicazione ODBC C++ native client sia integrata in una transazione distribuita. Successivamente, l'applicazione viene integrata in una seconda transazione distribuita. In questo caso, il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC di Native client lascia la transazione distribuita originale e viene integrata nella nuova transazione distribuita.

Per ulteriori informazioni, vedere [DTC Programmer ' s Reference](https://docs.microsoft.com/previous-versions/windows/desktop/ms686108\(v=vs.85\)).

## <a name="c-alternative-for-sql-database-in-the-cloud"></a>Alternativa C# per database SQL nel cloud

MSDTC non è supportato per il database SQL di Azure o per la Azure SQL Data Warehouse.

Tuttavia, è possibile creare una transazione distribuita per il database SQL facendo in modo che il programma C# usi la classe .NET [System. Transactions. TransactionScope](/dotnet/api/system.transactions.transactionscope).

### <a name="other-programming-languages"></a>Altri linguaggi di programmazione

Gli altri linguaggi di programmazione seguenti potrebbero non fornire alcun supporto per le transazioni distribuite con il servizio del database SQL:

- C++ nativo che usa driver ODBC
- Server collegato con Transact-SQL
- Driver JDBC

## <a name="see-also"></a>Vedere anche

[Esecuzione di transazioni (ODBC)](performing-transactions-in-odbc.md)
