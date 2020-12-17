---
title: Modelli di soluzioni di data science
description: Questo articolo descrive i modelli specifici del settore che illustrano le procedure consigliate e rendono disponibili gli elementi fondamentali per agevolare l'implementazione di una soluzione di Machine Learning.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 03/29/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15'
ms.openlocfilehash: e7d7b36c2c19d48fec393e38c741244f6713dcd3
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97470632"
---
# <a name="data-science-scenarios-and-solution-templates"></a>Scenari di data science e modelli di soluzioni
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

Questo articolo descrive una serie di modelli di soluzioni di Machine Learning di SQL Server. Questi modelli illustrano le procedure consigliate e rendono disponibili gli elementi fondamentali che consentono di implementare rapidamente una soluzione di Machine Learning. Ogni modello è progettato per risolvere un determinato problema di data science, per un settore specifico o verticale.
Le attività incluse in ogni modello vanno dalla preparazione dei dati alla progettazione della funzionalità fino al training e alla valutazione del modello. 

::: moniker range="=sql-server-2016"
Usare questi modelli per informazioni sul funzionamento di [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. I modelli possono essere personalizzati in base allo scenario in uso per creare una soluzione personalizzata.
::: moniker-end

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15"
Usare questi modelli per informazioni sul funzionamento di Machine Learning Services per SQL Server. I modelli possono essere personalizzati in base allo scenario in uso per creare una soluzione personalizzata.
::: moniker-end

Ogni soluzione include dati di esempio, codice R o codice Python e stored procedure SQL, se applicabili. Il codice può essere eseguito nell'ambiente di sviluppo R o Python preferito, con calcoli eseguiti in SQL Server. In alcuni casi è possibile eseguire il codice direttamente usando T-SQL e uno strumento client SQL qualsiasi, come SQL Server Management Studio.

> [!TIP]
> 
> La maggior parte dei modelli è disponibile in più versioni che supportano le piattaforme locali e cloud per Machine Learning. Ad esempio, è possibile compilare la soluzione usando solo SQL Server oppure è possibile compilarla in Microsoft R Server o in Azure Machine Learning.

+ Per istruzioni sul download e la configurazione, vedere [Come usare i modelli](#bkmk_HowTo).

## <a name="fraud-detection"></a>Rilevamento delle frodi

[Modello per il rilevamento di frodi online (R Services per SQL Server)](https://github.com/Microsoft/r-server-fraud-detection)

**Informazioni approfondite:** Per le aziende online è importante essere in grado di rilevare le transazioni illecite. Per ridurre le perdite correlate ai rimborsi, le aziende devono identificare rapidamente le transazioni effettuate usando strumenti di pagamento o credenziali rubate. Quando vengono rilevate transazioni illecite, le aziende in genere adottano misure per bloccare immediatamente determinati conti, al fine di evitare ulteriori perdite. In questo scenario verrà illustrato come usare dati di transazioni di acquisto online per identificare probabili frodi.

**Modalità:**  Il rilevamento di frodi viene risolto come un problema di classificazione binaria. La metodologia usata in questo modello può essere facilmente applicata al rilevamento di frodi in altri domini.


## <a name="campaign-optimization"></a>Ottimizzazione della campagna

[Stimare come e quando contattare i clienti potenziali](https://microsoft.github.io/r-server-campaign-optimization/)

**Informazioni approfondite:** Questa soluzione usa i dati del settore assicurativo per stimare i clienti potenziali in base a dati demografici, dati di risposta cronologici e dettagli specifici dei prodotti.  Vengono inoltre generate raccomandazioni per indicare il canale e il momento più appropriati per contattare gli utenti in modo da influenzarne il comportamento di acquisto.

**Modalità:** La soluzione consente di creare e confrontare più modelli. Illustra anche l'integrazione e la preparazione automatizzate dei dati tramite stored procedure. Sono disponibili esempi paralleli per SQL Server nel database, in Azure e in HDInsight Spark. 

## <a name="health-care-predict-length-of-stay-in-hospital"></a>Settore sanitario: stimare la durata della degenza in ospedale 

[Stima della durata della degenza negli ospedali](https://gallery.cortanaintelligence.com/Solution/Predicting-Length-of-Stay-in-Hospitals-1)

**Informazioni approfondite:** Una stima accurata dei pazienti che potrebbero richiedere un ricovero a lungo termine è una parte importante dell'assistenza e della pianificazione. Gli amministratori devono essere in grado di determinare quali strutture richiedono più risorse e il personale infermieristico vuole essere certo di poter soddisfare le esigenze dei pazienti.

**Modalità:** Questa soluzione usa Data Science Virtual Machine e include un'istanza di SQL Server con le funzioni di Machine Learning abilitate. Include anche un set di report di Power BI che è possibile usare per interagire con un modello distribuito.

## <a name="customer-churn"></a>Abbandono dei clienti

[Modello per la stima dell'abbandono dei clienti (R Services per SQL Server)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/Churn/README.md)

**Informazioni approfondite:** L'analisi e la stima dell'abbandono dei clienti sono importanti per i settori in cui la perdita di clienti a favore della concorrenza va gestita e impedita per quanto possibile, ad esempio nei settori bancario, delle telecomunicazioni e della vendita al dettaglio. L'obiettivo dell'analisi dell'abbandono dei clienti è l'identificazione dei clienti con alta probabilità di abbandono e l'adozione di misure appropriate per mantenere tali clienti e la loro attività.

**Modalità:** Questo modello formula il problema dell'abbandono come problema di **classificazione binaria**. Mediante dati di esempio provenienti da due origini (dati demografici e transazioni dei clienti), il modello indica se la probabilità di abbandono dei singoli clienti è alta o bassa.
  
## <a name="predictive-maintenance"></a>Manutenzione predittiva

[Modello di manutenzione predittiva (SQL Server 2016)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/PredictiveMaintenance/README.md)

**Informazioni approfondite:** La manutenzione predittiva ha lo scopo di aumentare l'efficienza delle attività di manutenzione registrando i guasti precedenti e usando le informazioni per prevedere quando o dove un determinato dispositivo potrebbe far registrare un guasto. La possibilità di prevedere l'obsolescenza dei dispositivi è particolarmente utile per le applicazioni che si basano su sensori o dati distribuiti. Questo metodo può essere applicato anche per monitorare o stimare gli errori nei dispositivi IoT (Internet delle cose).

**Modalità:** Questa soluzione è incentrata sulla risposta alla domanda "Quando si guasterà un dispositivo attualmente funzionante?" I dati di input rappresentano misurazioni simulate di sensori per motori di aerei. I dati ottenuti dal monitoraggio delle condizioni di funzionamento correnti del motore, quali ciclo di lavoro corrente, impostazioni e misurazioni dei sensori, vengono usati per creare tre tipi di modelli predittivi:

-   **Modelli di regressione** per stimare quanto un motore può continuare a funzionare prima di bloccarsi. Il modello di esempio consente di stimare la metrica "Vita utile rimanente", detta anche "Tempo fra i guasti".
  
-   **Modelli di classificazione** per determinare la probabilità che un motore si guasti.
  
    Il **modello di classificazione binario** stima se un motore si guasterà entro un determinato periodo di tempo.

    Il **modello di classificazione a più classi** stima se un determinato motore possa guastarsi e indica un intervallo di tempo probabile nel quale si verificherà il guasto. Ad esempio, per un determinato giorno, è possibile prevedere se un dispositivo potrebbe guastarsi in tale giorno o in un determinato periodo di tempo successivo al giorno specificato.

## <a name="energy-demand-forecasting"></a>Previsione della domanda elettrica

[Modello per la previsione della domanda elettrica con R Services per SQL Server](https://gallery.cortanaintelligence.com/Tutorial/Energy-Demand-Forecast-Template-with-SQL-Server-R-Services-1)

**Informazioni approfondite:** La previsione della domanda è un problema importante in diversi settori, tra cui energia, vendita al dettaglio e servizi. Una previsione accurata della domanda consente alle aziende di condurre una migliore pianificazione della produzione e allocazione delle risorse, nonché di prendere altre importanti decisioni aziendali. Nel settore energetico la previsione della domanda è fondamentale per ridurre i costi di stoccaggio dell'energia e il bilanciamento della domanda e dell'offerta.

**Modalità:** Questo modello usa R Services per SQL Server per stimare la domanda di energia elettrica. Il modello usato per la stima è un modello di regressione di foreste casuale basato su **rxDForest**, un algoritmo di Machine Learning ad alte prestazioni incluso in Microsoft R Server. La soluzione include un simulatore di domanda, tutto il codice R e T-SQL necessario per il training del modello e le stored procedure da usare per generare le previsioni e includerle in report. 


## <a name="how-to-use-the-templates"></a><a name="bkmk_HowTo"></a>Come usare i modelli

Per scaricare i file inclusi in ogni modello è possibile usare i comandi di GitHub oppure aprire il collegamento e fare clic su **Download Zip** (Scarica zip) per salvare tutti i file nel computer.  Dopo che è stata scaricata, la soluzione contiene in genere le seguenti cartelle:
  
-   **Data**: contiene i dati di esempio per ogni applicazione.
  
-   **R**: contiene tutto il codice di sviluppo R necessario per la soluzione. La soluzione richiede le librerie di Microsoft R Server, ma può essere aperta e modificata in qualsiasi IDE R. Il codice R è stato ottimizzato con l'esecuzione dei calcoli all'interno del database, impostando il contesto di calcolo su un'istanza di SQL Server.
  
-   **SQLR**: contiene più file con estensione sql eseguibili in un ambiente SQL quale [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per creare le stored procedure che eseguono attività correlate quali l'elaborazione dei dati, la progettazione delle caratteristiche e la distribuzione del modello.
  
    La cartella contiene anche uno script di PowerShell che consente di chiamare tutti gli script e di creare l'ambiente end-to-end. Modificare lo script in base alle esigenze dell'ambiente di elaborazione.

## <a name="next-steps"></a>Passaggi successivi

+ [Esercitazioni di Python](./python-tutorials.md)
+ [Esercitazioni di R](./r-tutorials.md)