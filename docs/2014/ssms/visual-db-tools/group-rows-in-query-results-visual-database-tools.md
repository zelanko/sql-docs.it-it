---
title: Raggruppare righe nei risultati di una query (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- summarizing table subsets
- grouping rows
- grouping query results
ms.assetid: b07082d5-4d55-4903-9af9-4c470554c6d3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4cd80e7d999314c549df4ebb5e51aa2a0ca2d3f8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63154829"
---
# <a name="group-rows-in-query-results-visual-database-tools"></a>Raggruppare righe nei risultati di una query (Visual Database Tools)
  Se si desidera creare dei subtotali o visualizzare altre informazioni riepilogative per i subset di una tabella, è possibile utilizzare una query di aggregazione. Ciascun gruppo creato riepiloga i dati per tutte le righe della tabella con lo stesso valore.  
  
 Può essere necessario, ad esempio, visualizzare il prezzo medio di un libro nella tabella `titles` , suddividendo i risultati in base all'editore. Per ottenere questo risultato, è necessario raggruppare la query in base all'editore (ad esempio, `pub_id`). L'output della query potrebbe essere analogo al seguente:  
  
 ![Risultati della query: prezzo medio raggruppato per server di pubblicazione](../../database-engine/media//dv3w9e1.gif "Risultati della query: prezzo medio raggruppato per server di pubblicazione")  
  
 Quando si raggruppano i dati, è possibile visualizzare solo dati riepilogativi o raggruppati, ad esempio:  
  
-   I valori delle colonne raggruppate (quelli che compaiono nella clausola GROUP BY). Nell'esempio precedente, `pub_id` è la colonna raggruppata.  
  
-   I valori prodotti da funzioni di aggregazione quali SUM( ) e AVG( ). Nell'esempio precedente, la seconda colonna viene generata usando la funzione AVG( ) con la colonna `price` .  
  
 Non è possibile visualizzare valori di singole righe. Se ad esempio si effettua il raggruppamento solo in base all'editore, non sarà possibile visualizzare anche singoli titoli nella query. Quindi, se si aggiungono colonne all'output della query, in [Progettazione query e Progettazione viste](visual-database-tools.md) queste verranno aggiunte automaticamente alla clausola GROUP BY dell'istruzione nel [riquadro SQL](sql-pane-visual-database-tools.md). Se invece si desidera che sia la colonna ad essere aggregata, sarà possibile specificare una funzione di aggregazione per tale colonna.  
  
 Se si definisce un raggruppamento in base a più colonne, in ogni gruppo della query verranno visualizzati i valori aggregati per tutte le colonne raggruppate.  
  
 Nella seguente query, ad esempio, effettuata sulla tabella `titles` il raggruppamento viene effettuato in base all'editore (`pub_id`) e al tipo di libro (`type`). I risultati della query vengono ordinati in base all'editore e mostrano informazioni di riepilogo su ogni tipo di libro prodotto dall'editore:  
  
```  
SELECT pub_id, type, SUM(price) Total_price  
FROM titles  
GROUP BY pub_id, type  
```  
  
 L'output risultante può essere analogo al seguente:  
  
 ![Risultati della query: prezzo raggruppato per server di pubblicazione e tipo](../../database-engine/media//dv3w9e2.gif "Risultati della query: prezzo raggruppato per server di pubblicazione e tipo")  
  
### <a name="to-group-rows"></a>Per raggruppare le righe  
  
1.  Iniziare la query aggiungendo le tabelle da riepilogare nel riquadro Diagramma.  
  
2.  Fare clic con il pulsante destro del mouse sullo sfondo del riquadro Diagramma, quindi scegliere **Aggiungi raggruppamento** dal menu di scelta rapida. In Progettazione query e Progettazione viste verrà aggiunta una colonna **Group By** alla griglia nel riquadro Criteri.  
  
3.  Aggiungere al riquadro Criteri la colonna o la combinazione di colonne da raggruppare. Per visualizzare la colonna nell'output della query, assicurarsi che la colonna **Output** sia selezionata per l'output.  
  
     In Progettazione query e Progettazione viste sarà aggiunta una clausola GROUP BY all'istruzione nel riquadro SQL. L'istruzione SQL, ad esempio, può essere analoga alla seguente:  
  
    ```  
    SELECT pub_id  
    FROM titles  
    GROUP BY pub_id  
    ```  
  
4.  Aggiungere al riquadro Criteri la colonna o la combinazione di colonne da aggregare. Assicurarsi che la colonna sia contrassegnata per l'output.  
  
5.  Nella cella della griglia **Group By** per la colonna da aggregare, selezionare la funzione di aggregazione appropriata.  
  
     Verrà assegnato automaticamente un alias di colonna alla colonna di cui si effettua il riepilogo. Tale alias generato automaticamente può essere sostituito con un alias più significativo. Per altre informazioni dettagliate, vedere [Creazione di alias di colonna &#40;Visual Database Tools&#41;](create-column-aliases-visual-database-tools.md).  
  
     ![Aggiunta di un alias di colonna al set di risultati della query](../../database-engine/media//dv3w9e3.gif "Aggiunta di un alias di colonna al set di risultati della query")  
  
     L'istruzione corrispondente nel riquadro **SQL** può essere analoga alla seguente:  
  
    ```  
    SELECT   pub_id, SUM(price) AS Totalprice  
    FROM     titles  
    GROUP BY pub_id  
    ```  
  
## <a name="see-also"></a>Vedere anche  
 [Ordinare e raggruppare i risultati delle query &#40;Visual Database Tools&#41;](sort-and-group-query-results-visual-database-tools.md)  
  
  
