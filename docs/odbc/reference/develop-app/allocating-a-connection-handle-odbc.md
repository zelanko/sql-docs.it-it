---
title: Allocazione di un handle di connessione ODBC Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 12e9f65ee81612e269c1f86ebabd049588443cb8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288521"
---
# <a name="allocating-a-connection-handle-odbc"></a>Allocazione di un handle di connessione ODBC
Prima che l'applicazione possa connettersi a un'origine dati o a un driver, deve allocare un handle di connessione, come indicato di seguito:Before the application can connect to a data source or driver, it must allocate a connection handle, as follows:  
  
1.  L'applicazione dichiara una variabile di tipo SQLHDBC. Chiama quindi **SQLAllocHandle** e passa l'indirizzo di questa variabile, l'handle dell'ambiente in cui allocare la connessione e l'opzione SQL_HANDLE_DBC. Ad esempio:  
  
    ```  
    SQLHDBC hdbc1;  
  
    SQLAllocHandle(SQL_HANDLE_DBC, henv1, &hdbc1);  
    ```  
  
2.  Gestione Driver alloca una struttura in cui archiviare le informazioni sull'istruzione e restituisce l'handle di connessione nella variabile.  
  
 Gestione Driver non chiama **SQLAllocHandle** nel driver in questo momento perché non sa quale driver da chiamare. Ritarda la chiamata **SQLAllocHandle** nel driver fino a quando l'applicazione chiama una funzione per connettersi a un'origine dati. Per ulteriori informazioni, vedere [Ruolo di Gestione Driver nel processo](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)di connessione , più avanti in questa sezione.  
  
 È importante notare che l'allocazione di un handle di connessione non equivale al caricamento di un driver. Il driver non viene caricato fino a quando non viene chiamata una funzione di connessione. Pertanto, dopo aver allocato un handle di connessione e prima di connettersi al driver o all'origine dati, le uniche funzioni che l'applicazione può chiamare con l'handle di connessione sono **SQLSetConnectAttr**, **SQLGetConnectAttr**o **SQLGetInfo** con l'opzione SQL_ODBC_VER. La chiamata ad altre funzioni con l'handle di connessione, ad esempio **SQLEndTran**, restituisce SQLSTATE 08003 (connessione non aperta). Per informazioni dettagliate, vedere [Appendice B: tabelle](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)di transizione dello stato ODBC .  
  
 Per ulteriori informazioni sugli handle di connessione, vedere [Handle di connessione](../../../odbc/reference/develop-app/connection-handles.md).
