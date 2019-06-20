---
title: Nei modelli tabulari di Analysis Services colonne calcolate | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2768449e242b7da66406b9c1a5b95084e0f04949
ms.sourcegitcommit: a6949111461eda0cc9a71689f86b517de3c5d4c1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/19/2019
ms.locfileid: "67263383"
---
# <a name="calculated-columns"></a>Colonne calcolate
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Colonne calcolate, nei modelli tabulari, consentono di aggiungere nuovi dati al modello. Anziché incollare o importare i valori nella colonna, si crea una formula DAX che definisce i valori a livello di riga della colonna. La colonna calcolata può quindi essere utilizzata in un report, in una tabella pivot o in un grafico pivot come qualsiasi altra colonna.  
 
  
  
##  <a name="bkmk_understanding"></a> Vantaggi  
 Le formule nelle colonne calcolate sono molto simili a quelle in Excel. A differenza di Excel tuttavia, non è possibile creare formule diverse per le diverse righe di una tabella, infatti la formula DAX viene applicata automaticamente a tutta la colonna.  
  
 Se in una colonna è contenuta una formula, il valore viene calcolato per ogni riga. I risultati vengono calcolati per la colonna quando si immette una formula valida. I valori della colonna vengono quindi ricalcolati se necessario, ad esempio quando vengono aggiornati i dati sottostanti.  
  
 È possibile creare colonne calcolate basate su misure e su altre colonne calcolate. È ad esempio possibile creare una colonna calcolata per estrarre un numero da una stringa di testo, quindi utilizzare tale numero in un'altra colonna calcolata.  
  
 Una colonna calcolata è basata sui dati già presenti in una tabella esistente o creati tramite una formula DAX. Ad esempio, è possibile scegliere di concatenare valori, di effettuare un'aggiunta, di estrarre sottostringhe o di confrontare i valori in altri campi. Per aggiungere una colonna calcolata, è necessario disporre già di almeno una tabella nel modello.  
  
 In questo esempio viene dimostrata una semplice formula in una colonna calcolata:  
  
```  
=EOMONTH([StartDate],0])  
  
```  
  
 Questa formula consente di estrarre il mese dalla colonna StartDate. Successivamente viene calcolato il valore di fine mese per ogni riga della tabella. Il secondo parametro consente di specificare il numero di mesi precedenti o successivi al mese indicato in StartDate; in questo caso, 0 indica che si tratta dello stesso mese. Ad esempio, se il valore nella colonna StartDate è 01/06/2001, il valore nella colonna calcolata sarà 30/06/2001.  
  
##  <a name="bkmk_naming"></a> Naming a calculated column  
 Per impostazione predefinita, le nuove colonne calcolate vengono aggiunte a destra delle altre colonne in una tabella e alla colonna viene assegnato automaticamente il nome predefinito **CalculatedColumn1**, **CalculatedColumn2**e così via. Per creare una nuova colonna tra due esistenti è anche possibile fare clic con il pulsante destro del mouse su una colonna e, successivamente, selezionare Inserisci colonna. Le colonne possono essere ridisposte all'interno della stessa tabella facendo clic su di esse e trascinandole, nonché rinominate dopo la relativa creazione; tuttavia, è consigliabile tenere presente le seguenti restrizioni relative alla modifica delle colonne calcolate:  
  
-   Ogni nome di colonna deve essere univoco all'interno di una tabella.  
  
-   Evitare nomi che sono già stati utilizzati per le misure all'interno dello stesso modello. Anche se una misura e una colonna calcolata possono avere lo stesso nome, se i nomi non sono univoci si possono facilmente verificare errori di calcolo. Per evitare di richiamare casualmente una misura, quando si fa riferimento a una colonna è meglio utilizzare sempre un riferimento alla colonna completo.  
  
-   Quando si rinomina una colonna calcolata, è necessario aggiornare tutte le formule basate sulla colonna manualmente. A meno che non si tratti di una modalità di aggiornamento manuale, l'aggiornamento dei risultati delle formule viene eseguito automaticamente. Tuttavia, questa operazione potrebbe richiedere del tempo.  
  
-   Vi sono determinati caratteri che non possono essere utilizzati all'interno dei nomi di colonne. Per altre informazioni, vedere "Requisiti per la denominazione" in [Riferimento alla sintassi DAX](/dax/dax-syntax-reference).  
  
##  <a name="bkmk_perf"></a> Performance of calculated columns  
 La formula per una colonna calcolata può richiedere un maggior numero di risorse rispetto alla formula utilizzata per una misura, poiché, ad esempio, il risultato di una colonna calcolata viene calcolato sempre per ogni riga di una tabella, mentre una misura viene calcolata solo per le celle definite dal filtro utilizzato in un report, in una tabella pivot o in un grafico pivot. In una tabella con un milione di righe, ad esempio, sarà sempre presente una colonna calcolata con un milione di risultati con conseguente effetto sulle prestazioni. Una tabella pivot, invece, consente in genere di filtrare i dati applicando le intestazioni di riga e colonna. Una misura viene pertanto calcolata solo per il subset di dati presente in ogni cella della tabella pivot.  
  
 Una formula dipende dagli oggetti a cui fa riferimento, quali altre colonne o espressioni che valutano i valori. Ad esempio, una colonna calcolata basata su un'altra colonna o un calcolo che contiene un'espressione con un riferimento a una colonna non può pertanto essere valutato fino a quando non viene valutata l'altra colonna. Per impostazione predefinita, l'aggiornamento automatico è abilitato nelle cartelle di lavoro; pertanto, tutte queste dipendenze possono influire sulle prestazioni mentre le formule e i valori vengono aggiornati.  
  
 Per evitare problemi di prestazioni quando si creano colonne calcolate, seguire queste linee guida:  
  
-   Anziché creare una sola formula contenente più dipendenze complesse, creare le formule in passaggi, salvando i risultati nelle colonne in modo che sia possibile convalidarli e valutare le prestazioni.  
  
-   La modifica dei dati comporta spesso il ricalcolo delle colonne calcolate. È possibile impedire questo comportamento impostando la modalità di ricalcolo manuale. Tuttavia, se i valori nella colonna calcolata non sono corretti, la colonna verrà disattivata fino a quando non si aggiornano e si ricalcolano i dati.  
  
-   Se si modificano o si eliminano relazioni tra tabelle, le formule per le quali vengono utilizzate le colonne di tali tabelle non saranno più valide.  
  
-   Se si crea una formula contenente una dipendenza circolare o autoreferenziale, si verificherà un errore.  
  
##  <a name="bkmk_rel_tasks"></a> Related tasks  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Creare una colonna calcolata](../../analysis-services/tabular-models/ssas-calculated-columns-create-a-calculated-column.md)|Nelle attività di questo argomento viene descritto come aggiungere una nuova colonna calcolata a una tabella.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle e colonne](../../analysis-services/tabular-models/tables-and-columns-ssas-tabular.md)   
 [Misure](../../analysis-services/tabular-models/measures-ssas-tabular.md)   
 [Calcoli](../../analysis-services/tabular-models/calculations-ssas-tabular.md)  
  
  
