---
title: Gruppi di disponibilità per SQL Server in Linux Always On
description: ''
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
manager: jroth
ms.date: 04/17/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: e37742d4-541c-4d43-9ec7-a5f9b2c0e5d1
ms.openlocfilehash: 1900a7156eaf98abb9a4c20bad5f7d1eafe365db
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2019
ms.locfileid: "67834217"
---
# <a name="always-on-availability-groups-on-linux"></a>Gruppi di disponibilità in Linux Always On

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questo articolo descrive le caratteristiche dei gruppi di disponibilità AlwaysOn (gruppi di disponibilità) in basato su Linux [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] installazioni. Vengono inoltre illustrate le differenze tra Linux - e Windows Server failover cluster (WSFC)-basato su gruppi di disponibilità. Vedere le [documentazione basata su Windows](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md) per le nozioni di base dei gruppi di disponibilità, perché hanno lo stesso funzionamento in Windows e Linux, ad eccezione del cluster WSFC.

Dal punto di vista di alto livello, dei gruppi di disponibilità in [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] in Linux sono uguali quando si trovano in implementazioni basate su WSFC. Ciò significa che tutte le limitazioni e le funzionalità sono gli stessi, con alcune eccezioni. Le differenze principali includono:

-   Microsoft Distributed Transaction Coordinator (DTC) non è supportato in Linux nel [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]. Se le applicazioni richiedono l'uso delle transazioni distribuite ed è necessario un gruppo di disponibilità, distribuire [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] su Windows.
-   Le distribuzioni basate su Linux usano Pacemaker invece di un cluster WSFC.
-   Diversamente dalla maggior parte delle configurazioni per gruppi di disponibilità in Windows, ad eccezione lo scenario del gruppo di lavoro del Cluster, Pacemaker non necessario mai Active Directory Domain Services (AD DS).
-   Come eseguire un gruppo di disponibilità da un nodo a un altro è diversa tra Linux e Windows.
-   Alcune impostazioni, ad esempio `required_synchronized_secondaries_to_commit` possono essere modificate solo tramite Pacemaker in Linux, mentre un'installazione basata su WSFC Usa Transact-SQL.

## <a name="number-of-replicas-and-cluster-nodes"></a>Numero di repliche e i nodi del cluster

Un gruppo di disponibilità [!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)] può avere due repliche totali: una primaria e una replica secondaria che può essere utilizzata solo per scopi di disponibilità. Non è utilizzabile per qualsiasi altra esigenza, ad esempio le query leggibile. Un gruppo di disponibilità [!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)] può avere fino a nove repliche totali: una primaria e fino a otto repliche secondarie, dei quali un massimo di tre (incluso quello primario) può essere sincrona. Se si usa un cluster sottostante, può esserci un massimo di 16 nodi totale quando è coinvolto Corosync. Un gruppo di disponibilità può estendersi al massimo nove di 16 nodi con [!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)]e due con [!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)].

Una configurazione con due repliche che richiede la possibilità di eseguire automaticamente il failover a un'altra replica richiede l'uso di una replica di sola configurazione, come descritto in [replica di sola configurazione e quorum](#configuration-only-replica-and-quorum). Le repliche di sola configurazione sono state introdotte in [!INCLUDE[sssql17-md](../includes/sssql17-md.md)] Cumulative Update 1 (CU1), in modo che deve essere la versione minima di distribuzione per questa configurazione.

Se Pacemaker è usato, deve essere configurata correttamente in modo che rimanga attivo e in esecuzione. Ciò significa che quorum e quorum di STONITH deve essere implementato correttamente da una prospettiva di Pacemaker, oltre a eventuali [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] requisiti, ad esempio una replica di sola configurazione.

Repliche secondarie leggibili sono supportate solo con [!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)].

## <a name="cluster-type-and-failover-mode"></a>Modalità di tipo e il failover del cluster

Novità di [!INCLUDE[sssql17-md](../includes/sssql17-md.md)] è l'introduzione di un tipo di cluster per gruppi di disponibilità. Per Linux, esistono due valori validi: Esterno e nessuno. Un tipo di cluster External significa che Pacemaker verrà usato di sotto del gruppo di disponibilità. Uso esterno per tipo di cluster richiede che la modalità di failover sia impostata anche su External (altra novità in [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]). Failover automatico è supportato, ma a differenza di un cluster WSFC, la modalità di failover è impostata su esterno, non è automatica, quando Pacemaker viene utilizzato. A differenza di un cluster WSFC, la parte di Pacemaker del gruppo di disponibilità viene creata dopo aver configurato il gruppo di disponibilità.

