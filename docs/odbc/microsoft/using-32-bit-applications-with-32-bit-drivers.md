---
title: Uso di applicazioni a 32 Bit con driver a 32 Bit | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], 32-bit applications
- 32-bit applications with 32-bit drivers [ODBC]
ms.assetid: 0cdd5788-5642-4280-8d53-b4ec461aafa1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5c4f0b21bba9e56cad076ae08f5a561cc972d2ff
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63213467"
---
# <a name="using-32-bit-applications-with-32-bit-drivers"></a>Uso delle applicazioni a 32 bit con driver a 32 bit
È possibile eseguire applicazioni a 32 bit con driver a 32 bit. Le applicazioni a 32 bit e il driver a 32 bit è possibile usare l'API Win32®.  
  
## <a name="architecture"></a>Architecture  
 La figura seguente mostra le applicazioni a 32 come comunicare con driver a 32 bit. L'applicazione chiama il gestore dei Driver a 32 bit che a sua volta chiama driver a 32 bit.  
  
 ![Come 32&#45;di comunicare con 32 bit app&#45;i driver di bit](../../odbc/microsoft/media/sdka6.gif "sdka6")  
  
> [!IMPORTANT]  
>  Non usare l'installazione thunk DLL a 32 bit su Windows NT o Windows 2000. Anche se presenta lo stesso nome di file del programma di installazione a 32 bit DLL, è un'altra DLL.  
  
## <a name="administration"></a>Amministrazione  
 È possibile gestire le origini dati per i driver a 32 bit con l'amministratore dell'origine dati ODBC. Per aprire l'amministratore ODBC in computer che eseguono Windows 2000, aprire il pannello di controllo di Windows, fare doppio clic su **strumenti di amministrazione**, quindi fare doppio clic su **origini dati (ODBC)**. Nei computer che eseguono versioni precedenti di Microsoft Windows, l'icona è denominata **ODBC a 32 bit** o semplicemente **ODBC**.  
  
## <a name="components"></a>Componenti  
 Il componente ODBC include i file seguenti per l'esecuzione di applicazioni a 32 bit con driver a 32 bit. Questi componenti si trovano nella directory \Redist.  
  
|Nome file|Descrizione|  
|---------------|-----------------|  
|Odbc32.dll|Gestione Driver a 32 bit|  
|Odbccp32.dll|DLL di installazione a 32 bit|  
|Odbcad32.exe|programma di amministrazione di ODBC 32-bit|  
|Odbcinst.hlp|File di programma di installazione della Guida|  
|Msvcrt40.dll|Libreria di runtime C|
