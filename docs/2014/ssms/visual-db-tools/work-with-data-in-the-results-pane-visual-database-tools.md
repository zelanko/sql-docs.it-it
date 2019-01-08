---
title: Usare i dati nel riquadro Risultati (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- View Designer, Results pane
- queries [Visual Database Tools]
- result sets [SQL Server], queries
- Query Designer [SQL Server], Results pane
- results [SQL Server], query
- Visual Database Tools [SQL Server], queries
- queries [SQL Server], results
- Results pane
ms.assetid: 4f8a0080-91ef-4442-83ae-53be2f478c54
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d5f3dffc7661fc5843dcd220f27beb1117a85729
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52757843"
---
# <a name="work-with-data-in-the-results-pane-visual-database-tools"></a>Utilizzo dei dati nel riquadro Risultati (Visual Database Tools)
  Dopo l'esecuzione di una query o di una vista, i risultati ottenuti vengono visualizzati nel riquadro Risultati e su di essi è possibile eseguire numerose operazioni, ad esempio aggiungere ed eliminare righe, immettere o modificare dati e navigare con facilità nell'ambito di set di risultati estesi.  
  
 Le informazioni riportate di seguito consentono di evitare problemi e di utilizzare in modo ottimale i set di risultati ottenuti.  
  
## <a name="returning-the-results-set"></a>Restituzione del set di risultati  
 È possibile ottenere risultati da una query o da una vista e scegliere di aprire solo il riquadro Risultati oppure tutti i riquadri. In entrambi i casi la query o la vista verrà visualizzata in Progettazione query e Progettazione viste. La differenza è che una viene visualizzata solo con il riquadro Risultati, mentre l'altra viene visualizzata con tutte le finestre selezionate nella finestra di dialogo Opzioni. L'impostazione predefinita prevede la visualizzazione di tutti e quattro i riquadri disponibili: Risultati, SQL, Diagramma e Criteri.  
  
 Per altre informazioni, vedere [Apertura di query & #40; Visual Database Tools & #41;](visual-database-tools.md).  
  
 Per modificare la struttura della query o della vista in modo che venga restituito un diverso set di risultati o che i record vengano riportati in un altro ordine, vedere gli argomenti elencati in [Procedure per la progettazione di query e viste&#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md).  
  
 È inoltre possibile decidere se la query deve restituire una parte o tutto il set di risultati procedendo in due modi diversi, ovvero arrestando la query durante l'esecuzione o scegliendo prima dell'esecuzione quanti risultati devono essere restituiti.  
  
## <a name="navigating-in-the-results-pane"></a>Navigazione all'interno del riquadro Risultati  
 Nella parte inferiore del riquadro Risultati è presente una barra di navigazione che consente di passare velocemente da un record all'altro.  
  
 Sono disponibili pulsanti per spostarsi sul primo e sull'ultimo record, sul record successivo e su quello precedente oppure direttamente su un record specifico.  
  
 Per spostarsi su un record specifico, digitare il numero delle riga nella casella di testo all'interno della barra di navigazione, quindi premere INVIO.  
  
 Per informazioni sull'uso di tasti di scelta rapida in Progettazione query e Progettazione viste, vedere [Navigazione all'interno di Progettazione viste e Progettazione query &#40;Visual Database Tools&#41;](navigate-in-the-query-and-view-designer-visual-database-tools.md).  
  
## <a name="committing-changes-to-the-database"></a>Esecuzione del commit delle modifiche nel database  
 Nel riquadro Risultati viene utilizzato il controllo della concorrenza ottimistica, in modo che nella griglia venga visualizzata una copia dei dati del database anziché una vista completamente live. In questo modo, viene eseguito il commit delle modifiche nel database solo quando si esce da una riga, consentendo così a più utenti di utilizzare contemporaneamente il database. In caso di conflitti, ad esempio se un altro utente nel frattempo ha modificato ed eseguito il commit nel database della stessa riga che si intende modificare, verrà visualizzato un messaggio in cui viene segnalato che si è verificato un conflitto e in cui vengono indicate le possibili soluzioni.  
  
## <a name="undo-changes-using-esc"></a>Annullamento delle modifiche tramite ESC  
 È possibile annullare una modifica solo se non ne è stato ancora eseguito il commit nel database. Il commit dei dati non viene eseguito se non si esce dal record o se, uscendo dal record, viene visualizzato un messaggio di errore indicante che non sarà possibile eseguire il commit della modifica. A quel punto, è possibile annullare la modifica premendo ESC.  
  
 Per annullare tutte le modifiche apportate in una riga, spostarsi su una cella della riga che non è stata modificata e premere ESC.  
  
 Per annullare le modifiche apportate a una cella specifica, spostarsi su tale cella e premere ESC.  
  
## <a name="adding-or-deleting-data-in-the-database"></a>Aggiunta o eliminazione di dati dal database  
 Per controllare se il proprio database funziona così com'è strutturato, è possibile aggiungere dati di esempio immettendoli direttamente nel riquadro Risultati oppure copiandoli da un altro programma, quale il Blocco note o Excel, e incollandoli nel riquadro Risultati.  
  
 Oltre a copiare righe nel riquadro Risultati, è possibile aggiungere nuovi record oppure modificare o eliminare record esistenti. Per altre informazioni vedere [Aggiunta di nuove righe nel riquadro Risultati &#40;Visual Database Tools& #41;](results-pane-visual-database-tools.md), [Eliminare le righe nel riquadro Risultati &#40;Visual Database Tools&#41;](delete-rows-in-the-results-pane-visual-database-tools.md), e [Modifica di righe nel riquadro Risultati &#40;Visual Database Tools&#41;](edit-rows-in-the-results-pane-visual-database-tools.md).  
  
## <a name="tips-for-working-with-null-values-and-empty-cells"></a>Suggerimenti per l'utilizzo di valori NULL e celle vuote  
 Quando si fa clic su una riga vuota per aggiungere un nuovo record, il valore iniziale per tutte le colonne è *NULL*. Se una colonna supporta i valori Null, è possibile lasciarla invariata.  
  
 Se si desidera sostituire un valore non Null con un valore Null, digitare NULL a lettere maiuscole. Nel riquadro Risultati la parola verrà visualizzata in corsivo per indicare che deve essere riconosciuta come valore Null anziché come stringa.  
  
 Per inserire la stringa "null", digitare le diverse lettere che la compongono senza racchiuderle tra virgolette. Purché anche solo una delle lettere sia in minuscolo, il valore verrà considerato come stringa anziché come valore Null.  
  
 Per impostazione predefinita, i valori delle colonne con tipo di dati binario sono valori NULL e non possono essere modificati nel riquadro Risultati.  
  
 Per inserire uno spazio vuoto anziché utilizzare un valore Null, eliminare il testo esistente e uscire dalla cella.  
  
## <a name="validating-data"></a>Convalida dei dati  
 In Progettazione query e Progettazione viste la convalida rispetto alle proprietà delle colonne è possibile con determinati tipi di dati. Se ad esempio si immette "abc" in una colonna con tipo di dati float, verrà visualizzato un messaggio di errore e non verrà eseguito il commit della modifica nel database.  
  
 Il modo più rapido per verificare il tipo di dati di una colonna quando si è posizionati nel riquadro Risultati è quello di aprire il riquadro Diagramma e spostare il puntatore del mouse sul nome della colonna nella tabella o nell'oggetto con valori di tabella.  
  
> [!NOTE]  
>  La lunghezza massima che il riquadro Risultati è in grado di visualizzare per un tipo di dati di testo è 2.147.483.647.  
  
## <a name="keeping-the-results-set-synchronized-with-the-query-definition"></a>Mantenimento della sincronizzazione tra il set di risultati e la definizione della query  
 Mentre si lavora sui risultati di una query o di una vista, è possibile che i record nel riquadro Risultati perdano la sincronizzazione con la definizione della query. Se ad esempio è stata eseguita una query per quattro delle cinque colonne di una tabella e quindi è stato utilizzato il riquadro Diagramma per aggiungere la quinta colonna alla definizione della query, i dati di tale colonna non verranno aggiunti automaticamente al riquadro Risultati. Perché il riquadro Risultati rifletta la nuova definizione della query, sarà necessario eseguire ancora una volta la query.  
  
 Quando si verifica questa situazione, nell'angolo inferiore destro del riquadro Risultati vengono visualizzati un'icona di avviso e un messaggio indicante che la query è cambiata. Tale icona viene ripetuta nell'angolo superiore sinistro.  
  
## <a name="reconciling-changes-made-by-multiple-users"></a>Riconciliazione delle modifiche apportate da più utenti  
 Mentre si lavora sui risultati di una query o di una vista, è possibile che i record vengano modificati da un altro utente che sta utilizzando lo stesso database.  
  
 In questo caso, verrà visualizzato un avviso non appena si uscirà dalla cella che causa il conflitto. A quel punto si avrà la possibilità di eseguire l'override della modifica apportata dall'altro utente, aggiornare il riquadro Risultati con la modifica dell'altro utente o continuare a modificare il riquadro Risultati senza riconciliare le differenze. Se si sceglie di non riconciliare le differenze, non verrà eseguito il commit delle proprie modifiche nel database.  
  
## <a name="limitations-in-the-results-pane"></a>Limitazioni relative al riquadro Risultati  
  
### <a name="what-can-not-be-updated"></a>Elementi che non possono essere aggiornati  
 Di seguito vengono forniti alcuni suggerimenti utili per una gestione ottimale dei dati nel riquadro Risultati.  
  
-   Le query in cui sono incluse colonne provenienti da più tabelle o viste non possono essere aggiornate.  
  
-   Le viste possono essere aggiornate solo se i vincoli del database lo consentono.  
  
-   I risultati restituiti da una stored procedure non possono essere aggiornati.  
  
-   Le query o le viste in cui viene utilizzata la clausola GROUP BY, DISTINCT o TO XML non possono essere aggiornate.  
  
-   I risultati restituiti da funzioni con valori di tabella possono essere aggiornati solo in alcuni casi.  
  
-   I dati delle colonne risultanti da un'espressione della query non possono essere aggiornati.  
  
-   I dati non convertiti correttamente dal provider non possono essere aggiornati.  
  
### <a name="what-can-not-be-represented-fully"></a>Elementi che non possono essere rappresentati in modo completo  
 Gli elementi restituiti dal database e visualizzati nel riquadro Risultati sono in gran parte controllati dal provider dell'origine dati in uso. Nel riquadro Risultati non sempre vengono convertiti i dati provenienti da tutti i sistemi di gestione di database. Di seguito vengono descritti alcuni casi in cui si verifica questa situazione.  
  
-   I tipi di dati binari spesso non sono di alcuna utilità per chi lavora nel riquadro Risultati, oltre a richiedere lunghi tempi di download. Vengono pertanto rappresentati da  *\<i dati binari >* oppure *Null*.  
  
-   Non è sempre possibile mantenere il livello di precisione e il fattore di scala. Il riquadro Risultati supporta ad esempio un livello di precisione pari a 27. Se i dati sono di un tipo di dati con una precisione maggiore, i dati potrebbero essere troncati o può essere rappresentati da  *\<non è possibile leggere i dati >*.  
  
## <a name="see-also"></a>Vedere anche  
 [Eseguire operazioni di base con le query &#40;Visual Database Tools&#41;](perform-basic-operations-with-queries-visual-database-tools.md)   
 [Specifica dei criteri di ricerca &#40;Visual Database Tools&#41;](specify-search-criteria-visual-database-tools.md)  
  
  
