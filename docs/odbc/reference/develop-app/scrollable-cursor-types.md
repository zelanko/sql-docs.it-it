---
title: Tipi di cursore scorrevoli | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 210b66a800670f033508f903b18778f88ddd4c8b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68061633"
---
# <a name="scrollable-cursor-types"></a>Tipi di cursore scorrevoli
I quattro tipi di cursori scorrevoli sono statici, dinamici, gestito da keyset e mista. I cursori statici rilevare le modifiche apportate poche o nessuna ma sono relativamente economici da implementare. I cursori dinamici rilevano tutte le modifiche, ma sono costosi da implementare. I cursori keyset e misti si trovano rilevano la maggior parte delle modifiche ma meno spese rispetto ai cursori dinamici.  
  
 I termini seguenti vengono usati per definire le caratteristiche di ogni tipo di cursore scorrevole:  
  
-   **Il proprietario degli aggiornamenti, eliminazioni e inserimenti.** Gli aggiornamenti, eliminazioni e inserimenti eseguiti nel cursore, con una chiamata a **SQLBulkOperations** oppure **SQLSetPos** o con un oggetto posizionato istruzione update o delete.  
  
-   **Altri aggiornamenti, si elimina e si inserisce.** Gli aggiornamenti, eliminazioni e inserimenti non effettuati dal cursore, comprese quelle apportate da altre operazioni nella stessa transazione, quelle effettuate tramite altre transazioni e quelle apportate da altre applicazioni.  
  
-   **Appartenenza al gruppo.** Il set di righe nel set di risultati.  
  
-   **Ordine.** L'ordine in cui vengono restituite righe dal cursore.  
  
-   **valori.** I valori in ogni riga nel set di risultati.  
  
 Per informazioni su come aggiornare, eliminare e inserire i dati, vedere [Panoramica di aggiornamento dati](../../../odbc/reference/develop-app/updating-data-overview.md).  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Cursori statici ODBC](../../../odbc/reference/develop-app/odbc-static-cursors.md)  
  
-   [Cursori dinamici ODBC](../../../odbc/reference/develop-app/odbc-dynamic-cursors.md)  
  
-   [Cursori gestiti da keyset](../../../odbc/reference/develop-app/keyset-driven-cursors.md)  
  
-   [Cursori misti](../../../odbc/reference/develop-app/mixed-cursors.md)
