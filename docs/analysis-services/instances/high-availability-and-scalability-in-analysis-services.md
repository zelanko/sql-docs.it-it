---
title: Disponibilità elevata e scalabilità in Analysis Services | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 09fc0a9d9814a399d679b1391678fb5e11ad8a3f
ms.sourcegitcommit: c3b190f8f87a4c80bc9126bb244896197a6dc453
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/26/2019
ms.locfileid: "56852926"
---
# <a name="high-availability-and-scalability-in-analysis-services"></a>Disponibilità elevata e scalabilità in Analysis Services
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Questo articolo descrive le tecniche usate più di frequente per garantire ai database di Analysis Services disponibilità elevata e scalabile. Ognuno di questi obiettivi potrebbe essere affrontato separatamente ma, in realtà, questi sono spesso correlati: una distribuzione scalabile per carichi di lavoro di elaborazione o di query di grandi dimensioni in genere prevede una disponibilità elevata.  
  
 Non è sempre vero il contrario, tuttavia. La disponibilità elevata, senza scalabilità, può essere l'unico obiettivo nel caso di contratti di servizio rigidi per carichi di lavoro di query di importanza critica, ma con volumi moderati.  
  
 Le tecniche per garantire disponibilità elevata e scalabilità ad Analysis Services tendono a essere le stesse per tutte le modalità server (multidimensionale, tabulare e integrazione con SharePoint). Se non specificato diversamente, le informazioni contenute in questo articolo si applicano a tutte le modalità.  
  
## <a name="key-points"></a>Punti chiave  
 Poiché le tecniche per la disponibilità e la scalabilità sono diverse da quelle del motore di database relazionale, può essere efficace presentare le tecniche usate con Analysis Services con un breve riepilogo dei punti chiave:  
  
-   Analysis Services usa i meccanismi di disponibilità elevata e scalabilità integrati nella piattaforma Windows Server: Bilanciamento carico di rete, clustering di failover di Window Server (WSFC, Window Server Failover Clustering) o entrambi.  
  
    > [!NOTE]  
    >  La funzionalità AlwaysOn del motore di database relazionale non si estende ad Analysis Services.  Non è possibile configurare un'istanza di Analysis Services per l'esecuzione in un gruppo di disponibilità AlwaysOn.  
    >   
    >  Analysis Services non funziona all'interno di gruppi di disponibilità AlwaysOn, ma può sia recuperare che elaborare i dati dai database relazionali Always On. Per istruzioni su come configurare un database relazionale a disponibilità elevata per l'uso con Analysis Services, vedere [Analysis Services con i gruppi di disponibilità AlwaysOn](../../database-engine/availability-groups/windows/analysis-services-with-always-on-availability-groups.md).  
  
-   Se la disponibilità elevata è l'unico obiettivo, è possibile ottenerla tramite ridondanza dei server in un cluster di failover. Si presume che i nodi di sostituzione abbiano una configurazione hardware e software identica a quella del nodo attivo.  La sola funzionalità di cluster di failover di Windows Server offre un'elevata disponibilità, ma senza scalabilità.  
  
-   È possibile ottenere la scalabilità, con o senza disponibilità, tramite Bilanciamento carico di rete su database di sola lettura.  La scalabilità di solito è un problema nel caso di grandi volumi di query o se tali volumi presentano picchi improvvisi.  
  
     Il bilanciamento del carico, associato a più database di sola lettura, offre sia scalabilità che disponibilità elevata, dato che tutti i nodi sono attivi e, in caso di indisponibilità di un server, le richieste vengono automaticamente ridistribuite tra i nodi rimanenti. Se sono necessarie sia la scalabilità che la disponibilità, un cluster di Bilanciamento carico di rete è la scelta giusta.  
  
 Per l'elaborazione, gli obiettivi di disponibilità elevata e scalabilità non rappresentano un problema altrettanto pressante, poiché è possibile controllare tempi e ambito delle operazioni. Attraverso le diverse parti di un modello l'elaborazione può essere sia parziale che incrementale, anche se a un certo punto è necessario elaborare il modello per intero in un unico server per garantire la coerenza dei dati tra tutti gli indici e tutte le aggregazioni. Una solida architettura scalabile si basa su hardware in grado di supportare un'elaborazione completa con qualsiasi frequenza. Per soluzioni di grandi dimensioni, questa attività è strutturata come operazione indipendente con risorse hardware riservate.  
  
