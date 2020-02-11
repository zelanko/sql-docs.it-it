---
title: Riferimento alle librerie ADO in un'applicazione Visual C++ | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67923028"
---
# <a name="referencing-the-ado-libraries-in-a-visual-c-application"></a>Riferimenti alle librerie ADO in un'applicazione Visual C++
Per usare la versione più recente di ADO in un'applicazione Visual C++, usare la `#import` direttiva seguente:  
  
```cpp
#import "msado15.dll" \  
    no_namespace rename("EOF", "EndOfFile")  
```  
  
 Per utilizzare ADO MD o ADOX, è necessario importare *msadomd. dll* o *msadox. dll*utilizzando la sintassi precedente.  
  
## <a name="backward-compatibility"></a>Backward Compatibility  
 Per utilizzare una versione precedente di ADO, sostituire *msado15. dll* con una delle librerie dei tipi seguenti.  
  
-   *Msado27. tlb*, libreria di tipi ADO 2,7  
  
-   *msado26. tlb*, libreria di tipi ADO 2,6  
  
-   *Msado25. tlb*, libreria di tipi ADO 2,5  
  
-   *Msado21. tlb*, libreria di tipi ADO 2,1  
  
-   *msado20. tlb*, libreria di tipi ADO 2,0
