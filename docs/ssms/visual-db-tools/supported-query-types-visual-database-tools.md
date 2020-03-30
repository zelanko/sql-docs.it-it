---
title: Tipi di query supportati
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
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
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.openlocfilehash: a8f5fae345543a3a63bacad0c5cdf0d8f62d2aa5
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "75242173"
---
# <a name="supported-query-types-visual-database-tools"></a>Tipi di query supportati (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Nei riquadri Diagramma e Criteri di [Progettazione query e Progettazione viste](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md)è possibile creare i tipi di query seguenti:  
  
-   **Query di selezione** Recupera dati da una o più tabelle o viste. Questo tipo di query crea un'istruzione SQL SELECT.  
  
-   **Accodamento** Crea nuove righe copiando righe esistenti da una tabella a un'altra o all'interno della stessa tabella come righe nuove. Questo tipo di query crea un'istruzione SQL INSERT INTO...SELECT.  
  
-   **Accodamento valori** Crea una nuova riga e inserisce valori nelle colonne specificate. Questo tipo di query crea un'istruzione SQL INSERT INTO...VALUES.  
  
-   **Query di aggiornamento** Modifica i valori di singole colonne di una o più righe esistenti in una tabella. Questo tipo di query crea un'istruzione SQL UPDATE...SET.  
  
-   **Query di eliminazione** Rimuove una o più righe da una tabella. Questo tipo di query crea un'istruzione SQL DELETE.  
  
    > [!NOTE]  
    > Una query di eliminazione rimuove intere righe dalla tabella. Se si desidera eliminare valori da singole colonne di dati, utilizzare una query di aggiornamento.  
  
-   **Query di creazione tabella** Crea una nuova tabella e le relative righe copiandovi i risultati di una query. Questo tipo di query crea un'istruzione SQL SELECT...INTO.  
  
Oltre a creare le query utilizzando i riquadri grafici, è possibile immettere qualsiasi istruzione SQL nel riquadro SQL per creare query come quelle di unione.  
  
Quando si creano query con istruzioni SQL che non possono essere rappresentate nei riquadri grafici, in Progettazione query e Progettazione viste tali riquadri vengono visualizzati in grigio, per indicare che non si riferiscono alla query creata. I riquadri visualizzati in grigio sono tuttavia ancora attivi e, in molti casi, consentono di apportare modifiche alla query. Se le modifiche apportate generano una query che può essere rappresentata nei riquadri grafici, tali riquadri non verranno più visualizzati in grigio.  
  
## <a name="see-also"></a>Vedere anche  
[Procedure per la progettazione di query e viste](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[Tipi di query](../../ssms/visual-db-tools/types-of-queries-visual-database-tools.md)  
  
