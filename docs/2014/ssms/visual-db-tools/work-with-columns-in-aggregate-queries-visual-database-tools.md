---
title: Usare colonne in query di aggregazione (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- HAVING clause, query summary results
- GROUP BY clause, query summary results
- aggregate queries [SQL Server]
- WHERE clause, query summary results
ms.assetid: 1b82681f-3d4f-4b9a-bb1d-2060e44f2577
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c14608a34c2df5a0e93fea985d8135a37d5ffa53
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63273281"
---
# <a name="work-with-columns-in-aggregate-queries-visual-database-tools"></a>Utilizzo di colonne in query di aggregazione (Visual Database Tools)
  Quando si creano query di aggregazione con [Progettazione query e Progettazione viste](visual-database-tools.md) , le operazioni vengono eseguite sulla base di alcuni presupposti che garantiscono la generazione di una query valida. Se, ad esempio, si crea una query di aggregazione e si contrassegna una colonna di dati per l'output, in Progettazione query e Progettazione viste la colonna viene automaticamente inserita nella clausola GROUP BY, in modo che non sia possibile visualizzare inavvertitamente il contenuto di una singola riga in un riepilogo.  
  
## <a name="using-group-by"></a>Utilizzo dell'opzione Group By  
 In Progettazione query e Progettazione viste vengono utilizzate le seguenti regole per le operazioni con le colonne:  
  
-   Quando si sceglie l'opzione Group By o si aggiunge una funzione di aggregazione a una query, tutte le colonne contrassegnate per l'output o utilizzate per l'ordinamento vengono aggiunte automaticamente alla clausola GROUP BY. Le colonne non vengono aggiunte automaticamente alla clausola GROUP BY se fanno già parte di una funzione di aggregazione.  
  
     Se non si desidera inserire una determinata colonna nella clausola GROUP BY, è necessario modificarla manualmente selezionando una diversa opzione nella colonna Group By del riquadro Criteri. È possibile, tuttavia, scegliere un'opzione che può dare come risultato una query non eseguibile.  
  
-   Se si aggiunge manualmente una colonna di output della query a una funzione di aggregazione nel riquadro Criteri o SQL, in Progettazione query e Progettazione viste le altre colonne di output non verranno rimosse automaticamente dalla query. Sarà quindi necessario rimuovere le restanti colonne dall'output della query o inserirle in una clausola GROUP BY o in una funzione di aggregazione manualmente.  
  
 Quando si immette una condizione di ricerca nella colonna Filtro del riquadro Criteri, in Progettazione query e Progettazione viste vengono rispettate le seguenti regole:  
  
-   Se la colonna **Group By** della griglia non è visualizzata perché non è stata ancora specificata una query di aggregazione, la condizione di ricerca verrà inserita nella clausola WHERE.  
  
-   Se ci si trova già in una query di aggregazione ed è stata selezionata l'opzione **Where** nella colonna **Group By** , la condizione di ricerca verrà inserita nella clausola WHERE.  
  
-   Se la colonna **Group By** contiene un valore diverso da **Where**, la condizione di ricerca verrà inserita nella clausola HAVING.  
  
## <a name="using-the-having-and-where-clauses"></a>Utilizzo delle clausole HAVING e WHERE  
 I seguenti principi descrivono come fare riferimento a colonne nelle condizioni di ricerca per una query di aggregazione. In generale, è possibile utilizzare una colonna in una condizione di ricerca per filtrare le righe da riepilogare (una clausola WHERE) o per determinare quali risultati raggruppati saranno presenti nell'output finale (una clausola HAVING).  
  
-   Le singole colonne di dati possono essere inserite nella clausola WHERE o HAVING, in base a come vengono utilizzate in altri punti della query.  
  
-   Le clausole WHERE vengono utilizzate per selezionare un subset di righe per i riepiloghi e i raggruppamenti e vengono pertanto applicate prima dell'esecuzione del raggruppamento. È quindi possibile utilizzare una colonna di dati in una clausola WHERE anche se non fa parte della clausola GROUP BY o non è contenuta in una funzione di aggregazione. La seguente istruzione seleziona, ad esempio, tutti i libri che costano più di 10 dollari e calcola il prezzo medio:  
  
    ```  
    SELECT AVG(price)  
    FROM titles  
    WHERE price > 10  
    ```  
  
-   Se si crea una condizione di ricerca che coinvolge una colonna usata anche in una clausola GROUP BY o in una funzione di aggregazione, la condizione di ricerca potrà essere indicata come una clausola WHERE o HAVING. La clausola da usare può essere scelta quando si definisce la condizione. La seguente istruzione consente di calcolare, ad esempio, il prezzo medio dei libri di ogni editore, quindi visualizza la media calcolata per gli editori il cui prezzo medio è maggiore di 10 dollari.  
  
    ```  
    SELECT pub_id, AVG(price)  
    FROM titles  
    GROUP BY pub_id  
    HAVING (AVG(price) > 10)  
    ```  
  
-   Se si utilizza una funzione di aggregazione in una condizione di ricerca, la condizione richiederà un riepilogo e dovrà pertanto essere inserita nella clausola HAVING.  
  
## <a name="see-also"></a>Vedere anche  
 [Riepilogare i risultati delle query &#40;Visual Database Tools&#41;](summarize-query-results-visual-database-tools.md)   
 [Ordinare e raggruppare i risultati delle query &#40;Visual Database Tools&#41;](sort-and-group-query-results-visual-database-tools.md)  
  
  
