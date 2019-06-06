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
manager: jroth
ms.openlocfilehash: 7eb96d739a95e1b75894ab3f561f6db3c6661a21
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66699822"
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
  
-   *msado27.tlb*, ADO 2.7 Type Library  
  
-   *msado26.tlb*, ADO 2.6 Type Library  
  
-   *msado25.tlb*, ADO 2.5 Type Library  
  
-   *msado21.tlb*, ADO 2.1 Type Library  
  
-   *msado20.tlb*, ADO 2.0 Type Library
