---
title: Thread di supporto (Driver ODBC Visual FoxPro) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 77187802bb57a832263ec2070564754e87f21345
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62632924"
---
# <a name="thread-support-visual-foxpro-odbc-driver"></a>Supporto dei thread (driver ODBC Visual FoxPro)
Il Driver ODBC Visual FoxPro è thread-safe. Accesso agli handle di ambiente (*uando*), gli handle di connessione (*hdbc*) e gli handle di istruzione (*hstmt*) viene eseguito il wrapping in semafori appropriati per impedire ad altri processi accedere e potenzialmente modificare le strutture dati interne del driver.  
  
 In un'applicazione multithreading, è possibile annullare una funzione che è in esecuzione in modo sincrono in un' *hstmt* chiamando [SQLCancel](../../odbc/microsoft/sqlcancel-visual-foxpro-odbc-driver.md) su un thread separato.  
  
 Il driver Usa un thread separato per recuperare i dati quando si usa il recupero progressivo. Per utilizzare il recupero progressivo per un'origine dati, selezionare la **recuperare i dati in background** casella di controllo la [nella finestra di dialogo programma di installazione di ODBC Visual FoxPro](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md) o usare la parola chiave attributi BackgroundFetch nella propria connessione stringa. Evitare l'utilizzo di recupero in background quando si chiama il driver da applicazioni multithread. Per informazioni sulle parole chiave attributo di stringa di connessione, vedere [uso di stringhe di connessione](../../odbc/microsoft/using-connection-strings.md).  
  
 Per altre informazioni sui thread e **SQLCancel**, vedere [SQLCancel](../../odbc/reference/syntax/sqlcancel-function.md) nel *riferimento per programmatori ODBC*.
