---
description: Riordinamento delle colonne di output (Visual Database Tools)
title: Riordinare le colonne di output
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- reordering output columns [SQL Server]
- output columns [SQL Server]
ms.assetid: 76462885-de4a-4290-a26b-90696d3671f4
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 9268fb47c89732ccaf5af6460119ddc9664daf24
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88497108"
---
# <a name="reorder-output-columns-visual-database-tools"></a>Riordinamento delle colonne di output (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
La sequenza di immissione delle colonne di dati in una query di selezione determina l'ordine in cui saranno visualizzate nei risultati. La prima colonna aggiunta alla query verrà visualizzata a sinistra nei risultati, seguita dalla seconda colonna e così via.  
  
Se si crea una query di aggiornamento o di inserimento, l'ordine in cui vengono aggiunte le colonne influenzerà l'ordine di elaborazione dei dati.  
  
Per controllare la posizione di visualizzazione o l'ordine di utilizzo di una colonna di dati nel set di risultati, è possibile riordinare le colonne.  
  
### <a name="to-reorder-columns-for-output"></a>Per riordinare le colonne per l'output  
  
1.  Nel [riquadro Criteri](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)selezionare la riga che contiene la colonna facendo clic sul pulsante di selezione posto alla sinistra della riga.  
  
2.  Fare clic sul selettore di riga e trascinare la riga nella nuova posizione.  
  
    -oppure-  
  
    Modificare l'ordine dei nomi di colonna nel [riquadro SQL](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md).  
  
> [!TIP]  
> Per aggiungere una riga di dati in una determinata posizione nel riquadro Criteri, inserire una riga vuota in tale riquadro, quindi specificare la colonna di dati da inserire. Per altre informazioni dettagliate, vedere [Aggiungere colonne a query &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/add-columns-to-queries-visual-database-tools.md).  
  
## <a name="see-also"></a>Vedere anche  
[Ordinare e raggruppare i risultati delle query &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[Creare un riepilogo dei risultati di query &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[Eseguire operazioni di base con le query &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
