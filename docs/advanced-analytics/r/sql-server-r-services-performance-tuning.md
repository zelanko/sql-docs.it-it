---
title: SQL Server R Services Performance Tuning - SQL Server Machine Learning Services
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: e547e2cd3c50e020d1164dc2b8aaffb31f4e3cb8
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58510108"
---
# <a name="performance-tuning-for-r-in-sql-server"></a>Ottimizzazione delle prestazioni per R in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo è il primo di una serie di quattro articoli che descrivono l'ottimizzazione delle prestazioni per R Services, basato su due case study:

- Test delle prestazioni eseguiti dal team di sviluppo del prodotto per convalidare il profilo delle prestazioni delle soluzioni R

- Ottimizzazione delle prestazioni dal team di analisi scientifica dei dati di Microsoft per uno scenario di apprendimento automatico specifica spesso richiesto dai clienti.

L'obiettivo di questa serie è fornire indicazioni sui tipi di tecniche che risultano più utili per eseguire processi R in SQL Server l'ottimizzazione delle prestazioni.

+ In questo argomento (primo) fornisce una panoramica dell'architettura e alcuni problemi comuni durante l'ottimizzazione per attività di analisi scientifica dei dati.
+ Nel secondo articolo illustra i componenti hardware specifici e le ottimizzazioni di SQL Server.
+ Il terzo articolo descrive le ottimizzazioni di codice R e le risorse per l'operazionalizzazione.
+ Il quarto articolo descrive in dettaglio e risultati di report e le conclusioni i metodi di test.

**Si applica a:** SQL Server 2016 R Services, SQL Server 2017 Machine Learning Services

## <a name="performance-goals-and-targeted-scenarios"></a>Obiettivi di prestazioni e scenari di destinazione

La funzionalità R Services è stato introdotto in SQL Server 2016 per supportare l'esecuzione di script R da SQL Server. Quando si usa questa funzionalità, il runtime di R viene eseguito in un processo separato dal motore di database, ma consente di scambiare i dati in modo sicuro con il motore di database, usando le risorse del server e servizi che interagiscono con SQL Server, ad esempio il servizio Trusted Launchpad.

In SQL Server 2017 è stato annunciato il supporto per l'esecuzione di script di Python con la stessa architettura, lingua aggiuntiva da seguire in futuro.

Man mano che aumenta il numero delle versioni supportate e lingua, è importante che l'amministratore del database e progettista database siano consapevoli del potenziale conflitto di risorse a causa dei processi di machine learning, e che siano in grado di configurare il server per supportare i nuovi carichi di lavoro. Anche se mantenere analitica vicino ai dati consente di eliminare gli spostamenti dei dati non protetti, anche spostamento di carichi di lavoro analitici disattivato sul computer portatile del data scientist e nuovamente in server che ospita i dati.

Ottimizzazione delle prestazioni per machine learning non è chiaramente una proposta di una soluzione universale. Le seguenti attività comuni potrebbero avere profili di prestazioni molto diversi:

- Attività di formazione: creazione e training di un modello di regressione rispetto al training di una rete neurale
- Progettazione di funzionalità con R e l'estrazione di funzioni mediante T-SQL
- Assegnazione dei punteggi in singole righe o batch di piccole dimensioni, e operazioni bulk tramite input in formato tabulare di punteggio
- Esecuzione di assegnazione dei punteggi in R e distribuzione dei modelli nell'ambiente di produzione in SQL Server nelle stored procedure
- La modifica del codice R per ridurre al minimo il trasferimento dei dati o rimuovere le trasformazioni di dati costosa
- Abilitare test automatizzati e ripetizione del training dei modelli

Poiché la scelta di tecniche di ottimizzazione dipende da quale attività è fondamentale per l'applicazione o un caso d'uso, i case study illustra suggerimenti sulle prestazioni generali e indicazioni su come ottimizzare per uno scenario specifico, ottimizzazione per il punteggio batch.

+ **Opzioni di ottimizzazione singoli in SQL Server**

    Nel primo case study sulle prestazioni, più test eseguiti su un singolo set di dati usando un singolo tipo di modello. È stato utilizzato l'algoritmo rxLinMod in RevoscaleR per compilare un modello e creare punteggi da esso, ma il codice, nonché le tabelle di dati sottostanti sono state modificate in modo sistematico per testare l'impatto di ogni modifica.

    In un'esecuzione dei test, ad esempio, il codice R è stato alterato in modo che è stato eseguito un confronto tra la progettazione di funzionalità con una funzione di trasformazione e le funzionalità di pre-elaborazione e quindi caricare funzionalità da una tabella. In un'altra esecuzione dei test, le prestazioni di training del modello è stata confrontata tra l'uso di una tabella con indicizzazione standard VS. dati di una tabella applicando diversi tipi di compressione o nuovi tipi di indice.

