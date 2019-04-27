---
title: "Configurare l'istanza del cluster di failover: SQL Server su Linux (RHEL) | Microsoft Docs"
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/28/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 31c8c92e-12fe-4728-9b95-4bc028250d85
ms.openlocfilehash: adfd7ad72fcc9f9e3e619c7798d68c536e4370e4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62635679"
---
# <a name="configure-failover-cluster-instance---sql-server-on-linux-rhel"></a>Configurare l'istanza del cluster di failover: SQL Server su Linux (RHEL)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Un'istanza cluster di failover di SQL Server nel disco condiviso due nodi fornisce ridondanza a livello di server per la disponibilità elevata. In questa esercitazione descrive come creare un'istanza del cluster di failover a due nodi di SQL Server in Linux. I passaggi specifici che è necessario completare includono:

> [!div class="checklist"]
> * Installare e configurare Linux
> * Installare e configurare SQL Server
> * Configurare il file hosts
> * Configurare l'archiviazione condivisa e spostare i file di database
> * Installare e configurare Pacemaker in ogni nodo del cluster
> * Configurare l'istanza del cluster di failover

Questo articolo illustra come creare un'istanza di cluster di failover (FCI) due nodi nel disco condiviso per SQL Server. L'articolo include istruzioni ed esempi di script per Red Hat Enterprise Linux (RHEL). Distribuzioni Ubuntu sono simili a RHEL in modo che gli esempi di script in genere funzionano anche in Ubuntu. 

Per informazioni concettuali, vedere [istanza SQL Server Failover Cluster (FCI) in Linux](sql-server-linux-shared-disk-cluster-concepts.md).

## <a name="prerequisites"></a>Prerequisiti

Per completare lo scenario end-to-end seguente, è necessario due macchine virtuali da distribuire il cluster a due nodi e un altro server per l'archiviazione. I passaggi seguenti illustrano la configurazione di questi server.

## <a name="set-up-and-configure-linux"></a>Installare e configurare Linux

Il primo passaggio consiste nel configurare il sistema operativo nei nodi del cluster. In ogni nodo del cluster, configurare una distribuzione linux. Usare la distribuzione e la versione stesso in entrambi i nodi. Usare uno o l'altra delle distribuzioni seguenti:
    
* RHEL con una sottoscrizione valida per il componente aggiuntivo a disponibilità elevata

## <a name="install-and-configure-sql-server"></a>Installare e configurare SQL Server

