---
title: Allocazione dell'handle dell'ambiente | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303004"
---
# <a name="allocating-the-environment-handle"></a>Allocazione dell'handle di ambiente
La prima attività per qualsiasi applicazione ODBC consiste nel caricare Gestione driver; il modo in cui questa operazione viene eseguita dipende dal sistema operativo. Ad esempio, in un computer in cui è in esecuzione Microsoft® Windows NT® Server/Windows 2000 Server, Windows NT Workstation/Windows 2000 Professional o Microsoft Windows® 95/98, l'applicazione è collegata alla libreria di gestione driver oppure chiama **LoadLibrary** per caricare la dll di gestione driver.  
  
 L'attività successiva, che deve essere eseguita prima che un'applicazione possa chiamare qualsiasi altra funzione ODBC, consiste nell'inizializzare l'ambiente ODBC e nell'allocazione di un handle di ambiente, come indicato di seguito:  
  
1.  L'applicazione dichiara una variabile di tipo SQLHENV. Chiama quindi **SQLAllocHandle** e passa l'indirizzo di questa variabile e l'opzione SQL_HANDLE_ENV. Ad esempio:  
  
    ```  
    SQLHENV henv1;  
  
    SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv1);  
    ```  
  
2.  Gestione driver alloca una struttura in cui archiviare le informazioni sull'ambiente e restituisce l'handle di ambiente nella variabile.  
  
 Gestione driver non chiama **SQLAllocHandle** nel driver in questo momento perché non sa quale driver chiamare. Ritarda la chiamata a **SQLAllocHandle** nel driver fino a quando l'applicazione non chiama una funzione per connettersi a un'origine dati. Per ulteriori informazioni, vedere [ruolo di gestione driver nel processo di connessione](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md), più avanti in questa sezione.  
  
 Quando l'applicazione ha terminato di usare ODBC, libera l'handle di ambiente con **SQLFreeHandle**. Dopo aver liberato l'ambiente, si tratta di un errore di programmazione dell'applicazione che usa l'handle dell'ambiente in una chiamata a una funzione ODBC. Questa operazione ha conseguenze indefinite ma probabilmente fatali.  
  
 Quando viene chiamato **SQLFreeHandle** , il driver rilascia la struttura utilizzata per archiviare le informazioni sull'ambiente. Si noti che non è possibile chiamare **SQLFreeHandle** per un handle di ambiente fino a quando non sono stati liberati tutti gli handle di connessione su tale handle di ambiente.  
  
 Per ulteriori informazioni sull'handle di ambiente, vedere [handle di ambiente](../../../odbc/reference/develop-app/environment-handles.md).
