---
title: Profiling di dati e notifiche in DQS
ms.date: 03/15/2020
ms.prod: sql
ms.reviewer: jroth
ms.technology: data-quality-services
ms.topic: conceptual
author: swinarko
ms.author: sawinark
ms.openlocfilehash: e0bd9585a48ee30368d145c79f8431e922801a9c
ms.sourcegitcommit: c30a2def43c86860aeec69d3e3029f2296544b13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/25/2020
ms.locfileid: "80243401"
---
# <a name="data-profiling-and-notifications-in-data-quality-services-dqs"></a>Profiling dei dati e notifiche in Data Quality Services (DQS)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)](DQS) è un servizio di profiling dei dati. DQS analizza i dati di un'origine e visualizza le statistiche sui dati nelle attività DQS.

## <a name="attributes-goals-benefits"></a>Attributi, obiettivi, vantaggi

### <a name="attributes-of-dqs"></a>Attributi di DQS

La profilatura DQS presenta gli attributi seguenti:

- Fornisce misure automatiche di qualità dei dati.
- È integrato nella gestione delle informazioni DQS e nei progetti di qualità dei dati.
- È dinamico e regolabile.

### <a name="goals-of-dqs"></a>Obiettivi di DQS

La profilatura con DQS presenta i due obiettivi principali seguenti:

- Guida per i processi di qualità dei dati e per supportare le decisioni.
- Per valutare l'efficacia dei processi.

### <a name="benefits-of-dqs"></a>Vantaggi di DQS

Il profiling DQS offre i vantaggi seguenti:

- Fornisce informazioni dettagliate sulla qualità dei dati di origine e consente di identificare i problemi di qualità dei dati.

- Valuta i processi di qualità dei dati e guida il:
  - Individuazione informazioni
  - Pulizia dei dati
  - Criteri di corrispondenza
  - Lavoro corrispondente

- Fornisce le informazioni più rilevanti al momento più rilevante.

- Genera notifiche che evidenziano statistiche o eventi importanti che potrebbero richiedere un'azione. Le notifiche DQS spesso indicano una condizione e consigliano un'azione correttiva.

La profilatura DQS fornisce l'individuazione delle informazioni, la pulizia dei dati e la corrispondenza dei dati. DQS è anche lo strumento di analisi dei dati. È possibile creare una Knowledge base per l'analisi. È quindi possibile eseguire l'individuazione delle informazioni utilizzando la Knowledge base. L'individuazione delle informazioni utilizza le statistiche di profiling per determinare se la Knowledge base soddisfa le esigenze di individuazione, pulizia e corrispondenza.

## <a name="how-dqs-profiling-works"></a><a name="How"></a>Funzionamento della profilatura DQS

La profilatura DQS non consente di misurare la qualità della Knowledge base. La profilatura misura la qualità dei dati di origine. Il profiling fornisce statistiche che indicano l'effetto degli sforzi seguenti:

- Operazione specifica nella gestione delle informazioni.
- Un progetto Data Quality sui dati di origine.

### <a name="activity-context"></a>Contesto attività

Il profiling ha sempre luogo nel contesto dell'attività specifica che si sta eseguendo. È possibile fare clic sulla scheda profiling in una schermata per visualizzare i dati di profilatura. Questo clic non consente di uscire dalla fase dell'attività che si sta eseguendo. La tabella di profilatura viene popolata in tempo reale durante l'esecuzione del processo. È pertanto possibile valutare le attività relative alla qualità dei dati durante l'esecuzione.

Dopo la pulizia o deduplicazione, è possibile determinare se la qualità dei dati di origine è migliorata e in quale misura.

### <a name="profiling-is-based-on-counts"></a>La profilatura è basata sui conteggi

Tutti i numeri di profiling si riferiscono al numero di occorrenze di valori specifici. In molti casi, i numeri si riferiscono alla percentuale del totale. Le metriche di univocità sono un'eccezione. Le metriche di univocità fanno riferimento al numero assoluto di valori, indipendentemente dal numero di occorrenze di tali valori.

### <a name="knowledge-driven-solution"></a>Soluzione basata sulle informazioni

Il profiling fa parte della soluzione DQS basata sulle informazioni Il profiling fornisce informazioni su una Knowledge base, una corrispondenza o un processo di pulizia dei dati. Le informazioni sono basate sul mapping tra i campi dell'origine dati e i domini della Knowledge base. La profilatura viene eseguita solo dopo il completamento del mapping. Durante la fase di mapping di qualsiasi attività non viene eseguita alcuna profilatura.

Il profiling è sempre collegato a un'attività. Il processo di profilatura viene eseguito sui dati di cui è stato eseguito il _mapping_ ai domini e non sui dati _nei_ domini.

Il profiling è integrato nei seguenti passaggi delle attività:

- Passaggi **individua** e **Gestisci valori di dominio** dell'attività di individuazione delle informazioni.

- Passaggi **Pulisci** e **Gestisci e visualizza risultati** dell'attività di pulizia.

- I **criteri di corrispondenza** e i passaggi dei **risultati corrispondenti** dell'attività dei criteri di corrispondenza.

- Passaggi di **corrispondenza** ed **esportazione** dell'attività corrispondente.

DQS non fornisce statistiche di profiling per l'attività di gestione del dominio.

## <a name="profiling-data-by-activity"></a><a name="Activity"></a>Profiling dei dati in base all'attività

La profilatura DQS usa le seguenti dimensioni standard di qualità dei dati per rappresentare la qualità dei dati:

- Completezza: la misura in cui sono presenti i dati.
- Accuratezza: la misura in cui i dati possono essere utilizzati per l'utilizzo previsto.
- Univocità: misura in cui valori diversi rappresentano entità diverse.

