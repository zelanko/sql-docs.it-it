---
title: Ottimizzazione delle prestazioni di SQL Server R Services
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 9d6dbc55281a725dea0373f2a4d61293b2ddb9c0
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469938"
---
# <a name="performance-tuning-for-r-in-sql-server"></a>Ottimizzazione delle prestazioni per R in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questo articolo è il primo di una serie di quattro articoli che descrivono l'ottimizzazione delle prestazioni per R Services, in base a due case study:

- Test delle prestazioni eseguiti dal team di sviluppo del prodotto per convalidare il profilo delle prestazioni delle soluzioni R

- Ottimizzazione delle prestazioni da parte del team di Microsoft data science per uno scenario di apprendimento automatico specifico spesso richiesto dai clienti.

L'obiettivo di questa serie è fornire indicazioni sui tipi di tecniche di ottimizzazione delle prestazioni più utili per l'esecuzione di processi R in SQL Server.

+ Questo argomento (primo) fornisce una panoramica dell'architettura e alcuni problemi comuni durante l'ottimizzazione per le attività data science.
+ Nel secondo articolo vengono illustrate le ottimizzazioni specifiche per hardware e SQL Server.
+ Il terzo articolo illustra le ottimizzazioni nel codice R e le risorse per la messa in funzione.
+ Il quarto articolo descrive in dettaglio i metodi di test e segnala i risultati e le conclusioni.

**Si applica a:** SQL Server 2016 R Services, SQL Server 2017 Machine Learning Services

## <a name="performance-goals-and-targeted-scenarios"></a>Obiettivi di prestazioni e scenari mirati

La funzionalità R Services è stata introdotta in SQL Server 2016 per supportare l'esecuzione di script R da SQL Server. Quando si usa questa funzionalità, il runtime di R opera in un processo separato dal motore di database, ma scambia i dati in modo sicuro con il motore di database, usando le risorse del server e i servizi che interagiscono con SQL Server, ad esempio la finestra di avvio attendibile.

In SQL Server 2017 è stato annunciato il supporto per l'esecuzione di script Python con la stessa architettura, con un linguaggio aggiuntivo da seguire in futuro.

Con l'aumentare del numero di versioni e linguaggi supportati, è importante che l'amministratore del database e l'architetto del database siano consapevoli del rischio di conflitti di risorse dovuti ai processi di machine learning e che siano in grado di configurare il server per supportare nuovi carichi di lavoro. Sebbene la funzionalità di analisi vicina ai dati elimini gli spostamenti dei dati non sicuri, sposta anche i carichi di lavoro analitici dal computer portatile del data scientist e viceversa nel server che ospita i dati.

L'ottimizzazione delle prestazioni per Machine Learning non è ovviamente una proposta di dimensioni adatte per tutti. Le attività comuni seguenti potrebbero avere profili di prestazioni molto diversi:

- Attività di training: creazione e training di un modello di regressione rispetto al training di una rete neurale
- Progettazione di funzionalità con R e l'estrazione di funzionalità con T-SQL
- Assegnazione di punteggi a singole righe o batch piccoli, confronto con l'assegnazione di punteggi in blocco tramite input tabulari
- Esecuzione del punteggio in R rispetto alla distribuzione di modelli in produzione in SQL Server nelle stored procedure
- Modifica del codice R per ridurre al minimo il trasferimento dei dati o rimuovere le trasformazioni dei dati costose
- Abilita test automatizzati e ripetizione del training dei modelli

Poiché la scelta delle tecniche di ottimizzazione dipende da quale attività è cruciale per l'applicazione o il caso d'uso, i case study coprono sia i suggerimenti generali sulle prestazioni sia le linee guida su come ottimizzare per uno scenario specifico, ottimizzando il Punteggio batch.

+ **Singole opzioni di ottimizzazione in SQL Server**

    Nel primo case study delle prestazioni, più test sono stati eseguiti su un singolo set di dati utilizzando un unico tipo di modello. L'algoritmo rxLinMod in RevoscaleR è stato utilizzato per compilare un modello e creare punteggi da esso, ma il codice e le tabelle di dati sottostanti sono stati sistematicamente modificati per verificare l'effetto di ogni modifica.

    Ad esempio, in un'esecuzione dei test, il codice R è stato modificato in modo da poter eseguire un confronto tra la progettazione delle funzionalità usando una funzione di trasformazione e il precomputing delle funzionalità e quindi il caricamento delle funzionalità da una tabella. In un'altra esecuzione dei test, le prestazioni di training del modello sono state confrontate tra l'utilizzo di una tabella indicizzata standard e i dati in una tabella con vari tipi di compressione o nuovi tipi di indice.

