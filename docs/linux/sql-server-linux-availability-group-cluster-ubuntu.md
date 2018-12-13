---
title: Configurare Cluster di Ubuntu per gruppo di disponibilità di SQL Server | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 04/30/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: dd0d6fb9-df0a-41b9-9f22-9b558b2b2233
ms.openlocfilehash: 33b5631fdf834ea9a998f1dd4ae149dfe4cc6109
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/15/2018
ms.locfileid: "51658381"
---
# <a name="configure-ubuntu-cluster-and-availability-group-resource"></a>Configurare Cluster di Ubuntu e risorsa gruppo di disponibilità

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questo documento illustra come creare un cluster a tre nodi in Ubuntu e aggiungere un gruppo di disponibilità creato in precedenza come risorsa nel cluster. Per la disponibilità elevata, un gruppo di disponibilità in Linux richiede tre nodi, vedere la [elevata disponibilità e protezione dei dati per le configurazioni di gruppo di disponibilità](sql-server-linux-availability-group-ha.md).

> [!NOTE] 
> A questo punto, l'integrazione con Pacemaker in Linux SQL Server non è accoppiato come con WSFC per Windows. All'interno di SQL, non è possibile sapere sulla presenza del cluster, tutte le orchestrazioni non rientra e il servizio viene controllato in base a un'istanza autonoma per Pacemaker. Inoltre, nome di rete virtuale è specifico al cluster WSFC, è disponibile un equivalente dello stesso in Pacemaker. Always On viste a gestione dinamica che eseguire query sulle informazioni del cluster restituiscono le righe vuote. È comunque possibile creare un listener per usarlo per la riconnessione dopo il failover trasparente, ma è necessario registrare manualmente il nome del listener nel server DNS con l'indirizzo IP usato per creare la risorsa IP virtuale (come illustrato nelle sezioni seguenti).

Le sezioni seguenti illustrano i passaggi per configurare una soluzione di cluster di failover. 

## <a name="roadmap"></a>Guida di orientamento

I passaggi per creare un gruppo di disponibilità nei server Linux per la disponibilità elevata sono diversi dai passaggi in un cluster di failover di Windows Server. L'elenco seguente descrive i passaggi generali: 

1. [Configurare SQL Server nei nodi del cluster](sql-server-linux-setup.md).

2. [Creare il gruppo di disponibilità](sql-server-linux-availability-group-configure-ha.md). 

