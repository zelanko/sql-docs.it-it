---
title: Esplorazione e pulizia dei dati | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 7c888c95-8986-461e-9f11-2395044b9d97
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 79d356aa1b14ac30ba5bc9a8f579fc66ddebea92
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66081265"
---
# <a name="exploring-and-cleaning-data"></a>Esplorazione e pulizia dei dati
  La preparazione dei dati non è una semplice pulizia dei dati. Si tenga presente che la modalità con cui i dati vengono preparati influisce anche su come i risultati alla fine vengono interpretati. La preparazione dei dati include le attività seguenti:  
  
-   Esplorazione e controllo della distribuzione dei dati.  
  
-   Pulizia dei record errati e scelta delle colonne per il data mining.  
  
-   Gestione corretta dei valori Null.  
  
-   Creazione di contenitori per i valori o aggregazione di valori in blocchi diversi di tempo.  
  
-   Aggiunta di etichette per migliorare l'utilizzabilità dei risultati.  
  
-   Conversione dei tipi di dati o categorizzazione dei valori se necessario per l'analisi.  
  
 Se non si ha familiarità con la modellazione dei dati, è consigliabile leggere l'argomento correlato [elenco di controllo della preparazione per il data mining](checklist-of-preparation-for-data-mining.md).  
  
## <a name="data-preparation-tools"></a>Strumenti di preparazione dei dati  
 I componenti aggiuntivi Data mining per Office includono i seguenti strumenti per la pulizia e la preparazione dei dati:  
  
### <a name="explore-data"></a>Esplorazione dati  
 Utilizzare la procedura guidata **Esplora dati** per le attività di preparazione dei dati seguenti:  
  
-   Visualizzare un'anteprima dei dati per identificare gli errori che devono essere corretti prima dell'analisi.  
  
-   Raccogliere informazioni statistiche utili per comprendere il bilanciamento dei dati e delle attività di pulizia necessarie.  
  
-   Identificare le colonne utili per l'analisi e pianificare la fase di modellazione dei dati.  
  
 [Esplorare i dati &#40;SQL Server componenti aggiuntivi Data Mining&#41;](explore-data-sql-server-data-mining-add-ins.md).  
  
### <a name="detect-and-handle-outliers"></a>Rilevamento e gestione degli outlier  
 La procedura guidata **outlier** esegue il grafico della distribuzione dei valori nei dati e consente di rimuovere i valori estremi. Utilizzare lo strumento **outlier** per le seguenti attività di preparazione dei dati:  
  
-   Determinare se i singoli valori siano affidabili, in base ai modelli individuati nei dati.  
  
-   Esaminare valori anomali ed eseguire le azioni appropriate per eliminarli o sostituirli.  
  
-   Definire l'ambito di un modello in un intervallo di valori specifico. Se, ad esempio, si hanno outlier per un negozio specifico, è possibile eliminare tale valore e ottenere un modello in grado di eseguire una migliore stima degli altri negozi.  
  
 [Outlier &#40;SQL Server i componenti aggiuntivi Data Mining&#41;](outliers-sql-server-data-mining-add-ins.md).  
  
### <a name="relabel-and-bin-data"></a>Modifica etichette e categorizzazione dati  
 La procedura guidata modifica **etichette** consente di raggruppare i dati in base ai valori in modo che sia possibile modificare le etichette nei dati. Utilizzare lo strumento Modifica etichette per le attività di preparazione dei dati seguenti:  
  
-   Modificare i codici numerici utilizzati nei risultati di un sondaggio con una descrizione del significato dei codici.  
  
     È ad esempio possibile sostituire Gender = 1 (Genere = 1) con Gender = Female (Genere = Femmina).  
  
-   Suddividere i dati creando gruppi per rappresentare intervalli di numeri.  
  
     È possibile, ad esempio, sostituire una colonna Income dei numeri con etichette quali **reddito-moderato** e **reddito-alto**.  
  
-   Comprimere i valori discreti in categorie.  
  
     Se ad esempio si possiedono troppi prodotti singoli per poter individuare un modello di acquisto, è possibile provare ad assegnare i prodotti a categorie più ampie.  
  
 [Modifica etichette &#40;SQL Server i componenti aggiuntivi Data mining&#41;](relabel-sql-server-data-mining-add-ins.md)  
  
### <a name="cleanse-data"></a>Pulizia dei dati  
 La pulizia dei dati include un'ampia gamma di attività, la maggior parte delle quali sono supportate da componenti aggiuntivi  
  
-   Identificare i valori NULL e determinare se devono essere modificati in valori reali o essere gestiti come valori `Missing`.  
  
-   Individuare i valori mancanti, quindi rimuoverli o assegnare loro un valore appropriato come medio, Null o un altro valore.  
  
 [Esplorare &#40;dati SQL Server componenti aggiuntivi Data mining&#41;](explore-data-sql-server-data-mining-add-ins.md)  
  
 [Modifica etichette &#40;SQL Server i componenti aggiuntivi Data mining&#41;](relabel-sql-server-data-mining-add-ins.md)  
  
 [Estendi da esempio](fill-from-example-table-analysis-tools-for-excel.md)  
  
### <a name="sample-data"></a>Dati di esempio  
 La procedura guidata Dati di esempio consente di creare set di dati equilibrati per il training e il testing dei modelli in due modi.  
  
-   **Campionamento casuale.** Utilizzare questa opzione per estrarre un set di dati rappresentativo da un più ampio set di dati, da utilizzare come training o test. I componenti aggiuntivi Data mining utilizzano il *campionamento stratificato* per assicurare che venga ottenuto un set di valori bilanciato per ogni variabile campionata.  
  
-   **Sovracampionamento.** Utilizzare questa opzione quando la quantità di dati a disposizione è inferiore a quella che si vorrebbe per un risultato di destinazione e occorre ponderare i dati con più precisione. Le frodi possono essere relativamente rare, ma è possibile sovracampionare i casi di frode per ottenere dati adeguati per la creazione di un modello.  
  
 [&#40;di dati di esempio SQL Server&#41;componenti aggiuntivi Data mining ](sample-data-sql-server-data-mining-add-ins.md).  
  
## <a name="see-also"></a>Vedi anche  
 [Creazione di un modello di data mining](creating-a-data-mining-model.md)   
 [Convalida di modelli e utilizzo di modelli per la stima &#40;componenti aggiuntivi Data mining per Excel&#41;](validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel.md)   
 [Distribuzione e scalabilità di modelli di data mining &#40;componenti aggiuntivi Data mining per Excel&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)  
  
  
