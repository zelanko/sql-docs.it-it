---
title: Transazioni in ODBC | Microsoft Docs
description: ODBC gestisce le transazioni a livello di connessione, eseguendo il commit o il rollback di tutte le operazioni completate, in modalità autocommit o con commit manuale.
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, transactions
- transactions [ODBC]
- ODBC, transactions
ms.assetid: c5a87fa5-827a-4e6f-a0d9-924bac881eb0
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e37533e1c57ccf55dfe8bb7b5cbc5aa3da60dd3f
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/09/2020
ms.locfileid: "91890792"
---
# <a name="performing-transactions-in-odbc"></a>Esecuzione di transazioni in ODBC
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Le transazioni in ODBC vengono gestite a livello di connessione. Quando un'applicazione completa una transazione, esegue il commit o il rollback di tutte le operazioni effettuate tramite tutti gli handle di istruzione nella connessione. Per eseguire il commit o il rollback di una transazione, le applicazioni devono chiamare [SQLEndTran](../../../relational-databases/native-client-odbc-api/sqlendtran.md) anziché inviare un'istruzione commit o rollback.  
  
 Un'applicazione chiama [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) per passare tra le due modalità ODBC di gestione delle transazioni:  
  
-   Modalità autocommit  
  
     Di ogni istruzione completata correttamente viene automaticamente eseguito il commit. Quando si utilizza la modalità autocommit, non sono necessarie altre funzioni di gestione delle transazioni.  
  
-   Modalità di commit manuale  
  
     Tutte le istruzioni eseguite sono incluse nella stessa transazione fino a quando non vengono arrestate in modo specifico chiamando **SQLEndTran**.  
  
 La modalità autocommit è la modalità di esecuzione delle transazioni predefinita per ODBC. Quando viene stabilita una connessione, è in modalità autocommit fino a quando non viene chiamato **SQLSetConnectAttr** per passare alla modalità di commit manuale impostando la modalità autocommit. Quando un'applicazione disattiva l'autocommit, l'istruzione successiva inviata al database avvia una transazione. La transazione rimane attiva fino a quando l'applicazione non chiama **SQLEndTran** con le opzioni SQL_COMMIT o SQL_ROLLBACK. Il comando inviato al database dopo **SQLEndTran** avvia la transazione successiva.  
  
 Se un'applicazione passa dalla modalità di commit manuale alla modalità autocommit, il driver esegue il commit di tutte le transazioni attualmente aperte nella connessione.  
  
 Le applicazioni ODBC non devono utilizzare istruzioni per transazioni Transact-SQL quali BEGIN TRANSACTION, COMMIT TRANSACTION o ROLLBACK TRANSACTION, in quanto tali istruzioni possono provocare un comportamento imprevedibile nel driver. Un'applicazione ODBC deve essere eseguita in modalità autocommit e non utilizzare le istruzioni o le funzioni di gestione delle transazioni oppure essere eseguita in modalità con commit manuale e utilizzare la funzione ODBC **SQLEndTran** per eseguire il commit o il rollback delle transazioni.  
  
## <a name="see-also"></a>Vedere anche  
 [Esecuzione di transazioni &#40;ODBC&#41;]()  
  
