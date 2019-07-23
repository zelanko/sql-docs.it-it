---
title: Rimuovere tabelle da query (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- deleting tables
- removing tables
- dropping tables
- queries [SQL Server], tables
ms.assetid: 8fea0b4f-99b7-4050-8d6f-a97ffb839619
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b0b861034b3d95fd653358b91e31352776e1dad3
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/16/2019
ms.locfileid: "68255993"
---
# <a name="remove-tables-from-queries-visual-database-tools"></a>Rimozione di tabelle da query (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
È possibile rimuovere una tabella o qualsiasi altro oggetto con valori di tabella dalla query.  
  
> [!NOTE]  
> Se viene rimossa una tabella o un oggetto con valori di tabella, la rimozione non riguarderà in alcun modo i dati contenuti nel database, ma solo la query corrente. Per informazioni dettagliate sulla rimozione di una tabella da un database, vedere [Procedura: Eliminare tabelle da un database (Visual Database Tools)](https://msdn.microsoft.com/ca6aa3e9-9885-44c3-bafc-aec441fd97ec).  
  
### <a name="to-remove-a-table-or-table-structured-object"></a>Per rimuovere una tabella o un oggetto con struttura di tabella  
  
-   Nel **riquadro diagramma**selezionare la tabella, la vista, la funzione definita dall'utente, il sinonimo o la query desiderata e premere CANC oppure fare clic con il pulsante destro del mouse sull'oggetto e scegliere **Rimuovi** nella finestra di dialogo visualizzata. È possibile selezionare e rimuovere più oggetti contemporaneamente.  
  
    oppure  
  
-   Rimuovere qualsiasi riferimento all'oggetto nel **riquadro SQL**.  
  
Quando viene rimossa una tabella o un oggetto con valori di tabella, in Progettazione query e Progettazione viste vengono eliminati automaticamente i join che lo riguardano e i riferimenti alle colonne dell'oggetto nel **riquadro SQL** e nel **riquadro Criteri**. Se tuttavia la query contiene espressioni complesse che coinvolgono l'oggetto, quest'ultimo non verrà automaticamente eliminato fino a che non siano stati eliminati tutti i riferimenti ad esso.  
  
## <a name="see-also"></a>Vedere anche  
[Aggiunta di tabelle a query (Visual Database Tools)](../../ssms/visual-db-tools/add-tables-to-queries-visual-database-tools.md)  
[Creazione di alias di tabella (Visual Database Tools)](../../ssms/visual-db-tools/create-table-aliases-visual-database-tools.md)  
[Specificare i criteri di ricerca (Visual Database Tools)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
[Riepilogo dei risultati di query (Visual Database Tools)](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[Eseguire operazioni di base con le query (Visual Database Tools)](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
