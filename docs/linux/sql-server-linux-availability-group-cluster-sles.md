---
title: Configurare Cluster SLES per gruppo di disponibilità di SQL Server
titleSuffix: SQL Server
description: Informazioni su come creare cluster di gruppo di disponibilità per SQL Server su SUSE Linux Enterprise Server (SLES)
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 04/30/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 85180155-6726-4f42-ba57-200bf1e15f4d
ms.openlocfilehash: 063adf4f1f180138150484e4ac9fc397ef886f5d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68003556"
---
# <a name="configure-sles-cluster-for-sql-server-availability-group"></a>Configurare Cluster SLES per gruppo di disponibilità di SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questa guida fornisce istruzioni per creare un cluster a tre nodi per SQL Server su SUSE Linux Enterprise Server (SLES) 12 SP2. Per la disponibilità elevata, un gruppo di disponibilità in Linux richiede tre nodi, vedere la [elevata disponibilità e protezione dei dati per le configurazioni di gruppo di disponibilità](sql-server-linux-availability-group-ha.md). Il livello di clustering si basa su SUSE [estensione a disponibilità elevata (Georgiano)](https://www.suse.com/products/highavailability) costruita basandosi su [Pacemaker](https://clusterlabs.org/). 

Per altre informazioni su configurazione del cluster, opzioni dell'agente di risorsa, gestione, le procedure consigliate e indicazioni, vedere [SUSE Linux Enterprise ad alta disponibilità estensione 12 SP2](https://www.suse.com/documentation/sle-ha-12/index.html).

>[!NOTE]
>A questo punto, l'integrazione con Pacemaker in Linux SQL Server non è accoppiato come con WSFC per Windows. Servizio SQL Server in Linux non è compatibile con i cluster. Pacemaker controlla tutti l'orchestrazione delle risorse del cluster, tra cui la risorsa del gruppo di disponibilità. In Linux, è consigliabile limitarsi a sempre nella disponibilità gruppo di viste a gestione dinamica (DMV) che forniscono informazioni sul cluster, ad esempio hadr_cluster. Inoltre, nome di rete virtuale è specifico al cluster WSFC, è disponibile un equivalente dello stesso in Pacemaker. È comunque possibile creare un listener per usarlo per la riconnessione dopo il failover trasparente, ma si dovrà registrare manualmente il nome del listener nel server DNS con l'indirizzo IP usato per creare la risorsa IP virtuale (come illustrato nelle sezioni seguenti).


## <a name="roadmap"></a>Guida di orientamento

La procedura per la creazione di un gruppo di disponibilità per la disponibilità elevata varia tra i server Linux e un cluster di failover di Windows Server. L'elenco seguente descrive i passaggi generali: 

1. [Configurare SQL Server nei nodi del cluster](sql-server-linux-setup.md).

2. [Creare il gruppo di disponibilità](sql-server-linux-availability-group-failover-ha.md). 

3. Configurare un cluster di resource manager, ad esempio Pacemaker. Queste istruzioni sono in questo documento.
   
   Il modo per configurare un gestore di risorse cluster dipende la distribuzione Linux specifica. 

   >[!IMPORTANT]
   >Gli ambienti di produzione richiedono un agente di isolamento, ad esempio STONITH per la disponibilità elevata. Gli esempi in questo articolo non usano gli agenti di fencing. Sono per i test e convalida solo. 
   
   >Un cluster Pacemaker Usa fencing per restituire il cluster a uno stato noto. Il modo per configurare l'isolamento varia a seconda della distribuzione e l'ambiente. A questo punto, l'isolamento non è disponibile in alcuni ambienti cloud. Visualizzare [estensione di disponibilità elevata di SUSE Linux Enterprise](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.fencing).

