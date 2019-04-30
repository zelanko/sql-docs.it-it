---
title: Origine dati i nomi e i sistemi operativi a 64 Bit | Documenti di Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: c2f86810-2775-4ddd-8df7-e8373785a7fc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4007543cbe06b8b80c28a3a2a35c1a3c3fdbb525
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63205863"
---
# <a name="data-source-names-and-64-bit-operating-systems"></a>Nomi di origine dati e sistemi operativi a 64 bit
  Per compilare ed eseguire un'applicazione come applicazione a 32 bit in un sistema operativo a 64 bit, è necessario creare l'origine dati ODBC con Amministratore ODBC in %windir%\SysWOW64\odbcad32.exe.  
  
## <a name="remarks"></a>Note  
 Un sistema operativo Windows a 64 bit include due file odbcad32.exe:  
  
-   %SystemRoot%\system32\odbcad32.exe viene utilizzato per creare e gestire nomi di origine dati per applicazioni a 64 bit.  
  
-   %SystemRoot%\SysWOW64\odbcad32.exe viene utilizzato per creare e gestire nomi di origine dati per applicazioni a 32 bit, incluse le applicazioni a 32 bit in esecuzione in sistemi operativi a 64 bit.  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Native Client &#40;ODBC&#41;](sql-server-native-client-odbc.md)  
  
  