3. Configurare un cluster di resource manager, ad esempio Pacemaker. Queste istruzioni sono in questo documento.
   
   Il modo per configurare un gestore di risorse cluster dipende la distribuzione Linux specifica. 

   >[!IMPORTANT]
   >Gli ambienti di produzione richiedono un agente di isolamento, ad esempio STONITH per la disponibilità elevata. Le dimostrazioni in questa documentazione non usano gli agenti di fencing. Le dimostrazioni sono per i test e convalida solo. 
   
   >Un cluster Linux Usa l'isolamento per restituire il cluster a uno stato noto. Il modo per configurare l'isolamento varia a seconda della distribuzione e l'ambiente. A questo punto, l'isolamento non è disponibile in alcuni ambienti cloud. Visualizzare [criteri di supporto per RHEL cluster disponibilità elevata - piattaforme di virtualizzazione](https://access.redhat.com/articles/29440) per altre informazioni.

5.  [Aggiungere il gruppo di disponibilità come una risorsa in cluster](sql-server-linux-availability-group-cluster-ubuntu.md#create-availability-group-resource). 

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>Installare e configurare Pacemaker in ogni nodo del cluster

1. Aprire le porte del firewall in tutti i nodi. Aprire la porta per il servizio a disponibilità elevata di Pacemaker, istanza di SQL Server e l'endpoint del gruppo di disponibilità. La porta TCP predefinita per il server che esegue SQL Server è 1433.  

   ```bash
   sudo ufw allow 2224/tcp
   sudo ufw allow 3121/tcp
   sudo ufw allow 21064/tcp
   sudo ufw allow 5405/udp
        
   sudo ufw allow 1433/tcp # Replace with TDS endpoint
   sudo ufw allow 5022/tcp # Replace with DATA_MIRRORING endpoint
        
   sudo ufw reload
   ```
   
   In alternativa, è possibile disabilitare semplicemente il firewall:
        
   ```bash
   sudo ufw disable
   ```

1. Installare i pacchetti Pacemaker. In tutti i nodi, eseguire i comandi seguenti:

   ```bash
   sudo apt-get install pacemaker pcs fence-agents resource-agents
   ```

2. Impostare la password per l'utente predefinito creato durante l'installazione dei pacchetti Pacemaker e Corosync. Usare la stessa password in tutti i nodi. 

   ```bash
   sudo passwd hacluster
   ```

## <a name="enable-and-start-pcsd-service-and-pacemaker"></a>Abilitare e avviare il servizio pcsd e Pacemaker

Il comando seguente Abilita e avvia servizio pcsd e pacemaker. Eseguire in tutti i nodi. In questo modo i nodi ricostituire il cluster dopo il riavvio. 

```bash
sudo systemctl enable pcsd
sudo systemctl start pcsd
sudo systemctl enable pacemaker
```
>[!NOTE]
>Comando Enable pacemaker venga completata con l'errore 'pacemaker di avvio predefinita non contiene nessun runlevels, l'interruzione'. Si tratta di innocuo, configurazione del cluster può continuare. 

## <a name="create-the-cluster"></a>Creare il Cluster

1. Rimuovere qualsiasi configurazione cluster esistente da tutti i nodi. 

   In esecuzione 'sudo apt-get install PC' Installa PC, corosync e pacemaker nello stesso momento e viene avviata l'esecuzione di tutte le 3 dei servizi.  Avviare corosync genera un modello ' / etc/cluster/corosync.conf' file.  Disporre i passaggi successivi di esito positivo di questo file non dovrebbe esistere: la soluzione alternativa consiste nell'arrestare pacemaker / corosync ed eliminare ' / etc/cluster/corosync.conf', e quindi i passaggi successivi completata correttamente. 'pcs cluster destroy' esegue la stessa operazione e usarlo come un passaggio della configurazione iniziale del cluster di tempo.
   
   Il comando seguente rimuove qualsiasi file di configurazione del cluster esistenti e interrompe tutti i servizi del cluster. Questo elimina definitivamente il cluster. Eseguire l'utilità come primo passaggio in un ambiente di pre-produzione. Si noti che 'pcs cluster destroy' disabilitato il servizio pacemaker e deve essere riabilitata. Eseguire il comando seguente in tutti i nodi.
   
   >[!WARNING]
   >Il comando Elimina tutte le risorse cluster esistente.

   ```bash
   sudo pcs cluster destroy 
   sudo systemctl enable pacemaker
   ```

1. Creare il cluster. 

   >[!WARNING]
   >A causa di un problema noto che il fornitore del clustering viene analisi, a partire il cluster ('pcs cluster start') ha esito negativo con errore. Questo avviene perché il file di log configurati in /etc/corosync/corosync.conf che viene creato quando il comando di installazione del cluster viene eseguito, non è corretto. Per risolvere questo problema, modificare il file di log: /var/log/corosync/corosync.log. In alternativa è possibile creare il file /var/log/cluster/corosync.log.
 
   ```Error
   Job for corosync.service failed because the control process exited with error code. 
   See "systemctl status corosync.service" and "journalctl -xe" for details.
   ```
  
Il comando seguente crea un cluster a tre nodi. Prima di eseguire lo script, sostituire i valori compresi tra `< ... >`. Eseguire il comando seguente nel nodo primario. 

   ```bash
   sudo pcs cluster auth <node1> <node2> <node3> -u hacluster -p <password for hacluster>
   sudo pcs cluster setup --name <clusterName> <node1> <node2…> <node3>
   sudo pcs cluster start --all
   sudo pcs cluster enable --all
   ```
   
   >[!NOTE]
   >Se in precedenza è stato configurato un cluster negli stessi nodi, è necessario usare l'opzione '--force' quando si esegue 'pcs cluster setup'. Si noti che ciò equivale all'esecuzione di 'pcs cluster destroy' e il servizio Pacemaker deve essere riabilitato usando 'sudo systemctl enable pacemaker'.


## <a name="configure-fencing-stonith"></a>Configurare l'isolamento (STONITH)

I fornitori del cluster pacemaker richiedono STONITH deve essere abilitata e un dispositivo di fencing configurato per l'installazione del cluster supportate. Quando cluster resource manager non è possibile determinare lo stato di un nodo o di una risorsa in un nodo, l'isolamento consente di visualizzare di nuovo il cluster a uno stato noto. Isolamento a livello di risorsa principalmente assicura che non vi sia alcun danneggiamento dei dati in caso di interruzione tramite la configurazione di una risorsa. È possibile utilizzare l'isolamento a livello di risorsa, ad esempio, con DRBD (Distributed replicati blocco dispositivo) per contrassegnare il disco in un nodo come obsoleta quando il collegamento di comunicazione si arresta. Isolamento a livello di nodo assicura che un nodo non viene eseguita alcuna risorsa. In tal caso, reimpostare il nodo e l'implementazione di Pacemaker di esso viene chiamato STONITH (che è l'acronimo di "girare in altro nodo nell'intestazione"). Pacemaker supporta una vasta gamma di dispositivi fencing, ad esempio, una continuità o gestione schede di interfaccia di per i server. Per altre informazioni, vedere [cluster Pacemaker da zero](https://clusterlabs.org/doc/en-US/Pacemaker/1.1-plugin/html/Clusters_from_Scratch/ch05.html) e [Fencing e Stonith](https://clusterlabs.org/doc/crm_fencing.html) 

Poiché il livello del nodo recinzioni configurazione dipende principalmente dall'ambiente, è disabilitata per questa esercitazione (può essere configurato in un secondo momento). Eseguire lo script seguente nel nodo primario: 

```bash
sudo pcs property set stonith-enabled=false
```

>[!IMPORTANT]
>La disabilitazione di STONITH è solo a scopo di test. Se si prevede di utilizzare Pacemaker in un ambiente di produzione, è necessario pianificare un'implementazione di STONITH a seconda dell'ambiente e lasciarla abilitata. Si noti che a questo punto esistono fencing agenti per tutti gli ambienti cloud (tra cui Azure) o Hyper-V. Consequentially, il fornitore del cluster non offre il supporto per l'esecuzione di cluster di produzione in questi ambienti. 

## <a name="set-cluster-property-cluster-recheck-interval"></a>Impostare proprietà di cluster del cluster-Ricontrolla-intervallo

`cluster-recheck-interval` indica l'intervallo di polling in corrispondenza del quale il cluster controlla modifiche nei parametri delle risorse, i vincoli o altre opzioni di cluster. Se una replica diventa inattiva, il cluster tenta di riavviare la replica in base all'intervallo è associato mediante il `failure-timeout` valore e il `cluster-recheck-interval` valore. Ad esempio, se `failure-timeout` è impostato su 60 secondi e `cluster-recheck-interval` è impostato su 120 secondi, il riavvio viene eseguito un tentativo in base all'intervallo è maggiore di 60 secondi ma inferiore a 120 secondi. È consigliabile impostare timeout errore 60s e controlla di nuovo-cluster-interval su un valore maggiore di 60 secondi. Non è consigliabile impostare intervallo-cluster-nuova verifica su un valore ridotto.

Per aggiornare il valore della proprietà da `2 minutes` eseguire:

```bash
sudo pcs property set cluster-recheck-interval=2min
```

> [!IMPORTANT] 
> Se si dispone già di una risorsa gruppo di disponibilità gestita da un cluster Pacemaker, tenere presente che tutte le distribuzioni che usano la versione più recente disponibile Pacemaker pacchetto 1.1.18-11.el7 introducano un cambiamento di comportamento per il cluster iniziale-errore-è-errore irreversibile impostazione quando relativo il valore è false. Questa modifica interessa il flusso di lavoro di failover. Se una replica primaria si verifica un'interruzione, il cluster è previsto per il failover su una delle repliche secondarie disponibili. Al contrario, gli utenti noteranno che il cluster insiste avviare la replica primaria non riuscita. Se tale database primario non torna online (a causa di un'interruzione dell'alimentazione permanente), il cluster mai effettua il failover a un'altra replica secondaria disponibile. Grazie a questa modifica, una configurazione consigliata in precedenza per impostare start-errore-è-errore irreversibile non è più valida e l'impostazione deve essere ripristinato il valore predefinito di `true`. Inoltre, la risorsa del gruppo di disponibilità deve essere aggiornato per includere il `failover-timeout` proprietà. 
>
>Per aggiornare il valore della proprietà da `true` eseguire:
>
>```bash
>sudo pcs property set start-failure-is-fatal=true
>```
>
>Aggiornare le proprietà della risorsa del gruppo di disponibilità esistente `failure-timeout` al `60s` eseguire (sostituire `ag1` con il nome della risorsa gruppo di disponibilità):
>
>```bash
>pcs resource update ag1 meta failure-timeout=60s
>```

## <a name="install-sql-server-resource-agent-for-integration-with-pacemaker"></a>Installare l'agente delle risorse SQL Server per l'integrazione con Pacemaker

Eseguire i comandi seguenti in tutti i nodi. 

```bash
sudo apt-get install mssql-server-ha
```

## <a name="create-a-sql-server-login-for-pacemaker"></a>Creare un account di accesso di SQL Server per Pacemaker

[!INCLUDE [SLES-Create-SQL-Login](../includes/ss-linux-cluster-pacemaker-create-login.md)]

## <a name="create-availability-group-resource"></a>Crea risorsa gruppo di disponibilità

Per creare la risorsa del gruppo di disponibilità, usare `pcs resource create` comando e impostare le proprietà della risorsa. Comando seguente crea una `ocf:mssql:ag` tipo di risorsa per il gruppo di disponibilità con primario/secondario `ag1`. 

```bash
sudo pcs resource create ag_cluster ocf:mssql:ag ag_name=ag1 meta failure-timeout=30s --master meta notify=true

```

[!INCLUDE [required-synchronized-secondaries-default](../includes/ss-linux-cluster-required-synchronized-secondaries-default.md)]

## <a name="create-virtual-ip-resource"></a>Creare una risorsa IP virtuale

Per creare la risorsa indirizzo IP virtuale, eseguire il comando seguente in un nodo. Usare un indirizzo IP statico disponibile dalla rete. Prima di eseguire lo script, sostituire i valori compresi tra `< ... >` con un indirizzo IP valido.

```bash
sudo pcs resource create virtualip ocf:heartbeat:IPaddr2 ip=<10.128.16.240>
```

Non c'è Nessun nome server virtuale equivalente in Pacemaker. Per usare una stringa di connessione che punta al nome di un server di stringa e non usare l'indirizzo IP, registrare l'indirizzo di risorsa IP e nome del server virtuale desiderato nel DNS. Per le configurazioni di ripristino di emergenza, registrare il nome del server virtuale desiderato e l'indirizzo IP con i server DNS primario sia il sito di ripristino di emergenza.

## <a name="add-colocation-constraint"></a>Aggiungi vincolo di condivisione del percorso

Quasi ogni decisione di in un cluster Pacemaker, come scegliere in cui deve essere eseguita una risorsa, viene eseguita confrontando i punteggi. I punteggi vengono calcolati per ogni risorsa e cluster resource manager sceglie il nodo con il punteggio più alto per una determinata risorsa. (Se un nodo ha un punteggio negativo per una risorsa, la risorsa non è possibile eseguire su tale nodo.) Per configurare le decisioni del cluster, usare i vincoli. I vincoli hanno un punteggio. Se un vincolo ha un punteggio inferiore a infinito, è solo un'indicazione. Un punteggio pari a infinito indica che è obbligatorio. Per assicurarsi che la replica primaria e la risorsa indirizzo ip virtuale siano nello stesso host, definire un vincolo di condivisione del percorso con un punteggio pari a infinito. Per aggiungere il vincolo di condivisione del percorso, eseguire il comando seguente in un nodo. 

```bash
sudo pcs constraint colocation add virtualip ag_cluster-master INFINITY with-rsc-role=Master
```

## <a name="add-ordering-constraint"></a>Aggiungi vincolo di ordinamento

Il vincolo di condivisione percorso ha un vincolo di ordinamento implicito. Sposta la risorsa IP virtuale prima di spostare la risorsa del gruppo di disponibilità. Per impostazione predefinita è la sequenza di eventi:

1. Problemi degli utenti `pcs resource move` al gruppo di disponibilità primario da node1 a node2.
1. La risorsa IP virtuale viene arrestata in node1.
1. La risorsa IP virtuale verrà avviata in node2.

   >[!NOTE]
   >A questo punto, l'indirizzo IP temporaneamente punta a node2 mentre node2 è ancora un pre-failover secondario. 
   
1. Il gruppo di disponibilità primario in node1 viene abbassato di livello a quello secondario.
1. Il gruppo di disponibilità secondario in node2 viene promossa a primaria. 

Per evitare temporaneamente che puntano al nodo con il database secondario pre-failover l'indirizzo IP, aggiungere un vincolo di ordinamento. 

Per aggiungere un vincolo di ordinamento, eseguire il comando seguente in un nodo:

```bash
sudo pcs constraint order promote ag_cluster-master then start virtualip
```

>[!IMPORTANT]
>Dopo aver configurato il cluster e aggiungere il gruppo di disponibilità come risorsa cluster, è possibile usare Transact-SQL per eseguire il failover le risorse di gruppo di disponibilità. Risorse del cluster SQL Server in Linux non sono collegate come strettamente con il sistema operativo perché sono in un Server Failover Cluster WSFC (Windows). Servizio SQL Server non riconosce la presenza del cluster. Tutte le orchestrazioni vengono eseguite mediante gli strumenti di gestione di cluster. In Ubuntu o RHEL utilizzare `pcs`. 

<!---[!INCLUDE [Pacemaker Concepts](..\includes\ss-linux-cluster-pacemaker-concepts.md)]--->

## <a name="next-steps"></a>Passaggi successivi

[Funzionamento di gruppo di disponibilità elevata](sql-server-linux-availability-group-failover-ha.md)