##  <a name="bkmk_serverconfig"></a> Configurazione a server singolo e configurazione multiserver  
 In una distribuzione a server singolo normale i carichi di lavoro relativi alle query e all'elaborazione vengono eseguiti contemporaneamente, presupponendo che le risorse di sistema siano sufficienti per entrambe le attività. Analysis Services mantiene intatte le strutture di dati esistenti per supportare le query durante l'elaborazione di una versione aggiornata in background. Una quantità di memoria e di spazio su disco sufficiente per la gestione di strutture di dati temporanee è un requisito hardware di tutte le modalità server, anche se ogni modalità impegna le risorse di sistema in modi diversi e presenta livelli diversi di compatibilità con NUMA.  
  
 **Server singoli e scalabilità**  
  
 Un server singolo di fascia alta multi-core potrebbe garantire da solo un livello di scalabilità sufficiente. Nei sistemi di fascia alta con un numero elevato di core e una grande disponibilità di RAM e spazio su disco è possibile aumentare le prestazioni anche nell'ambito di un unico sistema.  
  
 Per i database multidimensionali è possibile regolare le proprietà di configurazione del server in modo da creare affinità tra i processi e i processori. Per ulteriori informazioni, vedere [Thread Pool Properties](../../analysis-services/server-properties/thread-pool-properties.md) .  
  
 **Distribuzioni multiserver**  
  
 I requisiti operativi talvolta impongono l'uso di più server. I cluster di failover, ad esempio, sono multiserver per definizione. L'esecuzione di ogni nodo, infatti, avviene all'interno di configurazioni hardware e software identiche.  
  
 Analogamente, se la disponibilità elevata per i carichi di lavoro di query è un requisito importante, implica in genere l'uso di un certo numero di server. In questo scenario la configurazione consigliata per Analysis Services è una combinazione di database di sola lettura e di lettura e scrittura in esecuzione all'interno di istanze distinte di Analysis Services con hardware dedicato. I database di sola lettura gestiscono le richieste di query, mentre i database di lettura e scrittura vengono usati per l'elaborazione. Una descrizione più ampia di questa tecnica di uso comune viene fornita nella sezione successiva.  
  
 **Macchine virtuali e disponibilità elevata**  
  
 Un'altra strategia per soddisfare requisiti di disponibilità elevata prevede l'uso di macchine virtuali. Se per soddisfare i requisiti di disponibilità è sufficiente che un server sostitutivo sia pronto nel giro di qualche ora anziché di pochi minuti, è possibile usare macchine virtuali da avviare su richiesta e nelle quali siano caricati database recuperati da una posizione centrale.  
  
