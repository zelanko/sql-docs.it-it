---
title: Nozioni fondamentali sulla disponibilità di SQL Server per le distribuzioni Linux
description: ''
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 11/27/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: d597033e6ad09a735e621518883cedda6bef29a2
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/19/2019
ms.locfileid: "75243592"
---
# <a name="sql-server-availability-basics-for-linux-deployments"></a>Nozioni fondamentali sulla disponibilità di SQL Server per le distribuzioni Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

A partire da [!INCLUDE[sssql17-md](../includes/sssql17-md.md)], [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] è supportato sia in Linux che in Windows. Come nelle distribuzioni di [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] basate su Windows, i database e le istanze di [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] devono garantire la disponibilità elevata anche in Linux. Questo articolo illustra gli aspetti tecnici della pianificazione e della distribuzione di database e istanze di [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] basate su Linux a disponibilità elevata, oltre ad alcune delle differenze rispetto alle installazioni basate su Windows. Poiché i professionisti Linux potrebbero non avere familiarità con [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] e i professionisti [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] potrebbero non avere familiarità con Linux, l'articolo introduce a volte concetti che potrebbero essere più noti ad alcuni e meno ad altri.

## <a name="includessnoversion-mdincludesssnoversion-mdmd-availability-options-for-linux-deployments"></a>Opzioni di disponibilità di [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] per le distribuzioni Linux
Oltre al backup e al ripristino, in Linux sono presenti le stesse tre funzionalità di disponibilità delle distribuzioni basate su Windows:
-   Gruppi di disponibilità Always On
-   Istanze del cluster di failover Always On
-   [Log shipping](sql-server-linux-use-log-shipping.md)