1. Installare e configurare SQL Server su entrambi i nodi.  Per istruzioni dettagliate, vedere [installare SQL Server in Linux](sql-server-linux-setup.md).
1. Designare un nodo primario e l'altro come secondario, ai fini della configurazione. Usare questi termini per gli elementi seguenti in questa Guida.  
1. Nel nodo secondario, arrestare e disabilitare SQL Server.
    Nell'esempio seguente arresta e disattiva SQL Server: 
    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl disable mssql-server
    ```

    > [!NOTE] 
    > Set tempo di attività, viene generato per l'istanza di SQL Server e inserito in una chiave Master del Server `var/opt/mssql/secrets/machine-key`. In Linux, SQL Server viene sempre eseguito come un account locale denominato mssql. Poiché si tratta di un account locale, la propria identità non è condiviso tra i nodi. Pertanto, è necessario copiare la chiave di crittografia dal nodo primario in ogni nodo secondario in modo che ogni account mssql locale possono accedervi per decrittografare la chiave Master del Server. 

1.  Nel nodo primario, creare un account di accesso SQL server per Pacemaker e concedere l'autorizzazione di accesso per l'esecuzione `sp_server_diagnostics`. Pacemaker Usa questo account per verificare quale nodo è in esecuzione SQL Server. 

    ```bash
    sudo systemctl start mssql-server
    ```
   
   Connettersi a SQL Server `master` database con l'account sa e di eseguire il comando seguente:

   ```sql
   USE [master]
   GO
   CREATE LOGIN [<loginName>] with PASSWORD= N'<loginPassword>'
   ALTER SERVER ROLE [sysadmin] ADD MEMBER [<loginName>]
   ```

   In alternativa, è possibile impostare le autorizzazioni a un livello più granulare. Richiede l'accesso a Pacemaker `VIEW SERVER STATE` allo stato di integrità query con, sp_server_diagnostics `setupadmin` e `ALTER ANY LINKED SERVER` per aggiornare il nome dell'istanza FCI con il nome della risorsa tramite l'esecuzione sp_dropserver e sp_addserver. 

1. Nel nodo primario, arrestare e disabilitare SQL Server. 

## <a name="configure-the-hosts-file"></a>Configurare il file hosts

In ogni nodo del cluster, configurare il file hosts. Il file hosts deve includere l'indirizzo IP e nome di ogni nodo del cluster.

1. Controllare l'indirizzo IP per ogni nodo. Lo script seguente mostra l'indirizzo IP del nodo corrente. 

    ```bash
    sudo ip addr show
    ```

1. Impostare il nome del computer in ogni nodo. Assegnare a ogni nodo un nome univoco che è di 15 caratteri o meno. Impostare il nome del computer, aggiungerlo al `/etc/hosts`. Lo script seguente consente di modificare `/etc/hosts` con `vi`. 

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

## <a name="configure-storage--move-database-files"></a>Configurare l'archiviazione e spostare i file di database  

È necessario fornire spazio di archiviazione possono accedere a entrambi i nodi. È possibile usare NFS, iSCSI o SMB. Configurare l'archiviazione, presentare l'archiviazione per i nodi del cluster e quindi spostare i file di database nella nuova archiviazione. Gli articoli seguenti illustrano i passaggi per ogni tipo di archiviazione:

- [Configurare l'istanza del cluster di failover SQL Server in Linux - iSCSI:](sql-server-linux-shared-disk-cluster-configure-iscsi.md)
- [Configurare cluster di failover - NFS - SQL Server in Linux](sql-server-linux-shared-disk-cluster-configure-nfs.md)
- [Configurare cluster di failover - SMB - SQL Server in Linux](sql-server-linux-shared-disk-cluster-configure-smb.md)

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>Installare e configurare Pacemaker in ogni nodo del cluster

1. In entrambi i nodi del cluster creare un file per archiviare nome utente e password di SQL Server per l'accesso a Pacemaker. 

    Il comando seguente crea e popola questo file:

    ```bash
    sudo touch /var/opt/mssql/secrets/passwd
    sudo echo '<loginName>' >> /var/opt/mssql/secrets/passwd
    sudo echo '<loginPassword>' >> /var/opt/mssql/secrets/passwd
    sudo chown root:root /var/opt/mssql/secrets/passwd 
    sudo chmod 600 /var/opt/mssql/secrets/passwd    
    ```

1. In entrambi i nodi del cluster aprire le porte del firewall di Pacemaker. Per aprire queste porte con `firewalld`, eseguire il comando seguente:

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
1. Impostare la password per l'utente predefinito creato durante l'installazione dei pacchetti Pacemaker e Corosync. Usare la stessa password in entrambi i nodi. 

   ```bash
   sudo passwd hacluster
   ```
1. Abilitare e avviare il servizio `pcsd` e Pacemaker. In questo modo, i nodi potranno unirsi nuovamente in join con il cluster dopo il riavvio. Eseguire il comando seguente in entrambi i nodi.

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   sudo systemctl enable pacemaker
   ```

1. Installare l'agente delle risorse FCI per SQL Server. Eseguire i comandi seguenti in entrambi i nodi. 

   ```bash
   sudo yum install mssql-server-ha
   ```

## <a name="configure-the-failover-cluster-instance"></a>Configurare l'istanza del cluster di failover

Verrà creato l'istanza FCI in un gruppo di risorse. Questo è un po' più semplice perché il gruppo di risorse riduce la necessità per i vincoli. Tuttavia, aggiungere le risorse nel gruppo di risorse nell'ordine in che cui deve iniziare. L'ordine che devono avviare è: 

1. Risorsa di archiviazione
2. Risorse di rete
3. Risorsa dell'applicazione

Questo esempio viene creato un'istanza FCI NewLinFCIGrp del gruppo. Il nome del gruppo di risorse deve essere univoco rispetto a qualsiasi risorsa creata in Pacemaker.

