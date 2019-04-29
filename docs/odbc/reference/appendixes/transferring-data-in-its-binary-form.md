---
title: Trasferimento dei dati in forma binaria | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 44bf8de8ea4c33a20a6159c5702db0b7eaee9eed
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62735047"
---
# <a name="transferring-data-in-its-binary-form"></a>Trasferimento dei dati in forma binaria
Un'applicazione in modo sicuro possibile trasferire i dati (nel formato interno usato da un sistema DBMS specificato) tra due origini dati che usano la stessa DBMS e la piattaforma hardware. Per una determinata parte dei dati, i tipi di dati SQL devono essere uguale nelle origini dei dati di origine e di destinazione. Il tipo di dati C è SQL_C_BINARY.  
  
 Quando l'applicazione chiama **SQLFetch**, **SQLFetchScroll**, o **SQLGetData** per recuperare i dati dall'origine dei dati di origine, il driver recupera i dati dai dati origine e li trasferisce, senza conversione, in un percorso di archiviazione di tipo SQL_C_BINARY. Quando l'applicazione chiama **SQLBulkOperations**, **SQLExecute**, **SQLExecDirect**, **SQLPutData o SQLSetPos** per inviare i dati l'origine dati di destinazione, il driver recupera i dati dalla posizione di archiviazione e li trasferisce, senza conversione, all'origine dati di destinazione.  
  
> [!NOTE]  
>  Le applicazioni che trasferiscono i dati (tranne i dati binari) in questo modo non sono interoperative tra DBMS.  
  
 **SQLCopyDesc** può essere utilizzato per copiare le associazioni di riga dal sistema DBMS di origine alle associazioni di parametro nel sistema DBMS di destinazione.
