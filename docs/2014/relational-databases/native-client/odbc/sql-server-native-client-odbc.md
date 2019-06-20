---
title: SQL Server Native Client (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLNCLI, ODBC
- SQL Server Native Client ODBC driver, about SQL Server Native Client ODBC driver
- data access [SQL Server Native Client], ODBC
- SQL Server Native Client ODBC driver
- ODBC
- SQL Server Native Client, ODBC
- ODBC, about SQL Server Native Client ODBC driver
ms.assetid: 811d5ba3-a2b8-48c0-adbc-8c91f041f458
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 570c0574357d9315f0e6b153f3eeabac79ec673b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63055661"
---
# <a name="sql-server-native-client-odbc"></a>SQL Server Native Client (ODBC)
  ODBC è una definizione standard di un'API utilizzata per accedere ai dati nei database ISAM o relazionali o indicizzati. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] supporta ODBC, tramite il driver ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, come una delle API native per la scrittura delle applicazioni C e C++ mediante le quali è possibile comunicare con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 I programmi [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] scritti utilizzando il driver ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client comunicano con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] attraverso le chiamate di funzioni C. Le versioni specifiche di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] delle funzioni ODBC vengono implementate nel driver ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Il driver passa le istruzioni SQL a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e restituisce i risultati all'applicazione.  
  
 Il driver ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client è conforme alla specifica Microsoft Win32 ODBC 3.51. Il driver supporta le applicazioni scritte utilizzando versioni precedenti di ODBC nelle modalità definite nella specifica ODBC 3.51.  
  
## <a name="in-this-section"></a>In questa sezione  
  
-   [Nomi di origine dati e sistemi operativi a 64 bit](data-source-names-and-64-bit-operating-systems.md)  
  
-   [Creazione di un'applicazione driver ODBC di SQL Server Native Client](creating-a-driver-application.md)  
  
-   [Comunicazione con SQL Server &#40;ODBC&#41;](../../native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
-   [L'esecuzione di query &#40;ODBC&#41;](../../native-client-odbc-queries/executing-queries-odbc.md)  
  
-   [L'elaborazione dei risultati &#40;ODBC&#41;](../../native-client-odbc-results/processing-results-odbc.md)  
  
-   [Utilizzo di cursori &#40;ODBC&#41;](../../native-client-odbc-cursors/using-cursors-odbc.md)  
  
-   [Esecuzione di transazioni di &#40;ODBC&#41;](../../../database-engine/dev-guide/performing-transactions-odbc.md)  
  
-   [Gestione di errori e messaggi](../../native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
-   [Esecuzione delle stored procedure](../../native-client-odbc-stored-procedures/running-stored-procedures.md)  
  
-   [Uso delle funzioni catalogo](using-catalog-functions.md)  
  
-   [Esecuzione di operazioni di copia Bulk &#40;ODBC&#41;](../../native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
-   [Gestione di colonne di tipo text e image](../../native-client-odbc-text-image-columns/managing-text-and-image-columns.md)  
  
-   [Profilatura delle prestazioni del driver ODBC](profiling-odbc-driver-performance.md)  
  
-   [I parametri con valori di tabella &#40;ODBC&#41;](../../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
-   [Data e miglioramenti per la fase &#40;ODBC&#41;](../../native-client-odbc-date-time/date-and-time-improvements-odbc.md)  
  
-   [Tipi definiti dall'utente CLR di grandi dimensioni &#40;ODBC&#41;](large-clr-user-defined-types-odbc.md)  
  
-   [Supporto FILESTREAM &#40;ODBC&#41;](filestream-support-odbc.md)  
  
-   [Nomi dell'entità servizio &#40;entità servizio&#41; nelle connessioni Client &#40;ODBC&#41;](service-principal-names-spns-in-client-connections-odbc.md)  
  
-   [Supporto per colonne di tipo sparse &#40;ODBC&#41;](sparse-columns-support-odbc.md)  
  
-   [SQL Server Native Client &#40;ODBC&#41; riferimento](../../../database-engine/dev-guide/sql-server-native-client-odbc-reference.md)  
  
-   [Procedure relative a ODBC](../../native-client-odbc-how-to/odbc-how-to-topics.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Programmazione di SQL Server Native Client](../sql-server-native-client-programming.md)   
 [Installazione di SQL Server Native Client](../applications/installing-sql-server-native-client.md)  
  
  
