---
title: Ordinare righe (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- sorting rows [SQL Server]
- sorting query results [SQL Server]
ms.assetid: 780ef467-f96e-4373-8235-6dacbedb05a2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3235c9a9305e4476214add63f8710ba9de7b4c19
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63049154"
---
# <a name="sort-rows-visual-database-tools"></a>Ordinamento di righe (Visual Database Tools)
  È possibile ordinare le righe nel risultato di una query. In altre parole, è possibile identificare una colonna o un set di colonne particolare i cui valori determinano l'ordine delle righe nel set di risultati.  
  
> [!NOTE]  
>  Il criterio di ordinamento è determinato in parte dalla sequenza di confronto della colonna. Per cambiare la sequenza di confronto, è possibile usare la [finestra di dialogo Regole di confronto](visual-database-tools.md).  
  
 I risultati delle query possono essere ordinati in diversi modi:  
  
-   **È possibile disporre le righe in ordine crescente o decrescente** Per impostazione predefinita, in SQL vengono usate le colonne ORDER BY per disporre le righe in ordine crescente. Per disporre, ad esempio, i titoli dei libri in ordine crescente in base al prezzo, è sufficiente ordinare le righe in base alla colonna price. Il codice SQL risultante potrebbe essere simile al seguente:  
  
    ```  
    SELECT *  
    FROM titles  
    ORDER BY price  
  
    ```  
  
     Se invece si desidera disporre i titoli indicando per primi i libri più costosi, è possibile specificare in modo esplicito un ordinamento di questo tipo, ovvero indicare che le righe dei risultati devono essere disposte in ordine decrescente in base ai valori della colonna price. Il codice SQL risultante potrebbe essere simile al seguente:  
  
    ```  
    SELECT *  
    FROM titles  
    ORDER BY price DESC  
  
    ```  
  
-   **È possibile eseguire l'ordinamento in base a più colonne** È possibile, ad esempio, creare un set di risultati con una riga per ogni autore, eseguendo l'ordinamento prima in base alla nazione e poi in base alla città. Il codice SQL risultante potrebbe essere simile al seguente:  
  
    ```  
    SELECT *  
    FROM authors   
    ORDER BY state, city  
  
    ```  
  
-   **È possibile eseguire l'ordinamento in base a colonne non presenti nel set di risultati** È possibile, ad esempio, creare un set di risultati con i libri più costosi indicati per primi anche se i prezzi non sono specificati. Il codice SQL risultante potrebbe essere simile al seguente:  
  
    ```  
    SELECT title_id, title  
    FROM titles  
    ORDER BY price DESC  
  
    ```  
  
-   **È possibile eseguire l'ordinamento in base a colonne derivate**. Ad esempio, si può creare un set di risultati in cui ogni riga contiene il titolo di un libro, riportando per primi i libri con i diritti d'autore più elevati per singola copia. Il codice SQL risultante potrebbe essere simile al seguente:  
  
    ```  
    SELECT title, price * royalty / 100 as royalty_per_unit  
    FROM titles  
    ORDER BY royalty_per_unit DESC  
  
    ```  
  
     In questo esempio è evidenziata la formula che consente di calcolare i diritti di autore corrisposti per ciascuna copia di un libro.  
  
     Per calcolare una colonna derivata, è possibile utilizzare la sintassi SQL, come è stato fatto nell'esempio precedente, oppure è possibile utilizzare una funzione definita dall'utente che restituisca un valore scalare. Per ulteriori informazioni sulle funzioni definite dall'utente, vedere la documentazione di SQL Server.  
  
-   **È possibile ordinare righe raggruppate**. Ad esempio, si può creare un set di risultati in cui ogni riga descrive una città e il numero di autori in tale città, riportando per prime le città con più autori. Il codice SQL risultante potrebbe essere simile al seguente:  
  
    ```  
    SELECT city, state, COUNT(*)  
    FROM authors  
    GROUP BY city, state  
    ORDER BY COUNT(*) DESC, state  
  
    ```  
  
     Si noti che la query utilizza `state` come colonna di ordinamento secondaria. Due stati che hanno lo stesso numero di autori verranno quindi disposti in ordine alfabetico.  
  
-   **È possibile eseguire l'ordinamento usando dati internazionali** È possibile ordinare una colonna usando convenzioni di confronto diverse dalle convenzioni predefinite per tale colonna. Ad esempio, è possibile scrivere una query che recupera tutti i titoli dei libri da Jaime Pati?? o. Per visualizzare i titoli in ordine alfabetico, si utilizza una sequenza di confronto spagnola per la colonna title. Il codice SQL risultante potrebbe essere simile al seguente:  
  
    ```  
    SELECT title  
    FROM   
        authors   
        INNER JOIN   
            titleauthor   
            ON authors.au_id   
            =  titleauthor.au_id   
            INNER JOIN  
                titles   
                ON titleauthor.title_id   
                =  titles.title_id   
    WHERE   
         au_fname = 'Jaime' AND   
         au_lname = 'Pati??o'  
    ORDER BY   
         title COLLATE SQL_Spanish_Pref_CP1_CI_AS  
    ```  
  
## <a name="see-also"></a>Vedere anche  
 [Ordina e raggruppa i risultati della Query &#40;Visual Database Tools&#41;](sort-and-group-query-results-visual-database-tools.md)   
 [Procedure per la progettazione di query e viste &#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
  
