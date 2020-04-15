---
title: Conformità di SQL-92 Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], SQL-92 compliance
- desktop database drivers [ODBC], SQL-92 compliance
- SQL-92 compliance [ODBC]
- ODBC desktop database drivers [ODBC], SQL-92 compliance
ms.assetid: 50c8c7df-df01-4f4d-ad62-d059cf29d73a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9ac0ae5873e545afb8fcac9dd003c984b1ed303a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300701"
---
# <a name="sql-92-compliance"></a>Conformità SQL-92
I driver di database desktop ODBC e il motore Microsoft Jet sottostante non sono compatibili con SQL-92. Supportano molte funzionalità definite in SQL-92. Alcune funzionalità supportate nel driver non sono supportate in SQL-92. Per ulteriori informazioni, vedere *Microsoft Jet Database Engine Programmer's Guide*. Di seguito sono riportate le principali differenze tra i due:  
  
-   Il codice SQL utilizzato dai driver di database desktop supporta espressioni più potenti rispetto a quelle specificate da SQL-92.  
  
-   Al predicato BETWEEN si applicano regole diverse.  
  
-   Il codice SQL utilizzato dai driver di Database desktop e ANSI SQL supporta parole chiave diverse.  
  
 Le seguenti funzionalità di SQL-92 non sono supportate da Microsoft Jet SQL:  
  
-   Istruzioni di sicurezza, ad esempio GRANT e LOCK.  
  
-   DISTINCT con riferimenti a funzioni di aggregazione.  
  
 Le funzionalità seguenti sono miglioramenti apportati al codice SQL utilizzato dai driver di database desktop non specificati da SQL-92:  
  
-   Istruzione TRANSFORM che fornisce il supporto per le query a campi incrociati.  
  
-   Funzioni di aggregazione aggiuntive (**StDev** e **VarP**).  
  
> [!NOTE]  
>  I driver di database desktop supportano la sintassi ANSI standard per % (percentuale) e _ (carattere di sottolineatura), non (asterisco) e ? (punto interrogativo).
