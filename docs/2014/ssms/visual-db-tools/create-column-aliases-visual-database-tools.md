---
title: Creare alias di colonna (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- columns [SQL Server], aliases
- aliases [SQL Server], columns
ms.assetid: e2e1c166-8ea7-47a2-b6a7-e419bf0fa3bb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6a6be65da2da5da5c025520314c069258aeb7bfb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63184357"
---
# <a name="create-column-aliases-visual-database-tools"></a>Creazione di alias di colonna (Visual Database Tools)
  Gli alias dei nomi di colonna consentono di semplificare l'utilizzo dei nomi di colonna, dei calcoli e dei valori di riepilogo. È possibile ad esempio creare un alias di colonna per:  
  
-   Creare un nome di colonna quale "Importo totale" per un'espressione come `(quantity * unit_price)` o per una funzione di aggregazione.  
  
-   Creare una versione abbreviata di un nome di colonna, ad esempio `"d_id"` per `"discounts.stor_id."`  
  
 Dopo avere definito un alias di colonna, è possibile utilizzarlo in una query di selezione per specificare l'output della query.  
  
### <a name="to-create-a-column-alias"></a>Per creare un alias di colonna  
  
1.  Nel **riquadro Criteri**individuare la riga contenente la colonna di dati per la quale si vuole creare un alias e, se necessario, contrassegnarla per l'output. Se la colonna di dati non è già presente nella griglia, aggiungerla.  
  
2.  Nella colonna **Alias** per tale riga specificare l'alias. seguendo le convenzioni di denominazione del linguaggio SQL. Se si specifica un nome di alias contenente spazi, verranno inseriti automaticamente delimitatori all'inizio e alla fine di esso.  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiungere colonne a query &#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [Ordina e raggruppa i risultati della Query &#40;Visual Database Tools&#41;](sort-and-group-query-results-visual-database-tools.md)   
 [Riepilogo dei risultati di Query &#40;Visual Database Tools&#41;](summarize-query-results-visual-database-tools.md)   
 [Eseguire operazioni di base con le query &#40;Visual Database Tools&#41;](perform-basic-operations-with-queries-visual-database-tools.md)  
  
  
