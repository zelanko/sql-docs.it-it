---
title: Allocare un Handle di connessione ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- allocating connection handles [ODBC]
- data sources [ODBC], connection handles
- connecting to data source [ODBC], connection handles
- ODBC drivers [ODBC], connection handles
- connecting to driver [ODBC], connection handles
- connection handles [ODBC]
- handles [ODBC], connection
ms.assetid: c99a8159-7693-4f97-8dcf-401336550e77
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 83964bf1e76eef5c7c4ba4121b0c581e8d8a406b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63288321"
---
# <a name="allocating-a-connection-handle-odbc"></a>Allocazione di un handle di connessione ODBC
Prima che l'applicazione possa connettersi a un'origine dati o driver, è necessario allocare un handle di connessione, come indicato di seguito:  
  
1.  L'applicazione dichiara una variabile di tipo SQLHDBC. Chiama poi **SQLAllocHandle** e passa l'indirizzo di questa variabile, l'handle dell'ambiente in cui si desidera allocare la connessione e l'opzione SQL_HANDLE_DBC. Ad esempio:  
  
    ```  
    SQLHDBC hdbc1;  
  
    SQLAllocHandle(SQL_HANDLE_DBC, henv1, &hdbc1);  
    ```  
  
2.  Gestione Driver alloca una struttura in cui archiviare le informazioni sull'istruzione e restituisce l'handle di connessione nella variabile.  
  
 Gestione Driver non chiama **SQLAllocHandle** nel driver di questo tempo, poiché non conosce il driver da chiamare. Ritardare la chiamata **SQLAllocHandle** nel driver fino a quando l'applicazione chiama una funzione per la connessione a un'origine dati. Per altre informazioni, vedere [ruolo di gestione Driver nel processo di connessione](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md), più avanti in questa sezione.  
  
 È importante allocare un handle di connessione non è quello utilizzato per il caricamento di un driver. Il driver non viene caricato finché non viene chiamata una funzione di connessione. Dopo avere allocato un handle di connessione e prima della connessione del driver o origine dati, le funzioni sole l'applicazione può chiamare con l'handle di connessione sono pertanto **SQLSetConnectAttr**, **SQLGetConnectAttr**, oppure **SQLGetInfo** con l'opzione SQL_ODBC_VER. Chiamare altre funzioni con l'handle di connessione, quali **SQLEndTran**, restituisce SQLSTATE 08003 (connessione non aperta). Per informazioni dettagliate, vedere [appendice b: Tabelle della transizione di stato ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
 Per altre informazioni sugli handle di connessione, vedere [handle di connessione](../../../odbc/reference/develop-app/connection-handles.md).
