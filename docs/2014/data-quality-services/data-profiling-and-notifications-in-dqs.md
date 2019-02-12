---
title: Profiling di dati e notifiche in DQS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: a778bb5b-8e35-4a7b-b04a-ae2b46dec21b
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: a367f08cc77aebcad4c195a7921b7a75af619eae
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56041752"
---
# <a name="data-profiling-and-notifications-in-dqs"></a>Profiling di dati e notifiche in DQS
  Il profiling dei dati in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) è il processo di analisi dei dati in un'origine dati esistente e la visualizzazione di statistiche sui dati nelle attività DQS. L'attività consente di eseguire la misurazione automatizzata della qualità dei dati. Il profiling in DQS è integrato nei progetti di gestione e di qualità dei dati di DQS e si tratta di una funzionalità dinamica e adattabile. Gli obiettivi principali del profiling sono due: semplificare l'esecuzione dei processi relativi alla qualità dei dati, supportando il processo decisionale, e valutare l'efficacia di tali processi. Il profiling DQS offre i vantaggi seguenti:  
  
-   Il profiling fornisce informazioni dettagliate sulla qualità dei dati di origine e consente di identificare problemi relativi a tale qualità.  
  
-   Il profiling consente di valutare l'efficacia dei processi relativi alla qualità dei dati, guidando l'utente nelle procedure di individuazione delle informazioni, pulizia dei dati, creazione di criteri e altre operazioni relative all'individuazione delle corrispondenze.  
  
-   Il profiling consente di ottenere le informazioni più significative nel momento più rilevante.  
  
-   Il processo di profiling genera notifiche che evidenziano statistiche o eventi importanti che possono richiedere un intervento. In molti casi le notifiche di DQS indicheranno una condizione e consiglieranno l'azione che è possibile intraprendere per rimediare a tale condizione.  
  
 Il profiling consente di utilizzare Data Quality Services non solo per l'individuazione delle informazioni, la pulizia e l'individuazione delle corrispondenze, ma anche come strumento di analisi. È consigliabile creare una Knowledge Base per l'analisi, quindi eseguire l'individuazione delle informazioni utilizzandola per determinare, mediante le statistiche di profiling, se soddisfa le esigenze di individuazione, di pulizia e di corrispondenza.  
  
##  <a name="How"></a> Funzionamento del profiling  
 Il profiling non consente di misurare la qualità della Knowledge Base, ma viene utilizzato per la misurazione della qualità dei dati di origine. Il profiling fornisce statistiche che indicano l'effetto dell'operazione specifica che si esegue nell'ambito della gestione delle informazioni o di un progetto Data Quality sui dati di origine. Il profiling ha sempre luogo nel contesto dell'attività specifica che si sta eseguendo. È possibile fare clic sulla scheda relativa al profiling in una schermata per visualizzare i dati di profiling senza uscire dalla fase dell'attività che si sta eseguendo. La tabella relativa al profiling viene popolata in tempo reale durante l'esecuzione del processo, consentendo la valutazione delle attività relative alla qualità dei dati nel corso della loro esecuzione. Dopo la pulizia o deduplicazione, è possibile determinare se la qualità dei dati di origine è migliorata e in quale misura.  
  
 Tutti i numeri di profiling si riferiscono al numero di occorrenze di un valore, e in molti casi alla percentuale del totale, fatta eccezione per la metrica relativa all'univocità. La metrica di unicità si riferisce al numero assoluto di valori, indipendentemente dal numero di occorrenze di tali valori.  
  
 Il profiling fa parte della soluzione DQS basata sulle informazioni e fornisce informazioni su una Knowledge Base, su una corrispondenza o su un processo di pulizia dei dati in base al mapping tra i campi delle origini dati e domini della Knowledge Base. Il profiling viene eseguito solo dopo il completamento dell'esecuzione del mapping. Durante la fase di mapping di qualsiasi attività, non verrà pertanto eseguita alcuna attività di profiling. Il profiling è sempre collegato a un'attività. Il processo di profiling viene eseguito sui dati di cui è stato eseguito il mapping ai domini e non sui dati nei domini stessi. Il profiling è integrato nei seguenti passaggi delle attività:  
  
-   Passaggi **Individua** e **Gestisci valori di dominio** dell'attività di individuazione delle informazioni  
  
-   Passaggi **Pulisci** e **Gestisci e visualizza risultati** dell'attività di pulizia  
  
-   Passaggi **Criteri di corrispondenza** e **Risultati corrispondenza** dell'attività relativa ai criteri di corrispondenza  
  
-   Passaggi **Corrispondenza** e **Esporta** dell'attività relativa all'individuazione delle corrispondenze  
  
 DQS non fornisce statistiche di profiling per l'attività di gestione del dominio.  
  
