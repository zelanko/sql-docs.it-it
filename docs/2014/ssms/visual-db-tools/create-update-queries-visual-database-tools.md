---
title: Creare query di aggiornamento (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- tables [SQL Server], updating
- queries [SQL Server], types
- Update query
- updating tables
ms.assetid: 178b7b75-8078-4e61-b2a8-4719b9d8033d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 47951e101a5f8f480496c8570a22cd1a950b3309
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63270579"
---
# <a name="create-update-queries-visual-database-tools"></a>Creazione di query di aggiornamento (Visual Database Tools)
  Per modificare il contenuto di più righe contemporaneamente, è possibile utilizzare una query di aggiornamento. Ad esempio, in una tabella `titles` è possibile utilizzare una query di aggiornamento per aumentare del 10% il prezzo di tutti i libri di un determinato editore.  
  
 Durante la creazione di una query di aggiornamento è necessario specificare:  
  
-   la tabella da aggiornare;  
  
-   le colonne di cui si desidera aggiornare il contenuto;  
  
-   il valore o l'espressione da utilizzare per aggiornare le singole colonne;  
  
-   le condizioni di ricerca per la definizione delle righe da aggiornare.  
  
 Ad esempio, nella seguente query la tabella `titles` viene aggiornata aggiungendo il 10% al prezzo di tutti i titoli di un editore:  
  
```  
UPDATE titles  
SET price = price * 1.1  
WHERE (pub_id = '0766')  
```  
  
> [!CAUTION]  
>  Una volta eseguita, la query di aggiornamento non potrà essere annullata. È dunque opportuno eseguire una copia di backup dei dati prima di eseguire la query.  
  
### <a name="to-create-an-update-query"></a>Per creare una query di aggiornamento  
  
1.  Aggiungere al riquadro Diagramma la tabella da aggiornare.  
  
2.  Scegliere **Modifica tipo** dal menu **Progettazione query**e quindi **Aggiorna**.  
  
    > [!NOTE]  
    >  Se nel riquadro Diagramma è visualizzata più di una tabella quando si avvia la query di aggiornamento, in Progettazione query e Progettazione viste verrà visualizzata la [finestra di dialogo Scegliere la tabella di destinazione per Accodamento valori](visual-database-tools.md) , in cui sarà possibile specificare il nome della tabella da aggiornare.  
  
3.  Nel riquadro Diagramma selezionare le caselle di controllo relative alle colonne per cui si desidera specificare nuovi valori. Queste colonne verranno visualizzate nel riquadro Criteri. Verranno aggiornate solo le colonne aggiunte alla query.  
  
4.  Nella colonna **Nuovo valore** del riquadro Criteri immettere il valore aggiornato per la colonna. È possibile immettere valori letterali, nomi di colonna o espressioni. Il valore deve corrispondere o essere compatibile con il tipo di dati della colonna da aggiornare.  
  
    > [!CAUTION]  
    >  In Progettazione query e Progettazione viste non è possibile verificare la compatibilità di un valore rispetto alla lunghezza della colonna da aggiornare. Se il valore inserito è troppo lungo, è possibile che venga troncato senza preavviso. Ad esempio, se una colonna `name` è lunga 20 caratteri ma si specifica un valore di aggiornamento di 25 caratteri, è possibile che gli ultimi 5 caratteri vengano troncati.  
  
5.  Definire le righe da aggiornare immettendo le condizioni di ricerca nella colonna **Filtro**. Per informazioni dettagliate, vedere [Specifica di criteri di ricerca &#40;Visual Database Tools&#41;](specify-search-criteria-visual-database-tools.md).  
  
     Se non si specifica alcuna condizione di ricerca, verranno aggiornate tutte le righe della tabella specificata.  
  
    > [!NOTE]  
    >  Quando si aggiunge al riquadro Criteri una colonna da utilizzare in una condizione di ricerca, in Progettazione query e Progettazione viste la colonna verrà aggiunta anche all'elenco delle colonne da aggiornare. Se si desidera utilizzare una colonna per una condizione di ricerca senza aggiornarla, deselezionare la casella di controllo accanto al nome della colonna nel rettangolo che rappresenta la tabella o l'oggetto con valori di tabella.  
  
 Quando si esegue una query di aggiornamento, non viene restituito alcun risultato nel [riquadro Risultati](results-pane-visual-database-tools.md). Viene invece visualizzato un messaggio che indica il numero di righe modificate.  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi di Query supportati &#40;Visual Database Tools&#41;](supported-query-types-visual-database-tools.md)   
 [Procedure per le query e visualizzazioni di progettazione &#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)   
 [Eseguire operazioni di base con le query &#40;Visual Database Tools&#41;](perform-basic-operations-with-queries-visual-database-tools.md)  
  
  
