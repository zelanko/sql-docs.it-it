---
title: Allocazione dell'handle dell'ambiente Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e33b850b2786960a368720deaf89a2203c7dd159
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303004"
---
# <a name="allocating-the-environment-handle"></a>Allocazione dell'handle di ambiente
La prima attività per qualsiasi applicazione ODBC consiste nel caricare Gestione Driver; come questo viene fatto dipende dal sistema operativo. Ad esempio, in un computer che esegue Microsoft® Windows NT® Server/Windows 2000 Server, Windows NT Workstation/Windows 2000 Professional o Microsoft Windows® 95/98, l'applicazione si collega alla libreria Gestione Driver o chiama **LoadLibrary** per caricare la DLL di Gestione Driver.  
  
 L'attività successiva, che deve essere eseguita prima che un'applicazione possa chiamare qualsiasi altra funzione ODBC, consiste nell'inizializzare l'ambiente ODBC e allocare un handle di ambiente, come indicato di seguito:The next task, which must be done before an application can call any other ODBC function, is to initialize the ODBC environment and allocate an environment handle, as follows:  
  
1.  L'applicazione dichiara una variabile di tipo SQLHENV. Chiama quindi **SQLAllocHandle** e passa l'indirizzo di questa variabile e l'opzione SQL_HANDLE_ENV. Ad esempio:  
  
    ```  
    SQLHENV henv1;  
  
    SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv1);  
    ```  
  
2.  Gestione Driver alloca una struttura in cui archiviare le informazioni sull'ambiente e restituisce l'handle di ambiente nella variabile.  
  
 Gestione Driver non chiama **SQLAllocHandle** nel driver in questo momento perché non sa quale driver da chiamare. Ritarda la chiamata **SQLAllocHandle** nel driver fino a quando l'applicazione chiama una funzione per connettersi a un'origine dati. Per ulteriori informazioni, vedere [Ruolo di Gestione Driver nel processo](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)di connessione , più avanti in questa sezione.  
  
 Al termine dell'utilizzo di ODBC, l'handle di ambiente con **SQLFreeHandle**consente di liberare l'handle dell'ambiente. Dopo aver liberato l'ambiente, è un errore di programmazione dell'applicazione utilizzare l'handle dell'ambiente in una chiamata a una funzione ODBC; così facendo ha conseguenze indefinite, ma probabilmente fatali.  
  
 Quando **SQLFreeHandle** viene chiamato, il driver rilascia la struttura utilizzata per archiviare le informazioni sull'ambiente. Si noti che **SQLFreeHandle** non può essere chiamato per un handle di ambiente fino a dopo che tutti gli handle di connessione su tale handle di ambiente sono stati liberati.  
  
 Per ulteriori informazioni sull'handle di ambiente, vedere Handle di [ambiente](../../../odbc/reference/develop-app/environment-handles.md).