+ **Ottimizzazione per uno specifico scenario di assegnazione dei punteggi con volumi elevati**

    L'attività di machine learning nel secondo caso di Studio prevede l'elaborazione riprende molti inviati per più posizioni e trovare il miglior candidato per ogni posizione lavorativa. Il modello di machine learning stesso viene formulato come un problema di classificazione binaria: accetta una descrizione resume e processo come input e genera la probabilità per ogni coppia resume-job. Poiché l'obiettivo consiste nel trovare la migliore corrispondenza, una soglia di probabilità definita dall'utente viene utilizzata per filtrare ulteriormente e ottenere solo le corrispondenze valida.

    Per questa soluzione, l'obiettivo principale consisteva nel raggiungere la bassa latenza durante l'assegnazione dei punteggi. Tuttavia, questa attività è un'operazione costosa anche durante il processo di assegnazione dei punteggi, perché ogni nuovo processo deve essere confrontato con milioni di riattivazioni all'interno di un intervallo di tempo ragionevole. Inoltre, il passaggio di progettazione di funzioni produce funzionalità oltre 2000 per ogni processo o ripresa e costituisce un collo di bottiglia significativo delle prestazioni.

Si consiglia di esaminare tutti i risultati dal primo case study per determinare quali tecniche sono applicabili alla soluzione e valutare l'impatto potenziale.

Quindi, esaminare i risultati dell'assegnazione dei punteggi ottimizzazione case study per informazioni su come l'autore applicate diverse tecniche e ottimizzato il server per supportare un carico di lavoro specifico.

## <a name="performance-optimization-process"></a>Processo di ottimizzazione delle prestazioni

Configurazione e ottimizzazione delle prestazioni richiede la creazione di una solida base, in cui a ottimizzazioni del livello progettate per carichi di lavoro specifici:

- Scegliere un server appropriato per l'analitica host. In genere, un report secondario, data warehouse o altri server che è già usato per altri report o in analitica è preferito. Tuttavia, in una soluzione ibrida transazionale analytical processing (HTAP), elaborazione, sui dati operativi sono utilizzabile come input a R per il punteggio veloce.

- Configurare l'istanza di SQL Server per bilanciare le operazioni del motore di database e R o Python di esecuzione ai livelli appropriati di script. Può trattarsi di modifica delle impostazioni predefinite di SQL Server per la memoria e utilizzo della CPU, NUMA e le impostazioni affinità processori e la creazione di gruppi di risorse.

- Ottimizzare il computer del server per supportare l'utilizzo efficiente di script esterni. Ciò può includere l'aumento del numero di account usato per l'esecuzione di script esterni, abilitare la gestione del pacchetto, e assegnare gli utenti ai relativi ruoli di sicurezza.

- Applicare le ottimizzazioni specifiche per l'archiviazione dei dati e il trasferimento in SQL Server, tra cui l'indicizzazione e le strategie di statistiche, Progettazione query e l'ottimizzazione delle query e la progettazione di tabelle che vengono usate per machine learning. È anche possibile analizzare le origini dati e metodi di trasporto dei dati o modificare i processi ETL per ottimizzare l'estrazione di funzioni.

- Ottimizzare il modello analitico per evitare le inefficienze. L'ambito delle ottimizzazioni possibili variano a seconda della complessità del codice R e i pacchetti e i dati in uso. Attività principali includono eliminando le trasformazioni dei dati costose o il trasferimento di dati pianificazione o alcuna funzionalità le attività di progettazione da R o Python per SQL o i processi ETL. È anche potrebbe effettuare il refactoring di script, eliminare le installazioni del pacchetto in linea, dividere il codice R necessario seguire procedure separate per il training, assegnazione dei punteggi e valutazione o semplificare il codice per lavorare in modo più efficiente come una stored procedure.

## <a name="articles-in-this-series"></a>Articoli di questa serie

+ [Ottimizzazione delle prestazioni per R in SQL Server - hardware](../r/sql-server-configuration-r-services.md)

    Vengono fornite informazioni aggiuntive sulla configurazione dell'hardware che [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] viene installato e per la configurazione dell'istanza di SQL Server per supportare al meglio gli script esterni. È particolarmente utile per **gli amministratori del database**.

+ [Ottimizzazione delle prestazioni per R in SQL Server - codice e dati di ottimizzazione](../r/r-and-data-optimization-r-services.md)

    Vengono forniti suggerimenti specifici su come ottimizzare script esterno per evitare problemi noti. È più utile **ai data Scientist**.

    > [!NOTE]
    > Mentre molte delle informazioni in questa sezione si applica a R in generale, alcune informazioni sono specifiche per le funzioni analitiche RevoScaleR. Non sono disponibile per indicazioni dettagliate sulle prestazioni **revoscalepy** e altre librerie di Python è supportato.
    >

+ [Ottimizzazione delle prestazioni per R in SQL Server - metodi e i risultati](../r/performance-case-study-r-services.md)

    Riepiloga quali dati sono stati usati i due casi di Studio, come è stata testata sulle prestazioni e risultati di influenza le ottimizzazioni.