Un tipo di cluster None indica che non è presente alcun requisito per, e il gruppo di disponibilità userà, Pacemaker. Anche su server dotati di Pacemaker configurato, se un gruppo di disponibilità è configurato con un tipo di cluster None, Pacemaker non visualizzare o gestire tale gruppo di disponibilità. Un tipo di cluster None supporta solo il failover manuale da un database primario a una replica secondaria. Un gruppo di disponibilità creato con nessuno è destinata principalmente per la scalabilità in lettura out scenario così come gli aggiornamenti. Anche se può funzionare in scenari come il ripristino di emergenza o disponibilità locale in cui non è necessario alcun failover automatico, non è consigliabile. La storia del listener è anche più complessa senza Pacemaker.

Tipo di cluster verrà archiviato nel [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] vista a gestione dinamica (DMV) `sys.availability_groups`, nelle colonne `cluster_type` e `cluster_type_desc`.

## <a name="requiredsynchronizedsecondariestocommit"></a>required\_synchronized\_secondaries\_to\_commit

Familiarità con [!INCLUDE[sssql17-md](../includes/sssql17-md.md)] è un'impostazione utilizzata da gruppi di disponibilità denominati `required_synchronized_secondaries_to_commit`. Il gruppo di disponibilità indica il numero di repliche secondarie che devono essere indirizzata con la replica primaria. Ciò consente ad esempio il failover automatico (solo quando l'integrazione con Pacemaker con un tipo di cluster External) e controlla il comportamento delle operazioni, ad esempio la disponibilità del database primario se il numero corretto di repliche secondarie è online o offline. Per altre informazioni sul funzionamento, vedere [elevata disponibilità e protezione dei dati per le configurazioni di gruppo di disponibilità](sql-server-linux-availability-group-ha.md). Il `required_synchronized_secondaries_to_commit` valore è impostato per impostazione predefinita e gestita da Pacemaker / [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. È possibile eseguire manualmente l'override di questo valore.

La combinazione delle `required_synchronized_secondaries_to_commit` e il nuovo numero di sequenza (che viene archiviato `sys.availability_groups`) indica a Pacemaker e [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] che, ad esempio, può verificarsi il failover automatico. In tal caso, una replica secondaria avrebbe lo stesso numero di sequenza del database primario, vale a dire che viene aggiornato con tutte le informazioni di configurazione più recente.

Sono disponibili tre valori che possono essere impostati per `required_synchronized_secondaries_to_commit`: 0, 1 o 2. Questi controllano il comportamento di ciò che accade quando una replica diventa non disponibile. I numeri corrispondono al numero di repliche secondarie che devono essere sincronizzati con la replica primaria. Il comportamento è come indicato di seguito in Linux:

-   0 - le repliche secondarie non sono necessario essere in stato sincronizzato con la replica primaria. Tuttavia se le repliche secondarie non sono sincronizzate, non vi sarà alcun failover automatico. 
-   1 - una replica secondaria deve essere in uno stato sincronizzato con quello primario. il failover automatico è possibile. Il database primario non è disponibile fino a quando non è disponibile una replica secondaria sincrona.
-   2 - sia nelle repliche secondarie in una configurazione di gruppi di disponibilità tre o più nodi deve essere sincronizzato con quello primario. il failover automatico è possibile.

`required_synchronized_secondaries_to_commit` Consente di controllare non solo il comportamento di failover con repliche sincrone, ma la perdita di dati. Con un valore pari a 1 o 2, una replica secondaria deve sempre essere sincronizzati, pertanto sarà sempre presente la ridondanza dei dati. Ciò significa che senza perdita di dati.

Per modificare il valore di `required_synchronized_secondaries_to_commit`, usare la sintassi seguente:

>[!NOTE]
>La modifica del valore fa sì che la risorsa da riavviare, vale a dire una breve interruzione. L'unico modo per evitare questo problema consiste nell'impostare la risorsa non sia gestito con il cluster temporaneamente.

**Ubuntu e Red Hat Enterprise Linux (RHEL)**

```bash
sudo pcs resource update <AGResourceName> required_synchronized_secondaries_to_commit=<Value>
```

**SUSE Linux Enterprise Server (SLES)**

```bash
sudo crm resource param ms-<AGResourceName> set required_synchronized_secondaries_to_commit <value>
```

in cui *AGResourceName* è il nome della risorsa configurata per il gruppo di disponibilità, e *valore* è 0, 1 o 2. Per impostarla sul valore predefinito di gestire il parametro Pacemaker, eseguire la stessa istruzione non prevede alcun valore.

Failover automatico di un gruppo di disponibilità è possibile quando vengono soddisfatte le condizioni seguenti:

-   Il database primario e la replica secondaria sono impostate allo spostamento dei dati sincrono.
-   Il database secondario ha uno stato di sincronizzazione (non in sincronizzazione), vale a dire che i due sono nello stesso punto dati.
-   Il tipo di cluster è impostato su External. Il failover automatico non è possibile eseguire con un tipo di cluster None.
-   Il `sequence_number` della replica secondaria che diventerà il database primario è il numero di sequenza più alto, in altre parole, la replica secondaria `sequence_number` corrisponde a quello di replica primaria originale.

Se vengono soddisfatte queste condizioni e i server che ospita la replica primaria non riesce, il gruppo di disponibilità verrà modificata la proprietà a una replica sincrona. Il comportamento per le repliche sincrone (di cui può esserci tre totale: una primaria e due repliche secondarie) può essere controllato ulteriormente tramite `required_synchronized_secondaries_to_commit`. Questo funziona con gruppi di disponibilità sia Windows che Linux, ma è configurato in modo completamente diverso. In Linux, il valore viene configurato automaticamente dal cluster nella risorsa del gruppo di disponibilità se stesso.

## <a name="configuration-only-replica-and-quorum"></a>Quorum e la replica di sola configurazione

Altra novità in [!INCLUDE[sssql17-md](../includes/sssql17-md.md)] a partire da CU1 tratta di una replica di sola configurazione. Poiché Pacemaker è diverso rispetto a un cluster WSFC, soprattutto quando si tratta del quorum e che richiedono STONITH, avere solo una configurazione a due nodi non funzionerà quando si tratta di un gruppo di disponibilità. Per un'istanza FCI, i meccanismi di quorum forniti da Pacemaker possono costituire un problemi, perché tutti arbitrato vincolante failover FCI avviene a livello di cluster. Per un gruppo di disponibilità, arbitraggio in Linux si verifica in [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], in cui tutti i metadati vengono archiviati. Si tratta di dove entra in gioco la replica di sola configurazione.

Senza altri elementi, potrebbe essere necessario un terzo nodo e almeno una replica sincronizzata. La replica di sola configurazione archivia la configurazione del gruppo di disponibilità nel database master, come le altre repliche nella configurazione del gruppo di disponibilità. La replica di sola configurazione non è i database utente che fanno parte del gruppo di disponibilità. I dati di configurazione vengono inviati in modo sincrono dal database primario. Questi dati di configurazione vengano quindi usati durante i failover, sia automatico o manuale.

Per un gruppo di disponibilità mantenere il quorum e abilita i failover automatici con un tipo di cluster External, uno deve:

-   Avere tre repliche sincrone ([!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)] solo); o
-   Avere due repliche (primarie e secondarie), oltre a una replica di sola configurazione.

