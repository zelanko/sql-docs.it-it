---
title: Esplorazione e pulizia dei dati | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 7c888c95-8986-461e-9f11-2395044b9d97
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d212cf20e8701f9fc9af5266308f81873e6fc4c6
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52541247"
---
# <a name="exploring-and-cleaning-data"></a>Esplorazione e pulizia dei dati
  La preparazione dei dati non è una semplice pulizia dei dati. Si tenga presente che la modalità con cui i dati vengono preparati influisce anche su come i risultati alla fine vengono interpretati. La preparazione dei dati include le attività seguenti:  
  
-   Esplorazione e controllo della distribuzione dei dati.  
  
-   Pulizia dei record errati e scelta delle colonne per il data mining.  
  
-   Gestione corretta dei valori Null.  
  
-   Creazione di contenitori per i valori o aggregazione di valori in blocchi diversi di tempo.  
  
-   Aggiunta di etichette per migliorare l'utilizzabilità dei risultati.  
  
-   Conversione dei tipi di dati o categorizzazione dei valori se necessario per l'analisi.  
  
 Se si ha familiarità con la modellazione dei dati, è consigliabile leggere l'argomento correlato [elenco di controllo di preparazione per il Data Mining](checklist-of-preparation-for-data-mining.md).  
  
## <a name="data-preparation-tools"></a>Strumenti di preparazione dei dati  
 I componenti aggiuntivi Data mining per Office includono i seguenti strumenti per la pulizia e la preparazione dei dati:  
  
### <a name="explore-data"></a>Esplorazione dati  
 Usare la **Esplora dati** procedura guidata per le attività di preparazione dei dati:  
  
-   Visualizzare un'anteprima dei dati per identificare gli errori che devono essere corretti prima dell'analisi.  
  
-   Raccogliere informazioni statistiche utili per comprendere il bilanciamento dei dati e delle attività di pulizia necessarie.  
  
-   Identificare le colonne utili per l'analisi e pianificare la fase di modellazione dei dati.  
  
 [Esplorare i dati &#40;componenti aggiuntivi Data Mining di dati SQL Server&#41;](explore-data-sql-server-data-mining-add-ins.md).  
  
### <a name="detect-and-handle-outliers"></a>Rilevamento e gestione degli outlier  
 Il **Outlier** guidata grafici la distribuzione dei valori nei dati e consente di rimuovere i valori estremi. Usare la **Outlier** dello strumento per le attività di preparazione dei dati seguenti:  
  
-   Determinare se i singoli valori siano affidabili, in base ai modelli individuati nei dati.  
  
-   Esaminare valori anomali ed eseguire le azioni appropriate per eliminarli o sostituirli.  
  
-   Definire l'ambito di un modello in un intervallo di valori specifico. Se, ad esempio, si hanno outlier per un negozio specifico, è possibile eliminare tale valore e ottenere un modello in grado di eseguire una migliore stima degli altri negozi.  
  
 [Outlier &#40;componenti aggiuntivi Data Mining di dati SQL Server&#41;](outliers-sql-server-data-mining-add-ins.md).  
  
### <a name="relabel-and-bin-data"></a>Modifica etichette e categorizzazione dati  
 Il **Rietichettare** guidata Raggruppa i dati per i valori in modo che sia possibile modificare le etichette dei dati. Utilizzare lo strumento Modifica etichette per le attività di preparazione dei dati seguenti:  
  
-   Modificare i codici numerici utilizzati nei risultati di un sondaggio con una descrizione del significato dei codici.  
  
     È ad esempio possibile sostituire Gender = 1 (Genere = 1) con Gender = Female (Genere = Femmina).  
  
-   Suddividere i dati creando gruppi per rappresentare intervalli di numeri.  
  
     Potrebbe ad esempio, si desidera sostituire, ad esempio una colonna Income dei numeri con etichette **reddito - moderato** e **reddito - alto**.  
  
-   Comprimere i valori discreti in categorie.  
  
     Se ad esempio si possiedono troppi prodotti singoli per poter individuare un modello di acquisto, è possibile provare ad assegnare i prodotti a categorie più ampie.  
  
 [Modifica delle etichette &#40;componenti aggiuntivi Data Mining di dati SQL Server&#41;](relabel-sql-server-data-mining-add-ins.md)  
  
### <a name="cleanse-data"></a>Pulizia dei dati  
 La pulizia dei dati include un'ampia gamma di attività, la maggior parte delle quali sono supportate da componenti aggiuntivi  
  
-   Identificare i valori NULL e determinare se devono essere modificati in valori reali o essere gestiti come valori `Missing`.  
  
-   Individuare i valori mancanti, quindi rimuoverli o assegnare loro un valore appropriato come medio, Null o un altro valore.  
  
 [Esplorare i dati &#40;componenti aggiuntivi Data Mining di dati SQL Server&#41;](explore-data-sql-server-data-mining-add-ins.md)  
  
 [Modifica delle etichette &#40;componenti aggiuntivi Data Mining di dati SQL Server&#41;](relabel-sql-server-data-mining-add-ins.md)  
  
 [Estendi da esempio](fill-from-example-table-analysis-tools-for-excel.md)  
  
### <a name="sample-data"></a>Dati di esempio  
 La procedura guidata Dati di esempio consente di creare set di dati equilibrati per il training e il testing dei modelli in due modi.  
  
-   **Campionamento casuale.** Utilizzare questa opzione per estrarre un set di dati rappresentativo da un più ampio set di dati, da utilizzare come training o test. Usano i componenti aggiuntivi Data Mining *campionamento stratificato* per garantire che viene ottenuto un set di valori equilibrato per ciascuna variabile campionata.  
  
-   **Sovracampionamento.** Utilizzare questa opzione quando la quantità di dati a disposizione è inferiore a quella che si vorrebbe per un risultato di destinazione e occorre ponderare i dati con più precisione. Le frodi possono essere relativamente rare, ma è possibile sovracampionare i casi di frode per ottenere dati adeguati per la creazione di un modello.  
  
 [Dati di esempio &#40;componenti aggiuntivi Data Mining di dati SQL Server&#41;](sample-data-sql-server-data-mining-add-ins.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di un modello di Data Mining](creating-a-data-mining-model.md)   
 [Convalida dei modelli e utilizzo dei modelli per la stima &#40;dati di componenti aggiuntivi Data Mining per Excel&#41;](validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel.md)   
 [Distribuzione e scalabilità di modelli di Data Mining &#40;dati di componenti aggiuntivi Data Mining per Excel&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)  
  
  
