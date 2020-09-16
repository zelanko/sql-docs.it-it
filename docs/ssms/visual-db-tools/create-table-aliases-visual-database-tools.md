---
description: Creazione di alias di tabella (Visual Database Tools)
title: Creare alias di tabella
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- table aliases [SQL Server]
- aliases [SQL Server], tables
ms.assetid: 49e61e85-8abf-4ca7-8c70-7e9f8f1078bd
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: dcac7f46183579b3d96fb3a65b13f731ce114f9a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88462871"
---
# <a name="create-table-aliases-visual-database-tools"></a>Creazione di alias di tabella (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Gli alias possono semplificare l'utilizzo dei nomi di tabella. L'utilizzo degli alias è utile se:  
  
-   Si intende abbreviare e rendere più facilmente leggibile l'istruzione nel [riquadro SQL](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md) .  
  
-   Nella query si fa spesso riferimento al nome della tabella, ad esempio nei nomi che qualificano una colonna, e ci si vuole assicurare che venga rispettato un limite specifico per la lunghezza dei caratteri nella query. Alcuni database, infatti, impongono una lunghezza massima per le query.  
  
-   Si utilizzano più istanze della stessa tabella (come in un self-join) ed è necessario fare riferimento a un'istanza o un'altra.  
  
È ad esempio possibile creare un alias `"e"` per un nome di tabella `employee_information`, quindi fare riferimento alla tabella con `"e"` nella parte rimanente della query.  
  
### <a name="to-create-an-alias-for-a-table-or-table-valued-object"></a>Per creare un alias per una tabella o un oggetto con valori di tabella  
  
1.  Aggiungere alla query la tabella o l'oggetto con valori di tabella.  
  
2.  Nel **riquadro diagramma**fare clic con il pulsante destro del mouse sull'oggetto per cui si vuole creare un alias e scegliere **Proprietà** dal menu di scelta rapida.  
  
3.  Nella finestra **Proprietà** immettere l'alias nel campo **Alias** .  
  
## <a name="see-also"></a>Vedere anche  
[Aggiunta di tabelle a query &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/add-tables-to-queries-visual-database-tools.md)  
[Ordinare e raggruppare i risultati delle query &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[Creare un riepilogo dei risultati di query &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[Eseguire operazioni di base con le query &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
