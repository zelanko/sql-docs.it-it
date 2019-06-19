---
title: Documentazione di modelli di Data Mining (componenti aggiuntivi Data Mining per Excel i dati) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- documenting models
- mining structures, managing
- mining models, managing
- model properties
ms.assetid: 0a663e11-e40c-4708-ad18-fabb6c976fa4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: afe304e3fa76be805a64e9bd662bc21500ac2fa7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66081585"
---
# <a name="documenting-mining-models-data-mining-add-ins-for-excel"></a>Documentazione di modelli di data mining (componenti aggiuntivi Data mining per Excel)
  ![Pulsante modello di documento, barra multifunzione Data Mining](media/dmc-docmodel.gif "pulsante modello di documento, barra multifunzione Data Mining")  
  
 Il **modello di documento** procedura guidata crea un report che fornisce informazioni utili sui modelli di data mining creati. Documentando i modelli creati, è possibile tenere traccia dell'origine dei dati utilizzati per generare un modello, ottenere ulteriori informazioni relative al momento dell'elaborazione del modello e tenere traccia delle modifiche ai parametri che influiscono sui risultati del modello.  
  
## <a name="using-the-document-model-wizard"></a>Utilizzo della procedura guidata Modello di documento  
  
1.  Scegliere il **Data Mining** scheda.  
  
2.  Nel **modello di utilizzo** gruppo, fare clic su **modello di documento**.  
  
3.  Nel **Seleziona modello** finestra di dialogo, selezionare il modello su cui basare i report e quindi fare clic su **successivo**. È necessario eseguire la **modello di documento** guidata separatamente per ogni modello che si desidera documentare.  
  
4.  Nel **selezione dettagli della documentazione** finestra di dialogo scegliere una delle due opzioni: **Informazioni complete** oppure **informazioni di riepilogo**.  
  
5.  Scegliere **Fine**.  
  
6.  La procedura guidata crea automaticamente un nuovo foglio di lavoro che contiene il report specificato, denominato **documentazione sul modello**,  
  
## <a name="understanding-the-report"></a>Informazioni sul report  
 Quando si crea un report che documenta un modello di data mining, è possibile creare un riepilogo, contenente informazioni di base come il nome e la descrizione del modello, oppure un report completo, contenente i dettagli relativi alla struttura sottostante e informazioni avanzate sul modello di data mining.  
  
 A seconda dell'algoritmo utilizzato per creare il modello, vengono forniti diversi tipi di informazioni. In un modello di associazione, ad esempio, è più interessante conoscere il numero di set di elementi e di regole generati. Per un modello di clustering, è più interessante il numero di cluster.  
  
 Nella tabella seguente sono elencate le opzioni e le informazioni fornite nel report per ogni opzione.  
  
> [!NOTE]  
>  Le colonne del report hanno una dimensione predefinita. Se pertanto i nomi o i valori nelle colonne sono molto lunghi, potrebbero non venire visualizzati o potrebbero venire visualizzati come ### in Excel. Per visualizzare i valori, è possibile ridimensionare la riga. Se la cella è selezionata, è possibile fare clic e trascinare le doppie frecce all'estremità destra della barra della formula per visualizzare la stringa o il valore completo.  
  
### <a name="summary-report"></a>Report di riepilogo  
  
||||  
|-|-|-|  
|**Metadati**|Nome modello<br /><br /> Descrizione modello<br /><br /> Nome algoritmo<br /><br /> Data ultima elaborazione||  
|**Risultati modello**|Association Rules|Numero di set di elementi<br /><br /> Numero di regole|  
||Clustering|Numero di cluster<br /><br /> Supporto per ogni cluster|  
||Albero delle decisioni|Numero di alberi<br /><br /> Numero di nodi in ogni albero|  
||Linear Regression|Numero di alberi (sempre 1)<br /><br /> Numero di nodi (sempre 1)|  
||Naive Bayes|Attributi importanti|  
||Neural Network|Numero di nodi di input<br /><br /> Numero di nodi di output<br /><br /> Numero di nodi nascosti|  
||Sequence Clustering|Numero di cluster|  
  
### <a name="complete-report"></a>Report completo  
 Il report completo contiene tutti gli elementi presenti nel report di riepilogo, più informazioni dettagliate sulle colonne di dati utilizzate nel modello e sui risultati dell'analisi:  
  
||||  
|-|-|-|  
|**Metadati**|Metadati modello|Valori e parametri dell'algoritmo|  
||Metadati colonna|Nome colonna<br /><br /> Uso<br /><br /> Tipo di dati<br /><br /> Tipo di contenuto<br /><br /> Valori (elenco di valori discreti o intervallo di valori)|  
|**Statistiche del modello**|Colonne continue|Valore medio<br /><br /> Valore minimo<br /><br /> Valore massimo<br /><br /> Radice errore quadratico medio<br /><br /> Errore assoluto medio<br /><br /> Punteggio in forma logaritmica<br /><br /> Formula di regressione (solo per i modelli per la regressione lineare)|  
||Colonne discrete|Numero di test superati<br /><br /> Numero di test non superati<br /><br /> Punteggio in forma logaritmica<br /><br /> Accuratezza|  
  
> [!NOTE]  
>  È possibile documentare qualsiasi tipo di modello supportato da SQL Server Analysis Services. Nella tabella sono pertanto inclusi alcuni tipi di modelli che non è possibile creare tramite Strumenti di analisi tabelle o utilizzando le procedure guidate in Client di data mining. Tuttavia, è possibile creare tutti i tipi di modello utilizzando il **Editor avanzato Query Data Mining**. Per altre informazioni, vedere [Query &#40;componenti aggiuntivi Data Mining di SQL Server&#41;](query-sql-server-data-mining-add-ins.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Distribuzione e scalabilità di modelli di Data Mining &#40;dati di componenti aggiuntivi Data Mining per Excel&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)  
  
  
