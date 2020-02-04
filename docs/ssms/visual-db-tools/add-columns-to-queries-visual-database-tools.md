---
title: Aggiungere colonne a query
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- inserting columns
- columns [SQL Server], adding
- queries [SQL Server], columns
- adding columns
ms.assetid: 82f3ba72-3d72-4fb1-8179-2a953a782787
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.openlocfilehash: b6638a8b5a749c833d2d50ca0dc6fba78d61038c
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "75244192"
---
# <a name="add-columns-to-queries-visual-database-tools"></a>Aggiunta di colonne a query (Visual Database Tools)

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Per utilizzare una colonna in una query, è necessario aggiungerla alla query. È possibile aggiungere una colonna per visualizzarla nell'output della query, per utilizzarla per l'ordinamento oppure per ricercarne o riepilogarne il contenuto. È possibile decidere quali colonne utilizzate nella query devono essere incluse nel riquadro Risultati quando viene eseguita la query. Per altre informazioni, vedere [Rimuovere colonne dai risultati della query &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/remove-columns-from-query-results-visual-database-tools.md).  
  
> [!NOTE]  
> Per visualizzare il tipo di dati di una colonna in Progettazione query e Progettazione viste, selezionare la tabella o l'oggetto con valori di tabella nel **riquadro Diagramma** e nella finestra delle proprietà fare clic su Elenco colonne. Fare clic sui **puntini di sospensione (...)** per aprire la finestra di dialogo **Elenco colonne**.  
  
Ovunque si utilizzi una colonna in una query, è anche possibile utilizzare un'espressione costituita da una qualunque combinazione di colonne, valori letterali, operatori e funzioni.  
  
### <a name="to-add-an-individual-column"></a>Per aggiungere una singola colonna  
  
-   Nel **riquadro Diagramma**selezionare la casella di controllo accanto alla colonna da includere.  
  
    -oppure-  
  
-   Nel **riquadro Criteri**spostarsi sulla prima riga vuota della griglia, fare clic sul campo nella colonna **Colonna** e selezionare un nome di colonna dall'elenco a discesa.  
  
### <a name="to-add-all-columns-for-one-table-or-table-valued-object"></a>Per aggiungere tutte le colonne di una tabella o di un oggetto con valori di tabella  
  
-   Nel **riquadro Diagramma** selezionare la casella di controllo accanto a **#42;(Tutte le colonne)** .  
  
### <a name="to-add-all-columns-for-all-tables-and-table-structured-objects"></a>Per aggiungere tutte le colonne per tutte le tabelle e gli oggetti con struttura di tabella  
  
1.  Assicurarsi che non sia selezionata alcuna linea di join nel **Riquadro operazioni tabella** .  
  
2.  Fare clic con il pulsante destro del mouse nello spazio vuoto della finestra Progettazione e scegliere **Proprietà** dal menu di scelta rapida.  
  
3.  Nella finestra Proprietà fare clic su **Tutte le colonne** e scegliere **Sì** o **No** dall'elenco a discesa.  
  
## <a name="see-also"></a>Vedere anche  
[Rimuovere colonne dai risultati della query &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/remove-columns-from-query-results-visual-database-tools.md)  
[Rimozione di colonne da query &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/remove-columns-from-queries-visual-database-tools.md)  
[Specifica dei criteri di ricerca &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
[Creare un riepilogo dei risultati di query &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[Eseguire operazioni di base con le query &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
