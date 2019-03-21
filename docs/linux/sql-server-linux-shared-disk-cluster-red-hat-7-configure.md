---
title: Configurare cluster condiviso di Red Hat Enterprise Linux per SQL Server | Microsoft Docs
description: Implementare la disponibilità elevata tramite la configurazione del cluster di dischi condivisi di Red Hat Enterprise Linux per SQL Server.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: dcc0a8d3-9d25-4208-8507-a5e65d2a9a15
ms.openlocfilehash: 1801551b179cf7040f1eb5cbaa05d8eb3bebc564
ms.sourcegitcommit: 7d4a3fc0f2622cbc6930d792be4a9b3fcac4c4b6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/21/2019
ms.locfileid: "58306039"
---
# <a name="configure-red-hat-enterprise-linux-shared-disk-cluster-for-sql-server"></a>Configurare il cluster di dischi condivisi di Red Hat Enterprise Linux per SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questa guida fornisce istruzioni per creare un cluster di dischi condiviso a due nodi per SQL Server su Red Hat Enterprise Linux. Il livello di clustering si basa su Red Hat Enterprise Linux (RHEL) [componente aggiuntivo a disponibilità elevata](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf) costruita basandosi su [Pacemaker](https://clusterlabs.org/). L'istanza di SQL Server è attivo in un nodo o l'altro.

> [!NOTE] 
> L'accesso al componente aggiuntivo Red Hat a disponibilità elevata e alla documentazione richiede una sottoscrizione. 

Come illustrato nella figura seguente, archiviazione viene presentata a due server. Componenti di clustering - Corosync e Pacemaker - coordinano le comunicazioni e gestione delle risorse. Uno dei server con connessione attiva per le risorse di archiviazione e SQL Server. Quando Pacemaker rileva un errore i componenti di clustering gestiscono lo spostamento avvenga a altro nodo.  

![Red Hat Enterprise Linux 7 condiviso del disco Cluster SQL](./media/sql-server-linux-shared-disk-cluster-red-hat-7-configure/LinuxCluster.png) 

Per altre informazioni su configurazione del cluster, le opzioni degli agenti delle risorse e gestione, visitare [documentazione di riferimento RHEL](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/index.html).


> [!NOTE] 
> A questo punto, l'integrazione con Pacemaker di SQL Server non è accoppiato come con WSFC per Windows. All'interno di SQL, non è possibile sapere sulla presenza del cluster, tutte le orchestrazioni non rientra e il servizio viene controllato in base a un'istanza autonoma per Pacemaker. Inoltre, ad esempio, DM os_cluster_properties e DM os_cluster_nodes viste a gestione dinamica cluster non sarà alcun record.
Per usare una stringa di connessione che punta al nome di un server di stringa e non usare l'indirizzo IP, dovranno registrare i server DNS dell'indirizzo IP usato per creare la risorsa IP virtuale (come illustrato nelle sezioni seguenti) con il nome del server scelto.

Le sezioni seguenti illustrano i passaggi per configurare una soluzione di cluster di failover. 

## <a name="prerequisites"></a>Prerequisiti

Per completare lo scenario end-to-end seguente, è necessario due macchine virtuali da distribuire il cluster a due nodi e un altro server per configurare il server NFS. I passaggi seguenti illustrano la configurazione di questi server.

## <a name="setup-and-configure-the-operating-system-on-each-cluster-node"></a>Installare e configurare il sistema operativo in ogni nodo del cluster

Il primo passaggio consiste nel configurare il sistema operativo nei nodi del cluster. Per questa procedura dettagliata, usare RHEL con una sottoscrizione valida per il componente aggiuntivo a disponibilità elevata. 

## <a name="install-and-configure-sql-server-on-each-cluster-node"></a>Installare e configurare SQL Server in ogni nodo del cluster

1. Installare e configurare SQL Server su entrambi i nodi.  Per istruzioni dettagliate, vedere [installare SQL Server in Linux](sql-server-linux-setup.md).

1. Designare un nodo primario e l'altro come secondario, ai fini della configurazione. Usare questi termini per gli elementi seguenti in questa Guida.  

1. Nel nodo secondario, arrestare e disabilitare SQL Server.

   Nell'esempio seguente arresta e disattiva SQL Server: 

   ```bash
   sudo systemctl stop mssql-server
   sudo systemctl disable mssql-server
   ```
