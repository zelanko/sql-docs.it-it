---
title: Scenari di data science e modelli di soluzione - SQL Server Machine Learning
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: c40d5d60d43739ccfa6fa326ba0ca1c2688543a6
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58509848"
---
# <a name="data-science-scenarios-and-solution-templates"></a>Scenari di data science e modelli di soluzioni
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

I modelli sono soluzioni di esempio che illustrano le procedure consigliate e possono essere usati per implementare rapidamente una soluzione. Ogni modello è progettato per risolvere un problema specifico, per una specifica verticale o del settore. Le attività incluse in ogni modello vanno dalla preparazione dei dati alla progettazione della funzionalità fino al training e alla valutazione del modello. Usare questi modelli per informazioni su come [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] funziona. Quindi, è possibile personalizzare il modello per adattarsi allo scenario specifico e creare una soluzione personalizzata. 

Ogni soluzione include i dati di esempio, codice R o Python code e le stored procedure SQL se applicabile. Il codice può essere eseguito in preferito R o Python nell'ambiente di sviluppo con calcoli in SQL Server. In alcuni casi, è possibile eseguire codice direttamente usando T-SQL e qualsiasi strumento client SQL, ad esempio SQL Server Management Studio.

> [!TIP]
> 
> La maggior parte dei modelli sono disponibili in più versioni che supportano sia in locale e cloud piattaforme per machine learning. Ad esempio, è possibile compilare la soluzione Usa solo SQL Server, oppure è possibile compilare la soluzione in Microsoft R Server o in Azure Machine Learning.

