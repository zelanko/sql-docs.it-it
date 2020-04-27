---
title: Creare alias di tabella (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- table aliases [SQL Server]
- aliases [SQL Server], tables
ms.assetid: 49e61e85-8abf-4ca7-8c70-7e9f8f1078bd
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7e7172a7b9b17dfa4553d3179d8cc1a880040f13
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63306532"
---
# <a name="create-table-aliases-visual-database-tools"></a>Creazione di alias di tabella (Visual Database Tools)
  Gli alias possono semplificare l'utilizzo dei nomi di tabella. L'utilizzo degli alias è utile se:  
  
-   Si intende abbreviare e rendere più facilmente leggibile l'istruzione nel [riquadro SQL](visual-database-tools.md) .  
  
-   Nella query si fa spesso riferimento al nome della tabella, ad esempio nei nomi che qualificano una colonna, e ci si vuole assicurare che venga rispettato un limite specifico per la lunghezza dei caratteri nella query. Alcuni database, infatti, impongono una lunghezza massima per le query.  
  
-   Si utilizzano più istanze della stessa tabella (come in un self-join) ed è necessario fare riferimento a un'istanza o un'altra.  
  
 È ad esempio possibile creare un alias `"e"` per un nome di tabella `employee`_`information`, quindi fare riferimento alla tabella con `"e"` in tutto il resto della query.  
  
### <a name="to-create-an-alias-for-a-table-or-table-valued-object"></a>Per creare un alias per una tabella o un oggetto con valori di tabella  
  
1.  Aggiungere alla query la tabella o l'oggetto con valori di tabella.  
  
2.  Nel **riquadro diagramma**fare clic con il pulsante destro del mouse sull'oggetto per cui si vuole creare un alias e scegliere **Proprietà** dal menu di scelta rapida.  
  
3.  Nella finestra **Proprietà** immettere l'alias nel campo **Alias** .  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiunta di tabelle a query &#40;Visual Database Tools&#41;](add-tables-to-queries-visual-database-tools.md)   
 [Ordinare e raggruppare i risultati delle query &#40;Visual Database Tools&#41;](sort-and-group-query-results-visual-database-tools.md)   
 [Riepilogare i risultati delle query &#40;Visual Database Tools&#41;](summarize-query-results-visual-database-tools.md)   
 [Eseguire operazioni di base con le query &#40;Visual Database Tools&#41;](perform-basic-operations-with-queries-visual-database-tools.md)  
  
  
