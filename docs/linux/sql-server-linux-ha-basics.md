---
title: Nozioni fondamentali sulla disponibilità di SQL Server per le distribuzioni di Linux | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 11/27/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 4e42088227e22f6368426b9c4e8dc8134dbb49d7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66719366"
---
# <a name="sql-server-availability-basics-for-linux-deployments"></a>Nozioni fondamentali sulla disponibilità di SQL Server per le distribuzioni di Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

A partire [!INCLUDE[sssql17-md](../includes/sssql17-md.md)], [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] è supportato in Linux e Windows. Ad esempio basato su Windows [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] distribuzioni, [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] database e istanze devono essere a disponibilità elevata in Linux. Questo articolo illustra gli aspetti tecnici di pianificazione e distribuzione a disponibilità elevata basato su Linux [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] i database e istanze, nonché alcune delle differenze di installazioni basate su Windows. In quanto [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] potrebbero essere nuovi per i professionisti di Linux e Linux potrebbero essere nuovi per [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] professionisti, l'articolo in alcuni casi vengono introdotti i concetti che potrebbero essere familiare ad alcuni e poco familiare ad altri utenti.

## <a name="includessnoversion-mdincludesssnoversion-mdmd-availability-options-for-linux-deployments"></a>[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] opzioni di disponibilità per le distribuzioni di Linux
Oltre ai backup e ripristino, le stesse funzionalità di disponibilità di tre sono disponibili in Linux per le distribuzioni basate su Windows:
-   Gruppi di disponibilità Always On (gruppi di disponibilità)
-   Istanze del Cluster di Failover (FCI) Always On
-   [Log shipping](sql-server-linux-use-log-shipping.md)

In Windows, le istanze FCI richiedono sempre un cluster di failover di Windows Server (WSFC) sottostante. A seconda dello scenario di distribuzione, un gruppo di disponibilità in genere non richiede che un cluster WSFC sottostante, con l'eccezione in corso la nuova variante in [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]. Un cluster WSFC inesistente in Linux. Clustering di implementazione in Linux è descritto nella sezione [Pacemaker per cluster di failover e gruppi di disponibilità AlwaysOn di istanze Linux](#pacemaker-for-always-on-availability-groups-and-failover-cluster-instances-on-linux).

## <a name="a-quick-linux-primer"></a>Nozioni di base Linux
Anche se alcune installazioni di Linux potrebbero essere installati con un'interfaccia, la maggior parte non lo sono, vale a dire che quasi tutti gli oggetti a livello del sistema operativo viene effettuato tramite riga di comando. Il termine comune per questa riga di comando nel mondo Linux è un' *shell di bash*.

In Linux, molti comandi devono essere eseguite con privilegi elevati, analogamente a molte operazioni devono essere eseguite in Windows Server come amministratore. Esistono due metodi principali per l'esecuzione con privilegi elevati:
1. Eseguire nel contesto dell'utente corretto. Per modificare in un altro utente, usare il comando `su`. Se `su` viene eseguita in modo autonomo senza un nome utente, purché si conosca la password, sarà ora presente in una shell come *radice*.
   
2. I più comuni e sicurezza cosciente per eseguire operazioni consiste nell'utilizzo `sudo` prima di eseguire alcuna operazione. Molti degli esempi in questo articolo usano `sudo`.

Alcuni comandi comuni, ognuna delle quali dispone di diversi parametri e opzioni che possono essere analizzate in linea:
-   `cd` -modificare la directory
-   `chmod` -modificare le autorizzazioni di un file o directory
-   `chown` -modificare la proprietà di un file o directory
-   `ls` -visualizzare il contenuto di una directory
-   `mkdir` -creare una cartella (directory) in un'unità
-   `mv` -spostare un file da una posizione a un'altra
-   `ps` -Mostra tutti i processi di lavoro
-   `rm` -eliminare un file in un server locale
-   `rmdir` -eliminare una cartella (directory)
-   `systemctl` -avviare, arrestare o attivare i servizi
-   Comandi dell'editor di testo. In Linux, sono disponibili diverse opzioni di editor di testo, ad esempio emacs e vi.

