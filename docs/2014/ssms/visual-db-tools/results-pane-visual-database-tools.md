---
title: Riquadro Risultati (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- View Designer, Results pane
- result sets [SQL Server], queries
- synchronization [SQL Server], query results with definition
- displaying query results in grid
- grid showing query results [SQL Server]
- showing query results in grid
- Query Designer [SQL Server], Results pane
- results [SQL Server], query
- viewing query results
- queries [SQL Server], results
- Results pane
ms.assetid: 6309a1bc-a628-4141-8bb5-b35924bd19f9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 87bfaef1ad5dc4c9b1f907c27955ca3f156038a8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63067807"
---
# <a name="results-pane-visual-database-tools"></a>Results Pane (Visual Database Tools)
  Nel riquadro Risultati vengono visualizzati i risultati dell'ultima query di selezione (SELECT) eseguita. I risultati di altri tipi di query vengono visualizzati in finestre di messaggio. Il riquadro Risultati viene visualizzato automaticamente quando si apre o si crea una query o una vista oppure quando vengono restituiti i dati di una tabella. Se il riquadro Risultati non viene visualizzato per impostazione predefinita, scegliere **Pannello** dal menu **Progettazione query**, quindi **Risultati**.  
  
## <a name="what-you-can-do-in-the-results-pane"></a>Operazioni che è possibile eseguire nel riquadro Risultati  
  
-   Visualizzare in una griglia simile a un foglio di calcolo il set di risultati dell'ultima query SELECT eseguita.  
  
-   Nel caso di query o viste che visualizzano i dati di una sola tabella o vista, modificare i valori nelle singole colonne del set di risultati, aggiungere nuove righe ed eliminare righe esistenti.  
  
## <a name="limitations-in-the-results-pane"></a>Limitazioni relative al riquadro Risultati  
  
-   I risultati restituiti da funzioni con valori di tabella possono essere aggiornati solo in alcuni casi.  
  
-   Le query o le viste in cui sono incluse colonne provenienti da più tabelle o viste non possono essere aggiornate.  
  
-   I risultati restituiti da una stored procedure non possono essere aggiornati.  
  
-   Le query o le viste in cui viene utilizzata la clausola GROUP BY o DISTINCT non possono essere aggiornate.  
  
## <a name="navigating-in-the-results-pane"></a>Navigazione all'interno del riquadro Risultati  
 Nella parte inferiore del riquadro Risultati è presente una barra di navigazione che consente di passare velocemente da un record all'altro.  
  
 Sono disponibili pulsanti per spostarsi sul primo e sull'ultimo record, sul record successivo e su quello precedente oppure direttamente su un record specifico.  
  
 Per spostarsi su un record specifico, digitare il numero delle riga nella casella di testo all'interno della barra di navigazione, quindi premere INVIO.  
  
 Per informazioni sull'uso di tasti di scelta rapida in Progettazione query e Progettazione viste, vedere [Navigazione all'interno di Progettazione viste e Progettazione query &#40;Visual Database Tools&#41;](visual-database-tools.md).  
  
## <a name="keeping-the-results-set-synchronized-with-the-query-definition"></a>Mantenimento della sincronizzazione tra il set di risultati e la definizione della query  
 Mentre si lavora sui risultati di una query o di una vista, è possibile che i record nel riquadro Risultati perdano la sincronizzazione con la definizione della query. Se ad esempio è stata eseguita una query per quattro delle cinque colonne di una tabella e quindi è stato utilizzato il riquadro Diagramma per aggiungere la quinta colonna alla definizione della query, i dati di tale colonna non verranno aggiunti automaticamente al riquadro Risultati. Perché il riquadro Risultati rifletta la nuova definizione della query, sarà necessario eseguire ancora una volta la query.  
  
 Se una query è stata modificata, nell'angolo inferiore destro del riquadro Risultati verranno visualizzati un'icona di avviso e un messaggio indicante che la query è cambiata. L'icona verrà visualizzata anche nell'angolo superiore sinistro del riquadro.  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di query &#40;Visual Database Tools&#41;](create-queries-visual-database-tools.md)   
 [Eseguire query &#40;Visual Database Tools&#41;](run-queries-visual-database-tools.md)   
 [Procedure per le query e visualizzazioni di progettazione &#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)   
 [Riquadro Diagramma &#40;Visual Database Tools&#41;](diagram-pane-visual-database-tools.md)   
 [Riquadro Criteri &#40;Visual Database Tools&#41;](criteria-pane-visual-database-tools.md)   
 [Usare i dati nel riquadro Risultati &#40;Visual Database Tools&#41;](results-pane-visual-database-tools.md)  
  
  
