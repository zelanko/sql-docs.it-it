---
title: Scenari di analisi scientifica dei dati e modelli di soluzioni
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/29/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 313b00ff9c3863e8cd1c3de3b0919fc130b01d1e
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714929"
---
# <a name="data-science-scenarios-and-solution-templates"></a>Scenari di analisi scientifica dei dati e modelli di soluzioni
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

I modelli sono soluzioni di esempio che illustrano le procedure consigliate e possono essere usati per implementare rapidamente una soluzione. Ogni modello è progettato per risolvere un problema specifico, per un settore specifico o verticale. Le attività incluse in ogni modello vanno dalla preparazione dei dati alla progettazione della funzionalità fino al training e alla valutazione del modello. Usare questi modelli per informazioni [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] sul funzionamento di. Quindi, è possibile personalizzare il modello in base al proprio scenario e compilare una soluzione personalizzata. 

Ogni soluzione include dati di esempio, codice R o codice Python e stored procedure SQL, se applicabile. Il codice può essere eseguito nell'ambiente di sviluppo R o Python preferito, con calcoli eseguiti in SQL Server. In alcuni casi, è possibile eseguire il codice direttamente usando T-SQL e qualsiasi strumento client SQL, ad esempio SQL Server Management Studio.

> [!TIP]
> 
> La maggior parte dei modelli è presente in più versioni che supportano le piattaforme locali e cloud per Machine Learning. Ad esempio, è possibile compilare la soluzione usando solo SQL Server oppure è possibile compilare la soluzione in Microsoft R Server o in Azure Machine Learning.