1.  Creare la risorsa disco. Se non esiste un problema, non si otterrà alcuna risposta. Il modo per creare la risorsa disco dipende dal tipo di archiviazione. Di seguito è riportato un esempio per ogni tipo di archiviazione. Usare l'esempio in cui si applica al tipo di archiviazione per l'archiviazione in cluster.

    **iSCSI**

    ```bash
    sudo pcs resource create <iSCSIDiskResourceName> Filesystem device="/dev/<VolumeGroupName>/<LogicalVolumeName>" directory="<FolderToMountiSCSIDisk>" fstype="<FileSystemType>" --group RGName
    ```

    \<iSCSIDIskResourceName > è il nome della risorsa associato al disco iSCSI

    \<VolumeGroupName > è il nome del gruppo di volumi  

    \<LogicalVolumeName > è il nome del volume logico che è stato creato  

    \<FolderToMountiSCSIDIsk > è la cartella per montare il disco (per i database di sistema e il percorso predefinito, sarebbe /var/opt/mssql/data)

    \<FileSystemType > sarebbe EXT4 o XFS a seconda del modo in cui sono state formattate le cose e quali la distribuzione supporta. 

    **NFS**

    ```bash
    sudo pcs resource create <NFSDiskResourceName> Filesystem device="<IPAddressOfNFSServer>:<FolderOnNFSServer>" directory="<FolderToMountNFSShare>" fstype=nfs4 options=" nfsvers=4.2,timeo=14,intr" --group RGName
    mount -t nfs4 IPAddressOfNFSServer:FolderOnNFSServer /var/opt/mssql/data -o 
    ```

    \<NFSDIskResourceName > è il nome della risorsa associato nella condivisione NFS

    \<IPAddressOfNFSServer > è l'indirizzo IP del server NFS che si intende usare

    \<FolderOnNFSServer > è il nome della condivisione NFS

    \<FolderToMountNFSShare > è la cartella per montare il disco (per i database di sistema e il percorso predefinito, sarebbe /var/opt/mssql/data)

    Di seguito è riportato un esempio:

    ```bash
    mount -t nfs4 200.201.202.63:/var/nfs/fci1 /var/opt/mssql/data -o nfsvers=4.2,timeo=14,intr
    ```

    **SMB**

    ```bash
    sudo pcs resource create SMBDiskResourceName Filesystem device="//<ServerName>/<ShareName>" directory="<FolderName>" fstype=cifs options="vers=3.0,username=<UserName>,password=<Password>,domain=<ADDomain>,uid=<mssqlUID>,gid=<mssqlGID>,file_mode=0777,dir_mode=0777" --group <RGName>
    ```

    \<ServerName > è il nome del server con la condivisione SMB

    \<ShareName > è il nome della condivisione

    \<Nomecartella > è il nome della cartella creata nel passaggio precedente
    
    \<Nome utente > è il nome dell'utente per accedere alla condivisione

    \<Password > è la password per l'utente

    \<ADDomain > è il dominio di Active Directory Domain Services (se applicabile quando si usa una condivisione SMB basate su Windows Server)

    \<mssqlUID > è l'UID dell'utente mssql

    \<mssqlGID > è il GID dell'utente mssql

    \<RGName > è il nome del gruppo di risorse
 
2.  Creare l'indirizzo IP che verrà utilizzato dall'istanza FCI. Se non esiste un problema, non si otterrà alcuna risposta.

    ```bash
    sudo pcs resource create <IPResourceName> ocf:heartbeat:IPaddr2 ip=<IPAddress> nic=<NetworkCard> cidr_netmask=<NetMask> --group <RGName>
    ```

    \<IPResourceName > è il nome della risorsa associato all'indirizzo IP

    \<Indirizzo IP > è l'indirizzo IP per l'istanza FCI

    \<NetworkCard > è la scheda di rete associata alla subnet (ad esempio eth0)

    \<Subnet mask > è la subnet mask della subnet (ad esempio 24)

    \<RGName > è il nome del gruppo di risorse
 
3.  Creare la risorsa di infrastruttura di classificazione file. Se non esiste un problema, non si otterrà alcuna risposta.

    ```bash
    sudo pcs resource create FCIResourceName ocf:mssql:fci op defaults timeout=60s --group RGName
    ```

    \<FCIResourceName > è il nome della risorsa non solo, ma il nome descrittivo associato con l'istanza FCI. Questo è ciò che utenti e applicazioni useranno per connettersi. 

    \<RGName > è il nome del gruppo di risorse.
 
4.  Eseguire il comando `sudo pcs resource`. L'istanza FCI deve essere online.
 
5.  Connettersi all'istanza di FCI con SSMS o sqlcmd usando il nome DNS/risorsa dell'istanza FCI.

6.  Eseguire l'istruzione `SELECT @@SERVERNAME`. Deve restituire il nome dell'istanza FCI.

7.  Eseguire l'istruzione `SELECT SERVERPROPERTY('ComputerNamePhysicalNetBIOS')`. Deve restituire il nome del nodo in cui è in esecuzione l'istanza FCI.

8.  Effettuare manualmente l'infrastruttura di classificazione file per gli altri nodi. Vedere le istruzioni riportate sotto [istanza del cluster di failover Operate - SQL Server in Linux](sql-server-linux-shared-disk-cluster-operate.md).

9.  Infine, eseguire il failover sul nodo originale e rimuovere il vincolo con più sedi.

<!---

|Distribution |Topic 
|----- |-----
|**Red Hat Enterprise Linux with HA add-on** |[Configure](sql-server-linux-shared-disk-cluster-red-hat-7-configure.md)<br/>[Operate](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
|**SUSE Linux Enterprise Server with HA add-on** |[Configure](sql-server-linux-shared-disk-cluster-sles-configure.md)

-->
## <a name="summary"></a>Riepilogo

In questa esercitazione sono completate le attività seguenti.

> [!div class="checklist"]
> * Installare e configurare Linux
> * Installare e configurare SQL Server
> * Configurare il file hosts
> * Configurare l'archiviazione condivisa e spostare i file di database
> * Installare e configurare Pacemaker in ogni nodo del cluster
> * Configurare l'istanza del cluster di failover

## <a name="next-steps"></a>Passaggi successivi

- [Funzionamento di istanza del cluster di failover: SQL Server in Linux](sql-server-linux-shared-disk-cluster-operate.md)

<!--Image references-->
