---
title: Trasferimento dei dati nel formato binario | Microsoft Docs
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
ms.openlocfilehash: a2897f882dc9dcd78ee8b919de01126d6be510c2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68070018"
---
# <a name="transferring-data-in-its-binary-form"></a>Trasferimento dei dati in forma binaria
Un'applicazione può trasferire in modo sicuro i dati (nel form interno usato da un DBMS specificato) tra due origini dati che usano la stessa piattaforma hardware e DBMS. Per una determinata porzione di dati, i tipi di dati SQL devono essere uguali nelle origini dati di origine e di destinazione. Il tipo di dati C è SQL_C_BINARY.  
  
 Quando l'applicazione chiama **SQLFetch**, **SQLFetchScroll**o **SQLGetData** per recuperare i dati dall'origine dati di origine, il driver recupera i dati dall'origine dati e li trasferisce senza conversione in un percorso di archiviazione di tipo SQL_C_BINARY. Quando l'applicazione chiama **SQLBulkOperations**, **SQLExecute**, **SQLExecDirect**, **SQLPutData o SQLSetPos** per inviare i dati all'origine dati di destinazione, il driver recupera i dati dal percorso di archiviazione e li trasferisce, senza conversione, all'origine dati di destinazione.  
  
> [!NOTE]  
>  Le applicazioni che trasferiscono i dati, ad eccezione dei dati binari, in questo modo non sono interoperabili tra i sistemi DBMS.  
  
 **SQLCopyDesc** può essere usato per copiare le associazioni di riga dal sistema DBMS di origine alle associazioni di parametri nel sistema DBMS di destinazione.