+ Per istruzioni sul download e la configurazione, vedere [come usare i modelli](#bkmk_HowTo).

## <a name="fraud-detection"></a>Rilevamento di frodi

[Modello di rilevamento delle frodi online (R Services per SQL Server)](https://github.com/Microsoft/r-server-fraud-detection)

**Cosa** La possibilità di rilevare transazioni fraudolente è importante per le aziende online. Per ridurre le perdite di costi, le aziende devono identificare rapidamente le transazioni effettuate usando gli strumenti di pagamento o le credenziali rubate. Quando vengono rilevate transazioni illecite, le aziende in genere adottano misure per bloccare immediatamente determinati conti, al fine di evitare ulteriori perdite. In questo scenario si apprenderà come usare i dati delle transazioni di acquisto online per identificare probabili frodi.

**Come**  Il rilevamento di frodi viene risolto come un problema di classificazione binaria. La metodologia usata in questo modello può essere facilmente applicata al rilevamento di frodi in altri domini.


## <a name="campaign-optimization"></a>Ottimizzazione della campagna

[Prevedere come e quando contattare i lead](https://microsoft.github.io/r-server-campaign-optimization/)

**Cosa** Questa soluzione USA i dati del settore assicurativo per stimare i lead in base a dati demografici, dati di risposta cronologici e dettagli specifici del prodotto.  Vengono inoltre generate indicazioni per indicare il canale migliore e il tempo per avvicinare gli utenti a influenzare il comportamento di acquisto.

**Come** La soluzione consente di creare e confrontare più modelli. La soluzione illustra anche l'integrazione e la preparazione dei dati automatizzati tramite stored procedure. Sono disponibili esempi paralleli per SQL Server nel database, in Azure e in HDInsight Spark. 

## <a name="health-care-predict-length-of-stay-in-hospital"></a>Health Care: prevedere la durata della permanenza in ospedale 

[Previsione della durata della degenza negli ospedali](https://gallery.cortanaintelligence.com/Solution/Predicting-Length-of-Stay-in-Hospitals-1)

**Cosa** Una stima accurata dei pazienti che potrebbero richiedere un ricovero a lungo termine è una parte importante della cura e della pianificazione. Gli amministratori devono essere in grado di determinare quali strutture richiedono più risorse e i caregiver vogliono garantire che possano soddisfare le esigenze dei pazienti.

**Come** Questa soluzione USA il Data Science Virtual Machine e include un'istanza di SQL Server con l'apprendimento automatico abilitato. Include anche un set di report di Power BI che è possibile usare per interagire con un modello distribuito.

## <a name="customer-churn"></a>Varianza del cliente

[Modello di stima per varianza dei clienti (R Services per SQL Server)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/Churn/README.md)

**Cosa** L'analisi e la stima della varianza dei clienti sono importanti in tutti i settori in cui è necessario gestire e prevenire la perdita di clienti per i concorrenti: Banking, telecomunicazioni e vendite al dettaglio. L'obiettivo dell'analisi dell'abbandono dei clienti è l'identificazione dei clienti con alta probabilità di abbandono e l'adozione di misure appropriate per mantenere tali clienti e la loro attività.

**Come** Questo modello formula il problema di varianza come problema di **classificazione binaria** . Mediante dati di esempio provenienti da due origini (dati demografici e transazioni dei clienti), il modello indica se la probabilità di abbandono dei singoli clienti è alta o bassa.
  
## <a name="predictive-maintenance"></a>Manutenzione predittiva

[Modello di manutenzione predittiva (SQL Server 2016)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/PredictiveMaintenance/README.md)

**Cosa** La manutenzione predittiva mira ad aumentare l'efficienza delle attività di manutenzione acquisendo gli errori precedenti e usando tali informazioni per prevedere quando o dove un dispositivo potrebbe non riuscire. La possibilità di prevedere l'obsolescenza dei dispositivi è particolarmente utile per le applicazioni che si basano su dati o sensori distribuiti. Questo metodo può essere applicato anche per monitorare o stimare gli errori nei dispositivi Internet (Internet delle cose).

**Come** Questa soluzione è incentrata sulla risposta alla domanda "quando si verificherà un errore in un computer del servizio?" I dati di input rappresentano misurazioni simulate di sensori per motori di aerei. Per creare tre tipi di modelli predittivi, vengono usati i dati ottenuti dal monitoraggio delle condizioni operative correnti del motore, ad esempio il ciclo di lavoro corrente, le impostazioni e le misurazioni del sensore.

-   **Modelli di regressione**per stimare quanto un motore può continuare a funzionare prima di bloccarsi. Il modello di esempio prevede la metrica "vita utile rimanente" (RUL), denominata anche "tempo di errore" (TTF).
  
-   **Modelli di classificazione**per determinare la probabilità che un motore si guasti.
  
    Il **modello di classificazione binaria** stima se un motore non riuscirà entro un determinato intervallo di tempo.

    Il **modello di classificazione multiclasse** stima se un determinato motore potrebbe non riuscire e fornisce un probabile intervallo di tempo di errore. Ad esempio, per un determinato giorno, è possibile prevedere se un dispositivo potrebbe guastarsi in tale giorno o in un determinato periodo di tempo successivo al giorno specificato.

## <a name="energy-demand-forecasting"></a>Previsione della domanda di energia

[Modello di previsione della domanda di energia con R Services per SQL Server](https://gallery.cortanaintelligence.com/Tutorial/Energy-Demand-Forecast-Template-with-SQL-Server-R-Services-1)

**Cosa:** : La previsione della domanda è un problema importante in diversi domini, tra cui l'energia, la vendita al dettaglio e i servizi. Una previsione accurata della domanda consente alle aziende di condurre una pianificazione di produzione migliore, l'allocazione delle risorse e prendere altre importanti decisioni aziendali. Nel settore energetico, la previsione della domanda è fondamentale per ridurre i costi di archiviazione e la richiesta di bilanciamento del carico di energia.

**Come** Questo modello USA R Services per SQL Server per stimare la domanda di energia elettrica. Il modello usato per la stima è un modello di regressione di foresta casuale basato su **rxDForest**, un algoritmo di apprendimento automatico a prestazioni elevate incluso in Microsoft R server. La soluzione include un simulatore di domanda, tutto il codice R e T-SQL necessario per il training del modello e le stored procedure da usare per generare le previsioni e includerle in report. 


## <a name="bkmk_HowTo"></a>Come usare i modelli

Per scaricare i file inclusi in ogni modello è possibile usare i comandi di GitHub oppure aprire il collegamento e fare clic su **Download Zip** (Scarica zip) per salvare tutti i file nel computer.  Dopo che è stata scaricata, la soluzione contiene in genere le seguenti cartelle:
  
-   **Dati**: Contiene i dati di esempio per ogni applicazione.
  
-   **R**: Contiene tutto il codice di sviluppo R necessario per la soluzione. La soluzione richiede le librerie di Microsoft R Server, ma può essere aperta e modificata in qualsiasi IDE R. Il codice R è stato ottimizzato con l'esecuzione dei calcoli all'interno del database, impostando il contesto di calcolo su un'istanza di SQL Server.
  
-   **SQLR**: Contiene più file con estensione SQL che è possibile eseguire in un ambiente SQL, [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ad esempio per creare le stored procedure che eseguono attività correlate, ad esempio l'elaborazione dei dati, la progettazione delle funzionalità e la distribuzione del modello.
  
    La cartella contiene anche uno script di PowerShell che consente di chiamare tutti gli script e di creare l'ambiente end-to-end. Modificare lo script in base alle esigenze dell'ambiente di elaborazione.

## <a name="next-steps"></a>Passaggi successivi

+ [Esercitazioni SQL Server machine learning](machine-learning-services-tutorials.md)




