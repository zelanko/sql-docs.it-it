---
description: Riepilogo o aggregazione di valori mediante l'utilizzo di espressioni personalizzate (Visual Database Tools)
title: Riepilogare o aggregare valori mediante espressioni personalizzate
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- summarizing query results
- custom expressions to aggregate values [SQL Server]
ms.assetid: 34130ac1-0106-4766-b324-acb0b7bb6f6e
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: e71f0ffc06314678becda493f6e45c98060d3a32
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88312547"
---
# <a name="summarize-or-aggregate-values-using-custom-expressions-visual-database-tools"></a>Riepilogo o aggregazione di valori mediante l'utilizzo di espressioni personalizzate (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Oltre a utilizzare le funzioni di aggregazione per raggruppare i dati, è possibile creare espressioni personalizzate che producono valori aggregati. È possibile utilizzare espressioni personalizzate al posto di funzioni di aggregazione in qualsiasi punto di una query di aggregazione.  
  
Si supponga ad esempio che nella tabella `titles` si desideri creare una query in cui sia riportato non solo il prezzo medio ma anche il prezzo medio dopo l'applicazione di uno sconto.  
  
In questo caso non sarà possibile includere un'espressione basata su calcoli che coinvolgono solo singole righe della tabella; l'espressione dovrà essere basata su un valore aggregato in quanto al momento del calcolo dell'espressione sono disponibili solo i valori aggregati.  
  
### <a name="to-specify-a-custom-expression-for-a-summary-value"></a>Per specificare un'espressione personalizzata per un valore di riepilogo  
  
1.  Specificare i gruppi per la query. Per informazioni dettagliate, vedere [Raggruppare righe nei risultati di una query &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/group-rows-in-query-results-visual-database-tools.md).  
  
2.  Spostarsi su una riga vuota del riquadro Criteri e digitare l'espressione nella colonna **Columns**.  
  
    In [Progettazione query e Progettazione viste](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) verrà assegnato automaticamente all'espressione un alias di colonna in modo da creare un'intestazione di colonna utile nell'output della query. Per altre informazioni dettagliate, vedere [Creazione di alias di colonna &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-column-aliases-visual-database-tools.md).  
  
3.  Nella colonna **Group By** per l'espressione selezionare **Espressione**.  
  
4.  Eseguire la query.  
  
## <a name="see-also"></a>Vedere anche  
[Ordinare e raggruppare i risultati delle query &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[Creare un riepilogo dei risultati di query &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
  
