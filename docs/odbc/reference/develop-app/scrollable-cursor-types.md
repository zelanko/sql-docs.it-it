---
title: Tipi di cursore scorrevoli Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
ms.assetid: dbd32576-0453-4e90-ae45-1a81cee8259d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 63f29269ea209875a2e775cf8d523302fcb9a976
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304232"
---
# <a name="scrollable-cursor-types"></a>Tipi di cursore scorrevoli
I quattro tipi di cursori scorrevoli sono statici, dinamici, basati su keyset e misti. I cursori statici rilevano poche o nessuna modifica, ma sono relativamente economici da implementare. I cursori dinamici rilevano tutte le modifiche, ma sono costose da implementare. I cursori misti e basati su keyset si trovano in mezzo, rilevando la maggior parte delle modifiche ma a costi inferiori rispetto ai cursori dinamici.  
  
 Per definire le caratteristiche di ciascun tipo di cursore scorrevole vengono utilizzati i seguenti termini:  
  
-   **Proprietari di aggiornamenti, eliminazioni e inserimenti.** Aggiornamenti, eliminazioni e inserimenti eseguiti tramite il cursore, con una chiamata a **SQLBulkOperations** o **SQLSetPos** o con un'istruzione update o delete posizionata.  
  
-   **Altri aggiornamenti, eliminazioni e inserimenti.** Aggiornamenti, eliminazioni e inserimenti non effettuati dal cursore, inclusi quelli effettuati da altre operazioni nella stessa transazione, quelli effettuati tramite altre transazioni e quelli effettuati da altre applicazioni.  
  
-   **Iscrizione.** Set di righe nel set di risultati.  
  
-   **Ordine.** Ordine in cui le righe vengono restituite dal cursore.  
  
-   **Valori.** I valori in ogni riga del set di risultati.  
  
 Per informazioni su come aggiornare, eliminare e inserire dati, vedere [Panoramica dell'aggiornamento dei dati](../../../odbc/reference/develop-app/updating-data-overview.md).  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Cursori statici ODBC](../../../odbc/reference/develop-app/odbc-static-cursors.md)  
  
-   [Cursori dinamici ODBC](../../../odbc/reference/develop-app/odbc-dynamic-cursors.md)  
  
-   [Cursori gestiti da keyset](../../../odbc/reference/develop-app/keyset-driven-cursors.md)  
  
-   [Cursori misti](../../../odbc/reference/develop-app/mixed-cursors.md)
