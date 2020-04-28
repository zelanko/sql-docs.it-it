---
title: Uso di applicazioni a 32 bit con driver a 32 bit | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 31512f9339b9d46225bb4f1198cb617a48509acb
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307602"
---
# <a name="using-32-bit-applications-with-32-bit-drivers"></a>Uso delle applicazioni a 32 bit con driver a 32 bit
È possibile eseguire applicazioni a 32 bit con driver a 32 bit. Le applicazioni a 32 bit e i driver a 32 bit utilizzano l'API Win32®.  
  
## <a name="architecture"></a>Architecture  
 Nella figura seguente viene illustrato il modo in cui le applicazioni a 32 bit comunicano con i driver a 32 bit. L'applicazione chiama Gestione driver a 32 bit, che a sua volta chiama i driver a 32 bit.  
  
 ![Modalità di comunicazione delle app&#45;bit 32 con i driver di bit per la&#45;32](../../odbc/microsoft/media/sdka6.gif "sdka6")  
  
> [!IMPORTANT]  
>  Non usare la DLL del programma di installazione di thunk a 32 bit in WindowsNT/Windows2000. Anche se ha lo stesso nome di file della DLL del programma di installazione a 32 bit, è un'altra DLL.  
  
## <a name="administration"></a>Amministrazione  
 È possibile gestire le origini dati per i driver a 32 bit tramite Amministrazione origine dati ODBC. Per aprire Amministratore ODBC nei computer che eseguono Windows 2000, aprire il pannello di controllo di Windows, fare doppio clic su **strumenti di amministrazione**, quindi fare doppio clic su **origini dati (ODBC)**. Nei computer che eseguono versioni precedenti di Microsoft Windows, l'icona è denominata **ODBC a 32 bit** o semplicemente **ODBC**.  
  
## <a name="components"></a>Componenti  
 Il componente ODBC include i file seguenti per l'esecuzione di applicazioni a 32 bit con driver a 32 bit. Questi componenti si trovano nella directory redist  
  
|Nome file|Descrizione|  
|---------------|-----------------|  
|Odbc32. dll|Gestione driver a 32 bit|  
|Odbccp32. dll|DLL del programma di installazione a 32 bit|  
|Odbcad32. exe|programma di amministrazione ODBC a 32 bit|  
|Odbcinst. hlp|File della guida del programma di installazione|  
|MSVCRT40. dll|Libreria di runtime C|
