---
title: Panoramica dei dati di aggiornamento | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3edbd41bc5361d864abcc7d631a90521af98ef01
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62632666"
---
# <a name="updating-data-overview"></a>Panoramica sull'aggiornamento dei dati
Le applicazioni possono aggiornare i dati tramite l'esecuzione di istruzioni SQL o chiamando **SQLSetPos** oppure **SQLBulkOperations**. **UPDATE**, **eliminare**, e **Inserisci** istruzioni agire direttamente sull'origine dati e in genere sono supportate dal driver. Eseguire la ricerca di aggiornamenti e le istruzioni delete contengono una specifica delle righe da modificare. Aggiornamento posizionato ed eliminare le istruzioni e **SQLSetPos** agire sull'origine dati tramite un cursore e meno ampiamente supportati.  
  
 Se i cursori possono rilevare le modifiche apportate per il set di risultati con i metodi descritti in questa sezione varia a seconda del tipo di cursore e come implementarlo. I cursori forward-only non visitare di nuovo le righe e pertanto non rileverà le modifiche. Per informazioni sulla possibilità di rilevare le modifiche cursori scorrevoli, vedere [cursori scorrevoli](../../../odbc/reference/develop-app/scrollable-cursors.md).  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Istruzioni UPDATE, DELETE e INSERT](../../../odbc/reference/develop-app/update-delete-and-insert-statements.md)  
  
-   [Istruzioni di eliminazione e aggiornamento posizionato](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)  
  
-   [Simulazione di istruzioni di eliminazione e aggiornamento posizionato](../../../odbc/reference/develop-app/simulating-positioned-update-and-delete-statements.md)  
  
-   [Determinazione del numero di righe interessate](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md)  
  
-   [Aggiornamento dati con SQLSetPos](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)  
  
-   [Aggiornamento dei dati con SQLBulkOperations](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md)  
  
-   [Dati di tipo Long e SQLSetPos e SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)
