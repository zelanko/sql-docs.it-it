---
title: Creare query di accodamento (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- queries [SQL Server], types
- result sets [SQL Server], queries
- results [SQL Server], query
- Insert Results query
- queries [SQL Server], results
ms.assetid: 8770d630-09cc-47ec-a0e9-e9de2d7bbc89
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ebffc2246f0940c4643af2267086e727882a0633
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63031970"
---
# <a name="create-insert-results-queries-visual-database-tools"></a>Creazione di query di accodamento (Visual Database Tools)
  Le query di accodamento consentono di copiare righe da una tabella a un'altra oppure all'interno di una stessa tabella. Ad esempio, in una tabella `titles` è possibile utilizzare una query di accodamento per copiare le informazioni riguardanti tutti i titoli di un editore in una seconda tabella da presentare all'editore stesso. La query di accodamento è analoga alla query di creazione tabella, con la differenza che le righe vengono copiate in una tabella esistente.  
  
> [!TIP]  
>  Per copiare righe da una tabella a un'altra, è anche possibile utilizzare i comandi Copia e Incolla. Creare una query per ogni tabella ed eseguire le query, quindi copiare le righe desiderate da una griglia di risultati all'altra.  
  
 Durante la creazione di una query di accodamento è necessario specificare:  
  
-   La tabella di database in cui copiare le righe, ossia la tabella di destinazione.  
  
-   Le tabelle da cui copiare le righe, ossia le tabelle di origine. Le tabelle di origine entrano a far parte di una sottoquery. Se la copia viene effettuata all'interno della stessa tabella, la tabella di origine e quella di destinazione coincideranno.  
  
-   Le colonne della tabella di origine di cui si desidera copiare il contenuto.  
  
-   Le colonne della tabella di destinazione in cui si desidera copiare i dati.  
  
-   Le condizioni di ricerca per la definizione delle righe da copiare.  
  
-   Il criterio di ordinamento, se si desidera copiare le righe in un particolare ordine.  
  
-   Le opzioni di raggruppamento, se si desidera copiare solo le informazioni di riepilogo.  
  
 L'esempio di query fornito di seguito consente di copiare le informazioni sui titoli dalla tabella `titles` a una tabella di archivio denominata `archivetitles`: La query copia il contenuto di quattro colonne per tutti i titoli appartenenti all'editore specificato:  
  
```  
INSERT INTO archivetitles   
   (title_id, title, type, pub_id)  
SELECT title_id, title, type, pub_id  
FROM titles  
WHERE (pub_id = '0766')  
```  
  
> [!NOTE]  
>  Per inserire i valori in una nuova riga, utilizzare una query di accodamento valori.  
  
 È possibile copiare il contenuto delle colonne selezionate o di tutte le colonne in una riga. In entrambi i casi, è necessario che i dati copiati siano compatibili con le colonne delle righe di destinazione. Ad esempio, per copiare il contenuto di una colonna quale `price`, è necessario che la colonna di destinazione consenta l'inserimento di dati numerici con decimali. Se si copia una riga intera, è necessario che la tabella di destinazione disponga di colonne compatibili nella stessa posizione fisica rispetto alla colonna di origine.  
  
 Quando si crea una query di accodamento, nel riquadro Criteri vengono visualizzate le opzioni disponibili per la copia di dati. Verrà inoltre aggiunta una colonna Accodamento dove specificare le colonne in cui copiare i dati.  
  
> [!CAUTION]  
>  Una volta eseguita, la query di accodamento non potrà essere annullata. È dunque opportuno eseguire una copia di backup dei dati prima di eseguire la query.  
  
### <a name="to-create-an-insert-results-query"></a>Per creare una query di accodamento  
  
1.  Creare una nuova query e aggiungere la tabella da cui si desidera copiare le righe, ovvero la tabella di origine. Se si sta effettuando la copia di righe all'interno di una stessa tabella, sarà possibile aggiungere la tabella di origine come tabella di destinazione.  
  
2.  Scegliere **Modifica tipo** dal menu **Progettazione query**, quindi **Accodamento**.  
  
3.  Nella [finestra di dialogo Scegliere la tabella di destinazione per Accodamento](visual-database-tools.md)selezionare la tabella in cui copiare le righe (la tabella di destinazione).  
  
    > [!NOTE]  
    >  In Progettazione query e Progettazione viste non è possibile stabilire in anticipo le tabelle e le viste da aggiornare. Pertanto nell'elenco **Nome tabella** della finestra di dialogo **Choose Table for Insert From Query** (Scegli tabella per query di inserimento) sono visualizzate tutte le tabelle e le viste disponibili nella connessione dati su cui si esegue la query, anche quelle che non sono valide come tabelle o viste di destinazione.  
  
4.  Nel rettangolo che rappresenta la tabella o l'oggetto con valori di tabella scegliere i nomi delle colonne di cui si desidera copiare il contenuto. Per copiare righe intere, scegliere  **\* (tutte le colonne)** .  
  
     Le colonne selezionate verranno aggiunte alla colonna **Colonna** del riquadro Criteri.  
  
5.  Nella colonna **Aggiungi** del riquadro Criteri selezionare una colonna di destinazione nella tabella di destinazione per ogni colonna da copiare. Scegli *tablename.\**  se si desidera copiare righe intere. I tipi di dati nelle colonne della tabella di destinazione devono essere uguali o compatibili con quelli delle colonne nella tabella di origine.  
  
6.  Se si desidera copiare le righe in un particolare ordine, specificare il criterio di ordinamento. Per informazioni dettagliate, vedere [Ordinare e raggruppare i risultati delle query &#40;Visual Database Tools&#41;](sort-and-group-query-results-visual-database-tools.md).  
  
7.  Specificare le righe da copiare immettendo le condizioni di ricerca nella colonna **Filtro**. Per informazioni dettagliate, vedere [Specifica di criteri di ricerca &#40;Visual Database Tools&#41;](specify-search-criteria-visual-database-tools.md).  
  
     Se non si specifica alcuna condizione di ricerca, tutte le righe della tabella di origine verranno copiate nella tabella di destinazione.  
  
    > [!NOTE]  
    >  Quando nel riquadro Criteri si aggiunge una colonna da includere nella ricerca, tale colonna verrà aggiunta anche all'elenco delle colonne da copiare. Se si desidera utilizzare una colonna per la ricerca senza copiarla, deselezionare la casella di controllo accanto al nome della colonna nel rettangolo che rappresenta la tabella o l'oggetto con valori di tabella.  
  
8.  Se si desidera copiare le informazioni di riepilogo, specificare le opzioni di raggruppamento. Per informazioni dettagliate, vedere [Riepilogo dei risultati di query &#40;Visual Database Tools&#41;](summarize-query-results-visual-database-tools.md).  
  
 Quando si esegue una query di accodamento, non viene restituito alcun risultato nel [riquadro Risultati](results-pane-visual-database-tools.md). Viene invece visualizzato un messaggio che indica il numero di righe copiate.  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi di query &#40;Visual Database Tools&#41;](types-of-queries-visual-database-tools.md)   
 [Procedure per la progettazione di query e viste &#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
  
