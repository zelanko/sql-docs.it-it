---
title: Uso di applicazioni a 16 Bit con driver a 32 Bit | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3ebd6f25758f73e75fd96abb734bc7b0347d5ee0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63209981"
---
# <a name="using-16-bit-applications-with-32-bit-drivers"></a>Uso delle applicazioni a 16 bit con driver a 32 bit
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzarla nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che utilizzano attualmente questa funzionalità. Usare invece Gestione driver a 32 o 64 bit.  
  
 È possibile eseguire applicazioni a 16 bit con driver a 32 bit nel sistema basato su Windows, purché il driver a 32 bit non chiama in modo esplicito le funzioni API Win32 che creano thread. Il Windows nel sottosistema Windows (WOW) esegue le applicazioni in modalità a 16 bit e risolve le chiamate a 16 bit del sistema operativo. ODBC thunk delle chiamate a 16 bit DLL resolve dall'applicazione al driver a 32 bit. Le applicazioni a 16 bit usano l'API di Windows e driver a 32 bit usano l'API Win32.  
  
## <a name="architecture"></a>Architecture  
 La figura seguente mostra le applicazioni a 16 come comunicare con driver a 32 bit. Tra la gestione di Driver a 16 bit e il driver a 32 bit sono generici thunk delle DLL che consentono di convertire le chiamate ODBC 16 bit a chiamate ODBC 32-bit.  
  
 ![16 come&#45;di comunicare con 32 bit app&#45;i driver di bit](../../odbc/microsoft/media/sdka2.gif "sdka2")  
  
> [!NOTE]  
>  Ogni volta che un'applicazione a 16 bit interagisce con un driver a 32 bit, la gestione di Driver a 32 bit restituisce sempre "2.0" come versione di ODBC supportati dal driver.  
  
## <a name="administration"></a>Amministrazione  
 È possibile gestire le origini dati per i driver a 32 bit con l'amministratore dell'origine dati ODBC. Per aprire l'amministratore ODBC in computer che eseguono Microsoft® Windows® 2000, aprire il pannello di controllo di Windows, fare doppio clic su **strumenti di amministrazione**, quindi fare doppio clic su **origini dati (ODBC)** . Nei computer che eseguono versioni precedenti di Microsoft Windows, l'icona è denominata **ODBC a 32 bit** o semplicemente **ODBC**.  
  
 La figura seguente mostra come un'applicazione a 16 bit chiama una DLL di installazione di driver a 32 bit. Tra il programma di installazione a 16 bit DLL e il driver a 32 bit DLL di installazione è una DLL thunk generica che converte le chiamate DLL programma di installazione a 16 bit in chiamate DLL programma di installazione a 32 bit.  
  
 ![Come un 16&#45;app bit chiama un 32&#45;di tipo bit DLL di installazione driver](../../odbc/microsoft/media/sdka3.gif "sdka3")  
  
 In Windows in Windows (thunk di 16 bit a 32 bit), una DLL thunk aggiuntiva denominata Ds32gt converte i valori di argomento a 16 bit passati tramite un programma di installazione a 32 bit DLL eseguire il backup a 16 bit.  
  
## <a name="components"></a>Componenti  
 Il componente ODBC del SDK di MDAC 2.8 SP1 include i file seguenti per l'esecuzione di applicazioni a 16 bit con driver a 32 bit. Questi componenti si trovano nella directory \Redist.  
  
|Nome file|Descrizione|  
|---------------|-----------------|  
|Odbc16gt.dll|DLL thunk di 16 bit ODBC generico|  
|Odbc32gt.dll|ODBC generico thunk DLL a 32 bit|  
|Odbccp32.dll|DLL di installazione a 32 bit|  
|Odbcad32.exe|programma di amministrazione di 32 bit|  
|Odbcinst.hlp|File di programma di installazione della Guida|  
|Ds16gt.dll|installazione di driver a 16 bit generico thunk delle DLL|  
|Ctl3d32.dll|raccolta di stili di finestra tridimensionale a 32 bit|  
  
 Inoltre, i file seguenti con la gestione dei Driver di ODBC 2.10 16 bit, che non fanno parte di ODBC 3.51, richiesti dal e devono essere installati con l'applicazione a 16 bit.  
  
|Nome file|Descrizione|  
|---------------|-----------------|  
|Odbc.dll|Gestione Driver a 16 bit|  
|Odbcinst.dll|DLL di installazione a 16 bit|  
|Odbcadm.exe|programma di amministrazione di ODBC 16 bit|