In Windows le istanze del cluster di failover richiedono sempre un cluster WSFC (Windows Server Failover Cluster) sottostante. A seconda dello scenario di distribuzione, un gruppo di disponibilità richiede in genere un cluster WSFC sottostante, con l'eccezione della nuova variante None in [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]. Un cluster WSFC non esiste in Linux. L'implementazione del clustering viene illustrata nella sezione [Pacemaker per i gruppi di disponibilità Always On e le istanze del cluster di failover in Linux](#pacemaker-for-always-on-availability-groups-and-failover-cluster-instances-on-linux).

## <a name="a-quick-linux-primer"></a>Introduzione rapida A Linux
Nonostante alcune installazioni di Linux possano avere un'interfaccia, la maggior parte di esse non ne dispone e quindi quasi tutte le operazioni a livello del sistema operativo vengono eseguite tramite la riga di comando. Il termine comune per indicare la riga di comando in ambito Linux è *shell Bash*.

In Linux è necessario eseguire molti comandi con privilegi elevati, così come in Windows Server molte operazioni devono essere eseguite da un amministratore. Esistono due metodi principali per eseguire i comandi con privilegi elevati:
1. Eseguirli nel contesto dell'utente appropriato. Per passare a un utente diverso, usare il comando `su`. Se `su` viene eseguito senza un nome utente, a condizione di conoscere la password, si passerà a una shell come *utente root*.
   
2. Il modo più comune e sicuro di eseguire le operazioni consiste nell'usare sempre prima `sudo`. Molti degli esempi di questo articolo usano `sudo`.

Di seguito sono elencati alcuni comandi comuni, ognuno dei quali ha diverse opzioni che è possibile cercare online:
-   `cd`: cambia la directory
-   `chmod`: cambia le autorizzazioni di un file o di una directory
-   `chown`: cambia la proprietà di un file o di una directory
-   `ls`: visualizza il contenuto di una directory
-   `mkdir`: crea una cartella (directory) in un'unità
-   `mv`: sposta un file da un percorso a un altro
-   `ps`: visualizza tutti i processi di lavoro
-   `rm`: elimina un file in locale su un server
-   `rmdir`: elimina una cartella (directory)
-   `systemctl`: avvia, arresta o abilita i servizi
-   Comandi dell'editor di testo. In Linux sono disponibili diverse opzioni dell'editor di testo, ad esempio vi ed emacs.

## <a name="common-tasks-for-availability-configurations-of-includessnoversion-mdincludesssnoversion-mdmd-on-linux"></a>Attività comuni per le configurazioni della disponibilità di [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] in Linux
Questa sezione illustra le attività comuni a tutte le distribuzioni di [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] basate su Linux.

### <a name="ensure-that-files-can-be-copied"></a>Assicurarsi che i file possano essere copiati
Copiare i file da un server a un altro è un'attività che chiunque usi [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] in Linux dovrebbe riuscire a eseguire. Questa attività è molto importante per le configurazioni dei gruppo di disponibilità.

Sia in Linux che nelle installazioni basate su Windows possono verificarsi problemi relativi alle autorizzazioni. Tuttavia, chi ha familiarità con la copia da server a server in Windows potrebbe non averne con la stessa operazione in Linux. Un metodo comune prevede l'uso dell'utilità della riga di comando `scp`, che è l'acronimo di secure copy (copia sicura). In background `scp` usa OpenSSH. SSH è l'acronimo di Secure Shell. A seconda della distribuzione Linux, OpenSSH potrebbe non essere installato. Se non lo è, è necessario installare prima OpenSSH. Per altre informazioni sulla configurazione di OpenSSH, fare clic sui collegamenti seguenti a seconda della distribuzione in uso:
-   [Red Hat Enterprise Linux (RHEL)](https://access.redhat.com/documentation/red_hat_enterprise_linux/6/html/deployment_guide/ch-openssh)
-   [SUSE Linux Enterprise Server (SLES)](https://en.opensuse.org/SDB:Configure_openSSH)
-   [Ubuntu](https://help.ubuntu.com/community/SSH/OpenSSH/Configuring)

Quando si usa `scp`, è necessario specificare le credenziali del server se non si tratta dell'origine o della destinazione. Se ad esempio si usa

```bash
scp MyAGCert.cer username@servername:/folder/subfolder
```

il file MyAGCert.cer viene copiato nella cartella specificata nell'altro server. Tenere presente che è necessario avere le autorizzazioni e, possibilmente, la proprietà del file per copiarlo, quindi potrebbe essere necessario usare `chown` prima di eseguire la copia. Analogamente, sul lato ricevente, l'utente appropriato deve avere l'accesso per modificare il file. Ad esempio, per ripristinare il file del certificato, l'utente `mssql` deve potervi accedere.

È anche possibile usare Samba, ovvero la variante Linux di SMB (Server Message Block), per creare condivisioni accessibili tramite percorsi UNC, ad esempio `\\SERVERNAME\SHARE`. Per altre informazioni sulla configurazione di Samba, fare clic sui collegamenti seguenti a seconda della distribuzione in uso:
-   [RHEL](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Confined_Services/chap-Managing_Confined_Services-Samba.html)
-   [SLES](https://www.suse.com/documentation/sles11/book_sle_admin/data/cha_samba.html)
-   [Ubuntu](https://help.ubuntu.com/community/Samba)

Si possono usare anche condivisioni SMB basate su Windows. Non è necessario che le condivisioni SMB siano basate su Linux, purché la parte client di Samba sia configurata correttamente nel server Linux che ospita [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] e la condivisione abbia l'accesso corretto. Negli ambienti misti questa soluzione consente di sfruttare l'infrastruttura esistente per le distribuzioni di [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] basate su Linux.

È importante che la versione di Samba distribuita sia conforme a SMB 3.0. Da quando è stato aggiunto il supporto per SMB in [!INCLUDE[sssql11-md](../includes/sssql11-md.md)], è necessario che tutte le condivisioni supportino SMB 3.0. Se si usa Samba per la condivisione e non Windows Server, la condivisione basata su Samba dovrebbe usare Samba 4.0 o versione successiva. L'ideale è usare la versione 4.3 o successiva, che supporta SMB 3.1.1. Per informazioni su SMB e Linux, vedere [SMB3 in Samba](https://events.static.linuxfound.org/sites/events/files/slides/smb3-in-samba.pr__0.pdf).

È infine possibile usare una condivisione NFS (Network File System). NFS non può essere usato nelle distribuzioni basate su Windows di [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], ma solo per le distribuzioni basate su Linux.

### <a name="configure-the-firewall"></a>Configurare il firewall
Analogamente a Windows, le distribuzioni Linux includono un firewall predefinito. Se la società usa un firewall esterno ai server, la disabilitazione dei firewall in Linux può essere accettabile. Tuttavia, indipendentemente dalla posizione in cui è abilitato il firewall, è necessario aprire le porte. La tabella seguente elenca le porte comuni necessarie per le distribuzioni di [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] a disponibilità elevata in Linux.

| Numero della porta | Type     | Descrizione                                                                                                                 |
|-------------|----------|-----------------------------------------------------------------------------------------------------------------------------|
| 111         | TCP/UDP  | NFS: `rpcbind/sunrpc`                                                                                                    |
| 135         | TCP      | Samba (se usato): mapper di endpoint                                                                                          |
| 137         | UDP      | Samba (se usato): servizio nomi NetBIOS                                                                                      |
| 138         | UDP      | Samba (se usato): datagramma NetBIOS                                                                                          |
| 139         | TCP      | Samba (se usato): sessione NetBIOS                                                                                           |
| 445         | TCP      | Samba (se usato): SMB su TCP                                                                                              |
| 1433        | TCP      | [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]: porta predefinita, che, se necessario, può essere sostituita da `mssql-conf set network.tcpport <portnumber>`                       |
| 2049        | TCP, UDP | NFS (se usato)                                                                                                               |
| 2224        | TCP      | Pacemaker: usato da `pcsd`                                                                                                |
| 3121        | TCP      | Pacemaker: obbligatorio se sono presenti nodi remoti di Pacemaker                                                                    |
| 3260        | TCP      | Iniziatore iSCSI (se usato): può essere modificato in `/etc/iscsi/iscsid.config` (RHEL), ma deve corrispondere alla porta della destinazione iSCSI |
| 5022        | TCP      | [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]: porta predefinita usata per l'endpoint del gruppo di disponibilità, che può essere cambiata quando si crea l'endpoint                                |
| 5403        | TCP      | Pacemaker                                                                                                                   |
| 5404        | UDP      | Pacemaker: richiesto da Corosync se si usa UDP multicast                                                                     |
| 5405        | UDP      | Pacemaker: richiesto da Corosync                                                                                            |
| 21064       | TCP      | Pacemaker: richiesto dalle risorse che usano DLM                                                                                 |
| Variabile    | TCP      | Porta dell'endpoint del gruppo di disponibilità, il cui valore predefinito è 5022                                                                                           |
| Variabile    | TCP      | NFS: porta per `LOCKD_TCPPORT` (disponibile in `/etc/sysconfig/nfs` in RHEL)                                              |
| Variabile    | UDP      | NFS: porta per `LOCKD_UDPPORT` (disponibile in `/etc/sysconfig/nfs` in RHEL)                                              |
| Variabile    | TCP/UDP  | NFS: porta per `MOUNTD_PORT` (disponibile in `/etc/sysconfig/nfs` in RHEL)                                                |
| Variabile    | TCP/UDP  | NFS: porta per `STATD_PORT` (disponibile in `/etc/sysconfig/nfs` in RHEL)                                                 |

Per le altre porte che possono essere usate da Samba, vedere [Samba Port Usage](https://wiki.samba.org/index.php/Samba_Port_Usage) (Utilizzo delle porte in Samba).

In Linux, invece della porta, si può aggiungere anche il nome del servizio come eccezione, ad esempio `high-availability` per Pacemaker. Se si intende procedere in questo modo, fare riferimento alla distribuzione per i nomi. In RHEL, ad esempio, il comando da aggiungere a Pacemaker è

```bash
sudo firewall-cmd --permanent --add-service=high-availability
```

**Documentazione dei firewall:**
-   [RHEL](https://access.redhat.com/documentation/red_hat_enterprise_linux/7/html/high_availability_add-on_reference/s1-firewalls-haar)
-   [SLES](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html)

### <a name="install-includessnoversion-mdincludesssnoversion-mdmd-packages-for-availability"></a>Installare i pacchetti [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] per la disponibilità
In un'installazione di [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] basata su Windows alcuni componenti, a differenza di altri, vengono installati anche in un'installazione del motore di base. In Linux durante il processo di installazione viene installato solo il motore di [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. Tutti gli altri elementi sono facoltativi. Per le istanze di [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] a disponibilità elevata in Linux, con [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] o consigliabile installare due pacchetti: [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Agent (*mssql-server-agent*) e il pacchetto a disponibilità elevata (*mssql-server-ha*). [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], nonostante sia tecnicamente facoltativo, è l'utilità di pianificazione di [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] per i processi ed è necessario per il log shipping, quindi è consigliabile installarlo. Nelle installazioni basate su Windows [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] non è facoltativo.

>[!NOTE]
>Per chi non ha familiarità con [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Agent è l'utilità di pianificazione dei processi predefinita di [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. Per gli amministratori di database, è un modo comune di pianificare, ad esempio, i backup e altre operazioni di manutenzione di [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. Diversamente da un'installazione basata su Windows di [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], dove [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Agent è un servizio completamente distinto, in Linux [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Agent viene eseguito direttamente in [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)].

Quando i gruppi di disponibilità o le istanze del cluster di failover sono configurate in una configurazione basata su Windows, sono compatibili con il cluster. La compatibilità con il cluster implica che [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] abbia DLL delle risorse specifiche note a un cluster WSFC (sqagtres.dll e sqsrvres.dll per le istanze del cluster di failover, hadrres.dll per i gruppi di disponibilità) e usate dal cluster WSFC per assicurare che le funzionalità di [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] siano attive, in esecuzione e operino correttamente. Poiché il clustering è esterno non solo a [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], ma anche a Linux stesso, Microsoft ha dovuto codificare l'equivalente di una DLL della risorsa per le distribuzioni di gruppi di disponibilità e di istanze del cluster di failover basate su Linux. Si tratta del pacchetto *mssql-server-ha*, noto anche come agente della risorsa [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] per Pacemaker. Per installare il pacchetto *mssql-server-ha*, vedere [Installare i pacchetti a disponibilità elevata e SQL Server Agent](sql-server-linux-deploy-pacemaker-cluster.md#install-the-sql-server-ha-and-sql-server-agent-packages).

Gli altri pacchetti facoltativi per [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] in Linux, Ricerca full-text di [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] (*mssql-server-fts*) e [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Integration Services (*mssql-server-is*), non sono obbligatori per la disponibilità elevata, sia per un'istanza del cluster di failover che per un gruppo di disponibilità.

## <a name="pacemaker-for-always-on-availability-groups-and-failover-cluster-instances-on-linux"></a>Pacemaker per i gruppi di disponibilità Always On e le istanze del cluster di failover in Linux
Come indicato in precedenza, l'unico meccanismo di clustering attualmente supportato da Microsoft per i gruppi di disponibilità e le istanze del cluster di failover è Pacemaker con Corosync. Questa sezione fornisce le informazioni di base sulla soluzione e illustra come pianificarla e distribuirla per le configurazioni di [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)].

### <a name="ha-add-onextension-basics"></a>Nozioni di base sulle estensioni e sui componenti aggiuntivi a disponibilità elevata
Tutte le distribuzioni attualmente supportate forniscono un'estensione o un componente aggiuntivo a disponibilità elevata, basato sullo stack di clustering di Pacemaker. Questo stack incorpora due componenti principali: Pacemaker e Corosync. Tutti i componenti dello stack sono:
-   Pacemaker: il componente di clustering principale, che esegue operazioni come il coordinamento dei computer in cluster.
-   Corosync: un framework e un set di API che consente, ad esempio, il quorum, la possibilità di riavviare i processi non riusciti e così via.
-   libQB: consente, ad esempio, la registrazione.
-   Agente della risorsa: funzionalità specifica fornita per consentire l'integrazione di un'applicazione con Pacemaker.
-   Agente di isolamento: script/funzionalità che facilitano l'isolamento dei nodi e li gestiscono in caso di problemi.
    
> [!NOTE]
> Lo stack di cluster viene comunemente definito Pacemaker in ambito Linux.

Questa soluzione è simile alla distribuzione di configurazioni in cluster con Windows per certi aspetti, ma per altri è molto diversa. In Windows il formato di disponibilità del clustering, denominato WSFC (Windows Server Failover Cluster), è integrato nel sistema operativo e la funzionalità che consente la creazione di un cluster WSFC, il clustering di failover, è disabilitata per impostazione predefinita. In Windows i gruppi di disponibilità e le istanze del cluster di failover sono basati su un cluster WSFC e sono strettamente integrati a causa della DLL della risorsa specifica fornita da [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. Questa soluzione a stretto regime di controllo, in generale, è possibile perché tutti gli elementi provengono da un unico fornitore.

![](./media/sql-server-linux-ha-basics/image1.png)

In Linux ogni distribuzione supportata, nonostante disponga di Pacemaker, può essere personalizzata e avere implementazioni e versioni leggermente diverse. Alcune delle differenze risulteranno evidenti dalle istruzioni riportate in questo articolo. Il livello del clustering è open source, quindi anche se viene fornito con le distribuzioni, non è così strettamente integrato come un cluster WSFC in Windows. È proprio per questo motivo che Microsoft fornisce *mssql-server-ha*, in modo che [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] e lo stack di Pacemaker possano offrire un'esperienza simile, ma non identica, a quella di Windows per i gruppi di disponibilità e le istanze del cluster di failover.

Per la documentazione completa su Pacemaker, inclusa una spiegazione più approfondita di tutti i componenti con informazioni di riferimento complete, per RHEL e SLES:
-   [RHEL](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/ch-overview-HAAR.html)
-   [SLES](https://www.suse.com/documentation/sle_ha/book_sleha/data/book_sleha.html)

Ubuntu non ha una guida per la disponibilità.

Per altre informazioni sull'intero stack, vedere anche la [pagina della documentazione di Pacemaker](https://clusterlabs.org/doc/) ufficiale sul sito di Clusterlabs.

### <a name="pacemaker-concepts-and-terminology"></a>Concetti e terminologia di Pacemaker
Questa sezione illustra la terminologia e i concetti comuni per un'implementazione di Pacemaker.

#### <a name="node"></a>Nodo
Un nodo è un server che partecipa al cluster. Un cluster Pacemaker supporta a livello nativo un massimo di 16 nodi. Questo numero può essere superato se Corosync non è in esecuzione in altri nodi, ma Corosync è obbligatorio per [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], quindi il numero massimo di nodi che un cluster può avere per qualsiasi configurazione basata su [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] è 16. Questo è il limite di Pacemaker ed è completamente diverso dalle limitazioni massime per i gruppi di disponibilità e le istanze del cluster di failover imposte da [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. 

#### <a name="resource"></a>Risorsa
Il concetto di risorsa è proprio sia dei cluster WSFC che dei cluster Pacemaker. Una risorsa è una funzionalità specifica che viene eseguita nel contesto del cluster, ad esempio un disco o un indirizzo IP. Ad esempio, in Pacemaker possono essere create sia risorse di istanza del cluster di failover che risorse di gruppo di disponibilità. Qualcosa di simile accade in un cluster WSFC, in cui è presente una risorsa di [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] per una risorsa di istanza del cluster di failover o una risorsa di gruppo di disponibilità quando si configura un gruppo di disponibilità, ma esistono alcune differenze dovute al modo in cui [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] si integra con Pacemaker.

Pacemaker ha risorse standard e clone. Le risorse clone sono quelle che vengono eseguite simultaneamente in tutti i nodi. Un esempio può essere quello di un indirizzo IP eseguito su più nodi per bilanciare il carico. Tutte le risorse create per le istanze del cluster di failover usano una risorsa standard, perché in un determinato momento un solo nodo può ospitare un'istanza del cluster di failover.

Quando si crea un gruppo di disponibilità, è necessario un tipo specifico di risorsa clone denominata risorsa a più stati. Anche se un gruppo di disponibilità ha una sola replica primaria, il gruppo di disponibilità in sé è in esecuzione in tutti i nodi che è configurato per usare e può potenzialmente consentire azioni come l'accesso in sola lettura. Poiché si tratta di un uso "live" del nodo, le risorse hanno due tipi di stati: master e slave. Per altre informazioni, vedere [Multi-state resources: Resources that have multiple modes](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Configuring_the_Red_Hat_High_Availability_Add-On_with_Pacemaker/s1-multistateresource-HAAR.html) (Risorse a più stati: risorse con più modalità).

#### <a name="resource-groupssets"></a>Set/Gruppi di risorse
Analogamente ai ruoli in un cluster WSFC, un cluster Pacemaker si basa sul concetto di gruppo di risorse. Un gruppo di risorse, denominato set in SLES, è una raccolta di risorse che interagiscono tra loro e possono effettuare il failover da un nodo a un altro come singola unità. I gruppi di risorse non possono contenere risorse configurate come master/slave e quindi non possono essere usati per i gruppi di disponibilità. Anche se un gruppo di risorse può essere usato per le istanze del cluster di failover, non è in genere una configurazione consigliata.

#### <a name="constraints"></a>Vincoli
I cluster WSFC presentano diversi parametri per le risorse, oltre, ad esempio, alle dipendenze, che indicano al cluster WSFC una relazione padre/figlio tra due risorse diverse. Una dipendenza è semplicemente una regola che indica a cluster WSFC quale risorsa deve essere prima online.

Un cluster Pacemaker non prevede il concetto di dipendenze, ma quello dei vincoli. Esistono tre tipi di vincoli: condivisione del percorso, percorso e ordinamento.
-   Un vincolo di condivisione del percorso determina se due risorse devono essere in esecuzione nello stesso nodo o meno.
-   Un vincolo di percorso indica al cluster Pacemaker dove una risorsa può o non può essere eseguita.
-   Un vincolo di ordinamento indica al cluster Pacemaker l'ordine in cui le risorse devono essere avviate.

> [!NOTE]
> I vincoli di condivisione del percorso non sono necessari per le risorse in un gruppo di risorse, perché tali risorse sono considerate una singola unità.

#### <a name="quorum-fence-agents-and-stonith"></a>Quorum, agenti di isolamento e STONITH
Il concetto di quorum in Pacemaker è simile a quello di cluster WSFC. Lo scopo generale del meccanismo di quorum di un cluster è garantire che il cluster rimanga operativo. Sia il cluster WSFC che i componenti aggiuntivi a disponibilità elevata per le distribuzioni Linux presentano il concetto di voto, in cui ogni nodo viene conteggiato ai fini del quorum. È necessario che la maggior parte dei voti sia positiva. In caso contrario, nel peggiore degli scenari, il cluster verrà arrestato.

A differenza di un cluster WSFC, non esistono risorse di controllo da usare con il quorum. Analogamente a un cluster WSFC, l'obiettivo è quello di mantenere dispari il numero dei votanti. Nella configurazione del quorum le considerazioni per i gruppi di disponibilità sono diverse da quelle per le istanze del cluster di failover.

I cluster WSFC monitorano lo stato dei nodi partecipanti e li gestiscono quando si verifica un problema. Le versioni più recenti dei cluster WSFC offrono funzionalità di questo tipo, ad esempio la messa in quarantena di un nodo non funzionante o non disponibile (il nodo non è attivo, la comunicazione di rete è inattiva e così via). In ambito Linux questo tipo di funzionalità viene fornito da un agente di isolamento. Il concetto viene talvolta definito isolamento. Tuttavia, questi agenti di isolamento sono in genere specifici della distribuzione e spesso vengono messi a disposizione dai fornitori di hardware e da alcuni fornitori di software, ad esempio quelli che forniscono gli hypervisor. Ad esempio, VMware fornisce un agente di isolamento che può essere usato per le macchine virtuali Linux virtualizzate con vSphere.

Il quorum e l'isolamento sono collegati a un altro concetto, quello di STONITH (Shoot The Other Node In The Head). STONITH deve avere un cluster Pacemaker supportato in tutte le distribuzioni Linux. Per altre informazioni, vedere [Fencing in a Red Hat High Availability Cluster](https://access.redhat.com/solutions/15575) (RHEL) (Isolamento in un cluster a disponibilità elevata Red Hat - RHEL).

#### <a name="corosyncconf"></a>corosync.conf
Il file `corosync.conf` contiene la configurazione del cluster. È incluso in `/etc/corosync`. Nel corso delle normali operazioni quotidiane, se il cluster è configurato correttamente, non dovrebbe essere mai necessario modificare questo file.

#### <a name="cluster-log-location"></a>Percorso del registro cluster
I percorsi dei log per i cluster Pacemaker variano a seconda della distribuzione.
-   RHEL e SLES: `/var/log/cluster/corosync.log`
-   Ubuntu: `/var/log/corosync/corosync.log`

Per cambiare il percorso di registrazione predefinito, modificare `corosync.conf`.

## <a name="plan-pacemaker-clusters-for-includessnoversion-mdincludesssnoversion-mdmd"></a>Pianificare i cluster Pacemaker per [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]
Questa sezione illustra i punti di pianificazione importanti per un cluster Pacemaker.

### <a name="virtualizing-linux-based-pacemaker-clusters-for-includessnoversion-mdincludesssnoversion-mdmd"></a>Virtualizzazione dei cluster Pacemaker basati su Linux per [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]
L'uso di macchine virtuali per eseguire le distribuzioni di [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] basate su Linux per i gruppi di disponibilità e le istanze del cluster di failover è soggetto alle stesse regole delle controparti basate su Windows. Microsoft mette a disposizione un set di regole di base per supportare le distribuzioni di [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] virtualizzate nell'articolo della [Knowledge Base 956893 del supporto tecnico Microsoft](https://support.microsoft.com/help/956893/support-policy-for-microsoft-sql-server-products-that-are-running-in-a-hardware-virtualization-environment). Possono esserci delle differenze a seconda dell'hypervisor, ad esempio Hyper-V di Microsoft ed ESXi di VMware, dovute alle caratteristiche specifiche delle piattaforme.

Quando si tratta di gruppi di disponibilità e di istanze del cluster di failover soggetti a virtualizzazione, verificare che l'anti-affinità per i nodi di un determinato cluster Pacemaker sia impostata. Se configurate per la disponibilità elevata in una configurazione di gruppo di disponibilità o di istanza del cluster di failover, le macchine virtuali che ospitano [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] non devono mai essere eseguite nello stesso host dell'hypervisor. Se ad esempio viene distribuita un'istanza del cluster di failover a due nodi, dovranno essere presenti *almeno* tre host di hypervisor, in modo che sia disponibile uno spazio in cui trasferire una delle macchine virtuali che ospitano un nodo in caso di errore dell'host, soprattutto se si usano funzionalità come Live Migration o vMotion.

Per informazioni più specifiche, vedere:
-   Documentazione di Hyper-V: [Uso del clustering guest per la disponibilità elevata](https://technet.microsoft.com/library/dn440540(v=ws.11).aspx)
-   White paper (scritto per le distribuzioni basate su Windows, ma la maggior parte dei concetti è ugualmente valida): [Planning Highly Available, Mission Critical SQL Server Deployments with VMware vSphere](https://www.vmware.com/content/dam/digitalmarketing/vmware/en/pdf/solutions/vmware-vsphere-highly-available-mission-critical-sql-server-deployments.pdf) (Pianificazione di distribuzioni di SQL Server strategiche a disponibilità elevata con VMware vSphere)

### <a name="networking"></a>Rete
Diversamente da un cluster WSFC, Pacemaker non richiede un nome dedicato o nemmeno un indirizzo IP dedicato per il cluster Pacemaker in sé. I gruppi di disponibilità e le istanze del cluster di failover richiedono gli indirizzi IP (per altre informazioni, vedere la documentazione specifica), ma non i nomi, perché non sono disponibili risorse nome della rete. SLES consente la configurazione di un indirizzo IP per finalità amministrative, ma non è obbligatorio, come illustrato in [Creare il cluster Pacemaker](sql-server-linux-deploy-pacemaker-cluster.md#create).

Analogamente a un cluster WSFC, Pacemaker preferisce la rete ridondante, ovvero schede di rete distinte (schede di interfaccia di rete o schede di interfaccia di rete fisica per l'ambiente fisico) con indirizzi IP singoli. Per quanto riguarda la configurazione del cluster, ogni indirizzo IP avrà il cosiddetto anello specifico. Tuttavia, come avviene attualmente per i cluster WSFC, molte implementazioni sono virtualizzate o si trovano nel cloud pubblico, dove al server viene presentata una singola scheda di interfaccia di rete virtualizzata. Se tutte le schede di interfaccia di rete fisica e le schede di interfaccia di rete virtualizzata sono connesse allo stesso commutatore fisico o virtuale, non esiste una vera ridondanza a livello di rete, quindi la configurazione di più schede di interfaccia di rete è un po' illusoria per la macchina virtuale. La ridondanza di rete è in genere integrata nell'hypervisor per le distribuzioni virtualizzate ed è sicuramente integrata nel cloud pubblico.

Una differenza con le schede di interfaccia di rete multiple e Pacemaker rispetto a un cluster WSFC è che Pacemaker consente più indirizzi IP nella stessa subnet, un cluster WSFC invece no. Per altre informazioni sulle subnet multiple e sui cluster Linux, vedere l'articolo [Configurare più subnet](sql-server-linux-configure-multiple-subnet.md).

### <a name="quorum-and-stonith"></a>Quorum e STONITH
I requisiti e la configurazione quorum sono correlati alle distribuzioni specifiche del gruppo di disponibilità o dell'istanza del cluster di failover di [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)].

STONITH è necessario per un cluster Pacemaker supportato. Usare la documentazione della distribuzione per configurare STONITH. Per un esempio per SLES, vedere [Storage-based Fencing](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_storage_protect_fencing.html) (Isolamento basato sulla risorsa di archiviazione). Per le soluzioni basate su ESXI è disponibile anche un agente STONITH per VMware vCenter. Per altre informazioni, vedere [Stonith Plugin Agent for VMWare VM VCenter SOAP Fencing (Unofficial)](https://github.com/olafrv/fence_vmware_soap) (Agente di plug-in di Stonith per l'isolamento VCenter SOAP delle macchina virtuali VMWare - Non ufficiale).

### <a name="interoperability"></a>Interoperabilità
Questa sezione illustra come un cluster basato su Linux può interagire con un cluster WSFC o con altre distribuzioni di Linux.

#### <a name="wsfc"></a>WSFC
Attualmente, non è possibile interagire direttamente con un cluster WSFC e Pacemaker. Non è quindi possibile creare un gruppo di disponibilità o un'istanza del cluster di failover che funzioni in un cluster WSFC e in Pacemaker. Esistono tuttavia due soluzioni di interoperabilità, entrambe progettate per i gruppi di disponibilità. Un'istanza del cluster di failover può partecipare a una configurazione multipiattaforma solo se partecipa come istanza in uno di questi due scenari:
-   Un gruppo di disponibilità con un tipo di cluster None. Per altre informazioni, vedere la [documentazione sui gruppi di disponibilità](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md) di Windows.
-   Un gruppo di disponibilità distribuito, che è un particolare tipo di gruppo di disponibilità che consente di configurare due diversi gruppi di disponibilità come gruppo di disponibilità proprio. Per altre informazioni sui gruppi di disponibilità distribuiti, vedere la documentazione [Gruppi di disponibilità distribuiti](../database-engine/availability-groups/windows/distributed-availability-groups.md).

#### <a name="other-linux-distributions"></a>Altre distribuzioni Linux
In Linux tutti i nodi di un cluster Pacemaker devono trovarsi nella stessa distribuzione. Questo significa, ad esempio, che un nodo RHEL non può far parte di un cluster Pacemaker con un nodo SLES. Il motivo principale di questa condizione è stato spiegato in precedenza: le distribuzioni possono avere versioni e funzionalità diverse, quindi potrebbero verificarsi dei problemi. La combinazione di distribuzioni equivale alla combinazione di cluster WSFC e Linux: usare None o i gruppi di disponibilità distribuiti.

## <a name="next-steps"></a>Passaggi successivi
[Distribuire un cluster Pacemaker per SQL Server in Linux](sql-server-linux-deploy-pacemaker-cluster.md)
