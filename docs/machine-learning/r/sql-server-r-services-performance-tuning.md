---
title: Ottimizzazione delle prestazioni per R
description: Questo articolo descrive l'ottimizzazione delle prestazioni per R Services.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 04/15/2018
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: cedb8cd13db6c8d27b987c60881093caa91af50a
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/13/2020
ms.locfileid: "88180458"
---
# <a name="performance-tuning-for-r-in-sql-server"></a>Ottimizzazione delle prestazioni per R in SQL Server
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

Questo articolo è il primo di una serie di quattro articoli che descrivono l'ottimizzazione delle prestazioni per R Services, in base a due case study:

- Test delle prestazioni eseguiti dal team di sviluppo del prodotto per convalidare il profilo delle prestazioni delle soluzioni R

- Ottimizzazione delle prestazioni da parte del team di data science Microsoft per uno scenario di Machine Learning specifico spesso richiesto dai clienti.

L'obiettivo di questa serie è fornire indicazioni sui tipi di tecniche di ottimizzazione delle prestazioni più utili per l'esecuzione di processi R in SQL Server.

+ Questo argomento (il primo) offre una panoramica dell'architettura e di alcuni problemi comuni durante l'ottimizzazione per le attività di data science.
+ Nel secondo articolo vengono illustrate le ottimizzazioni specifiche per hardware e SQL Server.
+ Il terzo articolo illustra le ottimizzazioni nel codice R e le risorse per l'operazionalizzazione.
+ Il quarto articolo descrive in dettaglio i metodi di test e riporta i risultati e le conclusioni.

**Si applica a:** R Services per SQL Server 2016, Machine Learning Services per SQL Server

## <a name="performance-goals-and-targeted-scenarios"></a>Obiettivi di prestazioni e scenari previsti

La funzionalità R Services è stata introdotta in SQL Server 2016 per supportare l'esecuzione di script R da SQL Server. Quando si usa questa funzionalità, il runtime di R opera in un processo separato dal motore di database, ma scambia i dati in modo sicuro con il motore di database, usando le risorse del server e i servizi che interagiscono con SQL Server, ad esempio il servizio Launchpad attendibile.

In SQL Server 2017 è stato annunciato il supporto per l'esecuzione di script Python con la stessa architettura, con l'aggiunta di un ulteriore linguaggio prevista per il futuro.

Con l'aumentare del numero di versioni e linguaggi supportati, è importante che l'amministratore e l'architetto del database siano consapevoli del rischio di conflitti di risorse dovuti ai processi di Machine Learning e che siano in grado di configurare il server per supportare nuovi carichi di lavoro. Sebbene mantenere le funzionalità di analisi vicine ai dati consenta di evitare spostamenti dei dati non sicuri, anche i carichi di lavoro di analisi vengono spostati dal portatile del data scientist al server che ospita i dati.

L'ottimizzazione delle prestazioni per le operazioni di Machine Learning non prevede ovviamente una soluzione ideale per tutti li scenari. Le attività comuni seguenti potrebbero avere profili di prestazioni molto diversi:

- Attività di training: creazione e training di un modello di regressione rispetto al training di una rete neurale
- Progettazione di caratteristiche con R o estrazione di caratteristiche con T-SQL
- Assegnazione di punteggi a singole righe o batch piccoli rispetto all'assegnazione di punteggi in blocco tramite input tabulari
- Assegnazione di punteggi in R rispetto alla distribuzione di modelli in produzione in SQL Server nelle stored procedure
- Modifica del codice R per ridurre al minimo il trasferimento dei dati o rimuovere trasformazioni dei dati onerose
- Abilitazione di test automatizzati e ripetizione del training dei modelli

Poiché la scelta delle tecniche di ottimizzazione dipende da quale attività è cruciale per l'applicazione o il caso d'uso, i case study propongono sia suggerimenti generali sulle prestazioni sia linee guida per l'ottimizzazione in uno scenario specifico, ovvero l'ottimizzazione per l'assegnazione di punteggi in batch.

+ **Singole opzioni di ottimizzazione in SQL Server**

    Nel primo case study relativo alle prestazioni, sono stati eseguiti più test su un singolo set di dati usando un unico tipo di modello. L'algoritmo rxLinMod in RevoscaleR è stato usato per compilare un modello e creare punteggi da esso, ma sia il codice che le tabelle di dati sottostanti sono stati modificati sistematicamente per verificare l'effetto di ogni modifica.

    Ad esempio, in un'esecuzione dei test, il codice R è stato modificato in modo da poter eseguire un confronto tra la progettazione delle caratteristiche usando una funzione di trasformazione e il precalcolo delle caratteristiche e il relativo caricamento da una tabella. In un'altra esecuzione dei test, le prestazioni di training del modello sono state confrontate tra l'uso di una tabella indicizzata standard e i dati in una tabella con vari tipi di compressione o nuovi tipi di indice.

