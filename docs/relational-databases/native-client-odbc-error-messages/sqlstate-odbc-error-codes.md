---
title: SQLSTATE (codici di errore ODBC) | Microsoft Docs
description: Quando SQL Server driver ODBC esegue stored procedure come stored procedure remote, la procedura può avere codici restituiti e parametri di output di tipo Integer.
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
ms.openlocfilehash: a358a3cd071c3b0a986925a1ef5fc181536283c0
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/09/2020
ms.locfileid: "91868322"
---
# <a name="sqlstate-odbc-error-codes"></a>SQLSTATE (codici di errore ODBC)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  SQLSTATE fornisce informazioni dettagliate sulla causa di un avviso o di un errore. Per gli errori che si verificano nell'origine dati rilevata e restituita da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC di Native client esegue il mapping del numero di errore nativo restituito all'SQLSTATE appropriato. Se un numero di errore nativo non dispone di un codice di errore ODBC a cui eseguire il mapping, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC di Native Client restituisce SQLSTATE 42000 ("errore di sintassi o violazione di accesso"). Per gli errori rilevati dal driver, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC di Native Client genera il SQLSTATE appropriato.  
  
 Per ulteriori informazioni sui codici di errore di stato, vedere i seguenti argomenti:  
  
-   [Appendice A: codici di errore ODBC](../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md)  
  
-   [Mapping di SQLSTATE](../../odbc/reference/develop-app/sqlstate-mappings.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione di errori e messaggi](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
