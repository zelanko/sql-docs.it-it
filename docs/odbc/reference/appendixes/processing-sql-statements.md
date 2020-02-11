---
title: Elaborazione di istruzioni SQL | Microsoft Docs
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
ms.openlocfilehash: d9452ade90f6967dff6d72d5692efcf91b93154d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68057240"
---
# <a name="processing-sql-statements"></a>Elaborazione di istruzioni SQL
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzare questa funzionalità nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che attualmente utilizzano questa funzionalità. Microsoft consiglia di utilizzare la funzionalità di cursore del driver.  
  
 La libreria di cursori ODBC passa tutte le istruzioni SQL direttamente al driver, ad eccezione di quanto segue:  
  
-   Istruzioni Update e Delete posizionate  
  
-   **Select for Update** -istruzioni  
  
-   Istruzioni SQL in batch  
  
 Per eseguire le istruzioni Update e Delete posizionate e per posizionare il cursore su una riga per chiamare **SQLGetData** per tale riga, la libreria di cursori crea un'istruzione di ricerca che identifica la riga.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Elaborazione di istruzioni di eliminazione e aggiornamento posizionato](../../../odbc/reference/appendixes/processing-positioned-update-and-delete-statements.md)  
  
-   [Elaborazione di istruzioni SELECT FOR UPDATE](../../../odbc/reference/appendixes/processing-select-for-update-statements.md)  
  
-   [Elaborazione di batch di istruzioni SQL](../../../odbc/reference/appendixes/processing-batches-of-sql-statements.md)  
  
-   [Costruzione di istruzioni di ricerca](../../../odbc/reference/appendixes/constructing-searched-statements.md)
