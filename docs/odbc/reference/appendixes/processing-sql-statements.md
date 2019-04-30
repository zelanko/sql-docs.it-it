---
title: L'elaborazione delle istruzioni SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], statement processing
- SQL statements [ODBC], cursor library
- cursor library [ODBC], statement processing
ms.assetid: 54dad6a3-e86c-477b-ba7c-4e95e0385ec1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5d5aa94062f90154126fb18c3658adb39bb1d5c0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63057050"
---
# <a name="processing-sql-statements"></a>Elaborazione di istruzioni SQL
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzarla nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che utilizzano attualmente questa funzionalità. Microsoft consiglia di usare le funzionalità del driver del cursore.  
  
 La libreria di cursori ODBC restituisce tutte le istruzioni SQL direttamente al driver ad eccezione dei seguenti:  
  
-   Aggiornamento posizionato ed eliminare le istruzioni  
  
-   **SELECT FOR UPDATE** istruzioni  
  
-   Istruzioni SQL batch  
  
 Per eseguire l'aggiornamento posizionato ed eliminare le istruzioni e posizionare il cursore su una riga per chiamare **SQLGetData** per quella riga, la libreria di cursori costruisce viene eseguita un'istruzione che identifica la riga.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Elaborazione di istruzioni di eliminazione e aggiornamento posizionato](../../../odbc/reference/appendixes/processing-positioned-update-and-delete-statements.md)  
  
-   [Elaborazione di istruzioni SELECT FOR UPDATE](../../../odbc/reference/appendixes/processing-select-for-update-statements.md)  
  
-   [Elaborazione di batch di istruzioni SQL](../../../odbc/reference/appendixes/processing-batches-of-sql-statements.md)  
  
-   [Costruzione di istruzioni di ricerca](../../../odbc/reference/appendixes/constructing-searched-statements.md)
