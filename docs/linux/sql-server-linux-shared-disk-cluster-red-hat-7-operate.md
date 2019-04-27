---
title: Gestione di cluster condiviso di Red Hat Enterprise Linux per SQL Server | Microsoft Docs
description: Implementare la disponibilità elevata tramite la configurazione del cluster di dischi condivisi di Red Hat Enterprise Linux per SQL Server.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 075ab7d8-8b68-43f3-9303-bbdf00b54db1
ms.openlocfilehash: 2967277ca109b9ee55221a7b12f5af891a5e45a2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62635587"
---
# <a name="operate-red-hat-enterprise-linux-shared-disk-cluster-for-sql-server"></a>Gestione cluster di dischi condivisi di Red Hat Enterprise Linux per SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questo documento descrive come eseguire le attività seguenti per SQL Server in un cluster di failover nel disco condiviso con Red Hat Enterprise Linux.

- Eseguire il failover manuale del cluster
- Monitorare un cluster di failover del servizio SQL Server
- Aggiungere un nodo del cluster
- Rimuovere un nodo del cluster
- Modificare la frequenza di monitoraggio delle risorse SQL Server

## <a name="architecture-description"></a>Descrizione dell'architettura

Il livello di clustering si basa su Red Hat Enterprise Linux (RHEL) [componente aggiuntivo a disponibilità elevata](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf) costruita basandosi su [Pacemaker](https://clusterlabs.org/). Corosync e Pacemaker coordinare le comunicazioni del cluster e la gestione delle risorse. L'istanza di SQL Server è attivo in un nodo o l'altro.

Il diagramma seguente illustra i componenti in un cluster Linux con SQL Server. 

![Red Hat Enterprise Linux 7 condiviso del disco Cluster SQL](./media/sql-server-linux-shared-disk-cluster-red-hat-7-configure/LinuxCluster.png) 

Per altre informazioni su configurazione del cluster, le opzioni degli agenti delle risorse e gestione, visitare [documentazione di riferimento RHEL](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/index.html).

## <a name = "failManual"></a>Cluster di failover manuale

Il `resource move` comando crea un vincolo forzando la risorsa da avviare nel nodo di destinazione.  Dopo l'esecuzione di `move` comando, l'esecuzione di risorse `clear` rimuoverà il vincolo, pertanto è possibile spostare la risorsa nuovamente o avere le risorse automaticamente il failover. 

```bash
sudo pcs resource move <sqlResourceName> <targetNodeName>  
sudo pcs resource clear <sqlResourceName> 
```

L'esempio seguente sposta la **mssqlha** risorsa a un nodo denominato **sqlfcivm2**e quindi rimuove il vincolo in modo che la risorsa è possibile spostare in un altro nodo in un secondo momento.  

```bash
sudo pcs resource move mssqlha sqlfcivm2 
sudo pcs resource clear mssqlha 
```

## <a name="monitor-a-failover-cluster-sql-server-service"></a>Monitorare un cluster di failover del servizio SQL Server

Visualizzare lo stato corrente del cluster:

```bash
sudo pcs status  
```

Visualizzare lo stato attivo del cluster e le risorse:

```bash
sudo crm_mon 
```

Visualizzare i log dell'agente di risorsa in `/var/log/cluster/corosync.log`

## <a name="add-a-node-to-a-cluster"></a>Aggiungere un nodo a un cluster

1. Controllare l'indirizzo IP per ogni nodo. Lo script seguente mostra l'indirizzo IP del nodo corrente. 

   ```bash
   ip addr show
   ```

3. Il nuovo nodo è necessario un nome univoco che è di 15 caratteri o meno. Per impostazione predefinita in Red Hat Linux è il nome del computer `localhost.localdomain`. Questo nome predefinito potrebbe non essere univoco ed è troppo lungo. Impostare il nome del computer del nuovo nodo. Impostare il nome del computer, aggiungerlo al `/etc/hosts`. Lo script seguente consente di modificare `/etc/hosts` con `vi`. 

   ```bash
   sudo vi /etc/hosts
   ```

   L'esempio seguente illustra `/etc/hosts` con le aggiunte per i tre nodi denominati `sqlfcivm1`, `sqlfcivm2`, e`sqlfcivm3`.

   ```
   127.0.0.1   localhost localhost4 localhost4.localdomain4
   ::1         localhost localhost6 localhost6.localdomain6
   10.128.18.128 fcivm1
   10.128.16.77 fcivm2
   10.128.14.26 fcivm3
    ```
    
   Il file deve essere identica in ogni nodo. 

1. Arrestare il servizio SQL Server nel nuovo nodo.

1. Seguire le istruzioni per montare la directory del file di database per la posizione condivisa:

   Dal server NFS, installare `nfs-utils`

   ```bash
   sudo yum -y install nfs-utils 
   ``` 

   Aprire il firewall nel client e server NFS 

   ```bash
   sudo firewall-cmd --permanent --add-service=nfs
   sudo firewall-cmd --permanent --add-service=mountd
   sudo firewall-cmd --permanent --add-service=rpc-bind
   sudo firewall-cmd --reload
   ```

   Modificare il file /etc/fstab per includere il comando di montaggio: 

   ```bash
   <IP OF NFS SERVER>:<shared_storage_path> <database_files_directory_path> nfs timeo=14,intr
   ```

   Eseguire `mount -a` rendere effettive le modifiche.
   
1. Nel nuovo nodo, creare un file per archiviare il nome utente di SQL Server e la password per l'accesso a Pacemaker. Il comando seguente crea e popola questo file:

   ```bash
   sudo touch /var/opt/mssql/passwd
   sudo echo "<loginName>" >> /var/opt/mssql/secrets/passwd
   sudo echo "<loginPassword>" >> /var/opt/mssql/secrets/passwd
   sudo chown root:root /var/opt/mssql/passwd
   sudo chmod 600 /var/opt/mssql/passwd
   ```

3. Nel nuovo nodo, aprire le porte del firewall di Pacemaker. Per aprire queste porte con `firewalld`, eseguire il comando seguente:

   ```bash
   sudo firewall-cmd --permanent --add-service=high-availability
   sudo firewall-cmd --reload
   ```

   > [!NOTE]
   > Se si usa un altro firewall che non dispone di una configurazione a disponibilità elevata predefinita, le porte seguenti devono essere aperte per consentire a essere in grado di comunicare con altri nodi del cluster Pacemaker
   >
   > * TCP: Porte 2224, 3121, 21064
   > * UDP: Porta 5405

1. Installare i pacchetti Pacemaker nel nuovo nodo.

   ```bash
   sudo yum install pacemaker pcs fence-agents-all resource-agents
   ```
 
2. Impostare la password per l'utente predefinito creato durante l'installazione dei pacchetti Pacemaker e Corosync. Usare la stessa password per i nodi esistenti. 

   ```bash
   sudo passwd hacluster
   ```
 
3. Abilitare e avviare il servizio `pcsd` e Pacemaker. In questo modo il nuovo nodo a partecipare di nuovo il cluster dopo il riavvio. Eseguire il comando seguente nel nuovo nodo.

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   sudo systemctl enable pacemaker
   ```

4. Installare l'agente delle risorse FCI per SQL Server. Eseguire i comandi seguenti nel nuovo nodo. 

   ```bash
   sudo yum install mssql-server-ha
   ```

1. In un nodo esistente dal cluster, eseguire l'autenticazione del nuovo nodo e aggiungerla al cluster:

    ```bash
    sudo pcs    cluster auth <nodeName3> -u hacluster 
    sudo pcs    cluster node add <nodeName3> 
    ```

    L'esempio seguente aggiunge un nodo denominato **vm3** al cluster.

    ```bash
    sudo pcs    cluster auth  
    sudo pcs    cluster start 
    ```

## <a name="remove-nodes-from-a-cluster"></a>Rimuovere nodi da un cluster

Per rimuovere un nodo da un cluster di cui eseguire il comando seguente:

```bash
sudo pcs    cluster node remove <nodeName>  
```

## <a name="change-the-frequency-of-sqlservr-resource-monitoring-interval"></a>Modificare la frequenza dell'intervallo di monitoraggio delle risorse sqlservr

```bash
sudo pcs    resource op monitor interval=<interval>s <sqlResourceName> 
```

L'esempio seguente imposta l'intervallo di monitoraggio su 2 secondi per la risorsa mssql:

```bash
sudo pcs    resource op monitor interval=2s mssqlha 
```
## <a name="troubleshoot-red-hat-enterprise-linux-shared-disk-cluster-for-sql-server"></a>Risolvere i problemi del cluster di dischi condivisi di Red Hat Enterprise Linux per SQL Server

Risoluzione dei problemi del cluster può essere utile per comprendere come i tre daemon funzionano insieme per gestire le risorse del cluster. 

| Daemon | Descrizione 
| ----- | -----
| Corosync | Fornisce l'appartenenza al quorum e la messaggistica tra i nodi del cluster.
| Pacemaker | Si trova nella parte superiore Corosync e fornisce le macchine a stati per le risorse. 
| PCSD | Consente di gestire sia Pacemaker e Corosync attraverso il `pcs` strumenti

PCSD deve essere in esecuzione per poter utilizzare `pcs` strumenti. 

### <a name="current-cluster-status"></a>Stato corrente del cluster 

`sudo pcs status` Restituisce le informazioni di base sullo stato del cluster, quorum, nodi, risorse e daemon per ogni nodo. 

Un esempio di output un quorum integro pacemaker sarebbe:

```
Cluster name: MyAppSQL 
Last updated: Wed Oct 31 12:00:00 2016  Last change: Wed Oct 31 11:00:00 2016 by root via crm_resource on sqlvmnode1 
Stack: corosync 
Current DC: sqlvmnode1  (version 1.1.13-10.el7_2.4-44eb2dd) - partition with quorum 
3 nodes and 1 resource configured 

Online: [ sqlvmnode1 sqlvmnode2 sqlvmnode3] 

Full list of resources: 

mssqlha (ocf::sql:fci): Started sqlvmnode1 

PCSD Status: 
sqlvmnode1: Online 
sqlvmnode2: Online 
sqlvmnode3: Online 

Daemon Status: 
corosync: active/disabled 
pacemaker: active/enabled 
```

Nell'esempio `partition with quorum` significa che un quorum di maggioranza dei nodi sia in linea. Se il cluster perde un quorum di maggioranza dei nodi `pcs status` restituirà `partition WITHOUT quorum` e verranno arrestate tutte le risorse. 

`online: [sqlvmnode1 sqlvmnode2 sqlvmnode3]` Restituisce il nome di tutti i nodi che fanno parte attualmente del cluster. Se non fanno parte di tutti i nodi, `pcs status` restituisce `OFFLINE: [<nodename>]`.

`PCSD Status` Mostra lo stato del cluster per ogni nodo.

### <a name="reasons-why-a-node-may-be-offline"></a>Motivi per cui un nodo potrebbe essere offline

Controllare i seguenti elementi quando un nodo è offline.

- **Firewall**

    Le porte seguenti devono essere aperte in tutti i nodi per Pacemaker essere in grado di comunicare.
    
    - **TCP: 2224, 3121, 21064

- **Pacemaker o Corosync servizi in esecuzione**

- **Comunicazione da nodo**

- **Mapping dei nomi di nodo**

## <a name="additional-resources"></a>Risorse aggiuntive

* [Cluster da zero](https://clusterlabs.org/doc/Cluster_from_Scratch.pdf) Guida da Pacemaker

## <a name="next-steps"></a>Passaggi successivi

[Configurare il cluster di dischi condivisi di Red Hat Enterprise Linux per SQL Server](sql-server-linux-shared-disk-cluster-red-hat-7-configure.md)