## <a name="common-tasks-for-availability-configurations-of-includessnoversion-mdincludesssnoversion-mdmd-on-linux"></a>Attività comuni per le configurazioni con disponibilità del [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] in Linux
In questa sezione vengono descritte attività comuni a tutti i basati su Linux [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] le distribuzioni.

### <a name="ensure-that-files-can-be-copied"></a>Assicurarsi che i file possono essere copiati
Copia i file da un server a un'altra è un'attività che gli utenti che usano [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] in Linux deve essere in grado di eseguire. Questa attività è molto importante per le configurazioni del gruppo di disponibilità.

Ad esempio problemi di autorizzazione può essere presente in Linux, nonché nelle installazioni dei componenti basati su Windows. Tuttavia, chi ha familiarità con la procedura per copiare da server a server in Windows potrebbero non avere familiarità con come questa operazione viene eseguita in Linux. Un metodo comune consiste nell'usare l'utilità della riga di comando `scp`, che è l'acronimo di copia sicuro. Dietro le quinte, `scp` Usa OpenSSH. SSH è l'acronimo di shell sicura. A seconda della distribuzione di Linux, potrebbe non essere installato OpenSSH stesso. In caso contrario, deve essere installato per primo OpenSSH. Per altre informazioni sulla configurazione di OpenSSH, vedere le informazioni visitando i collegamenti seguenti per ogni distribuzione:
-   [Red Hat Enterprise Linux (RHEL)](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/deployment_guide/ch-openssh)
-   [SUSE Linux Enterprise Server (SLES)](https://en.opensuse.org/SDB:Configure_openSSH)
-   [Ubuntu](https://help.ubuntu.com/community/SSH/OpenSSH/Configuring)

Quando si usa `scp`, è necessario fornire le credenziali del server se non è l'origine o destinazione. Ad esempio, l'uso

```bash
scp MyAGCert.cer username@servername:/folder/subfolder
```

Copia il file MyAGCert.cer nella cartella specificata in altro server. Si noti che è necessario avere autorizzazioni - ed eventualmente la proprietà - del file da copiare, quindi `chown` potrebbe essere necessario anche essere usati prima della copia. Sul lato ricevente, allo stesso modo, l'utente deve accedere per modificare il file. Ad esempio, per ripristinare il file certificato, il `mssql` utente deve essere in grado di accedervi.

Samba, ovvero la variante Linux del (SMB) server message block, consente inoltre di creare le condivisioni a cui accede percorsi UNC, ad esempio `\\SERVERNAME\SHARE`. Per altre informazioni sulla configurazione Samba, vedere le informazioni visitando i collegamenti seguenti per ogni distribuzione:
-   [RHEL](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Confined_Services/chap-Managing_Confined_Services-Samba.html)
-   [SLES](https://www.suse.com/documentation/sles11/book_sle_admin/data/cha_samba.html)
-   [Ubuntu](https://help.ubuntu.com/community/Samba)

Consente inoltre alle condivisioni SMB basate su Windows; Non è necessario essere basato su Linux, purché la parte client di Samba sia configurata correttamente nei server Linux che ospita le condivisioni SMB [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] e la condivisione disponga dell'accesso a destra. Per quelle in un ambiente misto, sarebbe un modo per sfruttare l'infrastruttura esistente per basato su Linux [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] le distribuzioni.

Un aspetto importante è che la versione di Samba distribuito deve essere compatibile con SMB 3.0. Quando è stato aggiunto il supporto SMB in [!INCLUDE[sssql11-md](../includes/sssql11-md.md)], è necessaria tutte le condivisioni per supportare SMB 3.0. Se si usa Samba per la condivisione e non Windows Server, deve usare la condivisione Samba basata Samba 4.0 o versione successiva e idealmente 4.3 o versione successiva, che supporta SMB 3.1.1. È un'ottima fonte di informazioni su SMB e Linux [SMB3 in Samba](https://events.linuxfoundation.org/sites/events/files/slides/smb3-in-samba.pr__0.pdf).

Infine, è possibile usare una condivisione di file system (NFS) di rete. Uso di NFS non è un'opzione in distribuzioni basate su Windows di [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]e può essere usato solo per le distribuzioni basate su Linux.

### <a name="configure-the-firewall"></a>Configurare il firewall
Analogamente a Windows, distribuzioni Linux hanno un firewall incorporato. Se l'azienda Usa un firewall esterno per i server, disabilitare il firewall in Linux può essere accettabile. Tuttavia, indipendentemente dal fatto in cui è abilitato il firewall, porte devono essere aperta. La tabella seguente illustra le porte comuni necessari per la disponibilità elevata [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] le distribuzioni in Linux.

| Numero di porta | Tipo     | Description                                                                                                                 |
|-------------|----------|-----------------------------------------------------------------------------------------------------------------------------|
| 111         | TCP/UDP  | NFS - `rpcbind/sunrpc`                                                                                                    |
| 135         | TCP      | Samba (se usati) - Mapper di endpoint                                                                                          |
| 137         | UDP      | Samba (se usati) - servizio nomi NetBIOS                                                                                      |
| 138         | UDP      | Samba (se usati) - datagrammi NetBIOS                                                                                          |
| 139         | TCP      | Samba (se usati) - sessione NetBIOS                                                                                           |
| 445         | TCP      | Samba (se usati) - SMB su TCP                                                                                              |
| 1433        | TCP      | [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] -porta; predefinita Se si desidera, è possibile modificare con `mssql-conf set network.tcpport <portnumber>`                       |
| 2049        | TCP, UDP | NFS (se usati)                                                                                                               |
| 2224        | TCP      | Pacemaker - utilizzato da `pcsd`                                                                                                |
| 3121        | TCP      | Pacemaker - richiesto se sono presenti nodi remoti Pacemaker                                                                    |
| 3260        | TCP      | iSCSI Initiator (se usati) - può essere modificata `/etc/iscsi/iscsid.config` (RHEL), ma deve corrispondere a porta di destinazione iSCSI |
| 5022        | TCP      | [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] -usata per un endpoint del gruppo di disponibilità; porta predefinita può essere modificato durante la creazione dell'endpoint                                |
| 5403        | TCP      | Pacemaker                                                                                                                   |
| 5404        | UDP      | Pacemaker - richiesto dal Corosync se tramite multicast UDP                                                                     |
| 5405        | UDP      | Pacemaker - richiesto da Corosync                                                                                            |
| 21064       | TCP      | Pacemaker - necessari per le risorse usando DLM                                                                                 |
| Variabile    | TCP      | Porta dell'endpoint del gruppo di disponibilità; impostazione predefinita è la 5022                                                                                           |
| Variabile    | TCP      | La porta per NFS - `LOCKD_TCPPORT` (disponibili in `/etc/sysconfig/nfs` in RHEL)                                              |
| Variabile    | UDP      | La porta per NFS - `LOCKD_UDPPORT` (disponibili in `/etc/sysconfig/nfs` in RHEL)                                              |
| Variabile    | TCP/UDP  | La porta per NFS - `MOUNTD_PORT` (disponibili in `/etc/sysconfig/nfs` in RHEL)                                                |
| Variabile    | TCP/UDP  | La porta per NFS - `STATD_PORT` (disponibili in `/etc/sysconfig/nfs` in RHEL)                                                 |

Per altre porte che possono essere usate da Samba, vedere [uso delle porte Samba](https://wiki.samba.org/index.php/Samba_Port_Usage).

Al contrario, il nome del servizio in Linux può essere aggiunto anche come un'eccezione anziché sulla porta; ad esempio, `high-availability` per Pacemaker. Se questa è la direzione in cui che si vuole proseguire, fare riferimento in base alla distribuzione per i nomi. In RHEL, ad esempio, il comando per aggiungere in Pacemaker è

```bash
sudo firewall-cmd --permanent --add-service=high-availability
```

**Documentazione del firewall:**
-   [RHEL](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/high_availability_add-on_reference/s1-firewalls-haar)
-   [SLES](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html)

### <a name="install-includessnoversion-mdincludesssnoversion-mdmd-packages-for-availability"></a>Installare [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] pacchetti per la disponibilità
In un Windows basato su [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] installazione, alcuni componenti vengono installati anche in un'installazione del motore di base, mentre altri no. In Linux, solo il [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] motore viene installato come parte del processo di installazione. Tutto il resto è facoltativo. Per la disponibilità elevata [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] istanze in Linux, è consigliabile installare due pacchetti con [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]: [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Agent (*mssql-server-agent*) e il pacchetto di disponibilità elevata (HA) (*mssql-server-ha*). Sebbene [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] agente è tecnicamente facoltativo, ma [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]dell'utilità di pianificazione per i processi ed è richiesto dal log shipping, pertanto, è consigliabile installare. Nelle installazioni dei componenti basati su Windows, [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] agente non è facoltativo.

>[!NOTE]
>Per chi non ha esperienza a [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] agente è [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]dell'utilità di pianificazione di processi predefinite. È un modo comune per gli amministratori di database pianificare operazioni quali backup e altre [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] manutenzione. A differenza di un'installazione basata su Windows di [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] in cui [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Agent è un servizio completamente diverso, in Linux [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] agente viene eseguito nel contesto di [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] stesso.

Quando i gruppi di disponibilità o FCI sono configurate in una configurazione basata su Windows, sono compatibile con cluster. Compatibilità con cluster significa che [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] dispone di risorse specifico DLL che un cluster WSFC conosce (file sqagtres. dll e sqsrvres.dll per le istanze FCI, hadrres. dll per gruppi di disponibilità) e vengono utilizzati per il cluster WSFC per garantire che il [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] funzionalità cluster sia attivo, in esecuzione, e funzioni correttamente. Poiché il servizio cluster esterno non è solo a [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] ma Linux se stessa, Microsoft dovevano l'equivalente di una DLL di risorse per le distribuzioni del gruppo di disponibilità basati su Linux e infrastruttura di classificazione file di codice. Questo è il *mssql-server-disponibilità elevata* creare un pacchetto, noto anche come il [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] agente delle risorse per Pacemaker. Per installare il *mssql-server-disponibilità elevata* del pacchetto, vedere [installare i pacchetti a disponibilità elevata e SQL Server Agent](sql-server-linux-deploy-pacemaker-cluster.md#install-the-sql-server-ha-and-sql-server-agent-packages).

Gli altri pacchetti facoltativi per [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] in Linux [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] ricerca Full-Text (*mssql-server-fts*) e [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Integration Services (*mssql-server-è*), non sono obbligatorio per la disponibilità elevata, per un'istanza FCI o un gruppo di disponibilità.

## <a name="pacemaker-for-always-on-availability-groups-and-failover-cluster-instances-on-linux"></a>Pacemaker per gruppi di disponibilità AlwaysOn e le istanze del cluster di failover in Linux
Come in precedenza indicato, l'unico meccanismo clustering attualmente supportato da Microsoft per gruppi di disponibilità e le istanze FCI è Pacemaker con Corosync. Questa sezione descrive le informazioni di base per comprendere la soluzione, nonché come pianificare e distribuire per [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] configurazioni.

### <a name="ha-add-onextension-basics"></a>Nozioni di base componenti pratici/estensione a disponibilità elevata
Tutte le distribuzioni supportate attualmente spedire un'elevata disponibilità componenti-pratici/estensione, che si basa su di Pacemaker clustering dello stack. Questo stack include due componenti principali: Corosync e pacemaker. Tutti i componenti dello stack sono:
-   Pacemaker - di base del clustering di componente, che esegue operazioni come coordinata tra i computer in cluster.
-   Corosync - un framework e un set di API che fornisce elementi come quorum, la possibilità di riavvio non è riuscito dei processi e così via.
-   libQB - offre elementi quali la registrazione.
-   Agente delle risorse - funzionalità specifica fornita in modo che un'applicazione può essere integrato con Pacemaker.
-   Limite agent - script/funzionalità di isolare i nodi e gestirli se si verificano problemi.
    
> [!NOTE]
> Lo stack di cluster è noto come Pacemaker nel mondo Linux.

Questa soluzione è in qualche modo simile, ma in molti modi diversi dalla distribuzione le configurazioni in cluster usando Windows. In Windows, il modulo disponibilità del clustering, chiamata di un cluster di failover di Windows Server (WSFC) è incorporato nel sistema operativo e la funzionalità che consente la creazione di un cluster WSFC, clustering di failover, è disabilitato per impostazione predefinita. In Windows, gruppi di disponibilità e le istanze FCI vengono compilate in un cluster WSFC e condividere una stretta integrazione a causa di specifici DLL della risorsa che viene fornito da [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. Questa soluzione fortemente accoppiata è possibile in generale le perché è tutto da un unico fornitore.

![](./media/sql-server-linux-ha-basics/image1.png)

In Linux, mentre ogni distribuzione supportata è disponibile, Pacemaker ogni distribuzione può personalizzare e dispongono di versioni e implementazioni leggermente diverse. Alcune delle differenze si rifletteranno nelle istruzioni in questo articolo. Il livello di clustering è open source, in modo che anche se fornito con le distribuzioni, non è strettamente integrato nello stesso modo un cluster WSFC è in Windows. Questo è il motivo per cui Microsoft fornisce *mssql-server-disponibilità elevata*, in modo che [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] e lo stack di Pacemaker può fornire vicino al, ma non esattamente uguali, una migliore esperienza per gruppi di disponibilità e le istanze FCI come in Windows.

Per una documentazione completa su Pacemaker, tra cui una spiegazione più approfondita delle novità tutti gli elementi con informazioni di riferimento complete, per RHEL e SLES:
-   [RHEL](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/ch-overview-HAAR.html)
-   [SLES](https://www.suse.com/documentation/sle_ha/book_sleha/data/book_sleha.html)

Ubuntu non dispone di una Guida per la disponibilità.

Per altre informazioni sull'intero stack, vedere anche ufficiale [pagina della documentazione di Pacemaker](https://clusterlabs.org/doc/) sul sito Clusterlabs.

### <a name="pacemaker-concepts-and-terminology"></a>Pacemaker concetti e terminologia
Questa sezione illustra i concetti e terminologia per un'implementazione di Pacemaker comuni.

#### <a name="node"></a>Node
Un nodo è un server che fanno parte del cluster. Un cluster Pacemaker in modalità nativa supporta un massimo di 16 nodi. Questo numero può essere superato se Corosync non è in esecuzione nei nodi aggiuntivi, ma è necessaria per Corosync [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. Pertanto, il numero massimo di nodi per qualsiasi può avere un cluster [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]-configurazione basata su è 16, questo è il limite di Pacemaker e non ha nulla a che fare con le limitazioni massime per i gruppi di disponibilità o FCI sottopone [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. 

#### <a name="resource"></a>Risorsa
Un cluster WSFC sia un cluster Pacemaker prevedono il concetto di una risorsa. Una risorsa è una funzionalità specifica cui viene eseguito nel contesto del cluster, ad esempio un disco o un indirizzo IP. Ad esempio, in Pacemaker risorse di infrastruttura di classificazione file e del gruppo di disponibilità possono essere create. Questo non è simile a ciò che avviene in un cluster WSFC, in cui vengono visualizzate una [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] risorsa per sia un'istanza FCI o un gruppo di disponibilità quando si configura un gruppo di disponibilità, ma non è esattamente uguale a causa di differenze sottostanti nelle modalità [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] si integra con Pacemaker.

Pacemaker dispone di risorse standard e clone. Le risorse di clonazione sono quelle che vengono eseguiti simultaneamente in tutti i nodi. Un esempio sarebbe un indirizzo IP che viene eseguito su più nodi per scopi di bilanciamento del carico. Qualsiasi risorsa che viene creato per le istanze FCI utilizza una risorsa standard, poiché un solo nodo può ospitare un'istanza FCI in qualsiasi momento.

Quando viene creato un gruppo di disponibilità, richiede un tipo speciale di una risorsa clone denominata una risorsa più stata. Mentre un gruppo di disponibilità ha solo una replica primaria, il gruppo di disponibilità è in esecuzione in tutti i nodi che è configurato per funzionare su e può consentire operazioni quali accesso di sola lettura. Poiché si tratta di un utilizzo "attivo" del nodo, le risorse hanno il concetto di due stati: master e slave. Per altre informazioni, vedere [risorse più state: Le risorse con più modalità](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Configuring_the_Red_Hat_High_Availability_Add-On_with_Pacemaker/s1-multistateresource-HAAR.html).

#### <a name="resource-groupssets"></a>I gruppi o set di risorse
Analogamente ai ruoli in un cluster WSFC, un cluster Pacemaker è il concetto di un gruppo di risorse. Un gruppo di risorse (definito set di SLES) è una raccolta di risorse che funzionano insieme e possono eseguire il failover da un nodo a altro come singola unità. Gruppi di risorse non possono contenere le risorse che sono configurate come  primaria/secondaria; di conseguenza, non è possibile usare per gruppi di disponibilità. Mentre un gruppo di risorse può essere usato per le istanze FCI, non è in genere una configurazione consigliata.

#### <a name="constraints"></a>Vincoli
I cluster Wsfc dispone di diversi parametri per le risorse, nonché elementi come dipendenze, che indicano il cluster WSFC di una relazione padre/figlio tra due diverse risorse. Una dipendenza è solo una regola che informa il cluster WSFC risorsa a cui deve essere online prima di tutto.

Un cluster Pacemaker non prevedono il concetto di dipendenze, ma sono presenti vincoli. Esistono tre tipi di vincoli: con più sedi, la posizione e ordinamento.
-   Consente di applicare un vincolo di condivisione percorso se due risorse devono essere in esecuzione nello stesso nodo.
-   Un vincolo di percorso indica a del cluster Pacemaker in cui una risorsa può (o possibile) eseguire.
-   Un vincolo di ordinamento indica l'ordine in cui è consigliabile iniziare le risorse a del cluster Pacemaker.

> [!NOTE]
> I vincoli di condivisione del percorso non sono necessari per le risorse in un gruppo di risorse, perché tutti questi vengono interpretati come unità singola.

#### <a name="quorum-fence-agents-and-stonith"></a>Quorum, gli agenti di limite e STONITH
Quorum in Pacemaker è in qualche modo simile a un cluster WSFC concettualmente. Lo scopo del meccanismo del quorum del cluster è garantire che il cluster rimane attivo e in esecuzione. Un cluster WSFC sia i componenti aggiuntivi a disponibilità elevata per le distribuzioni di Linux hanno il concetto di voto, in cui ogni nodo viene conteggiato ai fini di quorum. Si desidera ripristinare una maggioranza dei voti, in caso contrario, nella peggiore delle eventualità, il cluster verrà arrestato.

A differenza di un cluster WSFC, non sono presenti risorse di controllo del mirroring per lavorare con quorum. Ad esempio un cluster WSFC, l'obiettivo è mantenere il numero degli elettori dispari. Configurazione del quorum ha diverse considerazioni per gruppi di disponibilità di istanze FCI.

I cluster Wsfc monitorare lo stato dei nodi che fanno parte e gestirli quando si verifica un problema. Nelle versioni successive di Wsfc offrono funzionalità quali la messa in quarantena un nodo che è un comportamento non corretto o non disponibile (nodo non è presente, comunicazione di rete è verso il basso e così via). Sul lato di Linux, questo tipo di funzionalità viene fornito da un agente di isolamento. Il concetto è detto a volte fencing. Tuttavia, questi agenti limite siano a livello generale per la distribuzione e spesso forniti da fornitori di hardware e alcuni fornitori di software, ad esempio agli utenti che forniscono gli hypervisor. Ad esempio, VMware fornisce un agente di isolamento che può essere utilizzato per le macchine virtuali Linux virtualizzati con vSphere.

Quorum e conflitti di valori equivalenti in un altro concetto chiamato STONITH o Shoot the Other Node in Head. STONITH è necessario disporre di un cluster Pacemaker supportate in tutte le distribuzioni di Linux. Per altre informazioni, vedere [conflitti in un Cluster a disponibilità elevata Red Hat](https://access.redhat.com/solutions/15575) (RHEL).

#### <a name="corosyncconf"></a>corosync.conf
Il `corosync.conf` file contiene la configurazione del cluster. Si trova in `/etc/corosync`. Durante lo svolgimento delle normali operazioni quotidiane, questo file non deve avere mai essere modificati se il cluster sia configurato correttamente.

#### <a name="cluster-log-location"></a>Percorso del registro cluster
Percorsi dei log per i cluster Pacemaker differiscono a seconda della distribuzione.
-   RHEL e SLES: `/var/log/cluster/corosync.log`
-   Ubuntu - `/var/log/corosync/corosync.log`

Per modificare il percorso di registrazione predefinito, modificare `corosync.conf`.

## <a name="plan-pacemaker-clusters-for-includessnoversion-mdincludesssnoversion-mdmd"></a>Pianificare cluster Pacemaker per [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]
Questa sezione illustra le considerazioni di pianificazione per un cluster Pacemaker.

### <a name="virtualizing-linux-based-pacemaker-clusters-for-includessnoversion-mdincludesssnoversion-mdmd"></a>Per i cluster Pacemaker virtualizzazione basati su Linux [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]
Utilizzo delle macchine virtuali per la distribuzione basati su Linux [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] le distribuzioni per gruppi di disponibilità e le istanze FCI è coperto dalle stesse regole per le relative controparti basati su Windows. È un set di regole per il supporto di base virtualizzata [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] fornite da Microsoft nelle distribuzioni [956893 KB di supporto Microsoft](https://support.microsoft.com/help/956893/support-policy-for-microsoft-sql-server-products-that-are-running-in-a-hardware-virtualization-environment). Gli hypervisor diversi, ad esempio Microsoft Hyper-V e VMware ESXi potrebbero hanno varianze diverse per di più, a causa di differenze tra le piattaforme autonomamente.

Quando si tratta di gruppi di disponibilità e le istanze FCI in virtualization, assicurarsi che Microsoft anti-affinità viene impostata per i nodi di un determinato cluster Pacemaker. Quando è configurato per la disponibilità elevata in una configurazione del gruppo di disponibilità o FCI, le macchine virtuali che ospitano [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] mai deve essere in esecuzione nello stesso host hypervisor. Ad esempio, se viene distribuita un'infrastruttura di classificazione file due nodi, si dovranno essere *almeno* tre host hypervisor in modo che in una posizione per una delle VM che ospita un nodo per passare in caso di un errore dell'host, soprattutto se le funzionalità come Live Migrazione o vMotion.

Per informazioni più specifiche, consultare:
-   Documentazione di Hyper-V - [tramite Clustering Guest per la disponibilità elevata](https://technet.microsoft.com/library/dn440540(v=ws.11).aspx)
-   White paper, scritti per le distribuzioni basate su Windows, ma la maggior parte dei concetti ancora applicare, - [pianificazione della disponibilità elevata, SQL Server distribuzioni di importanza strategica con VMware vSphere](https://www.vmware.com/content/dam/digitalmarketing/vmware/en/pdf/solutions/vmware-vsphere-highly-available-mission-critical-sql-server-deployments.pdf)

>[!NOTE]
>RHEL con un cluster Pacemaker con STONITH non è ancora supportato da Hyper-V. Fino a quando non supportata, per altre informazioni e aggiornamenti, consultare [criteri di supporto per i cluster a disponibilità elevata RHEL](https://access.redhat.com/articles/29440#3physical_host_mixing).

### <a name="networking"></a>Funzionalità di rete
A differenza di un cluster WSFC, Pacemaker non richiede un nome dedicato o almeno un indirizzo IP dedicato per il cluster Pacemaker. Gruppi di disponibilità e le istanze FCI richiede gli indirizzi IP (vedere la documentazione relativa a ciascuno di essi per ulteriori informazioni), ma non i nomi, poiché non sono presenti risorse nome di rete. SLES consente la configurazione di un indirizzo IP per finalità amministrative, ma non obbligatorio, come illustrato nella [creare il cluster Pacemaker](sql-server-linux-deploy-pacemaker-cluster.md#create).

Ad esempio un cluster WSFC, Pacemaker preferisce con ridondanza della rete, vale a dire le schede di rete distinto (schede di rete o pNICs per computer fisico) avere singoli indirizzi IP. In termini di configurazione del cluster, ogni indirizzo IP avrebbe ciò che è noto come il proprio anello. Tuttavia, come con i cluster Wsfc oggi, molte implementazioni sono virtualizzate o nel cloud pubblico in cui è presente realmente una sola virtualizzato NIC (vNIC) presentato al server. Se tutti i pNICs e Vnic sono connessi allo stesso commutatore fisico o virtuale, non è nessuna vera ridondanza a livello di rete, in modo che la configurazione di più schede di rete è un po' di un effetto ottico alla macchina virtuale. La ridondanza di rete viene generalmente compilata in hypervisor per le distribuzioni virtualizzate e sicuramente è incorporata nel cloud pubblico.

Una differenza con più schede di rete e Pacemaker rispetto a un cluster WSFC è che Pacemaker consente a più indirizzi IP nella stessa subnet, mentre non le supporta un cluster WSFC. Per altre informazioni su più subnet e i cluster Linux, vedere l'articolo [configurare più subnet](sql-server-linux-configure-multiple-subnet.md).

### <a name="quorum-and-stonith"></a>Quorum e quorum di STONITH
Configurazione del quorum e i requisiti sono relative alle distribuzioni del gruppo di disponibilità o FCI specifici di [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)].

STONITH è obbligatorio per un cluster Pacemaker supportate. Usare la documentazione dalla distribuzione di configurare STONITH. Ad esempio si trova [basato sull'archiviazione Fencing](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_storage_protect_fencing.html) per SLES. È anche disponibile un agente STONITH per i server VMware vCenter per soluzioni basate su ESXI. Per altre informazioni, vedere [Stonith plug-in di agente per VMWare VM VCenter SOAP recinzioni (Unofficial)](https://github.com/olafrv/fence_vmware_soap).

> [!NOTE]
> Al momento della stesura di questo articolo, Hyper-V non è una soluzione di STONITH. Questo vale per distribuzioni locali e influisce anche sulle distribuzioni basate su Azure Pacemaker con alcune distribuzioni, ad esempio RHEL.

### <a name="interoperability"></a>Interoperabilità
Questa sezione illustra come un cluster basato su Linux può interagire con un cluster WSFC o con altre distribuzioni di Linux.

#### <a name="wsfc"></a>WSFC
Attualmente, non è possibile dirette per un cluster WSFC e un cluster Pacemaker essere utilizzati insieme. Ciò significa che non è possibile creare un gruppo di disponibilità o FCI che funziona in un cluster WSFC e Pacemaker. Tuttavia, esistono due soluzioni di interoperabilità, che sono progettati per gruppi di disponibilità. L'unico modo di che un'istanza FCI può far parte di una configurazione cross-platform è se è inclusa come un'istanza in uno di questi due scenari:
-   Un gruppo di disponibilità con un tipo di cluster None. Per altre informazioni, vedere il Windows [documentazione dei gruppi di disponibilità](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md).
-   Un gruppo di disponibilità distribuito, che è un tipo speciale di gruppo di disponibilità che consente a due gruppi di disponibilità diversi per la configurazione come proprio gruppo di disponibilità. Per altre informazioni su gruppi di disponibilità distribuiti, vedere la documentazione [gruppi di disponibilità distribuiti](../database-engine/availability-groups/windows/distributed-availability-groups.md).

#### <a name="other-linux-distributions"></a>Altre distribuzioni di Linux
In Linux, tutti i nodi di un cluster Pacemaker devono essere nella stessa distribuzione. Ad esempio, ciò significa che un nodo RHEL non può essere parte di un cluster Pacemaker con un nodo SLES. Il motivo principale per questo oggetto è stato indicato in precedenza: le distribuzioni possono avere versioni diverse e la funzionalità di cose potrebbero non funzionare correttamente. Combinazione di distribuzioni con la stessa storia come combinare i cluster Wsfc e Linux: non utilizza alcuno o gruppi di disponibilità distribuito.

## <a name="next-steps"></a>Passaggi successivi
[Distribuire un cluster Pacemaker per SQL Server in Linux](sql-server-linux-deploy-pacemaker-cluster.md)
