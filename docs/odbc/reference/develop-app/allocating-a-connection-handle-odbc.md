---
description: Allocazione di un handle di connessione ODBC
title: Allocazione di un handle di connessione ODBC | Microsoft Docs
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
ms.openlocfilehash: c6c17003ed3746f2953eb167f2dc3d944659e352
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456437"
---
# <a name="allocating-a-connection-handle-odbc"></a>Allocazione di un handle di connessione ODBC
Prima che l'applicazione possa connettersi a un'origine dati o a un driver, deve allocare un handle di connessione, come indicato di seguito:  
  
1.  L'applicazione dichiara una variabile di tipo SQLHDBC. Chiama quindi **SQLAllocHandle** e passa l'indirizzo di questa variabile, l'handle dell'ambiente in cui allocare la connessione e l'opzione SQL_HANDLE_DBC. Ad esempio:  
  
    ```  
    SQLHDBC hdbc1;  
  
    SQLAllocHandle(SQL_HANDLE_DBC, henv1, &hdbc1);  
    ```  
  
2.  Gestione driver alloca una struttura in cui archiviare le informazioni sull'istruzione e restituisce l'handle di connessione nella variabile.  
  
 Gestione driver non chiama **SQLAllocHandle** nel driver in questo momento perché non sa quale driver chiamare. Ritarda la chiamata a **SQLAllocHandle** nel driver fino a quando l'applicazione non chiama una funzione per connettersi a un'origine dati. Per ulteriori informazioni, vedere [ruolo di gestione driver nel processo di connessione](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md), più avanti in questa sezione.  
  
 È importante notare che l'allocazione di un handle di connessione non equivale al caricamento di un driver. Il driver non viene caricato fino a quando non viene chiamata una funzione di connessione. Quindi, dopo avere allocato un handle di connessione e prima di connettersi al driver o all'origine dati, le uniche funzioni che l'applicazione può chiamare con l'handle di connessione sono **SQLSetConnectAttr**, **SQLGetConnectAttr**o **SQLGetInfo** con l'opzione SQL_ODBC_VER. La chiamata di altre funzioni con l'handle di connessione, ad esempio **SQLEndTran**, restituisce SQLState 08003 (connessione non aperta). Per informazioni complete, vedere [Appendice B: tabelle di transizione dello stato ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
 Per ulteriori informazioni sugli handle di connessione, vedere [handle di connessione](../../../odbc/reference/develop-app/connection-handles.md).
