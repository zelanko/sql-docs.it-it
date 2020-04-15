---
title: SQLSTATE (Codici di errore ODBC) Documenti Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, errors
- ODBC error handling, cause information
- messages [ODBC], cause information
- SQLSTATEs
- errors [ODBC], cause information
ms.assetid: 84cce528-edb0-473f-a85f-3eb87fbe2cf3
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8c7f3fbdf690989830cff2a41028ee0c1e2c9f37
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81291531"
---
# <a name="sqlstate-odbc-error-codes"></a>SQLSTATE (codici di errore ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  SQLSTATE fornisce informazioni dettagliate sulla causa di un avviso o di un errore. Per gli errori che si verificano [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]nell'origine dati rilevati e restituiti da , il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client esegue il mapping del numero di errore nativo restituito al SQLSTATE appropriato. Se un numero di errore nativo non dispone di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] un codice di errore ODBC a cui eseguire il mapping, il driver ODBC Native Client restituisce SQLSTATE 42000 ("errore di sintassi o violazione di accesso"). Per gli errori rilevati dal [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver, il driver ODBC Native Client genera il SQLSTATE appropriato.  
  
 Per ulteriori informazioni sui codici di errore di stato, vedere i seguenti argomenti:  
  
-   [Appendice A: codici di errore ODBC](https://go.microsoft.com/fwlink/?LinkId=89356)  
  
-   [Mapping di SQLSTATE](https://go.microsoft.com/fwlink/?LinkId=89355)  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione di errori e messaggi](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