+ **Ottimizzazione per uno scenario specifico di assegnazione dei punteggi a volumi elevati**

    L'attività machine learning nel secondo case study comporta l'elaborazione di molti riavvii inviati per più posizioni e la ricerca del candidato migliore per ogni posizione di processo. Il modello di apprendimento automatico viene formulato come un problema di classificazione binaria: accetta una descrizione del processo e di ripresa come input e genera la probabilità per ogni coppia Resume-job. Poiché l'obiettivo è trovare la corrispondenza migliore, viene usata una soglia di probabilità definita dall'utente per filtrare ulteriormente e ottenere solo le corrispondenze ottimali.

    Per questa soluzione, l'obiettivo principale era quello di ottenere una bassa latenza durante il punteggio. Questa attività, tuttavia, è costosa dal punto di vista del calcolo anche durante il processo di assegnazione dei punteggi, perché ogni nuovo processo deve corrispondere a milioni di ripristini entro un intervallo di tempo ragionevole. Inoltre, la fase di progettazione delle funzionalità produce più di 2000 funzionalità per ripresa o processo e rappresenta un collo di bottiglia significativo delle prestazioni.

Si consiglia di esaminare tutti i risultati del primo case study per determinare quali tecniche sono applicabili alla soluzione e ponderare il loro impatto potenziale.

Esaminare quindi i risultati dell'ottimizzazione per il Punteggio case study per vedere come l'autore ha applicato diverse tecniche e ottimizzato il server per supportare un carico di lavoro specifico.

## <a name="performance-optimization-process"></a>Processo di ottimizzazione delle prestazioni

Per la configurazione e l'ottimizzazione delle prestazioni è necessario creare una base solida, su cui eseguire l'ottimizzazione dei livelli progettata per carichi di lavoro specifici:

- Scegliere un server appropriato per ospitare l'analisi. In genere, è preferibile un server di report secondario, data warehouse o un altro server già usato per altri report o analisi. Tuttavia, in una soluzione di elaborazione analitica transazionale (HTAP) ibrida, i dati operativi possono essere usati come input per R per un punteggio rapido.

- Configurare l'istanza di SQL Server per bilanciare le operazioni del motore di database e l'esecuzione di script R o Python a livelli appropriati. Questo può includere la modifica delle impostazioni predefinite SQL Server per l'utilizzo della memoria e della CPU, le impostazioni di affinità del processore e NUMA e la creazione di gruppi di risorse.

- Ottimizzare il computer server per supportare l'utilizzo efficiente di script esterni. Ciò può includere l'aumento del numero di account utilizzati per l'esecuzione di script esterni, l'abilitazione della gestione dei pacchetti e l'assegnazione di utenti ai ruoli di sicurezza correlati.

- Applicazione di ottimizzazioni specifiche per l'archiviazione e il trasferimento dei dati in SQL Server, incluse strategie di indicizzazione e statistiche, progettazione di query e ottimizzazione delle query e progettazione di tabelle utilizzate per Machine Learning. È anche possibile analizzare le origini dati e i metodi di trasporto dei dati oppure modificare i processi ETL per ottimizzare l'estrazione delle funzionalità.

- Ottimizzare il modello analitico per evitare inefficienze. L'ambito delle ottimizzazioni possibili dipende dalla complessità del codice R e dai pacchetti e dai dati in uso. Le attività principali includono l'eliminazione di trasformazioni di dati costose o l'offload delle attività di preparazione dei dati o di progettazione di funzionalità da R o Python ai processi ETL o SQL. È anche possibile effettuare il refactoring degli script, eliminare le installazioni di pacchetti inline, dividere il codice R in procedure separate per la formazione, il punteggio e la valutazione oppure semplificare il codice per lavorare in modo più efficiente come stored procedure.

## <a name="articles-in-this-series"></a>Articoli della serie

+ [Ottimizzazione delle prestazioni per R in SQL Server-hardware](../r/sql-server-configuration-r-services.md)

    Vengono fornite informazioni aggiuntive per la configurazione [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] dell'hardware installato in e per la configurazione dell'istanza di SQL Server per supportare meglio gli script esterni. È particolarmente utile per gli **amministratori di database**.

+ [Ottimizzazione delle prestazioni per R in SQL Server-codice e ottimizzazione dei dati](../r/r-and-data-optimization-r-services.md)

    Fornisce suggerimenti specifici su come ottimizzare lo script esterno per evitare problemi noti. È particolarmente utile per **i data scientist**.

    > [!NOTE]
    > Sebbene la maggior parte delle informazioni contenute in questa sezione si applichi a R in generale, alcune informazioni sono specifiche delle funzioni analitiche RevoScaleR. Informazioni dettagliate sulle prestazioni non sono disponibili per **revoscalepy** e altre librerie Python supportate.
    >

+ [Ottimizzazione delle prestazioni per R in SQL Server-metodi e risultati](../r/performance-case-study-r-services.md)

    Vengono riepilogati i dati utilizzati nei due casi di studio, il modo in cui le prestazioni sono state testate e il modo in cui le ottimizzazioni hanno influenzato i risultati.
