---
title: Uso di applicazioni a 16 bit con driver a 32 bit | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], 16-bit applications
- 16-bit applications with 32-bit drivers [ODBC]
ms.assetid: 68feb3b7-c01a-4f42-8df9-f9c182d89325
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c919ed8c3f3791720d67ebdcbf5cfbdbea2a0455
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307632"
---
# <a name="using-16-bit-applications-with-32-bit-drivers"></a>Uso delle applicazioni a 16 bit con driver a 32 bit
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzare questa funzionalità nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che attualmente utilizzano questa funzionalità. Utilizzare invece Gestione driver a 32 bit o 64 bit.  
  
 È possibile eseguire applicazioni a 16 bit con driver a 32 bit nel sistema basato su Windows, purché il driver a 32 bit non chiami in modo esplicito le funzioni API Win32 che creano thread. Il sottosistema Windows on Windows (WOW) esegue le applicazioni in modalità a 16 bit e risolve le chiamate a 16 bit al sistema operativo. Le DLL di thunk ODBC risolvono le chiamate a 16 bit dall'applicazione ai driver a 32 bit. Le applicazioni a 16 bit utilizzano l'API Windows e i driver a 32 bit utilizzano l'API Win32.  
  
## <a name="architecture"></a>Architecture  
 Nella figura seguente viene illustrato il modo in cui le applicazioni a 16 bit comunicano con driver a 32 bit. Tra la gestione driver a 16 bit e i driver a 32 bit sono dll di thunk generiche che convertono le chiamate ODBC a 16 bit in chiamate ODBC a 32 bit.  
  
 ![Modalità di comunicazione delle applicazioni a 16&#45;bit con driver&#45;bit di 32](../../odbc/microsoft/media/sdka2.gif "sdka2")  
  
> [!NOTE]  
>  Ogni volta che un'applicazione a 16 bit interagisce con un driver a 32 bit, gestione driver 32 bit restituisce sempre "2,0" come versione di ODBC supportata dal driver.  
  
## <a name="administration"></a>Amministrazione  
 È possibile gestire le origini dati per i driver a 32 bit tramite Amministrazione origine dati ODBC. Per aprire Amministratore ODBC nei computer che eseguono Microsoft® Windows® 2000, aprire il pannello di controllo di Windows, fare doppio clic su **strumenti di amministrazione**, quindi fare doppio clic su **origini dati (ODBC)**. Nei computer che eseguono versioni precedenti di Microsoft Windows, l'icona è denominata **ODBC a 32 bit** o semplicemente **ODBC**.  
  
 Nella figura seguente viene illustrato come un'applicazione a 16 bit chiama una DLL di installazione del driver a 32 bit. Tra la dll del programma di installazione a 16 bit e la DLL di installazione del driver a 32 bit è una DLL di thunk generica che converte le chiamate di DLL del programma di installazione a 16 bit in chiamate DLL del programma di installazione a 32 bit.  
  
 ![Come un'app a 16&#45;bit chiama una DLL di installazione del driver a 32 bit&#45;](../../odbc/microsoft/media/sdka3.gif "sdka3")  
  
 In Windows in Windows (da 16 bit a 32 bit), una DLL di thunk aggiuntiva denominata ds32gt. dll converte i valori degli argomenti a 16 bit passati attraverso una DLL di installazione a 32 bit a 16 bit.  
  
## <a name="components"></a>Componenti  
 Il componente ODBC di MDAC 2,8 SP1 SDK include i file seguenti per l'esecuzione di applicazioni a 16 bit con driver a 32 bit. Questi componenti si trovano nella directory redist  
  
|Nome file|Descrizione|  
|---------------|-----------------|  
|Odbc16gt. dll|DLL di thunk generici ODBC a 16 bit|  
|Odbc32gt. dll|DLL di thunk generico ODBC a 32 bit|  
|Odbccp32. dll|DLL del programma di installazione a 32 bit|  
|Odbcad32. exe|programma di amministrazione a 32 bit|  
|Odbcinst. hlp|File della guida del programma di installazione|  
|Ds16gt. dll|DLL di thunk generico per la configurazione di driver a 16 bit|  
|Ctl3d32. dll|libreria di stili della finestra tridimensionale a 32 bit|  
  
 Inoltre, i file seguenti insieme alla gestione driver ODBC 2,10 a 16 bit, che non fanno parte di ODBC 3,51, sono richiesti da e devono essere installati con l'applicazione a 16 bit.  
  
|Nome file|Descrizione|  
|---------------|-----------------|  
|ODBC. dll|Gestione driver a 16 bit|  
|Odbcinst. dll|DLL del programma di installazione a 16 bit|  
|ODBCADM. exe|programma di amministrazione ODBC a 16 bit|
