---
title: SQL Server Native Client (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 48fc5ccd2973a530010975171a90f35a2f18a7e7
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73760255"
---
# <a name="sql-server-native-client-odbc"></a>SQL Server Native Client (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  ODBC è una definizione standard di un'API utilizzata per accedere ai dati nei database ISAM o relazionali o indicizzati. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] supporta ODBC, tramite il driver ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, come una delle API native per la scrittura delle applicazioni C e C++ mediante le quali è possibile comunicare con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 I programmi [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] scritti utilizzando il driver ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client comunicano con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] attraverso le chiamate di funzioni C. Le versioni specifiche di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] delle funzioni ODBC vengono implementate nel driver ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Il driver passa le istruzioni SQL a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e restituisce i risultati all'applicazione.  
  
 Il driver ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client è conforme alla specifica Microsoft Win32 ODBC 3.51. Il driver supporta le applicazioni scritte utilizzando versioni precedenti di ODBC nelle modalità definite nella specifica ODBC 3.51.  
  
## <a name="in-this-section"></a>Argomenti della sezione  
  
-   [Nomi di origine dati e sistemi operativi a 64 bit](../../../relational-databases/native-client/odbc/data-source-names-and-64-bit-operating-systems.md)  
  
-   [Creazione di un'applicazione driver ODBC di SQL Server Native Client](../../../relational-databases/native-client/odbc/creating-a-driver-application.md)  
  
-   [Comunicazione con SQL Server &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
-   [Esecuzione di query &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
-   [Elaborazione dei &#40;risultati ODBC&#41;](../../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
-   [Utilizzo di cursori &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md)  
  
-   [Esecuzione di &#40;transazioni ODBC&#41;](https://msdn.microsoft.com/library/f431191a-5762-4f0b-85bb-ac99aff29724)  
  
-   [Gestione di errori e messaggi](../../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
-   [Esecuzione delle stored procedure](../../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)  
  
-   [Uso delle funzioni catalogo](../../../relational-databases/native-client/odbc/using-catalog-functions.md)  
  
-   [Esecuzione di operazioni &#40;di copia bulk ODBC&#41;](../../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
-   [Gestione di colonne di tipo text e image](../../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)  
  
-   [Profilatura delle prestazioni del driver ODBC](../../../relational-databases/native-client/odbc/profiling-odbc-driver-performance.md)  
  
-   [ODBC Parameters &#40;con valori di tabella&#41;](../../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
-   [Miglioramenti &#40;di data e ora ODBC&#41;](../../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)  
  
-   [ODBC di tipi &#40;CLR definiti dall'utente di grandi dimensioni&#41;](../../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)  
  
-   [Supporto &#40;FILESTREAM ODBC&#41;](../../../relational-databases/native-client/odbc/filestream-support-odbc.md)  
  
-   [Nomi &#40;dell'entità servizio&#41; SPN nelle connessioni &#40;client ODBC&#41;](../../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md)  
  
-   [Le colonne di &#40;tipo sparse supportano ODBC&#41;](../../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md)  
  
-   [Riferimento &#40;ODBC&#41; SQL Server Native Client](https://msdn.microsoft.com/library/06b7edee-8636-49d9-9b5c-2c710bf4fa2d)  
  
-   [Procedure relative a ODBC](../../../relational-databases/native-client-odbc-how-to/odbc-how-to-topics.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Programmazione SQL Server Native Client](../../../relational-databases/native-client/sql-server-native-client-programming.md)   
 [Installazione di SQL Server Native Client](../../../relational-databases/native-client/applications/installing-sql-server-native-client.md)  
  
  
