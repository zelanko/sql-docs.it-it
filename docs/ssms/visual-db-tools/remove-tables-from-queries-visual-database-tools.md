---
title: Rimuovere tabelle da query
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
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
ms.manager: jroth
ms.reviewer: ''
ms.openlocfilehash: 32c25c3ded07e84e436b69af5baac5634909998c
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "75255253"
---
# <a name="remove-tables-from-queries-visual-database-tools"></a>Rimozione di tabelle da query (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
È possibile rimuovere una tabella o qualsiasi altro oggetto con valori di tabella dalla query.  
  
> [!NOTE]  
> Se viene rimossa una tabella o un oggetto con valori di tabella, la rimozione non riguarderà in alcun modo i dati contenuti nel database, ma solo la query corrente. Per informazioni dettagliate sulla rimozione di una tabella da un database, vedere [Procedura: Eliminare tabelle da un database (https://msdn.microsoft.com/ca6aa3e9-9885-44c3-bafc-aec441fd97ec).  
  
### <a name="to-remove-a-table-or-table-structured-object"></a>Per rimuovere una tabella o un oggetto con struttura di tabella  
  
-   Nel **riquadro diagramma**selezionare la tabella, la vista, la funzione definita dall'utente, il sinonimo o la query desiderata e premere CANC oppure fare clic con il pulsante destro del mouse sull'oggetto e scegliere **Rimuovi** nella finestra di dialogo visualizzata. È possibile selezionare e rimuovere più oggetti contemporaneamente.  
  
    -oppure-  
  
-   Rimuovere qualsiasi riferimento all'oggetto nel **riquadro SQL**.  
  
Quando viene rimossa una tabella o un oggetto con valori di tabella, in Progettazione query e Progettazione viste vengono eliminati automaticamente i join che lo riguardano e i riferimenti alle colonne dell'oggetto nel **riquadro SQL** e nel **riquadro Criteri**. Se tuttavia la query contiene espressioni complesse che coinvolgono l'oggetto, quest'ultimo non verrà automaticamente eliminato fino a che non siano stati eliminati tutti i riferimenti ad esso.  
  
## <a name="see-also"></a>Vedere anche  
[Aggiungere tabelle a query](../../ssms/visual-db-tools/add-tables-to-queries-visual-database-tools.md)  
[Creare alias di tabella](../../ssms/visual-db-tools/create-table-aliases-visual-database-tools.md)  
[Specificare criteri di ricerca](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
[Riepilogare i risultati di query](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[Eseguire operazioni di base con le query](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