+ Per informazioni dettagliate e gli aggiornamenti, vedere questo annuncio: [Interessanti nuovi modelli in Azure Machine Learning](https://blogs.technet.microsoft.com/machinelearning/2015/04/09/exciting-new-templates-in-azure-ml/)

+ Per scaricare e le istruzioni di installazione, vedere [come usare i modelli](#bkmk_HowTo).

## <a name="fraud-detection"></a>Rilevamento di frodi

[Modello di rilevamento di frodi online (SQL Server R Services)](https://github.com/Microsoft/r-server-fraud-detection)

**Cosa:** È importante per le aziende online consente di rilevare le transazioni illecite. Per ridurre le perdite di tariffazione, le aziende devono identificare rapidamente le transazioni effettuate utilizzando strumenti di pagamento rubate o le credenziali. Quando vengono rilevate transazioni illecite, le aziende in genere adottano misure per bloccare immediatamente determinati conti, al fine di evitare ulteriori perdite. In questo scenario descrive come usare i dati da transazioni di acquisto online per identificare probabili frodi.

**Procedura:**  Il rilevamento di frodi viene risolto come un problema di classificazione binaria. La metodologia usata in questo modello può essere facilmente applicata al rilevamento di frodi in altri domini.


## <a name="campaign-optimization"></a>Ottimizzazione della campagna

[Prevedere come e quando contattare i lead](https://microsoft.github.io/r-server-campaign-optimization/)

**Cosa:** Questa soluzione Usa dati di settore assicurativo per prevedere i clienti potenziali in base ai dati demografici, dati di risposta cronologico e dettagli specifici del prodotto.  Le raccomandazioni vengono generate anche per indicare il canale e l'ora agli utenti di approccio per influenzare il comportamento di acquisto migliore.

**Procedura:** La soluzione crea e confronta più modelli. Questa soluzione illustra anche l'integrazione dei dati automatizzata e preparazione dei dati di utilizzo delle stored procedure. Vengono forniti esempi parallela per in-database di SQL Server in Azure e HDInsight Spark. 

## <a name="health-care-predict-length-of-stay-in-hospital"></a>Health care: Prevedi la durata della degenza negli ospedali 

[Previsione della durata della degenza negli ospedali](https://gallery.cortanaintelligence.com/Solution/Predicting-Length-of-Stay-in-Hospitals-1)

**Cosa:** Prevedere con precisione quali patients potrebbero richiedere ospedaliero a lungo termine è una parte importante di attenzione e pianificazione. Gli amministratori devono essere in grado di determinare quali strutture richiedono più risorse e agli operatori del settore desidera garantire che soddisfino le esigenze dei pazienti.

**Procedura:** Questa soluzione Usa la macchina virtuale di Data Science e include un'istanza di SQL Server con machine learning abilitata. Contiene inoltre un set di report di Power BI che è possibile usare per interagire con un modello distribuito.

## <a name="customer-churn"></a>Varianza dei clienti

[Modello di stima della varianza del cliente (SQL Server R Services)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/Churn/README.md)

**Cosa:** L'analisi e stima abbandono dei clienti è importante per ogni settore in cui deve essere gestita e ha impedita la perdita di clienti di superare la concorrenza: banking, le telecomunicazioni e delle vendite al dettaglio, per citarne alcuni. L'obiettivo dell'analisi dell'abbandono dei clienti è l'identificazione dei clienti con alta probabilità di abbandono e l'adozione di misure appropriate per mantenere tali clienti e la loro attività.

**Procedura:** Questo modello formula il problema come un **classificazione binaria** problema. Mediante dati di esempio provenienti da due origini (dati demografici e transazioni dei clienti), il modello indica se la probabilità di abbandono dei singoli clienti è alta o bassa.
  
## <a name="predictive-maintenance"></a>Manutenzione predittiva

[Modello di manutenzione predittiva (SQL Server 2016)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/PredictiveMaintenance/README.md)

**Cosa:** Manutenzione predittiva è possibile aumentare l'efficienza delle attività di manutenzione attraverso l'acquisizione dopo gli errori e utilizzo di tali informazioni per prevedere quando o dove un dispositivo potrebbe non riuscire. La possibilità di prevedere l'obsolescenza dei dispositivi è particolarmente utile per le applicazioni basate su dati distribuiti o sensori. è anche possibile applicare questo metodo per monitorare o stimare errori nei dispositivi IoT (Internet of Things).

Vedere questo annuncio per altre informazioni: [Nuovo modello di manutenzione predittiva](https://blogs.technet.microsoft.com/machinelearning/2015/04/09/exciting-new-templates-in-azure-ml/)

**Procedura:** Questa soluzione è incentrata sulla risposta alla domanda, "Quando verrà guasterà un?" I dati di input rappresentano misurazioni simulate di sensori per motori di aerei. I dati ottenuti dal monitoraggio operazione condizioni correnti del motore, ad esempio il ciclo di lavoro corrente, impostazioni e le misurazioni del sensore, vengono usati per creare tre tipi di modelli predittivi:

-   **Modelli di regressione**per stimare quanto un motore può continuare a funzionare prima di bloccarsi. Il modello di esempio prevede la metrica "Vita utile rimanente" (RUL), l'acronimo di "Ora to Failure" (TTF).
  
-   **Modelli di classificazione**per determinare la probabilità che un motore si guasti.
  
    Il **modello di classificazione binaria** consente di stimare se un motore si guasterà entro un determinato periodo di tempo.

    Il **modello di classificazione multiclasse** consente di stimare se un determinato motore potrebbe non riuscire e fornisce un intervallo di tempo probabile dell'errore. Ad esempio, per un determinato giorno, è possibile prevedere se un dispositivo potrebbe guastarsi in tale giorno o in un determinato periodo di tempo successivo al giorno specificato.

## <a name="energy-demand-forecasting"></a>Previsione della domanda di energia

[Modello con SQL Server R Services la previsione della domanda di energia](https://gallery.cortanaintelligence.com/Tutorial/Energy-Demand-Forecast-Template-with-SQL-Server-R-Services-1)

**Cosa:**: Previsione della domanda è un problema importante in domini diversi tra cui energia delle vendite al dettaglio e servizi. Previsione della domanda accurata aiuta le aziende condurre produzione migliore pianificazione, l'allocazione delle risorse e prendere altre decisioni aziendali più importanti. Nel settore dell'energia, è fondamentale per ridurre il costo di archiviazione di energia e bilanciamento di domanda e la previsione della domanda.

**Procedura:** Questo modello Usa SQL Server R Services per stimare la domanda di energia elettrica. Il modello utilizzato per la stima è basato su un modello di regressione foresta casuale **rxDForest**, un'ad alte prestazioni algoritmo di machine learning inclusa in Microsoft R Server. La soluzione include un simulatore di domanda, tutto il codice R e T-SQL necessario per il training del modello e le stored procedure da usare per generare le previsioni e includerle in report. 


## <a name="bkmk_HowTo"></a>Come usare i modelli

Per scaricare i file inclusi in ogni modello è possibile usare i comandi di GitHub oppure aprire il collegamento e fare clic su **Download Zip** (Scarica zip) per salvare tutti i file nel computer.  Dopo che è stata scaricata, la soluzione contiene in genere le seguenti cartelle:
  
-   **Dati**: Contiene i dati di esempio per ogni applicazione.
  
-   **R**: Contiene tutto il codice di sviluppo R che è necessario per la soluzione. La soluzione richiede le librerie di Microsoft R Server, ma può essere aperta e modificata in qualsiasi IDE R. Il codice R è stato ottimizzato con l'esecuzione dei calcoli all'interno del database, impostando il contesto di calcolo su un'istanza di SQL Server.
  
-   **SQLR**: Contiene più file con estensione SQL che è possibile eseguire, ad esempio in un ambiente SQL [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per creare le stored procedure che eseguono attività correlate quali l'elaborazione dei dati, progettare funzionalità e distribuzione del modello.
  
    La cartella contiene anche uno script di PowerShell che consente di chiamare tutti gli script e di creare l'ambiente end-to-end. Modificare lo script in base alle esigenze dell'ambiente di elaborazione.

## <a name="next-steps"></a>Passaggi successivi

+ [Esercitazioni di SQL Server machine learning](machine-learning-services-tutorials.md)