##  <a name="Activity"></a> Profiling dei dati in base all'attività  
 Per il profiling DQS vengono utilizzate dimensioni standard per rappresentare la qualità dei dati: completezza (l'entità della presenza dei dati), accuratezza (la misura entro cui i dati possono essere utilizzati per gli scopi previsti) e univocità (la misura entro cui valori diversi rappresentano entità diverse). Per impostazione predefinita, i valori NULL e vuoti sono considerati mancanti, o abbassano la percentuale di completezza. È tuttavia possibile definire altri valori come equivalenti a NULL, in qual caso verranno anch'essi considerati come mancanti.  
  
 Il profiling fornisce le statistiche necessarie per valutare i processi, ma è necessario interpretare tali statistiche. È possibile decifrare i suggerimenti del profiling analizzando le statistiche colonna per colonna.  
  
 Le attività DQS offrono diversi set di statistiche di profiling, come descritto di seguito:  
  
-   Solo l'attività di pulizia presenta statistiche di profiling relative all'accuratezza (in percentuale e per dominio). L'accuratezza è interessata da regole relative a validità, coerenza, errori di sintassi e dominio.  
  
-   Solo l'attività di pulizia presenta statistiche di profiling per i valori Corretti, Con correzione e Suggeriti nell'origine e Con correzione e Suggeriti per dominio (con entrambi numero e percentuale).  
  
-   Le attività Pulizia e Individuazione informazioni presentano statistiche di profiling per la validità (Pulizia per record, Individuazione informazioni per record e dominio). Le attività Criteri di corrispondenza e Corrispondenza non presentano statistiche per la validità.  
  
-   L'attività Pulizia non presenta statistiche di profiling per l'univocità. Le attività Individuazione informazioni, Criteri di corrispondenza e Corrispondenza presentano statistiche di profiling per l'unicità in numero e percentuale per l'origine e per dominio.  
  
 Per ulteriori informazioni sulle statistiche di profiling specifiche correlate a un'attività, vedere le sezioni Profiling negli argomenti seguenti:  
  
-   [Eseguire l'individuazione di informazioni](../../2014/data-quality-services/perform-knowledge-discovery.md)  
  
-   [Pulire i dati mediante DQS &#40;informazioni interne&#41;](../../2014/data-quality-services/cleanse-data-using-dqs-internal-knowledge.md)  
  
-   [Creare criteri di corrispondenza](../../2014/data-quality-services/create-a-matching-policy.md)  
  
-   [Eseguire un progetto corrispondente](../../2014/data-quality-services/run-a-matching-project.md)  
  
##  <a name="Monitoring"></a> Profiling dei dati nel monitoraggio delle attività  
 Il profiling delle informazioni per le attività Individuazione informazioni, Criteri di corrispondenza, Corrispondenza e Pulizia sono disponibili non solo nelle pagine delle attività del client Data Quality, ma anche nel monitoraggio delle attività. Il monitoraggio delle attività fornisce una panoramica sulle attività correnti e precedenti. Oltre alle proprietà e ai processi di calcolo correlati delle attività, è possibile visualizzare le informazioni di profiling generate per ogni attività in una data posizione. Selezionare un'attività nella tabella delle attività per visualizzare i risultati del profiling in una tabella sottostante. È inoltre possibile esportare i risultati del profiling. Per altre informazioni, vedere [DQS Administration](../../2014/data-quality-services/dqs-administration.md).  
  
##  <a name="Notifications"></a> Notifiche  
 Oltre ad effettuare la raccolta e la visualizzazione di importanti statistiche e metriche tramite il profiling, DQS genererà notifiche (se abilitate) per indicare quando potrebbe essere necessario intraprendere azioni in base alle statistiche di profiling visualizzate. DQS utilizza le notifiche per evidenziare informazioni importanti sull'origine dati e mostrare l'efficacia dell'attività corrente in relazione allo scopo per il quale è stata eseguita. Le notifiche forniscono suggerimenti e raccomandazioni che indicano una condizione e forniscono consigli su come migliorare un'attività di individuazione di informazioni, di pulizia dei dati o di individuazione di corrispondenze.  
  
 Le notifiche di DQS vengono utilizzate per generare avvisi che potrebbero interessare l'operatore o indicare la soluzione a un potenziale problema. Se è o meno necessario intraprendere azioni in seguito alla notifica dipenderà dalla rilevanza di tale azione per gli scopi previsti. Si supponga ad esempio che DQS generi una notifica quando la pulizia dei dati non produce valori corretti o suggeriti, mentre la completezza e l'accuratezza sono entrambe del 100%. Questa notifica indicherebbe che potrebbe non essere necessario eseguire l'attività. L'esecuzione o meno dell'attività rimane tuttavia una decisione che prenderà l'utente.  
  
 Una notifica viene indicata da una descrizione comando con un punto esclamativo nella scheda **Profiling** . Le statistiche associate alla notifica sono colorate in rosso per indicare la giustificazione statistica per la notifica.  
  
 È possibile abilitare (valore predefinito) o disabilitare le notifiche nella scheda **Impostazioni generali** della sezione **Amministrazione** della home page del client Data Quality. Quando le notifiche sono disabilitate, le descrizioni comandi non vengono visualizzate e le statistiche non verranno visualizzate in colore rosso. La disabilitazione delle notifiche non comporta miglioramenti significativi delle prestazioni. Il profiling resta operativo anche qualora si disabilitino le notifiche.  
  
 Per condizioni specifiche associate alle notifiche per un'attività, vedere gli argomenti seguenti:  
  
-   [Eseguire l'individuazione di informazioni](../../2014/data-quality-services/perform-knowledge-discovery.md)  
  
-   [Pulire i dati mediante DQS &#40;informazioni interne&#41;](../../2014/data-quality-services/cleanse-data-using-dqs-internal-knowledge.md)  
  
-   [Creare criteri di corrispondenza](../../2014/data-quality-services/create-a-matching-policy.md)  
  
-   [Eseguire un progetto corrispondente](../../2014/data-quality-services/run-a-matching-project.md)  
  
## <a name="related-tasks"></a>Attività correlate  
  
|Descrizione dell'attività|Argomento|  
|----------------------|-----------|  
|Viene descritto come abilitare o disabilitare le notifiche in DQS.|[Abilitare o disabilitare le notifiche di profiling in DQS](../../2014/data-quality-services/enable-or-disable-profiling-notifications-in-dqs.md)|  
  
  
