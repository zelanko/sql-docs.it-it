---
title: Trasferimento di dati nella sua forma binaria Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], transferring in binary form
- transferring data in binary form [ODBC]
- binary data transfers [ODBC]
ms.assetid: 4b12a9de-51d0-416a-87f4-9bf84959cad9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 53531ff4a3b2e1441fabf22ec7a3ce12b15540eb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301413"
---
# <a name="transferring-data-in-its-binary-form"></a>Trasferimento dei dati in forma binaria
Un'applicazione può trasferire in modo sicuro i dati (nel formato interno utilizzato da un DBMS specificato) tra due origini dati che utilizzano lo stesso DBMS e la stessa piattaforma hardware. Per una determinata parte di dati, i tipi di dati SQL devono essere gli stessi nelle origini dati di origine e di destinazione. Il tipo di dati C è SQL_C_BINARY.  
  
 Quando l'applicazione chiama **SQLFetch**, **SQLFetchScroll**o **SQLGetData** per recuperare i dati dall'origine dati di origine, il driver recupera i dati dall'origine dati e li trasferisce, senza conversione, in un percorso di archiviazione di tipo SQL_C_BINARY. Quando l'applicazione chiama **SQLBulkOperations**, **SQLExecute**, **SQLExecDirect**, **SQLPutData o SQLSetPos** per inviare i dati all'origine dati di destinazione, il driver recupera i dati dal percorso di archiviazione e li trasferisce, senza conversione, all'origine dati di destinazione.  
  
> [!NOTE]  
>  Le applicazioni che trasferiscono tutti i dati (ad eccezione dei dati binari) in questo modo non sono interoperabili tra i DBS.  
  
 **SQLCopyDesc** può essere utilizzato per copiare le associazioni di riga dal DBMS di origine alle associazioni di parametri nel DBMS di destinazione.