## <a name="scalability-using-read-only-and-read-write-databases"></a>Scalabilità tramite database di sola lettura e di lettura e scrittura  
 Bilanciamento carico di rete è una funzionalità consigliata per carichi di lavoro di elaborazione e query elevati o in crescita. In una soluzione che prevede l'uso di Bilanciamento carico di rete, per garantire la coerenza delle query i database di Analysis Services devono essere definiti come database di sola lettura.  
  
 Anche se le indicazioni presentate nell'articolo [Aumentare il numero di istanze per l'esecuzione di query in Analysis Services tramite database di sola lettura](https://technet.microsoft.com/library/ff795582\(v=sql.100\).aspx) (pubblicato nel 2008) risalgono a molto tempo fa, in genere sono ancora valide. I sistemi operativi server e i componenti hardware dei computer si sono evoluti e i riferimenti specifici alle piattaforme e ai limiti dei diversi tipi di CPU sono obsoleti, ma la tecnica di base dell'uso di database di sola lettura e di lettura e scrittura per volumi di query di grandi dimensioni non è cambiata.  
  
 Questo approccio può essere riepilogato come segue:  
  
-   Usare hardware e istanze di Analysis Services dedicati per l'elaborazione del database. Impostare il database come di sola lettura al termine dell'elaborazione. Per istruzioni, vedere [Switch an Analysis Services database between ReadOnly and ReadWrite modes](../../analysis-services/multidimensional-models/switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md) .  
  
-   Usare più server di query identici per eseguire copie dello stesso database di Analysis Services di sola lettura. I server devono essere distribuiti in un cluster di Bilanciamento carico di rete, accessibile tramite un solo nome server virtuale che funge da singolo punto di ingresso al cluster.  
  
-   Usare robocopy per copiare un'intera directory di dati dal server di elaborazione a ogni server di query e collegare lo stesso database in modalità di sola lettura a tutti i server di query. È anche possibile usare snapshot SAN, eseguire una sincronizzazione o usare qualsiasi altro strumento o metodo tra quelli usati per lo spostamento di database di produzione.  
  
## <a name="resource-demands-for-tabular-and-multidimensional-workloads"></a>Domanda di risorse per carichi di lavoro tabulari e multidimensionali  
 La tabella seguente è un riepilogo generale dei modi in cui Analysis Services usa le risorse di sistema per le operazioni di query ed elaborazione, distinti per modalità server e archiviazione. Questo riepilogo può essere utile per capire a cosa dare maggiore importanza in una distribuzione multiserver che gestisce un carico di lavoro distribuito.  
  
|||  
|-|-|  
|**Modalità server e archiviazione**|**Impatto sulle risorse di sistema**|  
|Tabulare in memoria (impostazione predefinita) in cui le query vengono eseguite come scansioni di tabella di strutture di dati in memoria.|Dare importanza a RAM e CPU con velocità di clock elevata.|  
|Tabulare in modalità DirectQuery, in cui le query vengono scaricate su server di database relazionale back-end e l'elaborazione è limitata alla creazione di metadati nel modello.|Concentrarsi sulle prestazioni del database relazionale, riducendo la latenza di rete e ottimizzando la velocità effettiva. CPU più veloci possono anche migliorare le prestazioni del processore di query di Analysis Services.|  
|Modelli multidimensionali tramite archiviazione MOLAP|Scegliere una configurazione bilanciata che supporti le operazioni di I/O del disco per il caricamento rapido di dati e una quantità di RAM sufficiente per la memorizzazione di dati nella cache.|  
|Modelli multidimensionali tramite archiviazione ROLAP.|Ottimizzare le operazioni di I/O e ridurre al minimo la latenza di rete.|  
  
## <a name="high-availability-and-redundancy-through-wsfc"></a>Disponibilità elevata e ridondanza tramite WSFC  
 È possibile installare Analysis Services in un cluster di failover di Windows Server esistente per ottenere disponibilità elevata in grado di ripristinare il servizio nel minor tempo possibile.  
  
 I cluster di failover garantiscono accesso completo (in lettura e writeback) al database ma solo per un nodo alla volta. Database secondari in esecuzione all'interno di nodi aggiuntivi del cluster come server sostitutivi se il primo nodo diventa inattivo.  
  
 Il vantaggio principale della funzionalità di cluster di failover è la rapidità di ripristino dopo un errore del servizio. Questo vantaggio presenta alcune limitazioni. La prima è che se il failover non è mai necessario, le risorse dedicate a questa funzionalità al'interno del cluster rimangono inattive. La seconda limitazione è che, in caso di failover, tutte le connessioni vengono perse, e di conseguenza viene perso tutto il lavoro non salvato. La maggior parte delle applicazioni client deve essere in grado di gestire questa situazione. L'utilizzo del pulsante di aggiornamento nell'applicazione consente in genere di visualizzare di nuovo i risultati. 
 
 Quando si prende in considerazione una configurazione WSFC, tenere presente quanto segue:

- La configurazione Attivo/Attivo non è attualmente supportata. Attivo/Passivo (failover) è l'unica configurazione WSFC supportata per Analysis Services.
- Quando si esegue il clustering di Analysis Services, assicurarsi che tutti i nodi coinvolti nel cluster vengano eseguiti su hardware identico o simile e che il contesto operativo di ciascun nodo sia lo stesso in termini di versione del sistema operativo e dei relativi Service Pack, di versione di Analysis Services e dei relativi Service Pack (o aggiornamenti cumulativi) e della modalità server.
- Evitare il reimpiego di un nodo passivo come nodo attivo del carico di lavoro un altro. Se il nodo non è in grado di gestire entrambi i carichi di lavoro, qualsiasi vantaggio a breve termine riguardo l'utilizzo del computer si traduce in una perdita in caso di un'effettiva situazione di failover.
 
 In questo white paper vengono fornite istruzioni dettagliate e informazioni di base per la distribuzione di Analysis Services in un cluster di failover: [Come eseguire il clustering di SQL Server Analysis Services](https://msdn.microsoft.com/library/dn736073.aspx). Anche se scritte per SQL Server 2012, queste indicazioni sono ancora valide per le versioni più recenti di Analysis Services.  
  
## <a name="see-also"></a>Vedere anche  
 [Sincronizzare database di Analysis Services](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md)   
 [Forzare l'affinità NUMA per i database tabulari di Analysis Services](https://blogs.msdn.microsoft.com/sqlcat/2013/11/05/forcing-numa-node-affinity-for-analysis-services-tabular-databases/)   
 [Case Study un Analysis Services: Uso di modelli tabulari in una soluzione commerciale su vasta scala](https://msdn.microsoft.com/library/dn751533.aspx)  
  
  
