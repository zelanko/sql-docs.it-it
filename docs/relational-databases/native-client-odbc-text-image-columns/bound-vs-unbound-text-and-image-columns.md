---
description: Colonne di tipo text e image associate e non associate
title: Colonne di testo e di immagine non associato e associato | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- text columns [ODBC]
- SQL Server Native Client ODBC driver, image columns
- SQL Server Native Client ODBC driver, text columns
- data types [ODBC], image
- data types [ODBC], text
- columns [ODBC]
- ODBC data types, image columns
- ODBC data types, text columns
- image columns [ODBC]
ms.assetid: ffd3442e-d880-46e9-b848-2365a09a2406
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e6784e70d84927721eeab15d715221c519bdb1ae
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97473482"
---
# <a name="bound-vs-unbound-text-and-image-columns"></a>Colonne di tipo text e image associate e non associate
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Quando si utilizzano i cursori server, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC di Native Client è ottimizzato per non trasmettere i dati per le colonne di tipo **Text**, **ntext** o **Image** non associato al momento dell'esecuzione di **SQLFetch** . I dati di tipo **Text**, **ntext** o **Image** non vengono effettivamente recuperati dal server fino a quando l'applicazione non rilascia [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) per la colonna.  
  
 Molte applicazioni possono essere scritte in modo che non vengano visualizzati dati di tipo **Text**, **ntext** o **Image** quando un utente scorre verso l'alto e verso il basso un cursore. Quando un utente seleziona una riga per ottenere maggiori dettagli, l'applicazione può quindi chiamare **SQLGetData** per recuperare i dati di tipo **Text**, **ntext** o **Image** . In questo modo si impedisce la trasmissione dei dati di tipo **Text**, **ntext** o **Image** per le righe non selezionate dall'utente e pertanto è possibile impedire la trasmissione di grandi quantità di dati.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione delle colonne di testo e immagini](../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)   
 [Comportamenti del cursore](../../relational-databases/native-client-odbc-cursors/cursor-behaviors.md)  
  
  