+ **Ottimizzazione per uno scenario specifico di assegnazione di punteggi a volumi elevati**

    L'attività di Machine Learning nel secondo case study comporta l'elaborazione di molti curricula inviati per più posizioni lavorative e la ricerca del candidato migliore per ogni posizione. Il modello di Machine Learning stesso viene formulato come un problema di classificazione binaria: accetta un curriculum e una descrizione della posizione come input e genera la probabilità per ogni coppia curriculum-posizione. Poiché l'obiettivo è trovare la corrispondenza migliore, viene usata una soglia di probabilità definita dall'utente per filtrare ulteriormente e ottenere solo le corrispondenze ottimali.

    Per questa soluzione, l'obiettivo principale è ottenere una bassa latenza durante l'assegnazione dei punteggi. Questa attività, tuttavia, è onerosa dal punto di vista del calcolo anche durante il processo di assegnazione dei punteggi, perché per ogni nuova posizione è necessario trovare le corrispondenze cercando tra milioni di curricula entro un intervallo di tempo ragionevole. Inoltre, il passaggio di progettazione delle caratteristiche produce più di 2000 caratteristiche per ogni curriculum o posizione e rappresenta un collo di bottiglia significativo delle prestazioni.

Si consiglia di esaminare tutti i risultati del primo case study per determinare quali tecniche sono applicabili alla soluzione specifica, ponderandone il potenziale impatto.

Esaminare quindi i risultati del case study sull'ottimizzazione dell'assegnazione dei punteggi per vedere come l'autore ha applicato diverse tecniche e ottimizzato il server per supportare un carico di lavoro particolare.

## <a name="performance-optimization-process"></a>Processo di ottimizzazione delle prestazioni

Per la configurazione e l'ottimizzazione delle prestazioni è necessario creare una base solida, sulla quale applicare le ottimizzazioni progettate per carichi di lavoro specifici:

- Scegliere un server appropriato per ospitare l'analisi. In genere, è preferibile un server di report secondario, un data warehouse o un altro server già usato per altri report o analisi. Tuttavia, in una soluzione di elaborazione analitica transazionale (HTAP) ibrida, i dati operativi possono essere usati come input per R per l'assegnazione rapida dei punteggi.

- Configurare l'istanza di SQL Server per bilanciare le operazioni del motore di database e l'esecuzione di script R o Python a livelli appropriati. Questo può includere la modifica delle impostazioni predefinite di SQL Server per l'utilizzo della memoria e della CPU, le impostazioni di affinità del processore e NUMA e la creazione di gruppi di risorse.

- Ottimizzare il computer server per supportare l'uso efficiente di script esterni. Ciò può includere l'aumento del numero di account usati per l'esecuzione di script esterni, l'abilitazione della gestione dei pacchetti e l'assegnazione di utenti ai ruoli di sicurezza correlati.

- Applicazione di ottimizzazioni specifiche per l'archiviazione e il trasferimento dei dati in SQL Server, incluse strategie di indicizzazione e statistiche, progettazione e ottimizzazione delle query, nonché la progettazione delle tabelle usate per le operazioni di Machine Learning. È anche possibile analizzare le origini dati e i metodi di trasporto dei dati oppure modificare i processi ETL per ottimizzare l'estrazione delle caratteristiche.

- Ottimizzare il modello analitico per evitare inefficienze. L'ambito delle ottimizzazioni possibili dipende dalla complessità del codice R e dai pacchetti e dai dati in uso. Le attività principali includono l'eliminazione di trasformazioni di dati costose o l'offload delle attività di preparazione dei dati o di progettazione delle caratteristiche da R o Python ai processi ETL o SQL. È anche possibile effettuare il refactoring degli script, eliminare le installazioni di pacchetti inline, dividere il codice R in procedure separate per il training, l'assegnazione dei punteggi e la valutazione oppure semplificare il codice per usarlo in modo più efficiente come stored procedure.

## <a name="articles-in-this-series"></a>Articoli della serie

+ [Ottimizzazione delle prestazioni per R in SQL Server - Hardware](../r/sql-server-configuration-r-services.md)

    Vengono fornite linee guida per la configurazione dell'hardware su cui è installato [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] e per la configurazione dell'istanza di SQL Server per supportare meglio gli script esterni. È particolarmente utile per gli **amministratori di database**.

+ [Ottimizzazione delle prestazioni per R in SQL Server - Ottimizzazione del codice e dei dati](../r/r-and-data-optimization-r-services.md)

    Fornisce suggerimenti specifici su come ottimizzare lo script esterno per evitare problemi noti. L'argomento è particolarmente utile per i **data scientist**.

    > [!NOTE]
    > Anche se la maggior parte delle informazioni in questa sezione si applica a R in generale, alcune informazioni sono specifiche per le funzioni analitiche di RevoScaleR. Non sono disponibili linee guida dettagliate per **revoscalepy** e altre librerie Python supportate.
    >

+ [Ottimizzazione delle prestazioni per R in SQL Server - Metodi e risultati](../r/performance-case-study-r-services.md)

    Vengono riepilogati i dati usati nei due case study, le modalità di test delle prestazioni e gli effetti delle ottimizzazioni sui risultati.
