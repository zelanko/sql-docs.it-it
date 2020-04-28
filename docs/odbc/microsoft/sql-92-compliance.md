---
title: Conformità SQL-92 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300701"
---
# <a name="sql-92-compliance"></a>Conformità SQL-92
I driver del database desktop ODBC e il motore Microsoft Jet sottostante non sono conformi a SQL-92. Supportano numerose funzionalità definite in SQL-92. Alcune funzionalità supportate nel driver non sono supportate in SQL-92. Per ulteriori informazioni, vedere la *Guida per programmatori Microsoft Jet motore di database*. Di seguito sono riportate le principali differenze tra le due:  
  
-   Il database SQL utilizzato dai driver del database desktop supporta espressioni più potenti rispetto a quelle specificate da SQL-92.  
  
-   Regole diverse si applicano al predicato BETWEEN.  
  
-   SQL utilizzato dai driver del database desktop e ANSI SQL supporta parole chiave diverse.  
  
 Le funzionalità SQL-92 seguenti non sono supportate da Microsoft Jet SQL:  
  
-   Istruzioni di sicurezza, ad esempio GRANT e LOCK.  
  
-   DISTINCT con riferimenti a funzioni di aggregazione.  
  
 Le funzionalità seguenti sono i miglioramenti apportati a SQL utilizzati dai driver del database desktop non specificati da SQL-92:  
  
-   L'istruzione TRANSFORM fornisce supporto per le query a campi incrociati.  
  
-   Funzioni di aggregazione aggiuntive (**StDev** e **VarP**).  
  
> [!NOTE]  
>  I driver del database desktop supportano la sintassi standard ANSI per% (percentuale) e _ (carattere di sottolineatura), non * (asterisco) e? (punto interrogativo).
