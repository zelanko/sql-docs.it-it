---
title: Panoramica sull'aggiornamento dei dati - Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], about updating data
- data updates [ODBC]
- updating data [ODBC]
- data updates [ODBC], about data updates
ms.assetid: 062036a4-cda6-4aaa-9765-f1ec3e0b31b1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9972ab61f041385ae4ca616df093ae63ad7a47d9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300387"
---
# <a name="updating-data-overview"></a>Panoramica sull'aggiornamento dei dati
Le applicazioni possono aggiornare i dati eseguendo istruzioni SQL o chiamando **SQLSetPos** o **SQLBulkOperations**. **Le**istruzioni UPDATE , **DELETE**e **INSERT** agiscono direttamente sull'origine dati e sono in genere supportate dai driver. Le istruzioni di aggiornamento ed eliminazione ricercate contengono una specifica delle righe da modificare. Le istruzioni di aggiornamento ed eliminazione posizionate e **SQLSetPos** agiscono sull'origine dati tramite un cursore e sono meno ampiamente supportate.  
  
 Il fatto che i cursori siano in grado di rilevare le modifiche apportate al set di risultati con i metodi descritti in questa sezione dipende dal tipo di cursore e dalla modalità di implementazione. I cursori forward-only non rivisitano le righe e pertanto non rilevano alcuna modifica. Per informazioni sull'otazione a i cursori scorrevoli in grado di rilevare le modifiche, vedere [Cursori scorrevoli](../../../odbc/reference/develop-app/scrollable-cursors.md).  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Istruzioni UPDATE, DELETE e INSERT](../../../odbc/reference/develop-app/update-delete-and-insert-statements.md)  
  
-   [Istruzioni di eliminazione e aggiornamento posizionato](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)  
  
-   [Simulazione di istruzioni di eliminazione e aggiornamento posizionato](../../../odbc/reference/develop-app/simulating-positioned-update-and-delete-statements.md)  
  
-   [Determinazione del numero di righe interessate](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md)  
  
-   [Aggiornamento dati con SQLSetPos](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)  
  
-   [Aggiornamento dei dati con SQLBulkOperations](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md)  
  
-   [Dati di tipo Long e SQLSetPos e SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)
