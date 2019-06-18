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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cf6d8d056c1658a924de4b108d3c0d025e8a58f1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63313395"
---
# <a name="sql-92-compliance"></a>Conformità SQL-92
I driver di Database Desktop ODBC e di gestione di Microsoft Jet sottostante non sono compatibili con SQL-92. Supportano molte funzionalità che sono state definite in SQL-92. Alcune funzionalità è supportata nel driver non sono supportati in SQL-92. Per altre informazioni, vedere la *Guida per programmatori di Microsoft Jet Database Engine*. Di seguito è le differenze principali tra i due:  
  
-   Il codice SQL usato dai driver di Database Desktop supporta espressioni più efficaci rispetto a quelli specificati dal SQL-92.  
  
-   Diverse regole si applicano al predicato BETWEEN.  
  
-   Il codice SQL utilizzato dal driver di Database Desktop e ANSI SQL supporta le parole chiave diverse.  
  
 Le seguenti funzionalità di SQL-92 non sono supportate da Microsoft Jet SQL:  
  
-   Istruzioni di sicurezza, ad esempio GRANT e blocco.  
  
-   Parola chiave DISTINCT con riferimenti a funzioni di aggregazione.  
  
 Miglioramenti nel linguaggio SQL utilizzato per i driver di Database Desktop non sono specificati da SQL-92 sono le seguenti funzionalità:  
  
-   L'istruzione di trasformazione che fornisce supporto per le query a campi incrociati.  
  
-   Altre funzioni di aggregazione (**StDev** e **VarP**).  
  
> [!NOTE]  
>  I driver di Database Desktop supportano la sintassi ANSI standard per % (percentuale) e _ (carattere di sottolineatura), non * (asterisco) e? (punto interrogativo).
