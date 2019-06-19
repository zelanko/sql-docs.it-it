---
title: Includere o escludere righe (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- search criteria [SQL Server], excluding rows
- search criteria [SQL Server], WHERE clause
- included rows
- search conditions [SQL Server], HAVING clause
- search criteria [SQL Server], including rows
- row excluded in search [SQL Server]
- search criteria [SQL Server], HAVING clause
- search conditions [SQL Server], WHERE clause
- row included in search [SQL Server]
- excluding rows
ms.assetid: ba4e1202-31a2-444d-8365-c68a530ef223
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3785a777571ef7659b1ae21a693e6754659a80e5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63298585"
---
# <a name="include-or-exclude-rows-visual-database-tools"></a>Includere o escludere righe (Visual Database Tools)
  Per limitare il numero di righe restituite da una query di selezione, è necessario creare condizioni di ricerca o criteri di filtro. In SQL le condizioni di ricerca vengono indicate nella clausola WHERE dell'istruzione o, se si sta creando una query di aggregazione, nella clausola HAVING.  
  
> [!NOTE]  
>  È inoltre possibile utilizzare condizioni di ricerca per indicare le righe su cui ha effetto una query di aggiornamento, di accodamento, di accodamento valori, di eliminazione o di creazione tabella.  
  
 Al momento dell'esecuzione della query, il [!INCLUDE[ssDE](../../includes/ssde-md.md)] esamina e applica la condizione di ricerca a ciascuna riga delle tabelle in cui si esegue la ricerca. Se la riga soddisfa la condizione, verrà inclusa nella query. Ad esempio, una condizione per la ricerca di tutti i dipendenti di una determinata regione potrebbe essere:  
  
```  
region = 'UK'  
```  
  
 Per definire i criteri per l'inserimento di una riga in un risultato, è possibile utilizzare più condizioni di ricerca. Ad esempio, la seguente condizione di ricerca è costituita da due condizioni di ricerca. La query include una riga nel set di risultati soltanto se tale riga soddisfa entrambe le condizioni.  
  
```  
region = 'UK' AND product_line = 'Housewares'  
```  
  
 È possibile combinare queste condizioni con l'operatore AND o OR. Nell'esempio precedente è stato utilizzato AND, mentre nel criterio riportato di seguito viene utilizzato OR. In questo secondo caso il set di risultati includerà tutte le righe che soddisfano una o entrambe le condizioni di ricerca:  
  
```  
region = 'UK' OR product_line = 'Housewares'  
```  
  
 È inoltre possibile combinare condizioni di ricerca per una singola colonna. Ad esempio, il seguente criterio combina due condizioni per la colonna region:  
  
```  
region = 'UK' OR region = 'US'  
```  
  
 Per informazioni dettagliate sulla combinazione di condizioni di ricerca, vedere i seguenti argomenti:  
  
-   [Convenzioni per la combinazione delle condizioni di ricerca nel riquadro Criteri &#40;Visual Database Tools&#41;](conventions-combine-search-conditions-in-criteria-pane-visual-db-tools.md)  
  
-   [Definizione di più condizioni di ricerca per una sola colonna &#40;Visual Database Tools&#41;](visual-database-tools.md)  
  
-   [Definizione di più condizioni di ricerca per più colonne &#40;Visual Database Tools&#41;](specify-multiple-search-conditions-for-multiple-columns-visual-database-tools.md)  
  
-   [Combinazione di condizioni quando AND ha la precedenza &#40;Visual Database Tools&#41;](combine-conditions-when-and-has-precedence-visual-database-tools.md)  
  
-   [Combinazione di condizioni quando OR ha la precedenza &#40;Visual Database Tools&#41;](combine-conditions-when-or-has-precedence-visual-database-tools.md)  
  
## <a name="examples"></a>Esempi  
 Di seguito vengono forniti alcuni esempi di query che utilizzano vari operatori e criteri per le righe:  
  
-   **Valore letterale** Un singolo valore di testo, numerico, di data o logico. In questo esempio viene utilizzato un valore letterale per trovare tutte le righe relative ai dipendenti che vivono nel Regno Unito:  
  
    ```  
    WHERE region = 'UK'  
    ```  
  
-   **Riferimento a una colonna** Confronta i valori di due colonne. In questo esempio vengono cercate all'interno di una tabella `products` tutte le righe nelle quali il valore del costo di produzione è inferiore al costo di spedizione:  
  
    ```  
    WHERE prod_cost < ship_cost  
    ```  
  
-   **Funzione** Riferimento a una funzione che può essere risolto dal back-end del database per calcolare un valore per la ricerca. La funzione può essere una funzione definita dal server di database o una funzione definita dall'utente che restituisce un valore scalare. In questo esempio vengono cercati gli ordini inviati nel giorno corrente (la funzione GETDATE( ) restituisce la data corrente):  
  
    ```  
    WHERE order_date = GETDATE()  
    ```  
  
-   **NULL** In questo esempio vengono cercati all'interno di una tabella `authors` tutti gli autori per cui è stato registrato il nome:  
  
    ```  
    WHERE au_fname IS NOT NULL  
    ```  
  
-   **Calcolo** Il risultato di un calcolo può includere valori letterali, riferimenti a colonne o altre espressioni. In questo esempio viene eseguita una ricerca all'interno di una tabella `products` per trovare tutte le righe in cui il prezzo di vendita al dettaglio è più del doppio del costo di produzione:  
  
    ```  
    WHERE sales_price > (prod_cost * 2)  
    ```  
  
## <a name="see-also"></a>Vedere anche  
 [Procedure per le query e visualizzazioni di progettazione &#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)   
 [Specificare i criteri di ricerca &#40;Visual Database Tools&#41;](specify-search-criteria-visual-database-tools.md)   
 [Esecuzione di query con parametri &#40;Visual Database Tools&#41;](query-with-parameters-visual-database-tools.md)  
  
  