> [!NOTE] 
> In fase di installazione, viene generato per l'istanza di SQL Server e inserito in una chiave Master del Server `/var/opt/mssql/secrets/machine-key`. In Linux, SQL Server viene sempre eseguito come un account locale denominato mssql. Poiché si tratta di un account locale, la propria identità non è condiviso tra i nodi. Pertanto, è necessario copiare la chiave di crittografia dal nodo primario in ogni nodo secondario in modo che ogni account mssql locale possono accedervi per decrittografare la chiave Master del Server. 

1. Nel nodo primario, creare un account di accesso SQL server per Pacemaker e concedere l'autorizzazione di accesso per l'esecuzione `sp_server_diagnostics`. Pacemaker Usa questo account per verificare quale nodo è in esecuzione SQL Server. 

   ```bash
   sudo systemctl start mssql-server
   ```

   Connettersi a SQL Server `master` database con l'account sa e di eseguire il comando seguente:

   ```bashsql
   USE [master]
   GO
   CREATE LOGIN [<loginName>] with PASSWORD= N'<loginPassword>'

   ALTER SERVER ROLE [sysadmin] ADD MEMBER [<loginName>]
   ```
   In alternativa, è possibile impostare le autorizzazioni a un livello più granulare. Richiede l'accesso a Pacemaker `VIEW SERVER STATE` allo stato di integrità query con, sp_server_diagnostics `setupadmin` e `ALTER ANY LINKED SERVER` per aggiornare il nome dell'istanza FCI con il nome della risorsa tramite l'esecuzione sp_dropserver e sp_addserver. 

1. Nel nodo primario, arrestare e disabilitare SQL Server. 

1. Configurare il file hosts per ogni nodo del cluster. Il file host deve includere l'indirizzo IP e nome di ogni nodo del cluster. 

    Controllare l'indirizzo IP per ogni nodo. Lo script seguente mostra l'indirizzo IP del nodo corrente. 

   ```bash
   sudo ip addr show
   ```

   Impostare il nome del computer in ogni nodo. Assegnare a ogni nodo un nome univoco che è di 15 caratteri o meno. Impostare il nome del computer, aggiungerlo al `/etc/hosts`. Lo script seguente consente di modificare `/etc/hosts` con `vi`. 

   ```bash
   sudo vi /etc/hosts
   ```
   L'esempio seguente illustra `/etc/hosts` con le aggiunte di due nodi denominati `sqlfcivm1` e `sqlfcivm2`.

   ```bash
   127.0.0.1   localhost localhost4 localhost4.localdomain4
   ::1       localhost localhost6 localhost6.localdomain6
   10.128.18.128 sqlfcivm1
   10.128.16.77 sqlfcivm2
   ```

Nella sezione successiva si configurerà l'archiviazione condivisa e spostare i file di database in tale archivio. 

## <a name="configure-shared-storage-and-move-database-files"></a>Configurare l'archiviazione condivisa e spostare i file di database 