I failover manuali possono verificarsi se usando External o None tipi per le configurazioni del gruppo di disponibilità di cluster. Anche se una replica di sola configurazione può essere configurata con un gruppo di disponibilità con un tipo di cluster None, non è consigliabile, dal momento che complica la distribuzione. Per tali configurazioni, modificare manualmente `required_synchronized_secondaries_to_commit` per avere un valore pari ad almeno 1, in modo che sia disponibile almeno una replica sincronizzata.

Una replica di sola configurazione può essere ospitata in qualsiasi edizione di [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], tra cui [!INCLUDE[ssexpress-md](../includes/ssexpress-md.md)]. Questo riduce al minimo i costi di licenza e garantisce il funzionamento con gruppi di disponibilità in [!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)]. Ciò significa che il terzo necessari server sufficiente soddisfare i requisiti minimi per [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], dal momento che non riceve il traffico delle transazioni utente per il gruppo di disponibilità.

Quando viene utilizzata una replica di sola configurazione, ha il comportamento seguente:

-   Per impostazione predefinita, `required_synchronized_secondaries_to_commit` è impostato su 0. Ciò può essere modificato manualmente su 1 se lo si desidera.
-   Se il database primario ha esito negativo e `required_synchronized_secondaries_to_commit` è 0, la replica secondaria diventeranno il nuovo database primario e disponibili per la lettura e scrittura. Se il valore è 1, si verificherà il failover automatico, ma non verrà accettate nuove transazioni fino a quando non è online l'altra replica.
-   Se una replica secondaria ha esito negativo e `required_synchronized_secondaries_to_commit` è 0, la replica primaria continua ad accettare transazioni, ma se il database primario non riesce a questo punto, non vi è alcuna protezione per i dati né failover possibili (manuale o automatico), poiché una replica secondaria non è disponibile.
-   Se le repliche di sola configurazione non riesce, il gruppo di disponibilità funzionerà normalmente, ma non è possibile eseguire alcun failover automatico.
-   Se una replica secondaria asincrona sia la replica di sola configurazione non riesce, il database primario non può accettare transazioni e non è disponibile una destinazione per la replica primaria non è possibile.

