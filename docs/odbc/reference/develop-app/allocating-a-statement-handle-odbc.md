---
title: Allocare un Handle di istruzione ODBC | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9524f2e6b01d2a5827dcface3159b7c52a728c59
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63287866"
---
# <a name="allocating-a-statement-handle-odbc"></a>Allocazione di un handle di istruzione ODBC
Prima che l'applicazione può eseguire un'istruzione, è necessario allocare un handle di istruzione come indicato di seguito:  
  
1.  L'applicazione dichiara una variabile di tipo HSTMT. Chiama poi **SQLAllocHandle** e passa l'indirizzo di questa variabile, l'handle della connessione in cui si desidera allocare l'istruzione e l'opzione SQL_HANDLE_STMT. Ad esempio:  
  
    ```  
    SQLHSTMT hstmt1;  
  
    SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
    ```  
  
2.  Gestione Driver alloca una struttura in cui archiviare le informazioni sull'istruzione e chiama **SQLAllocHandle** nel driver con l'opzione SQL_HANDLE_STMT.  
  
3.  Il driver alloca la propria struttura in cui archiviare le informazioni sull'istruzione e restituisce l'handle di istruzione di driver per la gestione di Driver.  
  
4.  Gestione Driver restituisce l'handle di istruzione di gestione Driver per l'applicazione nella variabile di applicazione.  
  
 L'handle di istruzione identifica quale istruzione da usare quando si chiama funzioni ODBC. Per altre informazioni sugli handle di istruzione, vedere [handle di istruzione](../../../odbc/reference/develop-app/statement-handles.md).
