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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: ca071567d8151c2b620283c0da422e9963c7c01c
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82704295"
---
# <a name="sql-server-native-client-odbc"></a>SQL Server Native Client (ODBC)
  ODBC è una definizione standard di un'API utilizzata per accedere ai dati nei database ISAM o relazionali o indicizzati. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] supporta ODBC, tramite il driver ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, come una delle API native per la scrittura delle applicazioni C e C++ mediante le quali è possibile comunicare con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 I programmi [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] scritti utilizzando il driver ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client comunicano con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] attraverso le chiamate di funzioni C. Le versioni specifiche di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] delle funzioni ODBC vengono implementate nel driver ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Il driver passa le istruzioni SQL a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e restituisce i risultati all'applicazione.  
  
 Il driver ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client è conforme alla specifica Microsoft Win32 ODBC 3.51. Il driver supporta le applicazioni scritte utilizzando versioni precedenti di ODBC nelle modalità definite nella specifica ODBC 3.51.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
-   [Nomi di origine dati e sistemi operativi a 64 bit](data-source-names-and-64-bit-operating-systems.md)  
  
-   [Creazione di un'applicazione driver ODBC di SQL Server Native Client](creating-a-driver-application.md)  
  
-   [Comunicazione con SQL Server &#40;ODBC&#41;](../../native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
-   [Esecuzione di query &#40;ODBC&#41;](../../native-client-odbc-queries/executing-queries-odbc.md)  
  
-   [Elaborazione dei risultati &#40;&#41;ODBC](../../native-client-odbc-results/processing-results-odbc.md)  
  
-   [Utilizzo di cursori &#40;&#41;ODBC](../../native-client-odbc-cursors/using-cursors-odbc.md)  
  
-   [Esecuzione di transazioni &#40;ODBC&#41;](../../../database-engine/dev-guide/performing-transactions-odbc.md)  
  
-   [Gestione di errori e messaggi](../../native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
-   [Esecuzione delle stored procedure](../../native-client-odbc-stored-procedures/running-stored-procedures.md)  
  
-   [Uso delle funzioni catalogo](using-catalog-functions.md)  
  
-   [Esecuzione di operazioni di copia bulk &#40;ODBC&#41;](../../native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
-   [Gestione di colonne di tipo text e image](../../native-client-odbc-text-image-columns/managing-text-and-image-columns.md)  
  
-   [Profiling delle prestazioni del driver ODBC](profiling-odbc-driver-performance.md)  
  
-   [Parametri con valori di tabella &#40;&#41;ODBC](../../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
-   [Miglioramenti di data e ora &#40;ODBC&#41;](../../native-client-odbc-date-time/date-and-time-improvements-odbc.md)  
  
-   [Tipi CLR definiti dall'utente di grandi dimensioni &#40;ODBC&#41;](large-clr-user-defined-types-odbc.md)  
  
-   [Supporto FILESTREAM &#40;&#41;ODBC](filestream-support-odbc.md)  
  
-   [Nomi SPN &#40;Service Principal Name&#41; nelle connessioni client &#40;ODBC&#41;](service-principal-names-spns-in-client-connections-odbc.md)  
  
-   [Colonne di tipo sparse supportano &#40;ODBC&#41;](sparse-columns-support-odbc.md)  
  
-   [SQL Server Native Client &#40;riferimento&#41; ODBC](../../../database-engine/dev-guide/sql-server-native-client-odbc-reference.md)  
  
-   [Procedure per l'utilizzo di ODBC](../../native-client-odbc-how-to/odbc-how-to-topics.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Programmazione SQL Server Native Client](../sql-server-native-client-programming.md)   
 [Installazione di SQL Server Native Client](../applications/installing-sql-server-native-client.md)  
  
  
