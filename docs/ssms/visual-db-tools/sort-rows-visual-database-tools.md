---
description: Ordinamento di righe (Visual Database Tools)
title: Ordinare le righe
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- sorting rows [SQL Server]
- sorting query results [SQL Server]
ms.assetid: 780ef467-f96e-4373-8235-6dacbedb05a2
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 2cc6ae5da87b1ef1f70c7b66fe3f06d8e6b2ed90
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491584"
---
# <a name="sort-rows-visual-database-tools"></a>Ordinamento di righe (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
È possibile ordinare le righe nel risultato di una query. In altre parole, è possibile identificare una colonna o un set di colonne particolare i cui valori determinano l'ordine delle righe nel set di risultati.  
  
> [!NOTE]  
> Il criterio di ordinamento è determinato in parte dalla sequenza di confronto della colonna. Per cambiare la sequenza di confronto, è possibile usare la [finestra di dialogo Regole di confronto](../../ssms/visual-db-tools/collation-dialog-box-visual-database-tools.md).  
  
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
  
-   **È possibile eseguire l'ordinamento usando dati internazionali** È possibile ordinare una colonna usando convenzioni di confronto diverse dalle convenzioni predefinite per tale colonna. È possibile ad esempio scrivere una query che recuperi tutti i libri di Jaime Patiño. Per visualizzare i titoli in ordine alfabetico, si utilizza una sequenza di confronto spagnola per la colonna title. Il codice SQL risultante potrebbe essere simile al seguente:  
  
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
         au_lname = 'Patiño'  
    ORDER BY   
         title COLLATE SQL_Spanish_Pref_CP1_CI_AS  
    ```  
  
## <a name="see-also"></a>Vedere anche  
[Ordinare e raggruppare i risultati delle query &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[Procedure per la progettazione di query e viste &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
