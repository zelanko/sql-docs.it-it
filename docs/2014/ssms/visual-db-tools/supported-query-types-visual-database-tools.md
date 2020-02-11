---
title: Tipi di query supportati (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Delete query
- queries [SQL Server], types
- Update query
- Query Designer [SQL Server], query types
- Criteria pane
- Insert Values query
- Select query
- Make Table query
- Insert Results query
- Diagram pane [Visual Database Tools]
- View Designer, query types
ms.assetid: 72b9116c-c128-4078-a78d-257a2955a3f6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 752467d058a6618ccfa44d7e2f75ac33b632878e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63204654"
---
# <a name="supported-query-types-visual-database-tools"></a>Tipi di query supportati (Visual Database Tools)
  È possibile creare i tipi di query seguenti nei riquadri diagramma e criteri (i riquadri grafici) di [Progettazione query e Progettazione viste](visual-database-tools.md):  
  
-   **Seleziona query** Recupera i dati da una o più tabelle o viste. Questo tipo di query crea un'istruzione SQL SELECT.  
  
-   **Inserisci risultati** Crea nuove righe copiando righe esistenti da una tabella a un'altra o nella stessa tabella come nuove righe. Questo tipo di query crea un'istruzione SQL INSERT INTO...SELECT.  
  
-   **Inserisci valori** Crea una nuova riga e inserisce valori in colonne specificate. Questo tipo di query crea un'istruzione SQL INSERT INTO...VALUES.  
  
-   **Aggiorna query** Modifica i valori di singole colonne di una o più righe esistenti in una tabella. Questo tipo di query crea un'istruzione SQL UPDATE...SET.  
  
-   **Elimina query** Rimuove una o più righe da una tabella. Questo tipo di query crea un'istruzione SQL DELETE.  
  
    > [!NOTE]  
    >  Una query di eliminazione rimuove intere righe dalla tabella. Se si desidera eliminare valori da singole colonne di dati, utilizzare una query di aggiornamento.  
  
-   **Esegui query tabella** Crea una nuova tabella e crea righe al suo interno copiando i risultati di una query. Questo tipo di query crea un'istruzione SQL SELECT...INTO.  
  
 Oltre a creare le query utilizzando i riquadri grafici, è possibile immettere qualsiasi istruzione SQL nel riquadro SQL per creare query come quelle di unione.  
  
 Quando si creano query con istruzioni SQL che non possono essere rappresentate nei riquadri grafici, in Progettazione query e Progettazione viste tali riquadri vengono visualizzati in grigio, per indicare che non si riferiscono alla query creata. I riquadri visualizzati in grigio sono tuttavia ancora attivi e, in molti casi, consentono di apportare modifiche alla query. Se le modifiche apportate generano una query che può essere rappresentata nei riquadri grafici, tali riquadri non verranno più visualizzati in grigio.  
  
## <a name="see-also"></a>Vedere anche  
 [Procedure per la progettazione di query e viste &#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)   
 [Tipi di query &#40;Visual Database Tools&#41;](types-of-queries-visual-database-tools.md)  
  
  