Per impostazione predefinita, i valori NULL e vuoti sono considerati mancanti o abbassano la percentuale di completezza. È tuttavia possibile definire altri valori come equivalenti NULL. Anche questi valori sono considerati mancanti.

Il profiling fornisce le statistiche necessarie per valutare i processi, ma è necessario interpretare tali statistiche. È possibile decifrare i suggerimenti del profiling analizzando le statistiche colonna per colonna.

### <a name="differing-sets-of-profiling-statistics"></a>Set di statistiche di profilatura diversi

Le attività DQS offrono diversi set di statistiche di profiling, come descritto di seguito:

- Solo l'attività di pulizia presenta statistiche di profiling relative all'accuratezza (in percentuale e per dominio). L'accuratezza è interessata da regole relative a validità, coerenza, errori di sintassi e dominio.

- Solo l'attività di pulizia presenta statistiche di profiling per i valori Corretti, Con correzione e Suggeriti nell'origine e Con correzione e Suggeriti per dominio (con entrambi numero e percentuale).

- Le attività Pulizia e Individuazione informazioni presentano statistiche di profiling per la validità (Pulizia per record, Individuazione informazioni per record e dominio). Le attività Criteri di corrispondenza e Corrispondenza non presentano statistiche per la validità.

- Vengono fornite statistiche di profiling per l'univocità, per l'origine e per dominio. Questa istruzione si applica alle attività seguenti:
  - Individuazione delle informazioni.
  - Criteri di corrispondenza.
  - Corrispondenza.
  - Ma _non_ per l'attività di pulizia.

DQS offre statistiche di profiling specifiche correlate a un'attività. Per informazioni dettagliate, vedere le sezioni relative alla **profilatura** negli argomenti seguenti:

- [Esecuzione dell'individuazione delle informazioni](../data-quality-services/perform-knowledge-discovery.md)

- [Pulire i dati mediante DQS &#40;informazioni interne sulla&#41;](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md)

- [Creazione di criteri di corrispondenza](../data-quality-services/create-a-matching-policy.md)

- [Eseguire un progetto corrispondente](../data-quality-services/run-a-matching-project.md)

## <a name="profiling-data-in-activity-monitoring"></a><a name="Monitoring"></a>Profiling dei dati nel monitoraggio delle attività

Le informazioni di profilatura sono disponibili non solo nelle pagine attività del client Data Quality, ma anche nel monitoraggio delle attività. Le informazioni riguardano le attività di individuazione delle informazioni, criteri di corrispondenza, corrispondenza e pulizia. Le informazioni sono disponibili nelle pagine attività del client Data Quality e nel monitoraggio delle attività.

È possibile visualizzare tutti gli elementi seguenti in un'unica posizione:

- Proprietà
- Processi di calcolo correlati delle attività
- Informazioni di profiling generate per ogni attività

È possibile selezionare un'attività nella tabella delle attività per visualizzare i risultati della profilatura nella seconda tabella. È inoltre possibile esportare i risultati del profiling.

Per altre informazioni, vedere [DQS Administration](../data-quality-services/dqs-administration.md).

## <a name="notifications"></a><a name="Notifications"></a>Notifiche

DQS genera notifiche per indicare quando potrebbe essere necessario eseguire un'azione in base alle statistiche profilate. DQS utilizza le notifiche per informazioni importanti sull'origine dati. Questi fact mostrano l'efficacia dell'attività corrente in relazione allo scopo per cui è stata eseguita. Le notifiche forniscono suggerimenti e raccomandazioni che indicano una condizione. Le notifiche possono inoltre consigliare come migliorare un'attività di individuazione delle informazioni, pulizia dei dati o corrispondenza dei dati.

DQS invia una notifica quando rileva un problema che potrebbe essere importante. Come situazione di esempio, quando la completezza e l'accuratezza sono entrambe del 100%, l'attività di pulizia dei dati potrebbe non produrre valori corretti o suggeriti. DQS può inviare una notifica per questa situazione. Questa notifica indica che l'attività potrebbe non essere necessaria. Se eseguire l'attività, è necessario prendere una decisione.

Una notifica viene indicata da una descrizione comando con un punto esclamativo nella scheda **profilatura** . le statistiche associate alla notifica sono colorate in rosso per indicare la giustificazione statistica per la notifica.

### <a name="disable-notifications"></a>Disabilitare le notifiche

Le notifiche sono abilitate per impostazione predefinita. È tuttavia possibile disabilitare le notifiche usando il home page Data Quality Client. Nella sezione **Amministrazione** usare la scheda **Impostazioni generali** .

Quando le notifiche sono disabilitate, le descrizioni comandi non vengono visualizzate e le statistiche non vengono colorate in rosso. La profilatura rimane operativa mentre le notifiche sono disabilitate. La disabilitazione delle notifiche non comporta un miglioramento delle prestazioni.

Per condizioni specifiche associate alle notifiche per un'attività, vedere gli argomenti seguenti:

- [Esecuzione dell'individuazione delle informazioni](../data-quality-services/perform-knowledge-discovery.md)

- [Pulire i dati mediante DQS &#40;informazioni interne sulla&#41;](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md)

- [Creazione di criteri di corrispondenza](../data-quality-services/create-a-matching-policy.md)

- [Eseguire un progetto corrispondente](../data-quality-services/run-a-matching-project.md)

## <a name="related-tasks"></a>Attività correlate

| Descrizione dell'attività | Argomento |
| :--------------- | :---- |
| Viene descritto come abilitare o disabilitare le notifiche in DQS. | [Abilitare o disabilitare le notifiche di profiling in DQS](../data-quality-services/enable-or-disable-profiling-notifications-in-dqs.md) |
|||
