---
title: Specificare le condizioni per i gruppi (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- HAVING clause, query groups
- group query conditions [SQL Server]
ms.assetid: 269ad9c5-3261-4526-badf-7be3c869f229
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 851245e9e294a5b7f5dfe0db9945bf6c2005ea0e
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/16/2019
ms.locfileid: "68263593"
---
# <a name="specify-conditions-for-groups-visual-database-tools"></a>Definizione di condizioni per i gruppi (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Per limitare i gruppi inclusi in una query, è possibile specificare una condizione che si applica a tutti i gruppi, ossia una clausola HAVING. Dopo il raggruppamento e l'aggregazione dei dati, vengono applicate le condizioni nella clausola HAVING. Nella query verranno inseriti solo i gruppi che soddisfano le condizioni.  
  
Può ad esempio essere necessario visualizzare il prezzo medio di tutti i libri di ciascun editore nella tabella `titles` , ma solo se il prezzo medio è maggiore di 10 dollari. In questo caso, è possibile specificare una clausola HAVING con una condizione quale `AVG(price) > 10`.  
  
> [!NOTE]  
> In alcuni casi, può essere necessario escludere singole righe dai gruppi prima di applicare una condizione a tutti i gruppi. Per informazioni dettagliate, vedere [Utilizzo delle clausole HAVING e WHERE nella stessa query &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/use-having-and-where-clauses-in-the-same-query-visual-database-tools.md).  
  
È possibile creare condizioni complesse per una clausola HAVING utilizzando AND e OR per collegare le condizioni. Per informazioni dettagliate sull'uso di AND e OR nelle condizioni di ricerca, vedere [Definizione di più condizioni di ricerca per una sola colonna & #40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-multiple-search-conditions-for-one-column-visual-database-tools.md).  
  
### <a name="to-specify-a-condition-for-a-group"></a>Per specificare una condizione per un gruppo  
  
1.  Specificare i gruppi per la query. Per informazioni dettagliate, vedere [Raggruppare righe nei risultati di una query &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/group-rows-in-query-results-visual-database-tools.md).  
  
2.  Se necessario, aggiungere nel [riquadro Criteri](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md) la colonna su cui si vuole basare la condizione. In genere la condizione riguarda una colonna che fa già parte di un gruppo o di un riepilogo. Non è possibile utilizzare una colonna che non fa parte di una funzione di aggregazione o della clausola GROUP BY.  
  
3.  Nella colonna **Filtro** specificare la condizione da applicare al gruppo.  
  
    In [Progettazione query e Progettazione viste](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) verrà creata automaticamente una clausola HAVING nell'istruzione del [riquadro SQL](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md), come nell'esempio seguente:  
  
    ```  
    SELECT pub_id, AVG(price)  
    FROM titles  
    GROUP BY pub_id  
    HAVING (AVG(price) > 10)  
    ```  
  
4.  Ripetere i passaggi 2 e 3 per tutte le altre condizioni da specificare.  
  
## <a name="see-also"></a>Vedere anche  
[Ordinare e raggruppare i risultati delle query &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
  
