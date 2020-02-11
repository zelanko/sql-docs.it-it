---
title: Contatori delle prestazioni (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 05d7d5ab-a96c-4f82-94b1-48a657d7c580
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: aa9d5a5352afd10617358a032824d275b14b6c5e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66079705"
---
# <a name="performance-counters-ssas"></a>Contatori delle prestazioni (SSAS)
  Con Performance Monitor è possibile monitorare le prestazioni di un'istanza di Microsoft SQL Server Analysis Services (SSAS) tramite i contatori delle prestazioni.  
  
 Performance Monitor è uno snap-in di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Control (MMC) che consente di tenere traccia dell'utilizzo delle risorse. È possibile avviare lo snap-in MMC digitando **PerfMon** al prompt dei comandi o dal Pannello di controllo facendo clic su **Strumenti di amministrazione**, quindi su **Performance Monitor**. Performance Monitor consente di tenere traccia delle prestazioni e delle attività del server e dei processi tramite oggetti e contatori predefiniti, nonché monitorare eventi tramite contatori definiti dall'utente. Tramite Performance Monitor vengono raccolti i conteggi anziché i dati sugli eventi, ad esempio l'utilizzo della memoria, il numero di transazioni attive o l'attività della CPU. È inoltre possibile impostare valore soglia per contatori specifici allo scopo di generare avvisi per la notifica agli operatori.  
  
 Con Performance Monitor è possibile monitorare le istanze remote e locali di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per ulteriori informazioni, vedere la pagina relativa all' [utilizzo di Performance Monitor](https://technet.microsoft.com/library/cc749115.aspx).  
  
 Per visualizzare la descrizione dei contatori che possono essere utilizzati con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], in Performance Monitor visualizzare la finestra di dialogo **Aggiungi contatori** , selezionare un oggetto prestazione, quindi fare clic su **Mostra descrizione**. I contatori più importanti sono Utilizzo CPU, Utilizzo memoria e Velocità di trasferimento di I/O su disco. È consigliabile familiarizzare innanzitutto con questi contatori per passare poi a utilizzare contatori più dettagliati che consentono di eseguire un monitoraggio più dettagliato. Per ulteriori informazioni sui contatori da includere, vedere la pagina relativa alla [guida sulle operazioni di SQL Server 2008 R2](https://go.microsoft.com/fwlink/?LinkID=225539).  
  
 I contatori sono stati raggruppati in modo da agevolare la ricerca dei contatori correlati.  
  
## <a name="counters-by-groups"></a>Contatori per gruppi  
  
|Group|Descrizione|  
|-----------|-----------------|  
|[Cache](#bkmk_Cache)|Statistiche correlate alla cache delle aggregazioni di Analysis Services.|  
|[Connessione](#bkmk_Connection)|Statistiche correlate alle connessioni di Microsoft Analysis Services.|  
|[Stima di data mining](#bkmk_DataMiningPrediction)|Statistiche correlate all'elaborazione del modello di data mining.|  
|[Elaborazione del modello di data mining](#bkmk_DataMiningModelProcessing)|Statistiche correlate alla creazione di stime dai modelli di data mining.|  
|[Locks](#bkmk_Locks)|Statistiche correlate ai blocchi del server interni di Microsoft Analysis Services.|  
|[MDX](#bkmk_MDX)|Statistiche correlate ai calcoli MDX di Microsoft Analysis Services.|  
|[Memoria](#bkmk_Memory)|Statistiche correlate alla memoria interna del server di Microsoft Analysis Services.|  
|[Memorizzazione nella cache attiva](#bkmk_ProactiveCaching)|Statistiche correlate al caching attivo di Microsoft Analysis Services.|  
|[Elaborazione di aggregazioni](#bkmk_ProcAggregations)|Statistiche correlate all'elaborazione di aggregazioni nei file di dati MOLAP.|  
|[Elaborazione degli indici](#bkmk_ProcIndexes)|Statistiche correlate all'elaborazione degli indici per i file di dati MOLAP.|  
|[Elaborazione](#bkmk_Processing)|Statistiche correlate all'elaborazione dei dati.|  
|[Query del motore di archiviazione](#bkmk_StorageEngineQuery)|Statistiche correlate alle query del motore di archiviazione di Microsoft Analysis Services.|  
|[Thread](#bkmk_Threads)|Statistiche correlate ai thread di Microsoft Analysis Services.|  
  
###  <a name="bkmk_Cache"></a>Cache  
 Statistiche correlate alla cache delle aggregazioni di Microsoft Analysis Services.  
  
|Contatore|Descrizione|  
|-------------|-----------------|  
|KB memoria corrente|Memoria attualmente utilizzata dalla cache delle aggregazioni, in KB.|  
|KB aggiunti/sec|Velocità con cui la memoria viene aggiunta alla cache, in KB al secondo.|  
|Voci correnti|Numero corrente di voci nella cache.|  
|Inserimenti/sec|Frequenza degli inserimenti nella cache,  indicati per partizione, cubo e database.|  
|Eliminazioni/sec|Frequenza delle eliminazioni dalla cache,  indicate per partizione, cubo e database.  Dovute in genere a operazioni di pulitura della memoria.|  
|Totale inserimenti|Numero totale degli inserimenti nella cache,  indicati per partizione, cubo e database.|  
|Totale eliminazioni|Numero totale delle eliminazioni dalla cache,  indicate per partizione, cubo e database.  Dovute in genere a operazioni di pulitura della memoria.|  
|Accessi diretti/sec|Frequenza degli accessi diretti alla cache. Un accesso alla cache indica che le risposte alle query vengono generate utilizzando una voce esistente nella cache.|  
|Mancati riscontri/sec|Frequenza dei mancati riscontri nella cache.|  
|Ricerche/sec|Frequenza delle ricerche nella cache.|  
|Totale riscontri diretti|Numero totale dei riscontri diretti nella cache.  Un riscontro diretto nella cache indica che le risposte alle query vengono generate utilizzando le voci presenti nella cache.|  
|Totale mancati riscontri|Numero totale dei mancati riscontri nella cache.|  
|Totale ricerche|Numero totale delle ricerche nella cache.|  
|Rapporto accessi diretti|Rapporto tra gli accessi diretti alla cache e le ricerche nella cache, nell'intervallo di tempo tra due operazioni di recupero dei valori dei contatori.|  
|Totale riscontri relativi a iteratore nella cache filtrata|Numero totale di riscontri nella cache che hanno restituito un iteratore indicizzato sui risultati filtrati.|  
|Totale mancati riscontri nella cache filtrata dell'iteratore|Numero totale di riscontri nella cache per cui non è stato possibile compilare un iteratore indicizzato sui risultati filtrati ed è stato necessario compilare una nuova cache con i risultati filtrati.|  
  
###  <a name="bkmk_Connection"></a>Connessione  
 Statistiche correlate alle connessioni di Microsoft Analysis Services.  
  
|Contatore|Descrizione|  
|-------------|-----------------|  
|connessioni correnti|Numero corrente delle connessioni client stabilite.|  
|Richieste/sec|Frequenza delle richieste di connessione  in arrivo.|  
|Totale richieste|Numero totale delle richieste di connessione  in arrivo.|  
|Richieste con esito positivo/sec|Numero delle connessioni completate correttamente al secondo.|  
|Totale esiti positivi|Numero totale delle connessioni con esito positivo.|  
|Errori/sec|Frequenza degli errori di connessione.|  
|Totale errori|Numero totale dei tentativi di connessione non riusciti.|  
|Sessioni utente correnti|Numero corrente di sessioni utente attive.|  
  
###  <a name="bkmk_DataMiningModelProcessing"></a>Elaborazione del modello di data mining  
 Statistiche correlate all'elaborazione del modello di data mining di Microsoft Analysis Services.  
  
|Contatore|Descrizione|  
|-------------|-----------------|  
|Case/sec|Frequenza di elaborazione dei case.|  
|Modelli elaborati correnti|Numero corrente dei modelli in fase di elaborazione.|  
  
###  <a name="bkmk_DataMiningPrediction"></a>Stima di data mining  
 Statistiche correlate alle stime basate sui modelli di data mining di Microsoft Analysis Services.  
  
|Contatore|Descrizione|  
|-------------|-----------------|  
|Query di data mining simultanee|Numero corrente delle query di data mining in fase di elaborazione.|  
|Stime/sec|Numero di stime generate nelle query di data mining|  
|Righe/sec|Numero di righe gestite durante una query di stima di data mining.|  
|Query/sec|Numero di query di data mining gestite.|  
|Totale query|Numero totale delle query di data mining ricevute dal server.|  
|Righe del totale|Numero totale delle righe restituite dalle query di data mining.|  
|Totale stime|Numero totale delle query di stima basate sul modello di data mining ricevute dal server.|  
  
###  <a name="bkmk_Locks"></a>Serrature  
 Statistiche correlate ai blocchi del server interni di Microsoft Analysis Services.  
  
|Contatore|Descrizione|  
|-------------|-----------------|  
|Attese di latch correnti|Numero corrente dei thread in attesa di un latch.  Si riferisce alle richieste di latch che non possono essere soddisfatte immediatamente e sono in stato di attesa.|  
|Attese latch/sec|Frequenza delle richieste di latch che non possono essere soddisfatte immediatamente e devono attendere la concessione del latch.|  
|Blocchi correnti|Numero corrente degli oggetti bloccati.|  
|Attese di blocco correnti|Numero corrente di client in attesa di un blocco.|  
|Richieste di blocco/sec|Numero di richieste di blocco al secondo.|  
|Blocchi concessi/sec|Numero dei blocchi concessi al secondo.|  
|Attese di blocco/sec|Numero delle attese di blocco al secondo.  Si tratta di richieste di blocco che non possono essere soddisfatte immediatamente e vengono messe in uno stato di attesa.|  
|Blocchi negati/sec|Frequenza dei blocchi negati.|  
|Richieste di sblocco/sec|Numero delle richieste di sblocco al secondo.|  
|Totale deadlock rilevati|Numero totale di deadlock rilevati.|  
  
###  <a name="bkmk_MDX"></a>MDX  
 Statistiche correlate ai calcoli MDX di Microsoft Analysis Services.  
  
|Contatore|Descrizione|  
|-------------|-----------------|  
|Numero di calcoli copertura|Numero totale di nodi di valutazione creati dai piani di esecuzione MDX, compresi quelli attivi e memorizzati nella cache.|  
|Numero corrente di nodi di valutazione|Numero corrente (approssimativo) di nodi di valutazione creati dai piani di esecuzione MDX, compresi quelli attivi e memorizzati nella cache.|  
|Numero di nodi di valutazione del motore di archiviazione|Numero totale di nodi di valutazione del motore di archiviazione creati dai piani di esecuzione MDX.|  
|Numero di nodi di valutazione cella per cella|Numero totale di nodi di valutazione cella per cella creati dai piani di esecuzione MDX.|  
|Numero di nodi di valutazione in modalità bulk|Numero totale di nodi di valutazione in modalità bulk creati dai piani di esecuzione MDX.|  
|Numero di nodi di valutazione che coprono una singola cella|Numero totale di nodi di valutazione creati dai piani di esecuzione MDX che coprono una sola cella.|  
|Numero di nodi di valutazione con calcoli alla stessa granularità|Numero totale di nodi di valutazione creati dai piani di esecuzione MDX per cui la granularità dei calcoli è identica a quella del nodo di valutazione.|  
|Numero corrente di nodi di valutazione memorizzati nella cache|Numero corrente (approssimativo) di nodi di valutazione memorizzati nella cache creati dai piani di esecuzione MDX.|  
|Numero di nodi di valutazione del motore di archiviazione memorizzati nella cache|Numero totale di nodi di valutazione del motore di archiviazione memorizzati nella cache creati dai piani di esecuzione MDX.|  
|Numero di nodi di valutazione in modalità bulk memorizzati nella cache|Numero totale di nodi di valutazione in modalità bulk memorizzati nella cache creati dai piani di esecuzione MDX.|  
|Numero di nodi di valutazione di altro tipo memorizzati nella cache|Numero totale di nodi di valutazione memorizzati nella cache creati dai piani di esecuzione MDX che non sono del motore di archiviazione né in modalità bulk.|  
|Numero di eliminazioni dei nodi di valutazione|Numero totale di eliminazioni dei nodi di valutazione dalla cache a causa di collisioni.|  
|Numero di riscontri relativi all'indice hash nella cache dei nodi di valutazione|Numero totale di riscontri nella cache dei nodi di valutazione soddisfatti dall'indice hash.|  
|Numero di riscontri cella per cella nella cache dei nodi di valutazione|Numero totale di riscontri cella per cella nella cache dei nodi di valutazione.|  
|Numero di mancati riscontri cella per cella nella cache dei nodi di valutazione|Numero totale di mancati riscontri cella per cella nella cache dei nodi di valutazione.|  
|Numero di riscontri relativi a sottocubi nella cache dei nodi di valutazione|Numero totale di riscontri relativi a sottocubi nella cache dei nodi di valutazione.|  
|Numero di mancati riscontri relativi a sottocubi nella cache dei nodi di valutazione|Numero totale di mancati riscontri relativi a sottocubi nella cache dei nodi di valutazione.|  
|Totale sottocubi Sonar|Numero totale di sottocubi generati da Query Optimizer.|  
|Totale celle calcolate|Numero totale di proprietà di cella calcolate.|  
|Totale celle ricalcolate|Numero totale di celle ricalcolate a causa di un errore.|  
|Totale inserimenti nella cache flat|Numero totale di valori di cella inseriti nella cache di calcolo flat.|  
|Totale cache di calcolo registrate|Numero totale di cache di calcolo registrate.|  
|Totale NON EMPTY|Numero totale di operazioni in cui sono stati utilizzati algoritmi NON EMPTY.|  
|Totale NON EMPTY non ottimizzati|Numero totale di operazioni in cui sono stati utilizzati algoritmi NON EMPTY non ottimizzati.|  
|Totale NON EMPTY per membri calcolati|Numero totale di cicli dell'algoritmo NON EMPTY eseguiti su membri calcolati.|  
|Totale Auto Exist|Numero totale di esecuzioni di Autoexist.|  
|Totale EXISTING|Numero totale di esecuzioni dell'operatore sui set EXISTING.|  
  
###  <a name="bkmk_Memory"></a>Memoria  
 Statistiche correlate alla memoria interna del server di Microsoft Analysis Services.  
  
|Contatore|Descrizione|  
|-------------|-----------------|  
|Riserva di paging da 64 KB allocata|Memory presa in prestito dal sistema, in KB.  Tale memoria viene allocata ad altre aree del server.|  
|KB riserva di paging in elenco lookaside da 64 KB|Memoria corrente (in KB) nell'elenco lookaside da 64 KB.  Si riferisce alle pagine di memoria pronte all'uso.|  
|Riserva di paging da 8 KB allocata|Memory presa in prestito dal pool di pagine da 64 KB, in KB.  Tale memoria viene allocata ad altre aree del server.|  
|KB riserva di paging in elenco lookaside da 8 KB|Memoria corrente (in KB) nell'elenco lookaside da 8 KB.  Si riferisce alle pagine di memoria pronte all'uso.|  
|Riserva di paging da 1 KB allocata|Memory presa in prestito dal pool di pagine da 64 KB, in KB.  Tale memoria viene allocata ad altre aree del server.|  
|KB riserva di paging in elenco lookaside da 1 KB|Memoria corrente (in KB) nell'elenco lookaside da 8 KB.  Si riferisce alle pagine di memoria pronte all'uso.|  
|prezzo corrente pulitura memoria|Prezzo corrente della memoria, in €/byte/tempo, moltiplicato per 1000.|  
|Pulitura memoria - bilanciamento/sec|Frequenza delle operazioni di bilanciamento e compattazione.|  
|Pulitura memoria - KB/sec memoria completata|Frequenza di compattazione, in KB al secondo.|  
|Pulitura memoria - KB memoria compattabile|Quantità di memoria, in KB, soggetta a ripulitura da parte del servizio di pulitura in background.|  
|Pulitura memoria - KB memoria non compattabile|Quantità di memoria, in KB, non soggetta a ripulitura da parte del servizio di pulitura in background.|  
|Pulitura memoria - KB memoria|Quantità di memoria, in KB, nota al servizio di pulitura della memoria in background,  ottenuta sommando la memoria compattabile e quella non compattabile.|  
|KB memoria utilizzata|Utilizzo della memoria del processo server utilizzato per il calcolo del prezzo di una memoria più pulita.  Equivale al contatore Process\PrivateBytes più le dimensioni dei dati con mapping in memoria, ignorando la memoria con mapping o allocazione eseguita dal motore di analisi in memoria xVelocity (VertiPaq) in eccesso rispetto al limite di memoria del motore xVelocity.|  
|KB limite inferiore memoria|Limite inferiore della memoria, dal file di configurazione.|  
|KB limite superiore memoria|Limite superiore della memoria, dal file di configurazione.|  
|AggCacheKB|Memoria attualmente allocata alla cache delle aggregazioni, in KB.|  
|KB quota|Quota di memoria corrente, in KB.  Le quote di memoria sono note anche come concessioni di memoria o prenotazioni di memoria.|  
|quota bloccata|Numero corrente di richieste di quota bloccate fino a quando non vengono liberate altre quote di memoria.|  
|KB cache dei file|Memoria attualmente allocata alla cache dei file, in KB.|  
|Cache dei file - errori di pagina/sec|Frequenza degli errori di pagina nella cache dei file.|  
|Cache dei file - letture/sec|Numero delle operazioni di lettura eseguite nella cache dei file al secondo.|  
|Cache dei file - letture in KB/sec|Frequenza delle operazioni di lettura eseguite nella cache dei file, in KB al secondo.|  
|Cache dei file - scritture/sec|Pagine FileStore scritte/sec.  Le Scritture sono asincrone.|  
|Cache dei file - scritture in KB/sec|KB FileStore scritti/sec.  Le Scritture sono asincrone.|  
|Cache dei file - errori di I/O/sec|Frequenza degli errori di I/O nella cache dei file.|  
|Cache dei file - errori di I/O|Totale degli errori di I/O nella cache dei file.|  
|Cache dei file - pagine clock esaminate/sec|Frequenza con cui il servizio di pulitura della memoria in background esamina le pagine per determinare quelle da eliminare.|  
|Cache dei file - pagine clock con riferimenti/sec|Frequenza con cui il servizio di pulitura della memoria in background esamina le pagine per cui esiste un conteggio di riferimenti corrente (pagine attualmente in uso).|  
|Cache dei file - pagine clock valide/sec|Frequenza con cui il servizio di pulitura della memoria in background esamina le pagine che costituiscono candidati validi per l'eliminazione.|  
|Cache dei file - KB memoria bloccata|Memoria della cache dei file attualmente bloccata, in KB.|  
|KB file di proprietà delle dimensioni in memoria|File di proprietà delle dimensioni attualmente in memoria, in KB.|  
|KB/sec file di proprietà delle dimensioni in memoria|Numero delle operazioni di scrittura nel file di proprietà delle dimensioni in memoria, in KB.|  
|File di proprietà delle dimensioni potenzialmente in memoria, in KB|Dimensioni potenziali del file di proprietà delle dimensioni in memoria, in KB.|  
|File di proprietà delle dimensioni|Numero di file di proprietà delle dimensioni.|  
|KB file indice (hash) delle dimensioni in memoria|Dimensioni del file indice (hash) delle dimensioni in memoria, in KB.|  
|KB/sec file indice (hash) delle dimensioni in memoria|Numero delle operazioni di scrittura nel file indice (hash) delle dimensioni in memoria, in KB.|  
|File indice (hash) delle dimensioni potenzialmente in memoria, in KB|Dimensioni potenziali del file indice (hash) delle dimensioni in memoria, in KB.|  
|File indice (hash) delle dimensioni|Numero di file indice (hash) delle dimensioni.|  
|KB file di stringhe delle dimensioni in memoria|Dimensioni correnti del file di stringhe delle dimensioni in memoria, in KB.|  
|KB/sec file di stringhe delle dimensioni in memoria|Numero delle operazioni di scrittura nel file di stringhe delle dimensioni in memoria, in KB.|  
|File di stringhe delle dimensioni potenzialmente in memoria, in KB|Dimensioni potenziali del file di stringhe delle dimensioni in memoria, in KB.|  
|File di stringhe delle dimensioni|Numero di file di stringhe delle dimensioni.|  
|KB file di mapping in memoria|Dimensioni correnti del file di mapping in memoria, in KB.|  
|KB/sec file di mapping in memoria|Numero delle operazioni di scrittura nel file di mapping in memoria, in KB.|  
|File di mapping potenzialmente in memoria, in KB|Dimensioni potenziali del file di mapping in memoria, in KB.|  
|File di mapping|Numero di file di mapping.|  
|KB file di mapping delle aggregazioni in memoria|Dimensioni correnti del file di mapping delle aggregazioni in memoria, in KB.|  
|KB/sec file di mapping delle aggregazioni in memoria|Numero delle operazioni di scrittura nel file di mapping delle aggregazioni in memoria, in KB.|  
|File di mapping delle aggregazioni potenzialmente in memoria, in KB|Dimensioni del file di mapping delle aggregazioni potenzialmente in memoria, in KB.|  
|File di mapping delle aggregazioni|Numero di file di mapping delle aggregazioni.|  
|KB file di dati delle tabelle dei fatti in memoria|Dimensioni del file di dati delle tabelle dei fatti attualmente in memoria, in KB.|  
|KB/sec file di dati delle tabelle dei fatti in memoria|Numero delle operazioni di scrittura nel file di dati delle tabelle dei fatti in memoria, in KB.|  
|File di dati delle tabelle dei fatti potenzialmente in memoria, in KB|Dimensioni del file di dati delle tabelle dei fatti potenzialmente in memoria, in KB.|  
|File di dati delle tabelle dei fatti|Numero di file di dati delle tabelle dei fatti.|  
|KB file di stringhe delle tabelle dei fatti in memoria|Dimensioni del file di stringhe delle tabelle dei fatti attualmente in memoria, in KB.|  
|KB/sec file di stringhe delle tabelle dei fatti in memoria|Numero delle operazioni di scrittura nel file di stringhe delle tabelle dei fatti in memoria, in KB.|  
|File di stringhe delle tabelle dei fatti potenzialmente in memoria, in KB|Dimensioni del file di stringhe delle tabelle dei fatti potenzialmente in memoria, in KB.|  
|File di stringhe delle tabelle dei fatti|Numero di file di stringhe delle tabelle dei fatti.|  
|KB file di aggregazione delle tabelle dei fatti in memoria|Dimensioni correnti del file di aggregazione delle tabelle dei fatti in memoria, in KB.|  
|KB/sec file di aggregazione delle tabelle dei fatti in memoria|Numero delle operazioni di scrittura nel file di aggregazione delle tabelle dei fatti in memoria, in KB.|  
|File di aggregazione delle tabelle dei fatti potenzialmente in memoria, in KB|Dimensioni del file di aggregazione delle tabelle dei fatti potenzialmente in memoria, in KB.|  
|File di aggregazione delle tabelle dei fatti|Numero di file di aggregazione delle tabelle dei fatti.|  
|KB altri file in memoria|Dimensioni di altri file attualmente in memoria, in KB.|  
|KB/sec altri file in memoria|Numero delle operazioni di scrittura in altri file in memoria, in KB.|  
|Altri file potenzialmente in memoria, in KB|Dimensioni di altri file potenzialmente in memoria, in KB.|  
|Altri file|Numero di altri file.|  
|KB di paging VertiPaq|Kilobyte di memoria di paging in uso per i dati in memoria.|  
|KB non di paging VertiPaq|Kilobyte di memoria bloccata nel working set per l'utilizzo dal motore in memoria.|  
|KB di mapping in memoria VertiPaq|Kilobyte di memoria paginabile in uso per i dati in memoria.|  
|KB limite superiore memoria|Limite assoluto della memoria, dal file di configurazione.|  
|KB limite memoria VertiPaq|Limite in memoria dal file di configurazione.|  
  
###  <a name="bkmk_ProactiveCaching"></a>Memorizzazione nella cache attiva  
 Statistiche correlate al caching attivo di Microsoft Analysis Services.  
  
|Contatore|Descrizione|  
|-------------|-----------------|  
|Notifiche/sec|Frequenza delle notifiche inviate dal database relazionale.|  
|Annullamenti elaborazione/sec|Frequenza di annullamenti dell'elaborazione causati dalle notifiche.|  
|Inizio caching attivo/sec|Frequenza delle operazioni di caching attivo iniziate.|  
|Completamento del caching attivo/sec|Frequenza delle operazioni di caching attivo completate.|  
  
###  <a name="bkmk_ProcAggregations"></a>Elaborazione di aggregazioni  
 Statistiche correlate all'elaborazione di aggregazioni di Microsoft Analysis Services nei file di dati MOLAP.  
  
|Contatore|Descrizione|  
|-------------|-----------------|  
|Partizioni correnti|Numero corrente delle partizioni da elaborare.|  
|Totale partizioni|Numero totale delle partizioni elaborate (con esito positivo o negativo).|  
|Numero aggregazioni in memoria|Dimensioni delle aggregazioni in memoria.  Valore stimato.|  
|Byte aggregazioni in memoria|Dimensioni delle aggregazioni in memoria.  Valore stimato.|  
|Righe unite/sec|Velocità di unione o inserimento delle righe in un'aggregazione.|  
|Righe create/sec|Velocità di creazione delle righe di un'aggregazione.|  
|Righe scritte in file temporanei/sec|Velocità di scrittura in un file temporaneo.  La scrittura nei file temporanei avviene quando le aggregazioni superano i limiti di memoria.|  
|Byte scritti in file temporanei/sec|Velocità di scrittura in un file temporaneo.  La scrittura nei file temporanei avviene quando le aggregazioni superano i limiti di memoria.|  
  
###  <a name="bkmk_ProcIndexes"></a>Elaborazione degli indici  
 Statistiche correlate all'elaborazione di Microsoft Analysis Services degli indici per i file di dati MOLAP.  
  
|Contatore|Descrizione|  
|-------------|-----------------|  
|Partizioni correnti|Numero corrente delle partizioni da elaborare.|  
|Totale partizioni|Numero totale delle partizioni elaborate (con esito positivo o negativo).|  
|Righe/sec|Numero delle righe di file MOLAP utilizzate al secondo per la creazione degli indici.|  
|Righe del totale|Totale delle righe di file MOLAP utilizzate per la creazione degli indici.|  
  
###  <a name="bkmk_Processing"></a>Elaborazione  
 Statistiche correlate all'elaborazione dei dati di Microsoft Analysis Services.  
  
|Contatore|Descrizione|  
|-------------|-----------------|  
|Righe lette/sec|Velocità di lettura delle righe da tutti i database relazionali.|  
|Totale righe lette|Numero totale delle righe lette da tutti i database relazionali.|  
|Righe convertite/sec|Velocità di conversione delle righe durante l'elaborazione.|  
|Totale righe convertite|Numero totale delle righe convertite durante l'elaborazione.|  
|Righe scritte/sec|Velocità di scrittura delle righe durante l'elaborazione.|  
|Totale righe scritte|Numero totale delle righe scritte durante l'elaborazione.|  
  
###  <a name="bkmk_StorageEngineQuery"></a>Query del motore di archiviazione  
 Statistiche correlate alle query del motore di archiviazione di Microsoft Analysis Services.  
  
|Contatore|Descrizione|  
|-------------|-----------------|  
|Query correnti gruppo di misure|Numero corrente delle query sul gruppo di misure in fase di elaborazione.|  
|Query gruppo di misure/sec|Frequenza delle query sul gruppo di misure|  
|Totale query gruppo di misure|Numero totale delle query sul gruppo di misure.|  
|Query correnti dimensione|Numero corrente di query sulla dimensione in fase di elaborazione.|  
|Query dimensione/sec|Frequenza delle query sulla dimensione|  
|Totale query dimensione.|Numero totale di query sulla dimensione.|  
|Query risposte/sec|Velocità di risposta alle query.|  
|Totale query risposte|Numero totale delle query alle quali è stata restituita una risposta.|  
|Byte inviati/sec|Byte al secondo inviati dal server ai client in risposta alle query.|  
|Totale byte inviati|Numero totale dei byte inviati dal server ai client in risposta alle query.|  
|Righe inviate/sec|Righe inviate dal server ai client al secondo.|  
|Totale righe inviate|Numero totale delle righe inviate dal server ai client.|  
|Query dirette dalla cache/sec|Numero delle query al secondo per cui è stato possibile ottenere la risposta direttamente dalla cache.|  
|Query dalla cache filtrate/sec|Numero delle query al secondo per cui è stato possibile ottenere una risposta filtrando le voci esistenti nella cache.|  
|Query da file/sec|Numero delle query al secondo per cui è stato possibile ottenere una risposta dai file.|  
|Totale query dalla cache dirette|Numero totale delle query risolte direttamente dalla cache,  indicato per partizione.|  
|Totale query dalla cache filtrate|Numero totale delle query per cui è stato possibile ottenere una risposta filtrando le voci esistenti nella cache.|  
|Totale query da file|Numero totale delle query per cui è stato possibile ottenere una risposta dai file.|  
|Letture mapping/sec|Numero delle operazioni di lettura logica eseguite utilizzando il file di mapping.|  
|Byte mapping/sec|Velocità di lettura dal file di mapping, in byte al secondo.|  
|Letture dati/sec|Numero delle operazioni di lettura logica eseguite utilizzando il file di dati.|  
|Byte dati/sec|Velocità di lettura dal file di dati, in byte al secondo.|  
|Tempo medio/query|Tempo di risposta medio per query, in millisecondi.  Il tempo di risposta è basato sulle query risolte dopo l'ultima misurazione del contatore.|  
|Round trip in rete/sec|Frequenza dei round trip in rete.  Sono incluse tutte le comunicazioni client/server.|  
|Numero totale dei round trip in rete|Numero totale dei round trip in rete.  Sono incluse tutte le comunicazioni client/server.|  
|Ricerca nella cache flat/sec|Frequenza delle ricerche nella cache flat.  Sono incluse le cache flat in ambito globale, sessione e query.|  
|Riscontri nella cache/sec|Frequenza di riscontri nella cache flat.  Sono incluse le cache flat in ambito globale, sessione e query.|  
|Ricerche nella cache di calcolo/sec|Frequenza delle ricerche nella cache di calcolo.  Sono incluse le cache di calcolo in ambito globale, sessione e query.|  
|Riscontri nella cache di calcolo/sec|Frequenza dei riscontri nella cache di calcolo.  Sono incluse le cache di calcolo in ambito globale, sessione e query.|  
|Ricerche nella cache persistente/sec|Frequenza delle ricerche nella cache persistente.  Le cache persistenti vengono create dall'istruzione CACHE dello script MDX.|  
|Riscontri nella cache persistente/sec|Frequenza di riscontri nella cache persistente.  Le cache persistenti vengono create dall'istruzione CACHE dello script MDX.|  
|Ricerche nella cache di dimensione/sec|Frequenza delle ricerche nella cache di dimensione.|  
|Riscontri nella cache di dimensione/sec|Frequenza di riscontri nella cache di dimensione.|  
|Ricerche nella cache di gruppi di misure/sec|Frequenza delle ricerche nella cache di gruppi di misure.|  
|Riscontri nella cache di gruppi di misure/sec|Frequenza dei riscontri nella cache di gruppi di misure.|  
|Ricerche di aggregazione/sec|Frequenza delle ricerche di aggregazione.|  
|Riscontri di aggregazione/sec|Frequenza di riscontri di aggregazione.|  
  
###  <a name="bkmk_Threads"></a>Thread  
 Statistiche correlate ai thread di Microsoft Analysis Services.  
  
|Contatore|Descrizione|  
|-------------|-----------------|  
|thread inattivi per analisi dei thread brevi|Numero dei thread inattivi nel pool dei thread per l'analisi dei thread brevi.|  
|thread occupati per analisi dei thread brevi|Numero dei thread occupati nel pool dei thread per l'analisi dei thread brevi.|  
|lunghezza coda processi di analisi dei thread brevi|Numero dei processi nella coda del pool dei thread per l'analisi dei thread brevi.|  
|Frequenza processi di analisi dei thread brevi|Frequenza dei processi nel pool dei thread per l'analisi dei thread brevi.|  
|thread inattivi per analisi dei thread lunghi|Numero dei thread inattivi nel pool dei thread per l'analisi dei thread lunghi.|  
|thread occupati per analisi dei thread lunghi|Numero dei thread occupati nel pool dei thread per l'analisi dei thread lunghi.|  
|lunghezza coda processi di analisi dei thread lunghi|Numero dei processi nella coda del pool dei thread per l'analisi dei thread lunghi.|  
|Frequenza processi di analisi dei thread lunghi|Frequenza dei processi nel pool dei thread per l'analisi dei thread lunghi.|  
|thread inattivi nel pool di query|Numero dei thread inattivi nel pool dei thread di query.|  
|Thread occupati pool di query|Numero dei thread occupati nel pool dei thread di query.|  
|lunghezza coda processi nel pool di query|Numero dei processi nella coda del pool dei thread di query.|  
|Frequenza processi pool di query|Frequenza dei processi nel pool dei thread di query.|  
|thread non di I/O inattivi nel pool di elaborazione|Numero di thread inattivi nel pool dei thread di elaborazione dedicato a processi non di I/O.|  
|thread non di I/O occupati nel pool di elaborazione|Numero dei thread che eseguono processi non di I/O nel pool dei thread di elaborazione.|  
|Lunghezza coda processi nel pool di elaborazione|Numero dei processi non di I/O nella coda del pool dei thread di elaborazione.|  
|Frequenza processi pool di elaborazione|Frequenza dei processi non di I/O nel pool dei thread di elaborazione.|  
|thread di processi di I/O inattivi nel pool di elaborazione|Numero di thread inattivi per i processi di I/O nel pool dei thread di elaborazione.|  
|thread di processi di I/O occupati nel pool di elaborazione|Numero di thread che eseguono processi di I/O nel pool dei thread di elaborazione.|  
|lunghezza coda processi di I/O nel pool di elaborazione|Numero di processi di I/O nella coda del pool dei thread di elaborazione.|  
|Percentuale di completamento dei processi di I/O nel pool di elaborazione|Percentuale dei processi di I/O nel pool dei thread di elaborazione.|  
  
  
