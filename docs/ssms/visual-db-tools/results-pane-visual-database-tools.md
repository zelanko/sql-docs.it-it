---
title: Riquadro Risultati
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
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
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.openlocfilehash: b6c7817fd90085ab4a7520cb98481dabea3b9558
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "75255204"
---
# <a name="results-pane-visual-database-tools"></a>Results Pane (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
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
  
Per informazioni sull'uso di tasti di scelta rapida in Progettazione query e Progettazione viste, vedere [Navigazione all'interno di Progettazione viste e Progettazione query &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/navigate-in-the-query-and-view-designer-visual-database-tools.md).  
  
## <a name="keeping-the-results-set-synchronized-with-the-query-definition"></a>Mantenimento della sincronizzazione tra il set di risultati e la definizione della query  
Mentre si lavora sui risultati di una query o di una vista, è possibile che i record nel riquadro Risultati perdano la sincronizzazione con la definizione della query. Se ad esempio è stata eseguita una query per quattro delle cinque colonne di una tabella e quindi è stato utilizzato il riquadro Diagramma per aggiungere la quinta colonna alla definizione della query, i dati di tale colonna non verranno aggiunti automaticamente al riquadro Risultati. Perché il riquadro Risultati rifletta la nuova definizione della query, sarà necessario eseguire ancora una volta la query.  
  
Se una query è stata modificata, nell'angolo inferiore destro del riquadro Risultati verranno visualizzati un'icona di avviso e un messaggio indicante che la query è cambiata. L'icona verrà visualizzata anche nell'angolo superiore sinistro del riquadro.  
  
## <a name="see-also"></a>Vedere anche  
[Creare query &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-queries-visual-database-tools.md)  
[Eseguire query &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/run-queries-visual-database-tools.md)  
[Procedure per la progettazione di query e viste &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[Riquadro Diagramma &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md)  
[Riquadro Criteri &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)  
[Usare i dati nel riquadro Risultati &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/work-with-data-in-the-results-pane-visual-database-tools.md)  
  
