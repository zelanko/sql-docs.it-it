---
title: Assegnazione di un handle di istruzione ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], statement handles
- statement handles [ODBC]
- allocating statement handles [ODBC]
- handles [ODBC], statement
ms.assetid: 4ce3b446-34ab-46dc-96e5-f40ec95c267e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bf9a15bc4622b15afa9838327edd90383a812270
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81288431"
---
# <a name="allocating-a-statement-handle-odbc"></a>Allocazione di un handle di istruzione ODBC
Prima che l'applicazione possa eseguire un'istruzione, deve allocare un handle di istruzione come indicato di seguito:  
  
1.  L'applicazione dichiara una variabile di tipo HSTMT. Chiama quindi **SQLAllocHandle** e passa l'indirizzo di questa variabile, l'handle della connessione in cui allocare l'istruzione e l'opzione SQL_HANDLE_STMT. Ad esempio:  
  
    ```  
    SQLHSTMT hstmt1;  
  
    SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
    ```  
  
2.  Gestione driver alloca una struttura in cui archiviare le informazioni sull'istruzione e chiama **SQLAllocHandle** nel driver con l'opzione SQL_HANDLE_STMT.  
  
3.  Il driver alloca la propria struttura in cui archiviare le informazioni sull'istruzione e restituisce l'handle dell'istruzione del driver a gestione driver.  
  
4.  Gestione driver restituisce l'handle dell'istruzione Gestione driver all'applicazione nella variabile dell'applicazione.  
  
 L'handle di istruzione identifica l'istruzione da utilizzare quando si chiamano le funzioni ODBC. Per ulteriori informazioni sugli handle di istruzione, vedere [handle di istruzione](../../../odbc/reference/develop-app/statement-handles.md).