Esistono numerose soluzioni per fornire spazio di archiviazione condiviso. Questa procedura dettagliata viene illustrata la configurazione di archiviazione condivisa con NFS. È consigliabile seguire le procedure consigliate e usare Kerberos per la protezione di NFS (è possibile trovare un esempio di seguito: https://www.certdepot.net/rhel7-use-kerberos-control-access-nfs-network-shares/). 

>[!Warning]
>Se non si protegge NFS, quindi chiunque può accedere alla rete ed effettuare lo spoofing l'indirizzo IP di un nodo SQL sarà in grado di accedere ai file di dati. Come sempre, assicurarsi che il sistema una modellazione delle minacce è prima di utilizzarlo nell'ambiente di produzione. Un'altra opzione di archiviazione consiste nell'usare condivisione file SMB.

### <a name="configure-shared-storage-with-nfs"></a>Configurare l'archiviazione condivisa con NFS

> [!IMPORTANT] 
> Che ospitano i file di database in un server NFS con la versione < 4 non è supportata in questa versione. Ciò include l'uso di NFS per disco condiviso clustering di failover, nonché i database nelle istanze non cluster. Stiamo lavorando sull'abilitazione di altre versioni di server NFS nelle prossime versioni. 

Il Server NFS eseguire le operazioni seguenti:

1. Installare `nfs-utils`

   ```bash
   sudo yum -y install nfs-utils
   ```

1. Abilitare e avviare `rpcbind`

   ```bash
   sudo systemctl enable rpcbind && sudo systemctl start rpcbind
   ```

1. Abilitare e avviare `nfs-server`
 
   ```bash
   sudo systemctl enable nfs-server && sudo systemctl start nfs-server
   ```
 
1.  Modifica `/etc/exports` per esportare la directory in cui si vuole condividere. È necessario 1 riga per ogni condivisione desiderata. Esempio: 

   ```bash
   /mnt/nfs  10.8.8.0/24(rw,sync,no_subtree_check,no_root_squash)
   ```

1. Esporta le condivisioni

   ```bash
   sudo exportfs -rav
   ```

1. Verificare che i percorsi siano condivisi/esportato, eseguire dal server NFS

   ```bash
   sudo showmount -e
   ```

1. Aggiungere l'eccezione in SELinux

   ```bash
   sudo setsebool -P nfs_export_all_rw 1
   ```
   
1. Aprire il firewall, il server.

   ```bash 
   sudo firewall-cmd --permanent --add-service=nfs
   sudo firewall-cmd --permanent --add-service=mountd
   sudo firewall-cmd --permanent --add-service=rpc-bind
   sudo firewall-cmd --reload
   ```

### <a name="configure-all-cluster-nodes-to-connect-to-the-nfs-shared-storage"></a>Configurare tutti i nodi del cluster per la connessione alla risorsa di archiviazione condivise NFS

Eseguire i passaggi seguenti in tutti i nodi del cluster.

1.  Installare `nfs-utils`

   ```bash
   sudo yum -y install nfs-utils
   ```

1. Aprire il firewall nel client e server NFS

   ```bash
   sudo firewall-cmd --permanent --add-service=nfs
   sudo firewall-cmd --permanent --add-service=mountd
   sudo firewall-cmd --permanent --add-service=rpc-bind
   sudo firewall-cmd --reload
   ```

1. Verificare che è possibile visualizzare le condivisioni NFS nei computer client

   ```bash
   sudo showmount -e <IP OF NFS SERVER>
   ```

1. Ripetere questi passaggi in tutti i nodi del cluster.

Per altre informazioni sull'uso di NFS, vedere le risorse seguenti:

* [NFS Server e firewalld | Stack Exchange](https://unix.stackexchange.com/questions/243756/nfs-servers-and-firewalld)
* [Montare un Volume NFS | Manuale dell'amministratore di rete Linux](https://www.tldp.org/LDP/nag2/x-087-2-nfs.mountd.html)
* [Configurazione del server NFS | Red Hat Customer Portal](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/storage_administration_guide/nfs-serverconfig)

### <a name="mount-database-files-directory-to-point-to-the-shared-storage"></a>Montare directory dei file di database in modo che punti all'archiviazione condivisa

1.  **Nel nodo primario solo**, salvare i file di database in un percorso temporaneo. Lo script seguente, crea una nuova directory temporanee, copia i file di database nella nuova directory e consente di rimuovere i vecchi file di database. Come SQL Server viene eseguito come utente locale mssql, è necessario assicurarsi che dopo il trasferimento dei dati per la condivisione montata, utente locale abbia accesso in lettura-scrittura alla condivisione. 

   ``` 
   $ sudo su mssql
   $ mkdir /var/opt/mssql/tmp
   $ cp /var/opt/mssql/data/* /var/opt/mssql/tmp
   $ rm /var/opt/mssql/data/*
   $ exit
   ``` 

1.  In tutti i nodi del cluster modificare `/etc/fstab` file da includere il comando di montaggio.  

   ```bash
   <IP OF NFS SERVER>:<shared_storage_path> <database_files_directory_path> nfs timeo=14,intr 
   ```
   
   Lo script seguente illustra un esempio di modifica.  

   ``` 
   10.8.8.0:/mnt/nfs /var/opt/mssql/data nfs timeo=14,intr 
   ``` 
> [!NOTE] 
>Se si usa una risorsa di File System (FS) come consigliato in questo caso, non è necessario mantenere il comando di montaggio in /etc/fstab. Pacemaker si occuperà di montaggio nella cartella quando avvia la risorsa di ADFS in cluster. Con l'aiuto di fencing, garantirà che il FS mai è montata due volte. 

1.  Eseguire `mount -a` comando dal sistema aggiornare i percorsi montati.  

1.  Copiare i file di database e di log salvato `/var/opt/mssql/tmp` per la condivisione montata appena `/var/opt/mssql/data`. Questo deve essere svolto **nel nodo primario**. Accertarsi di assegnare le autorizzazioni di lettura / scrittura all'utente locale 'mssql'.

   ``` 
   $ sudo chown mssql /var/opt/mssql/data
   $ sudo chgrp mssql /var/opt/mssql/data
   $ sudo su mssql
   $ cp /var/opt/mssql/tmp/* /var/opt/mssql/data/
   $ rm /var/opt/mssql/tmp/*
   $ exit
   ``` 
 
1.  Verificare che SQL Server viene avviato correttamente con il nuovo percorso del file. Eseguire questa operazione in ogni nodo. A questo punto un solo nodo deve eseguire SQL Server alla volta. Non possono entrambi eseguono contemporaneamente perché sono entrambi tenterà di accedere ai file di dati contemporaneamente (per evitare accidentalmente l'avvio di SQL Server su entrambi i nodi, usare una risorsa cluster di File System per assicurarsi che la condivisione non è montata due volte per i vari nodi). I seguenti comandi avviare SQL Server, controllare lo stato e quindi arrestare SQL Server.
 
   ```bash
   sudo systemctl start mssql-server
   sudo systemctl status mssql-server
   sudo systemctl stop mssql-server
   ```
 
A questo punto, entrambe le istanze di SQL Server configurate per eseguire con i file di database nello spazio di archiviazione condiviso. Il passaggio successivo consiste nel configurare SQL Server per Pacemaker. 

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>Installare e configurare Pacemaker in ogni nodo del cluster


2. In entrambi i nodi del cluster creare un file per archiviare nome utente e password di SQL Server per l'accesso a Pacemaker. Il comando seguente crea e popola questo file:

   ```bash
   sudo touch /var/opt/mssql/secrets/passwd
   echo '<loginName>' | sudo tee -a /var/opt/mssql/secrets/passwd
   echo '<loginPassword>' | sudo tee -a /var/opt/mssql/secrets/passwd
   sudo chown root:root /var/opt/mssql/secrets/passwd 
   sudo chmod 600 /var/opt/mssql/secrets/passwd    
   ```

3. In entrambi i nodi del cluster aprire le porte del firewall di Pacemaker. Per aprire queste porte con `firewalld`, eseguire il comando seguente:

   ```bash
   sudo firewall-cmd --permanent --add-service=high-availability
   sudo firewall-cmd --reload
   ```

   > Se si usa un altro firewall che non dispone di una configurazione a disponibilità elevata predefinita, le porte seguenti devono essere aperte per consentire a essere in grado di comunicare con altri nodi del cluster Pacemaker
   >
   > * TCP: Porte 2224, 3121, 21064
   > * UDP: Porta 5405

1. Installare i pacchetti Pacemaker in ogni nodo.

   ```bash
   sudo yum install pacemaker pcs fence-agents-all resource-agents
   ```

    

2. Impostare la password per l'utente predefinito creato durante l'installazione dei pacchetti Pacemaker e Corosync. Usare la stessa password in entrambi i nodi. 

   ```bash
   sudo passwd hacluster
   ```

    

3. Abilitare e avviare il servizio `pcsd` e Pacemaker. In questo modo, i nodi potranno unirsi nuovamente in join con il cluster dopo il riavvio. Eseguire il comando seguente in entrambi i nodi.

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   sudo systemctl enable pacemaker
   ```

4. Installare l'agente delle risorse FCI per SQL Server. Eseguire i comandi seguenti in entrambi i nodi. 

   ```bash
   sudo yum install mssql-server-ha
   ```

## <a name="create-the-cluster"></a>Creare il cluster 

1. In uno dei nodi, creare il cluster.

   ```bash
   sudo pcs cluster auth <nodeName1 nodeName2 ...> -u hacluster
   sudo pcs cluster setup --name <clusterName> <nodeName1 nodeName2 ...>
   sudo pcs cluster start --all
   ```

   > Componente aggiuntivo RHEL a disponibilità elevata include conflitti degli agenti per KVM e VMWare. Fencing deve essere disabilitato in tutti gli altri hypervisor. La disabilitazione degli agenti di fencing è sconsigliata negli ambienti di produzione. A partire da periodo di tempo, esistono agenti fencing per gli ambienti Hyper-v o il cloud. Se si esegue una di queste configurazioni, è necessario disabilitare l'isolamento. \**NON è consigliato in un sistema di produzione.**

   Questo comando disabilita gli agenti di fencing.

   ```bash
   sudo pcs property set stonith-enabled=false
   sudo pcs property set start-failure-is-fatal=false
   ```

2. Configurare le risorse del cluster di SQL Server, File System e le risorse IP virtuali ed eseguire il push della configurazione del cluster. Sono necessarie le informazioni seguenti:

   - **Nome risorsa SQL Server**: Un nome per la risorsa cluster di SQL Server. 
   - **Nome della risorsa IP mobile**: Un nome per la risorsa indirizzo IP virtuale.
   - **Indirizzo IP**: L'indirizzo IP che i client useranno per connettersi all'istanza del cluster di SQL Server. 
   - **Il nome di risorsa sistema**: Un nome per la risorsa File System.
   - **device**: Percorso di condivisione NFS
   - **device**: Il percorso locale che viene montata la condivisione
   - **fstype**: Tipo di condivisione file (ad esempio nfs)

   Aggiornare i valori dallo script seguente per l'ambiente. Eseguire in un nodo per configurare e avviare il servizio cluster.  

   ```bash
   sudo pcs cluster cib cfg 
   sudo pcs -f cfg resource create <sqlServerResourceName> ocf:mssql:fci
   sudo pcs -f cfg resource create <floatingIPResourceName> ocf:heartbeat:IPaddr2 ip=<ip Address>
   sudo pcs -f cfg resource create <fileShareResourceName> Filesystem device=<networkPath> directory=<localPath>         fstype=<fileShareType>
   sudo pcs -f cfg constraint colocation add <virtualIPResourceName> <sqlResourceName>
   sudo pcs -f cfg constraint colocation add <fileShareResourceName> <sqlResourceName> 
   sudo pcs cluster cib-push cfg
   ```

   Ad esempio, lo script seguente crea una risorsa cluster di SQL Server denominata `mssqlha`e una risorsa IP mobile con l'indirizzo IP `10.0.0.99`. Inoltre crea una risorsa del file System e aggiunge i vincoli in modo che tutte le risorse condivideranno il percorso sul nodo stesso come risorsa di SQL. 

   ```bash
   sudo pcs cluster cib cfg
   sudo pcs -f cfg resource create mssqlha ocf:mssql:fci
   sudo pcs -f cfg resource create virtualip ocf:heartbeat:IPaddr2 ip=10.0.0.99
   sudo pcs -f cfg resource create fs Filesystem device="10.8.8.0:/mnt/nfs" directory="/var/opt/mssql/data" fstype="nfs"
   sudo pcs -f cfg constraint colocation add virtualip mssqlha
   sudo pcs -f cfg constraint colocation add fs mssqlha
   sudo pcs cluster cib-push cfg
   ```

   Dopo la configurazione viene eseguito il push, SQL Server viene avviato in un nodo. 

3. Verificare che SQL Server è stato avviato. 

   ```bash
   sudo pcs status 
   ```

   Negli esempi seguenti vengono illustrati i risultati quando Pacemaker è avviata un'istanza cluster di SQL Server. 

   ```
   fs     (ocf::heartbeat:Filesystem):    Started sqlfcivm1
   virtualip     (ocf::heartbeat:IPaddr2):      Started sqlfcivm1
   mssqlha  (ocf::mssql:fci): Started sqlfcivm1
   
   PCSD Status:
    slqfcivm1: Online
    sqlfcivm2: Online
   
   Daemon Status:
    corosync: active/disabled
    pacemaker: active/enabled
    pcsd: active/enabled
   ```

## <a name="additional-resources"></a>Risorse aggiuntive

* [Cluster da zero](https://clusterlabs.org/doc/Cluster_from_Scratch.pdf) Guida da Pacemaker

## <a name="next-steps"></a>Passaggi successivi

[Funzionamento di SQL Server in cluster di dischi condivisi di Red Hat Enterprise Linux](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
