---
title: Rimuovere tabelle da query (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- deleting tables
- removing tables
- dropping tables
- queries [SQL Server], tables
ms.assetid: 8fea0b4f-99b7-4050-8d6f-a97ffb839619
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bda582c7b9171e89a43b6870b3b6c2df139b7b11
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62670464"
---
# <a name="remove-tables-from-queries-visual-database-tools"></a>Rimozione di tabelle da query (Visual Database Tools)
  È possibile rimuovere una tabella o qualsiasi altro oggetto con valori di tabella dalla query.  
  
> [!NOTE]  
>  Se viene rimossa una tabella o un oggetto con valori di tabella, la rimozione non riguarderà in alcun modo i dati contenuti nel database, ma solo la query corrente. Per informazioni dettagliate sulla rimozione di una tabella da un database, vedere [eliminare tabelle &#40;motore di database&#41;](../../relational-databases/tables/delete-tables-database-engine.md).  
  
### <a name="to-remove-a-table-or-table-structured-object"></a>Per rimuovere una tabella o un oggetto con struttura di tabella  
  
-   Nel **riquadro diagramma**selezionare la tabella, la vista, la funzione definita dall'utente, il sinonimo o la query desiderata e premere CANC oppure fare clic con il pulsante destro del mouse sull'oggetto e scegliere **Rimuovi** nella finestra di dialogo visualizzata. È possibile selezionare e rimuovere più oggetti contemporaneamente.  
  
     -oppure-  
  
-   Rimuovere qualsiasi riferimento all'oggetto nel **riquadro SQL**.  
  
 Quando viene rimossa una tabella o un oggetto con valori di tabella, in Progettazione query e Progettazione viste vengono eliminati automaticamente i join che lo riguardano e i riferimenti alle colonne dell'oggetto nel **riquadro SQL** e nel **riquadro Criteri**. Se tuttavia la query contiene espressioni complesse che coinvolgono l'oggetto, quest'ultimo non verrà automaticamente eliminato fino a che non siano stati eliminati tutti i riferimenti ad esso.  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiunta di tabelle a query &#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [Creazione di alias di tabella &#40;Visual Database Tools&#41;](create-table-aliases-visual-database-tools.md)   
 [Specificare i criteri di ricerca &#40;Visual Database Tools&#41;](specify-search-criteria-visual-database-tools.md)   
 [Riepilogare i risultati delle query &#40;Visual Database Tools&#41;](summarize-query-results-visual-database-tools.md)   
 [Eseguire operazioni di base con le query &#40;Visual Database Tools&#41;](perform-basic-operations-with-queries-visual-database-tools.md)  
  
  
