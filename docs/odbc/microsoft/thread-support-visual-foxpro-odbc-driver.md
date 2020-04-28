---
title: Supporto di thread (driver ODBC Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- thread support [ODBC]
- Visual FoxPro ODBC driver [ODBC], thread support
- FoxPro ODBC driver [ODBC], thread support
- multithreaded applications [ODBC]
ms.assetid: 0c6abbbc-012b-41aa-bded-5e7e362d015b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2aa19eb233525b5a65ef67fe9903814fc1163177
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303082"
---
# <a name="thread-support-visual-foxpro-odbc-driver"></a>Supporto dei thread (driver ODBC Visual FoxPro)
Il driver ODBC Visual FoxPro è thread-safe. L'accesso a handle di ambiente (*Hen*), handle di connessione (*HDBC*) e handle di istruzione (*HSTMT*) viene incapsulato in semafori appropriati per impedire ad altri processi di accedere e potenzialmente modificare le strutture di dati interne del driver.  
  
 In un'applicazione multithread è possibile annullare una funzione in esecuzione in modo sincrono su un *HSTMT* chiamando [SQLCancel](../../odbc/microsoft/sqlcancel-visual-foxpro-odbc-driver.md) su un thread separato.  
  
 Il driver utilizza un thread separato per recuperare i dati quando si utilizza il recupero progressivo. Per utilizzare il recupero progressivo per un'origine dati, selezionare la casella di controllo **Recupera dati in background** nella finestra di [dialogo Configurazione ODBC Visual FoxPro](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md) oppure utilizzare la parola chiave dell'attributo BackgroundFetch nella stringa di connessione. Evitare di utilizzare il recupero in background quando si chiama il driver da applicazioni multithread. Per informazioni sulle parole chiave degli attributi della stringa di connessione, vedere [utilizzo delle stringhe di connessione](../../odbc/microsoft/using-connection-strings.md).  
  
 Per ulteriori informazioni sui thread e **SQLCancel**, vedere [SQLCancel](../../odbc/reference/syntax/sqlcancel-function.md) in *ODBC Programmer ' s Reference*.