In CU1 c'è un bug noto alla registrazione nel file corosync.log generato tramite `mssql-server-ha`. Se una replica secondaria non è in grado di diventare il database primario a causa del numero di repliche necessarie disponibile, viene visualizzato il messaggio corrente "prevista la ricezione di numeri di sequenza 1 ma ricevuti solo 2. Non sono sufficienti le repliche sono in linea per alzare di livello in modo sicuro la replica locale." I numeri devono essere invertiti e dovrebbe risultare "prevedesse di ricevere i numeri di sequenza 2 ma ricevuta solo 1. Non sono sufficienti le repliche sono in linea per alzare di livello in modo sicuro la replica locale." 

## <a name="multiple-availability-groups"></a>Più gruppi di disponibilità 

È possibile creare più di un gruppo di disponibilità per ogni set di server o cluster Pacemaker. L'unica limitazione è le risorse di sistema. La proprietà del gruppo di disponibilità viene visualizzata dal master. Gruppi di disponibilità diversi possono essere di proprietà da nodi diversi; non tutti devono essere in esecuzione nello stesso nodo.

## <a name="drive-and-folder-location-for-databases"></a>Percorso di unità e la cartella per i database

Come nei gruppi di disponibilità basati su Windows, la struttura di cartelle e unità per i database utente che fanno parte di un gruppo di disponibilità deve essere identica. Ad esempio, se i database utente vengono `/var/opt/mssql/userdata` sul Server A, tale cartella stessa deve esistere nel Server B. L'unica eccezione è indicato nella sezione [interoperabilità con i gruppi di disponibilità basati su Windows e le repliche](#interoperability-with-windows-based-availability-groups-and-replicas).

## <a name="the-listener-under-linux"></a>Il listener in Linux

