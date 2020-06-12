---
title: Documentazione di modelli di data mining (componenti aggiuntivi Data mining per Excel) | Microsoft Docs
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
ms.openlocfilehash: 92ed5c43fa2b7484485b915d42946121487386d9
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84528487"
---
# <a name="documenting-mining-models-data-mining-add-ins-for-excel"></a>Documentazione di modelli di data mining (componenti aggiuntivi Data mining per Excel)
  ![Pulsante Modello di documento, barra multifunzione Data mining](media/dmc-docmodel.gif "Pulsante Modello di documento, barra multifunzione Data mining")  
  
 La procedura guidata **modello di documento** consente di creare un report che fornisce informazioni utili sui modelli di data mining creati. Documentando i modelli creati, è possibile tenere traccia dell'origine dei dati utilizzati per generare un modello, ottenere ulteriori informazioni relative al momento dell'elaborazione del modello e tenere traccia delle modifiche ai parametri che influiscono sui risultati del modello.  
  
## <a name="using-the-document-model-wizard"></a>Utilizzo della procedura guidata Modello di documento  
  
1.  Fare clic sulla scheda **data mining** .  
  
2.  Nel gruppo **utilizzo modelli** fare clic su **modello di documento**.  
  
3.  Nella finestra di dialogo **Seleziona modello** selezionare il modello in cui eseguire il report, quindi fare clic su **Avanti**. È necessario eseguire la procedura guidata **modello di documento** separatamente per ogni modello che si desidera documentare.  
  
4.  Nella finestra di dialogo **Selezione dettagli della documentazione** scegliere una delle due opzioni seguenti: **informazioni complete** o **informazioni di riepilogo**.  
  
5.  Fare clic su **Fine**.  
  
6.  La procedura guidata crea automaticamente un nuovo foglio di foglio contenente il report specificato, denominato **documentazione del modello**,  
  
## <a name="understanding-the-report"></a>Informazioni sul report  
 Quando si crea un report che documenta un modello di data mining, è possibile creare un riepilogo, contenente informazioni di base come il nome e la descrizione del modello, oppure un report completo, contenente i dettagli relativi alla struttura sottostante e informazioni avanzate sul modello di data mining.  
  
 A seconda dell'algoritmo utilizzato per creare il modello, vengono forniti diversi tipi di informazioni. In un modello di associazione, ad esempio, è più interessante conoscere il numero di set di elementi e di regole generati. Per un modello di clustering, è più interessante il numero di cluster.  
  
 Nella tabella seguente sono elencate le opzioni e le informazioni fornite nel report per ogni opzione.  
  
> [!NOTE]  
>  Le colonne del report hanno una dimensione predefinita. Se pertanto i nomi o i valori nelle colonne sono molto lunghi, potrebbero non venire visualizzati o potrebbero venire visualizzati come ### in Excel. Per visualizzare i valori, è possibile ridimensionare la riga. Se la cella è selezionata, è possibile fare clic e trascinare le doppie frecce all'estremità destra della barra della formula per visualizzare la stringa o il valore completo.  
  
### <a name="summary-report"></a>Report di riepilogo  
  
||||  
|-|-|-|  
|**Metadati**|Nome modello<br /><br /> Descrizione del modello<br /><br /> Nome algoritmo<br /><br /> Data ultima elaborazione||  
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
||Metadati colonna|Nome colonna<br /><br /> Utilizzo<br /><br /> Tipo di dati<br /><br /> Tipo di contenuto<br /><br /> Valori (elenco di valori discreti o intervallo di valori)|  
|**Statistiche modello**|Colonne continue|Valore medio<br /><br /> Valore minimo<br /><br /> Valore massimo<br /><br /> Radice errore quadratico medio<br /><br /> Errore assoluto medio<br /><br /> Punteggio in forma logaritmica<br /><br /> Formula di regressione (solo per i modelli per la regressione lineare)|  
||Colonne discrete|Numero di test superati<br /><br /> Numero di test non superati<br /><br /> Punteggio in forma logaritmica<br /><br /> Accuratezza|  
  
> [!NOTE]  
>  È possibile documentare qualsiasi tipo di modello supportato da SQL Server Analysis Services. Nella tabella sono pertanto inclusi alcuni tipi di modelli che non è possibile creare tramite Strumenti di analisi tabelle o utilizzando le procedure guidate in Client di data mining. Tuttavia, è possibile creare tutti i tipi di modello utilizzando l' **Editor avanzato query di data mining**. Per ulteriori informazioni, vedere [Query &#40;SQL Server componenti aggiuntivi Data Mining&#41;](query-sql-server-data-mining-add-ins.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Distribuzione e scalabilità di modelli di data mining &#40;componenti aggiuntivi Data mining per Excel&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)  
  
  
