---
title: Allocare l'Handle di ambiente | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], environment handles
- allocating environment handles [ODBC]
- connecting to driver [ODBC], environment handles
- environment handles [ODBC]
- data sources [ODBC], environment handles
- connecting to data source [ODBC], environment handles
- handles [ODBC], environment
ms.assetid: 77b5d1d6-7eb7-428d-bf75-a5c5a325d25c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7a8eefe5bc6678462099afda8381d6b16bd076dd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63287670"
---
# <a name="allocating-the-environment-handle"></a>Allocazione dell'handle di ambiente
La prima attività per qualsiasi applicazione ODBC consiste nel caricare il Driver Manager; Questa operazione è dipendente dal sistema operativo. Ad esempio, in un computer che eseguono Microsoft® Windows NT® Server o Windows 2000 Server, Windows NT Workstation o Windows 2000 Professional o Microsoft Windows® 95 o 98, l'applicazione sia collegata alla libreria di gestione Driver o chiamate  **LoadLibrary** a caricare la DLL di gestione Driver.  
  
 L'attività successiva, che deve essere eseguita prima di un'applicazione può chiamare qualsiasi altra funzione ODBC, consiste nell'inizializzare l'ambiente ODBC e allocare un handle di ambiente, come indicato di seguito:  
  
1.  L'applicazione dichiara una variabile di tipo SQLHENV. Chiama poi **SQLAllocHandle** e passa l'indirizzo di questa variabile e l'opzione SQL_HANDLE_ENV. Ad esempio:   
  
    ```  
    SQLHENV henv1;  
  
    SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv1);  
    ```  
  
2.  Gestione Driver alloca una struttura in cui archiviare informazioni sull'ambiente e restituisce l'handle di ambiente nella variabile.  
  
 Gestione Driver non chiama **SQLAllocHandle** nel driver di questo tempo, poiché non conosce il driver da chiamare. Ritardare la chiamata **SQLAllocHandle** nel driver fino a quando l'applicazione chiama una funzione per la connessione a un'origine dati. Per altre informazioni, vedere [ruolo di gestione Driver nel processo di connessione](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md), più avanti in questa sezione.  
  
 Quando l'applicazione ha terminato l'utilizzo di ODBC, rilascia l'handle di ambiente con **SQLFreeHandle**. Dopo avere liberato l'ambiente, è un'applicazione un errore di programmazione per l'uso di handle dell'ambiente in una chiamata a una funzione ODBC; Questa operazione ha conseguenze non definiti, ma probabilmente irreversibile.  
  
 Quando **SQLFreeHandle** viene chiamato, le versioni di driver la struttura utilizzata per archiviare le informazioni sull'ambiente. Si noti che **SQLFreeHandle** non può essere chiamato per un handle di ambiente fino a dopo che tutti gli handle di connessione su tale handle di ambiente sono stati liberati.  
  
 Per altre informazioni sull'handle di ambiente, vedere [gestisce l'ambiente](../../../odbc/reference/develop-app/environment-handles.md).
