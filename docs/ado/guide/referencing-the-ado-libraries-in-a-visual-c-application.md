---
title: Riferimenti alle librerie ADO In un'applicazione Visual C++ | Microsoft Docs
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- libraries [ADO]
- referencing libraries in a Visual C++ application[ADO]
- ADO, libraries
ms.assetid: d3ea12ec-bca8-48c3-af57-ce14576108c9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 62fb1b89299af1f466e446c8adba422a841f0196
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67923028"
---
# <a name="referencing-the-ado-libraries-in-a-visual-c-application"></a>Riferimenti alle librerie ADO in un'applicazione Visual C++
Per usare la versione più recente di ADO in un'applicazione Visual C++, usare il comando seguente `#import` direttiva:  
  
```cpp
#import "msado15.dll" \  
    no_namespace rename("EOF", "EndOfFile")  
```  
  
 Per utilizzare ADO MD o ADOX, è necessario importare *msadomd* oppure *Msadox*, usando la sintassi precedente.  
  
## <a name="backward-compatibility"></a>Backward Compatibility  
 Per usare qualsiasi versione precedente di ADO, sostituire *msado15.dll* sopra con una delle librerie dei tipi seguenti.  
  
-   *msado27.tlb*, libreria dei tipi 2.7 ADO  
  
-   *msado26.tlb*, ADO 2.6 libreria di tipi  
  
-   *msado25.tlb*, libreria dei tipi 2,5 ADO  
  
-   *Msado21*, libreria dei tipi 2.1 ADO  
  
-   *msado20.tlb*, libreria dei tipi 2.0 ADO
