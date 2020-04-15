---
title: Utilizzo di applicazioni a 16 bit con driver a 32 bit Documenti Microsoft
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307632"
---
# <a name="using-16-bit-applications-with-32-bit-drivers"></a>Uso delle applicazioni a 16 bit con driver a 32 bit
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzare questa funzionalità nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che attualmente utilizzano questa funzionalità. Utilizzare invece Gestione driver a 32 o 64 bit.  
  
 È possibile eseguire applicazioni a 16 bit con driver a 32 bit nel sistema basato su Windows, purché il driver a 32 bit non chiami in modo esplicito le funzioni API Win32 che creano thread. Il sottosistema Windows on Windows (WOW) esegue le applicazioni in modalità a 16 bit e risolve le chiamate a 16 bit al sistema operativo. Le DLL di thunking ODBC risolvono le chiamate a 16 bit dall'applicazione ai driver a 32 bit. Le applicazioni a 16 bit utilizzano l'API di Windows e i driver a 32 bit utilizzano l'API Win32.  
  
## <a name="architecture"></a>Architecture  
 Nella figura seguente viene illustrato come le applicazioni a 16 bit comunicano con i driver a 32 bit. Tra Gestione Driver a 16 bit e i driver a 32 bit sono generiche DLL thunking che convertono chiamate ODBC a 16 bit in chiamate ODBC a 32 bit.  
  
 ![Comunicazione di 16 app a bit&#45;con driver a 32&#45;bit](../../odbc/microsoft/media/sdka2.gif "sdka2 (informazioni in due)")  
  
> [!NOTE]  
>  Ogni volta che un'applicazione a 16 bit interagisce con un driver a 32 bit, Gestione Driver a 32 bit restituisce sempre "2.0" come versione di ODBC supportata dal driver.  
  
## <a name="administration"></a>Amministrazione  
 È possibile gestire le origini dati per i driver a 32 bit utilizzando l'Amministratore origine dati ODBC. Per aprire l'Amministratore ODBC nei computer che eseguono Microsoft® Windows® 2000, aprire il Pannello di controllo di Windows, fare doppio clic su **Strumenti di amministrazione**, quindi su Origini dati **(ODBC)**. Nei computer che eseguono versioni precedenti di Microsoft Windows, l'icona è denominata **ODBC a 32 bit** o semplicemente **ODBC**.  
  
 Nella figura seguente viene illustrato come un'applicazione a 16 bit chiama una DLL di installazione del driver a 32 bit. Tra la DLL del programma di installazione a 16 bit e la DLL di installazione del driver a 32 bit è una DLL tunking generica che converte le chiamate DLL del programma di installazione a 16 bit in chiamate DLL del programma di installazione a 32 bit.  
  
 ![Come un'applicazione a 16&#45;bit chiama una DLL di installazione del driver a 32&#45;bitHow a 16&#45;bit app calls a 32&#45;bit driver setup DLL](../../odbc/microsoft/media/sdka3.gif "sdka3 (informazioni in due)")  
  
 In Windows su Windows (thunking da 16 bit a 32 bit), una DLL tunking aggiuntiva denominata Ds32gt.dll converte i valori degli argomenti a 16 bit passati tramite una DLL di installazione a 32 bit a 16 bit.  
  
## <a name="components"></a>Componenti  
 Il componente ODBC di MDAC 2.8 SP1 SDK include i file seguenti per l'esecuzione di applicazioni a 16 bit con driver a 32 bit. Questi componenti si trovano nella directory Redist.  
  
|Nome file|Descrizione|  
|---------------|-----------------|  
|Odbc16gt.dll|DLL tunking generica ODBC a 16 bit|  
|Odbc32gt.dll|DLL di thunking generica ODBC a 32 bit|  
|Odbccp32.dll (informazioni in stati intratto)|DLL del programma di installazione a 32 bit|  
|Odbcad32.exe (informazioni in o via in cui è stato inesulto)|Programma di amministrazione a 32 bit|  
|Odbcinst.hlp|File della Guida del programma di installazione|  
|Ds16gt.dll|DLL tunking generica di installazione del driver a 16 bit|  
|Ctl3d32.dll|Libreria di stili tridimensionali della finestra a 32 bit|  
  
 Inoltre, i seguenti file insieme a Gestione driver ODBC 2.10 a 16 bit, che non fanno parte di ODBC 3.51, sono necessari da e devono essere installati con l'applicazione a 16 bit.  
  
|Nome file|Descrizione|  
|---------------|-----------------|  
|Odbc.dll|Gestione driver a 16 bit|  
|Odbcinst.dll|DLL del programma di installazione a 16 bit|  
|Odbcadm.exe|Programma di amministrazione ODBC a 16 bit|
