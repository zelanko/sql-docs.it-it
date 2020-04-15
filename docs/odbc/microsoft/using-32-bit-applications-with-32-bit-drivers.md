---
title: Utilizzo di applicazioni a 32 bit con driver a 32 bit Documenti Microsoft
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307602"
---
# <a name="using-32-bit-applications-with-32-bit-drivers"></a>Uso delle applicazioni a 32 bit con driver a 32 bit
È possibile eseguire applicazioni a 32 bit con driver a 32 bit. Le applicazioni a 32 bit e i driver a 32 bit utilizzano l'API Win32®.  
  
## <a name="architecture"></a>Architecture  
 Nella figura seguente viene illustrato come le applicazioni a 32 bit comunicano con i driver a 32 bit. L'applicazione chiama Gestione Driver a 32 bit, che a sua volta chiama i driver a 32 bit.  
  
 ![Comunicazione con driver a 32&#45;bit da 32&#45;bit](../../odbc/microsoft/media/sdka6.gif "sdka6 (informazioni in inglese)")  
  
> [!IMPORTANT]  
>  Non utilizzare la DLL del programma di installazione del thunking a 32 bit in WindowsNT/Windows2000. Anche se ha lo stesso nome di file della DLL del programma di installazione a 32 bit, è una DLL diversa.  
  
## <a name="administration"></a>Amministrazione  
 È possibile gestire le origini dati per i driver a 32 bit utilizzando l'Amministratore origine dati ODBC. Per aprire l'Amministratore ODBC nei computer che eseguono Windows 2000, aprire il Pannello di controllo di Windows, fare doppio clic su **Strumenti di amministrazione**, quindi su Origini dati **(ODBC)**. Nei computer che eseguono versioni precedenti di Microsoft Windows, l'icona è denominata **ODBC a 32 bit** o semplicemente **ODBC**.  
  
## <a name="components"></a>Componenti  
 Il componente ODBC include i seguenti file per l'esecuzione di applicazioni a 32 bit con driver a 32 bit. Questi componenti si trovano nella directory Redist.  
  
|Nome file|Descrizione|  
|---------------|-----------------|  
|Odbc32.dll|Gestione driver a 32 bit|  
|Odbccp32.dll (informazioni in stati intratto)|DLL del programma di installazione a 32 bit|  
|Odbcad32.exe (informazioni in o via in cui è stato inesulto)|Programma di amministrazione ODBC a 32 bit|  
|Odbcinst.hlp|File della Guida del programma di installazione|  
|Msvcrt40.dll|Libreria di runtime del c|