5. [Aggiungere il gruppo di disponibilità come una risorsa in cluster](sql-server-linux-availability-group-cluster-sles.md#configure-the-cluster-resources-for-sql-server). 

## <a name="prerequisites"></a>Prerequisiti

Per completare lo scenario end-to-end seguente, è necessario tre macchine virtuali da distribuire il cluster di tre nodi. I passaggi seguenti illustrano come configurare questi server.

## <a name="setup-and-configure-the-operating-system-on-each-cluster-node"></a>Installare e configurare il sistema operativo in ogni nodo del cluster 

Il primo passaggio consiste nel configurare il sistema operativo nei nodi del cluster. Per questa procedura dettagliata, usare SLES 12 SP2 con una sottoscrizione valida per il componente aggiuntivo a disponibilità elevata.

### <a name="install-and-configure-sql-server-service-on-each-cluster-node"></a>Installare e configurare il servizio SQL Server in ogni nodo del cluster

1. Installare e configurare il servizio SQL Server in tutti i nodi. Per istruzioni dettagliate, vedere [installare SQL Server in Linux](sql-server-linux-setup.md).

1. Designare un nodo primari e di altri nodi come repliche secondarie. Usare questi termini all'interno di questa Guida.

1. Assicurarsi che i nodi che faranno parte del cluster possono comunicare tra loro.

   L'esempio seguente mostra `/etc/hosts` con aggiunte per tre nodi denominati SLES1, SLES2 e SLES3.

   ```
   127.0.0.1   localhost
   10.128.16.33 SLES1
   10.128.16.77 SLES2
   10.128.16.22 SLES3
   ```

   Tutti i nodi del cluster devono essere in grado di accedere reciprocamente tramite SSH. Strumenti come `hb_report` o `crm_report` (per la risoluzione dei problemi) e History Explorer di Hawk richiedono l'accesso a SSH tra i nodi, in caso contrario, essi possono raccogliere dati solo dal nodo corrente. Nel caso in cui si usa una porta SSH non standard, usare l'opzione -X (vedere `man` pagina). Ad esempio, se la porta SSH è 3479, richiamare un `crm_report` con:

   ```bash
   sudo crm_report -X "-p 3479" [...]
   ```

   Per altre informazioni, vedere la [Guida all'amministrazione di SLES - sezione varie](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.troubleshooting.misc).


## <a name="create-a-sql-server-login-for-pacemaker"></a>Creare un account di accesso di SQL Server per Pacemaker

[!INCLUDE [SLES-Create-SQL-Login](../includes/ss-linux-cluster-pacemaker-create-login.md)]

## <a name="configure-an-always-on-availability-group"></a>Configurare un gruppo di disponibilità Always On

Nei server Linux, configurare il gruppo di disponibilità e quindi configurare le risorse del cluster. Per configurare il gruppo di disponibilità, vedere [Configura gruppo di disponibilità AlwaysOn per SQL Server in Linux](sql-server-linux-availability-group-configure-ha.md)

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>Installare e configurare Pacemaker in ogni nodo del cluster

1. Installare l'estensione di disponibilità elevata

   Per riferimento, vedere [installazione SUSE Linux Enterprise Server e l'estensione per la disponibilità elevata](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.installation)

1. Installa pacchetto dell'agente di risorse SQL Server su entrambi i nodi.

   ```bash
   sudo zypper install mssql-server-ha
   ```

## <a name="set-up-the-first-node"></a>Configurare il primo nodo

   Fare riferimento a [istruzioni di installazione di SLES](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.setup.1st-node)

1. Accedere come `root` per la macchina fisica o virtuale da usare come nodo del cluster.
2. Avviare lo script di bootstrap eseguendo:
   ```bash
   sudo ha-cluster-init
   ```

   NTP non è stato configurato per l'esecuzione all'avvio, verrà visualizzato un messaggio. 

   Se si decide di continuare comunque, lo script genera le chiavi per l'accesso SSH e per lo strumento di sincronizzazione Csync2 automaticamente e avvia i servizi necessari per entrambi. 

3. Per configurare il livello di comunicazione del cluster (Corosync): 

   a. Immettere un indirizzo di rete a cui associarsi. Per impostazione predefinita, lo script viene proposto l'indirizzo di rete di eth0. In alternativa, immettere un indirizzo di rete diversi, ad esempio l'indirizzo di bond0. 

   b. Immettere un indirizzo multicast. Lo script viene proposto un indirizzo casuale che è possibile utilizzare come valore predefinito. 

   c. Immettere una porta di multicast. Lo script viene proposto 5405 come predefinito. 

   d. Per configurare `SBD ()`, immettere un percorso persistente per la partizione del dispositivo di blocco che si desidera utilizzare per SBD. Il percorso deve essere coerente in tutti i nodi del cluster. 
   Infine, lo script avvierà il servizio Pacemaker per connettere il cluster a nodo singolo e abilitare l'interfaccia di gestione Web Hawk2. L'URL da utilizzare per Hawk2 viene visualizzato sullo schermo. 

4. Per i dettagli del processo di installazione, controllare `/var/log/sleha-bootstrap.log`. È ora disponibile un cluster in esecuzione un nodo. Controllare lo stato del cluster con lo stato di crm:

   ```bash
   sudo crm status
   ```

   È anche possibile visualizzare la configurazione del cluster con `crm configure show xml` o `crm configure show`.

5. La procedura di bootstrap viene creato un utente di Linux denominato hacluster con la password per linux. Sostituire la password predefinita con una protezione appena possibile: 

   ```bash
   sudo passwd hacluster
   ```

## <a name="add-nodes-to-the-existing-cluster"></a>Aggiungere nodi al cluster esistente

Se si dispone di un cluster in esecuzione con uno o più nodi, aggiungere più nodi del cluster con lo script di bootstrap a disponibilità elevata-cluster-join. Lo script necessita esclusivamente l'accesso a un nodo del cluster esistente e verrà completata automaticamente la configurazione di base sul computer corrente. Usare la procedura seguente:

Se sono stati configurati i nodi del cluster esistente con il `YaST` modulo di cluster, assicurarsi che siano soddisfatti i prerequisiti seguenti prima di eseguire `ha-cluster-join`:
- L'utente radice sui nodi esistenti include le chiavi SSH per l'accesso senza password. 
- `Csync2` è configurato sui nodi esistenti. Per altre informazioni, vedere configurazione Csync2 con YaST. 

1. Accedere come utente root per la macchina fisica o virtuale dovrebbe essere aggiunti al cluster. 
2. Avviare lo script di bootstrap eseguendo: 

   ```bash
   sudo ha-cluster-join
   ```

   NTP non è stato configurato per l'esecuzione all'avvio, verrà visualizzato un messaggio. 

3. Se si decide di continuare comunque, verrà richiesto per l'indirizzo IP di un nodo esistente. Immettere l'indirizzo IP. 

4. Se non si è già configurato un accesso a SSH senza password tra entrambi i computer, è anche richiederà la password radice del nodo esistente. 

   Dopo l'accesso al nodo specificato, lo script copia la configurazione di Corosync, configura SSH e `Csync2`e riporta online il computer corrente come nuovo nodo del cluster. A parte ciò, viene avviato il servizio richiesto perché Hawk. Se è stata configurata l'archiviazione condivisa con `OCFS2`, viene creato automaticamente anche la directory del punto di montaggio per i `OCFS2` file system. 

5. Ripetere i passaggi precedenti per tutti i computer da aggiungere al cluster. 

6. Per informazioni dettagliate del processo, controllare `/var/log/ha-cluster-bootstrap.log`. 

1. Controllare lo stato del cluster con `sudo crm status`. Se il secondo nodo è stato aggiunto correttamente, l'output sarà simile al seguente:

   ```bash
   sudo crm status
   
   3 nodes configured
   1 resource configured
   Online: [ SLES1 SLES2 SLES3]
   Full list of resources:   
   admin_addr     (ocf::heartbeat:IPaddr2):       Started node1
   ```

   >[!NOTE]
   >`admin_addr` è la risorsa cluster IP virtuale configurata durante l'installazione iniziale del cluster a nodo singolo.

Dopo aver aggiunto tutti i nodi, controllare se è necessario modificare i criteri di quorum no nelle opzioni di cluster globale. Ciò è particolarmente importante per i cluster a due nodi. Per altre informazioni, vedere sezione 4.1.2, opzione no-quorum-policy. 

## <a name="set-cluster-property-cluster-recheck-interval"></a>Impostare proprietà di cluster del cluster-Ricontrolla-intervallo

`cluster-recheck-interval` indica l'intervallo di polling in corrispondenza del quale il cluster controlla modifiche nei parametri delle risorse, i vincoli o altre opzioni di cluster. Se una replica diventa inattiva, il cluster tenta di riavviare la replica in base all'intervallo è associato mediante il `failure-timeout` valore e il `cluster-recheck-interval` valore. Ad esempio, se `failure-timeout` è impostato su 60 secondi e `cluster-recheck-interval` è impostato su 120 secondi, il riavvio viene eseguito un tentativo in base all'intervallo è maggiore di 60 secondi ma inferiore a 120 secondi. È consigliabile impostare timeout errore 60s e controlla di nuovo-cluster-interval su un valore maggiore di 60 secondi. Non è consigliabile impostare intervallo-cluster-nuova verifica su un valore ridotto.

Per aggiornare il valore della proprietà da `2 minutes` eseguire:

```bash
crm configure property cluster-recheck-interval=2min
```

> [!IMPORTANT] 
> Se si dispone già di una risorsa gruppo di disponibilità gestita da un cluster Pacemaker, tenere presente che tutte le distribuzioni che usano la versione più recente disponibile Pacemaker pacchetto 1.1.18-11.el7 introducano un cambiamento di comportamento per il cluster iniziale-errore-è-errore irreversibile impostazione quando relativo il valore è false. Questa modifica interessa il flusso di lavoro di failover. Se una replica primaria si verifica un'interruzione, il cluster è previsto per il failover su una delle repliche secondarie disponibili. Al contrario, gli utenti noteranno che il cluster insiste avviare la replica primaria non riuscita. Se tale database primario non torna online (a causa di un'interruzione dell'alimentazione permanente), il cluster mai effettua il failover a un'altra replica secondaria disponibile. Grazie a questa modifica, una configurazione consigliata in precedenza per impostare start-errore-è-errore irreversibile non è più valida e l'impostazione deve essere ripristinato il valore predefinito di `true`. Inoltre, la risorsa del gruppo di disponibilità deve essere aggiornato per includere il `failover-timeout` proprietà. 
>
>Per aggiornare il valore della proprietà da `true` eseguire:
>
>```bash
>crm configure property start-failure-is-fatal=true
>```
>
>Aggiornare le proprietà della risorsa del gruppo di disponibilità esistente `failure-timeout` al `60s` eseguire (sostituire `ag1` con il nome della risorsa gruppo di disponibilità): 
>
>```bash
>crm configure edit ag1
># In the text editor, add `meta failure-timeout=60s` after any `param`s and before any `op`s
>```

Per altre informazioni sulle proprietà del cluster Pacemaker, vedere [configurazione di risorse Cluster](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_config_crm_resources.html).

## <a name="configure-fencing-stonith"></a>Configurare l'isolamento (STONITH)
I fornitori del cluster pacemaker richiedono STONITH deve essere abilitata e un dispositivo di fencing configurato per l'installazione del cluster supportate. Quando cluster resource manager non è possibile determinare lo stato di un nodo o di una risorsa in un nodo, l'isolamento consente di visualizzare di nuovo il cluster a uno stato noto.

Isolamento a livello di risorsa principalmente assicura che non vi sia alcun danneggiamento dei dati durante un'interruzione del servizio tramite la configurazione di una risorsa. È possibile utilizzare l'isolamento a livello di risorsa, ad esempio, con DRBD (Distributed replicati blocco dispositivo) per contrassegnare il disco in un nodo come obsoleta quando il collegamento di comunicazione si arresta.

Isolamento a livello di nodo assicura che un nodo non viene eseguita alcuna risorsa. In tal caso, reimpostare il nodo e l'implementazione di Pacemaker di esso viene chiamato STONITH (che è l'acronimo di "girare in altro nodo nell'intestazione"). Pacemaker supporta una vasta gamma di dispositivi, ad esempio un uninterruptible power supply o gestione schede di interfaccia di per i server di conflitti.

Per altre informazioni, vedere [cluster Pacemaker da zero](https://clusterlabs.org/pacemaker/doc/en-US/Pacemaker/1.1/html/Clusters_from_Scratch/), [Fencing e Stonith](https://clusterlabs.org/doc/crm_fencing.html) e [documentazione SUSE a disponibilità elevata: L'isolamento e STONITH](https://www.suse.com/documentation/sle_ha/book_sleha/data/cha_ha_fencing.html).

In fase di inizializzazione del cluster, se non viene rilevata alcuna configurazione di STONITH è disabilitata. Può essere abilitata in un secondo momento usando il comando seguente:

```bash
sudo crm configure property stonith-enabled=true
```
  
>[!IMPORTANT]
>La disabilitazione di STONITH è solo a scopo di test. Se si prevede di utilizzare Pacemaker in un ambiente di produzione, è necessario pianificare un'implementazione di STONITH a seconda dell'ambiente e lasciarla abilitata. SUSE fornisce gli agenti di fencing per tutti gli ambienti cloud (tra cui Azure) o Hyper-V. Consequentially, il fornitore del cluster non offre il supporto per l'esecuzione di cluster di produzione in questi ambienti. Microsoft sta lavorando a una soluzione per questo divario che sarà disponibile nelle versioni future.


## <a name="configure-the-cluster-resources-for-sql-server"></a>Configurare le risorse del cluster per SQL Server

Fare riferimento a [SLES amministrazione Guid](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.manual_config)

## <a name="enable-pacemaker"></a>Enable Pacemaker

Enable Pacemaker in modo che venga avviato automaticamente.

Eseguire il comando seguente in ogni nodo del cluster.

```bash
systemctl enable pacemaker
```

### <a name="create-availability-group-resource"></a>Crea risorsa gruppo di disponibilità

Il comando seguente crea e configura la risorsa del gruppo di disponibilità per tre repliche del gruppo di disponibilità [ag1]. Le operazioni di monitoraggio e i timeout devono essere specificate in modo esplicito in SLES basata sul fatto che i timeout sono altamente dipendente dal carico di lavoro e devono essere attentamente regolato per ogni distribuzione.
Eseguire il comando in uno dei nodi del cluster:

1. Eseguire `crm configure` aprire il prompt dei comandi di crm:

   ```bash
   sudo crm configure 
   ```

1. Nel prompt di crm, eseguire il comando seguente per configurare le proprietà della risorsa.

   ```bash
   primitive ag_cluster \
      ocf:mssql:ag \
      params ag_name="ag1" \
      meta failure-timeout=60s \
      op start timeout=60s \
      op stop timeout=60s \
      op promote timeout=60s \
      op demote timeout=10s \
      op monitor timeout=60s interval=10s \
      op monitor timeout=60s interval=11s role="Master" \
      op monitor timeout=60s interval=12s role="Slave" \
      op notify timeout=60s
   ms ms-ag_cluster ag_cluster \
      meta master-max="1" master-node-max="1" clone-max="3" \
     clone-node-max="1" notify="true" \
   commit
      ```

[!INCLUDE [required-synchronized-secondaries-default](../includes/ss-linux-cluster-required-synchronized-secondaries-default.md)]

### <a name="create-virtual-ip-resource"></a>Creare una risorsa IP virtuale

Se non è stato creato la risorsa IP virtuale durante l'esecuzione `ha-cluster-init` è possibile creare questa risorsa ora. Il comando seguente crea una risorsa IP virtuale. Sostituire `<**0.0.0.0**>` con un indirizzo disponibile dalla rete e `<**24**>` con il numero di bit nella maschera di subnet CIDR. Eseguire in un nodo.

```bash
crm configure \
primitive admin_addr \
   ocf:heartbeat:IPaddr2 \
   params ip=<**0.0.0.0**> \
      cidr_netmask=<**24**>
```

### <a name="add-colocation-constraint"></a>Aggiungi vincolo di condivisione del percorso
Quasi ogni decisione di in un cluster Pacemaker, come scegliere in cui deve essere eseguita una risorsa, viene eseguita confrontando i punteggi. I punteggi vengono calcolati per ogni risorsa e cluster resource manager sceglie il nodo con il punteggio più alto per una determinata risorsa. (Se un nodo ha un punteggio negativo per una risorsa, la risorsa non è possibile eseguire su tale nodo.) È possibile gestire le decisioni del cluster con vincoli. I vincoli hanno un punteggio. Se un vincolo ha un punteggio inferiore a infinito, è solo un'indicazione. Un punteggio pari a infinito significa che è indispensabile. Microsoft vuole garantire che primaria del gruppo di disponibilità e virtuale risorsa ip vengono eseguiti nello stesso host, quindi viene definito un vincolo di condivisione del percorso con un punteggio pari a infinito. 

Per impostare il vincolo di condivisione percorso per l'indirizzo IP virtuale per l'esecuzione nello stesso nodo master, eseguire il comando seguente in un nodo:

```bash
crm configure
colocation vip_on_master inf: \
    admin_addr ms-ag_cluster:Master
commit
```

### <a name="add-ordering-constraint"></a>Aggiungi vincolo di ordinamento
Il vincolo di condivisione percorso ha un vincolo di ordinamento implicito. Sposta la risorsa IP virtuale prima di spostare la risorsa del gruppo di disponibilità. Per impostazione predefinita è la sequenza di eventi: 

1. Risorsa utente di problemi la migrazione da node1 a node2 a principale del gruppo di disponibilità.
2. La risorsa IP virtuale viene arrestata nel nodo 1.
3. La risorsa IP virtuale verrà avviata nel nodo 2. A questo punto, l'indirizzo IP temporaneamente punti al nodo 2 mentre il nodo 2 è ancora un pre-failover secondario. 
4. Viene abbassato di livello principale del gruppo di disponibilità nel nodo 1 per slave.
5. Lo slave di gruppo di disponibilità nel nodo 2 venga innalzato di livello master. 

Per evitare temporaneamente che puntano al nodo con il database secondario pre-failover l'indirizzo IP, aggiungere un vincolo di ordinamento. Per aggiungere un vincolo di ordinamento, eseguire il comando seguente in un nodo: 

```bash
crm crm configure \
   order ag_first inf: ms-ag_cluster:promote admin_addr:start
```


>[!IMPORTANT]
>Dopo aver configurato il cluster e aggiungere il gruppo di disponibilità come risorsa cluster, è possibile usare Transact-SQL per eseguire il failover le risorse di gruppo di disponibilità. Risorse del cluster SQL Server in Linux non sono collegate come strettamente con il sistema operativo perché sono in un Server Failover Cluster WSFC (Windows). Servizio SQL Server non riconosce la presenza del cluster. Tutte le orchestrazioni vengono eseguite mediante gli strumenti di gestione di cluster. SLES usare `crm`. 

Eseguire manualmente il failover il gruppo di disponibilità con `crm`. Non avviare il failover con Transact-SQL. Per altre informazioni, vedere [Failover](sql-server-linux-availability-group-failover-ha.md#failover).


Per altre informazioni, vedere:
- [La gestione delle risorse cluster](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.config.crm).   
- [Disponibilità elevata di concetti](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.concepts)
- [Riferimento rapido di pacemaker](https://github.com/ClusterLabs/pacemaker/blob/master/doc/pcs-crmsh-quick-ref.md) 

<!---[!INCLUDE [Pacemaker Concepts](..\includes\ss-linux-cluster-pacemaker-concepts.md)]--->

## <a name="next-steps"></a>Passaggi successivi

[Funzionamento di gruppo di disponibilità elevata](sql-server-linux-availability-group-failover-ha.md)