Il listener è una funzionalità facoltativa per un gruppo di disponibilità. Fornisce un singolo punto di ingresso per tutte le connessioni (lettura/scrittura per la replica primaria e/o repliche di sola lettura al database secondario) in modo che le applicazioni e gli utenti finali non è necessario sapere quali server ospita i dati. In un cluster WSFC, questa è la combinazione di una risorsa nome di rete e una risorsa IP, che viene quindi registrata nel dominio di Active Directory (se necessario) nonché DNS. In combinazione con la risorsa del gruppo di disponibilità stesso, fornisce tale astrazione. Per altre informazioni su un listener, vedere [listener, connettività Client e Failover dell'applicazione](../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md).

Il listener in Linux è configurato in modo diverso, ma la relativa funzionalità è lo stesso. Non è presente alcun concetto di una risorsa nome di rete in Pacemaker, e viene creato un oggetto in Active Directory Domain Services; è solo una risorsa di indirizzo IP creata in Pacemaker eseguibili su tutti i nodi. È necessario creare una voce associata alla risorsa IP per il listener nel servizio DNS con un "nome descrittivo". La risorsa IP per il listener sarà attiva solo sul server che ospita la replica primaria per tale gruppo di disponibilità.

Se Pacemaker è utilizzato e viene creata una risorsa indirizzo IP associato con il listener, esisterà una breve interruzione come l'indirizzo IP si arresta in un server e viene avviato in altro, se si tratta di failover automatico o manuale. Sebbene questo offra astrazione tramite la combinazione di un singolo nome e indirizzo IP, non maschera quella l'interruzione del servizio. Un'applicazione deve essere in grado di gestire la disconnessione facendo in modo che una sorta di funzionalità per rilevare questa situazione e ristabilire la connessione.

Tuttavia, la combinazione del nome DNS e indirizzo IP è ancora non sono sufficienti fornire tutte le funzionalità che fornisce un listener per un cluster WSFC, ad esempio di routing di sola lettura per le repliche secondarie. Quando si configura un gruppo di disponibilità, un "listener" ancora deve essere configurato [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. Ciò può essere visualizzato nella procedura guidata, nonché la sintassi Transact-SQL. Esistono due modi che ciò può essere configurato per il funzionamento anche in Windows:

-   Per un gruppo di disponibilità con un tipo di cluster External, l'indirizzo IP associato con il "listener" creati in [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] deve essere l'indirizzo IP della risorsa creata in Pacemaker.
-   Per un gruppo di disponibilità creato con un tipo di cluster None, usare l'indirizzo IP associato alla replica primaria.

L'istanza associata quindi l'indirizzo IP specificato diventa il coordinatore per elementi quali le richieste di routine di sola lettura da applicazioni.

## <a name="interoperability-with-windows-based-availability-groups-and-replicas"></a>Interoperabilità con le repliche e gruppi di disponibilità basati su Windows 

Un gruppo di disponibilità che è di tipo cluster External o quella più cluster WSFC non può contenere le repliche tra piattaforme. Ciò è vero che il gruppo di disponibilità sia [!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)] o [!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)]. Ciò significa che in una configurazione del gruppo di disponibilità tradizionali con un cluster sottostante, non può essere una replica in un cluster WSFC e l'altro in Linux con Pacemaker.

Un gruppo di disponibilità con un tipo di cluster NONE può avere le relative repliche superano i limiti del sistema operativo, pertanto potrebbe verificarsi entrambe le repliche basato su Linux e Windows nello stesso gruppo di disponibilità. Come illustrato di seguito in cui la replica primaria è basato su Windows, mentre il database secondario è su una delle distribuzioni Linux.

![Ibrida None](./media/sql-server-linux-availability-group-overview/image1.png)

Un gruppo di disponibilità distribuito può coinvolgere anche i limiti del sistema operativo. I gruppi di disponibilità sottostanti sono associati dalle regole per la relativa configurazione, ad esempio quello configurato con l'esterno da solo Linux, ma è stato possibile configurare il gruppo di disponibilità è unita in join alla usando un cluster WSFC. Si consideri l'esempio seguente:

![Gruppo di disponibilità del database di distribuzione ibrida](./media/sql-server-linux-availability-group-overview/image2.png)

<!-- Distributed AGs are also supported for upgrades from [!INCLUDE[sssql15-md](../includes/sssql15-md.md)] to [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]. For more information on how to achieve this, see [the article "x"].

If using automatic seeding with a distributed availability group that crosses OSes, it can handle the differences in folder structure. How this works is described in [the documentation for automatic seeding].
-->
 
## <a name="next-steps"></a>Passaggi successivi
[Configurare il gruppo di disponibilità per SQL Server in Linux](sql-server-linux-availability-group-configure-ha.md)

[Configurare il gruppo di disponibilità con scalabilità in lettura per SQL Server in Linux](sql-server-linux-availability-group-configure-rs.md)

[Aggiungere il gruppo di disponibilità risorsa Cluster in RHEL](sql-server-linux-availability-group-cluster-rhel.md)

[Aggiungere il gruppo di disponibilità risorsa Cluster in SLES](sql-server-linux-availability-group-cluster-sles.md)

[Aggiungere il gruppo di disponibilità risorsa Cluster in Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md)

[Configurare un gruppo di disponibilità multipiattaforma](sql-server-linux-availability-group-cross-platform.md)

