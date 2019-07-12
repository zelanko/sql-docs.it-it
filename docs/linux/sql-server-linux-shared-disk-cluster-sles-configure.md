---
title: Configurare cluster di dischi condiviso SLES per SQL Server
description: Implementare la disponibilità elevata tramite la configurazione del cluster di dischi condivisi per SUSE Linux Enterprise Server (SLES) per SQL Server.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
manager: jroth
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: e5ad1bdd-c054-4999-a5aa-00e74770b481
ms.openlocfilehash: 0b65c2cca781dc077e72ff06fb7de5ae8ee2e8c5
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2019
ms.locfileid: "67834652"
---
# <a name="configure-sles-shared-disk-cluster-for-sql-server"></a>Configurare cluster di dischi condiviso SLES per SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questa guida fornisce istruzioni per creare un cluster di dischi condivisi di due nodi per SQL Server su SUSE Linux Enterprise Server (SLES). Il livello di clustering si basa su SUSE [estensione a disponibilità elevata (Georgiano)](https://www.suse.com/products/highavailability) costruita basandosi su [Pacemaker](https://clusterlabs.org/). 

Per altre informazioni su configurazione del cluster, opzioni dell'agente di risorsa, gestione, le procedure consigliate e indicazioni, vedere [SUSE Linux Enterprise ad alta disponibilità estensione 12 SP2](https://www.suse.com/documentation/sle-ha-12/index.html).

## <a name="prerequisites"></a>Prerequisiti

Per completare lo scenario end-to-end seguente, è necessario due macchine virtuali da distribuire il cluster a due nodi e un altro server per configurare la condivisione NFS. I passaggi seguenti illustrano la configurazione di questi server.

## <a name="setup-and-configure-the-operating-system-on-each-cluster-node"></a>Installare e configurare il sistema operativo in ogni nodo del cluster

Il primo passaggio consiste nel configurare il sistema operativo nei nodi del cluster. Per questa procedura dettagliata, usare SLES con una sottoscrizione valida per il componente aggiuntivo a disponibilità elevata.

## <a name="install-and-configure-sql-server-on-each-cluster-node"></a>Installare e configurare SQL Server in ogni nodo del cluster

1. Installare e configurare SQL Server su entrambi i nodi. Per istruzioni dettagliate, vedere [installare SQL Server in Linux](sql-server-linux-setup.md).
2. Designare un nodo primario e l'altro come secondario, ai fini della configurazione. Usare questi termini per gli elementi seguenti in questa Guida. 
3. Nel nodo secondario, arrestare e disabilitare SQL Server. Nell'esempio seguente arresta e disattiva SQL Server:

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl disable mssql-server
    ```

    > [!NOTE]
    > In fase di installazione, viene generato per l'istanza di SQL Server e inserito in una chiave Master del Server `/var/opt/mssql/secrets/machine-key`. In Linux, SQL Server viene sempre eseguito come un account locale denominato mssql. Poiché si tratta di un account locale, la propria identità non è condiviso tra i nodi. Pertanto, è necessario copiare la chiave di crittografia dal nodo primario in ogni nodo secondario in modo che ogni account mssql locale possono accedervi per decrittografare la chiave Master del Server.
4. Nel nodo primario, creare un account di accesso SQL server per Pacemaker e concedere l'autorizzazione di accesso per l'esecuzione `sp_server_diagnostics`. Pacemaker Usa questo account per verificare quale nodo è in esecuzione SQL Server.

    ```bash
    sudo systemctl start mssql-server
    ```
    Connettersi al database master di SQL Server con l'account 'sa' ed eseguire il comando seguente:

    ```sql
    USE [master]
    GO
    CREATE LOGIN [<loginName>] with PASSWORD= N'<loginPassword>'
    GRANT VIEW SERVER STATE TO <loginName>
    ```
5. Nel nodo primario, arrestare e disabilitare SQL Server.
6. Seguire le istruzioni riportate [nella documentazione di SUSE](https://www.suse.com/documentation/sles11/book_sle_admin/data/sec_basicnet_yast.html) per configurare e aggiornare il file hosts per ogni nodo del cluster. Il file "hosts" deve includere l'indirizzo IP e nome di ogni nodo del cluster.

    Per controllare l'indirizzo IP del nodo corrente eseguire:

    ```bash
    sudo ip addr show
    ```

    Impostare il nome del computer in ogni nodo. Assegnare a ogni nodo un nome univoco che è di 15 caratteri o meno. Impostare il nome del computer, aggiungerlo al `/etc/hostname` usando [yast](https://www.suse.com/documentation/sles11/book_sle_admin/data/sec_basicnet_yast.html) oppure [manualmente](https://www.suse.com/documentation/sled11/book_sle_admin/data/sec_basicnet_manconf.html).

    L'esempio seguente illustra `/etc/hosts` con le aggiunte di due nodi denominati `SLES1` e `SLES2`.

    ```
    127.0.0.1   localhost
    10.128.18.128 SLES1
    10.128.16.77 SLES2
    ```

    > [!NOTE]
    > Tutti i nodi del cluster devono essere in grado di accedere reciprocamente tramite SSH. Strumenti come hb_report o crm_report (per la risoluzione dei problemi) e History Explorer di Hawk richiedono l'accesso a SSH tra i nodi senza password, in caso contrario possono raccogliere dati solo dal nodo corrente. Nel caso in cui si usa una porta SSH non standard, usare l'opzione -X ([vedere pagina](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_requirements_other.html)). Ad esempio, se la porta SSH è 3479, richiamare un crm_report con:
    >
    >```bash
    >crm_report -X "-p 3479" [...]
    >```
    >Per altre informazioni, vedere [Guida all'amministrazione]. (https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.troubleshooting.misc)

Nella sezione successiva si configurerà l'archiviazione condivisa e spostare i file di database in tale archivio.  

## <a name="configure-shared-storage-and-move-database-files"></a>Configurare l'archiviazione condivisa e spostare i file di database

Esistono numerose soluzioni per fornire spazio di archiviazione condiviso. Questa procedura dettagliata viene illustrata la configurazione di archiviazione condivisa con NFS. È consigliabile seguire le procedure consigliate e usare Kerberos per proteggere NFS: 

- [La condivisione di File System con NFS](https://www.suse.com/documentation/sles-12/singlehtml/book_sle_admin/book_sle_admin.html#cha.nfs)

Se non si segue questo materiale sussidiario, chiunque può accedere alla rete ed effettuare lo spoofing l'indirizzo IP di un nodo SQL sarà in grado di accedere ai file di dati. Come sempre, assicurarsi che il sistema una modellazione delle minacce è prima di utilizzarlo nell'ambiente di produzione. 

Un'altra opzione di archiviazione consiste nell'usare una condivisione file SMB:

- [Sezione Samba della documentazione di SUSE](https://www.suse.com/documentation/sles-12/singlehtml/book_sle_admin/book_sle_admin.html#cha.samba)

### <a name="configure-an-nfs-server"></a>Configurare un server NFS

Per configurare un server NFS, vedere i passaggi seguenti nella documentazione di SUSE: [Configurazione di Server NFS](https://www.suse.com/documentation/sles-12/singlehtml/book_sle_admin/book_sle_admin.html#sec.nfs.configuring-nfs-server).

### <a name="configure-all-cluster-nodes-to-connect-to-the-nfs-shared-storage"></a>Configurare tutti i nodi del cluster per la connessione alla risorsa di archiviazione condivise NFS

Prima di configurare il client NFS per montare il percorso di file di database di SQL Server in modo che punti al percorso di archiviazione condiviso, assicurarsi di che salvare i file di database in un percorso temporaneo per essere in grado di copiarli in un secondo momento la condivisione:

1. **Nel nodo primario solo**, salvare i file di database in un percorso temporaneo. Lo script seguente, crea una nuova directory temporanee, copia i file di database nella nuova directory e consente di rimuovere i vecchi file di database. Come SQL Server viene eseguito come utente locale mssql, è necessario assicurarsi che dopo il trasferimento dei dati per la condivisione montata, utente locale abbia accesso in lettura-scrittura alla condivisione. 

    ```bash
    su mssql
    mkdir /var/opt/mssql/tmp
    cp /var/opt/mssql/data/* /var/opt/mssql/tmp
    rm /var/opt/mssql/data/*
    exit
    ```

    Configurare il client NFS in tutti i nodi del cluster:

    - [Configurazione dei client](https://www.suse.com/documentation/sles-12/singlehtml/book_sle_admin/book_sle_admin.html#sec.nfs.configuring-nfs-clients)

    > [!NOTE]
    > È consigliabile seguire le procedure consigliate e indicazioni relative alle archivio altamente disponibile NFS di SUSE: [Archivio NFS a disponibilità elevata con DRBD e Pacemaker](https://www.suse.com/documentation/sle-ha-12/book_sleha_techguides/data/art_ha_quick_nfs.html).

2. Verificare che SQL Server viene avviato correttamente con il nuovo percorso del file. Eseguire questa operazione in ogni nodo. A questo punto un solo nodo deve eseguire SQL Server alla volta. Non possono entrambi eseguono contemporaneamente perché sono entrambi tenterà di accedere ai file di dati contemporaneamente (per evitare accidentalmente l'avvio di SQL Server su entrambi i nodi, usare una risorsa cluster di File System per assicurarsi che la condivisione non è montata due volte per i vari nodi). I seguenti comandi avviare SQL Server, controllare lo stato e quindi arrestare SQL Server.

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    sudo systemctl stop mssql-server
    ```

A questo punto, entrambe le istanze di SQL Server configurate per eseguire con i file di database nello spazio di archiviazione condiviso. Il passaggio successivo consiste nel configurare SQL Server per Pacemaker. 

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>Installare e configurare Pacemaker in ogni nodo del cluster

1. **In entrambi i nodi del cluster creare un file per archiviare nome utente e password di SQL Server per l'accesso a Pacemaker**. Il comando seguente crea e popola questo file:

    ```bash
    sudo touch /var/opt/mssql/secrets/passwd
    sudo echo '<loginName>' >> /var/opt/mssql/secrets/passwd
    sudo echo '<loginPassword>' >> /var/opt/mssql/secrets/passwd
    sudo chown root:root /var/opt/mssql/secrets/passwd 
    sudo chmod 600 /var/opt/mssql/secrets/passwd
    ```
2. **Tutti i nodi del cluster devono essere in grado di accedere uno all'altro tramite SSH**. Strumenti come hb_report o crm_report (per la risoluzione dei problemi) e History Explorer di Hawk richiedono l'accesso a SSH tra i nodi senza password, in caso contrario possono raccogliere dati solo dal nodo corrente. Nel caso in cui si usi una porta SSH non standard, usare l'opzione -X (vedere la pagina relativa a man). Se, ad esempio, la porta SSH è 3479, richiamare un oggetto hb_report con:

    ```bash
    crm_report -X "-p 3479" [...]
    ```

    Per altre informazioni, vedere i [requisiti di sistema e consigli nella documentazione di SUSE](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_requirements_other.html).

3. **Installare l'estensione per la disponibilità elevata**. Per installare l'estensione, seguire la procedura nell'argomento SUSE seguente:
    
    [Guida introduttiva all'installazione e alla configurazione](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html)

4. **Installare l'agente delle risorse FCI per SQL Server**. Eseguire i comandi seguenti in entrambi i nodi:

    ```bash
    sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo
    sudo zypper --gpg-auto-import-keys refresh
    sudo zypper install mssql-server-ha
    ```

5. **Configurare automaticamente il primo nodo**. Il passaggio successivo consiste nel configurare un cluster a un nodo in esecuzione configurando il primo nodo, SLES1. Seguire le istruzioni nell'argomento SUSE [Setting Up the First Node](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.setup.1st-node) (Configurazione del primo nodo).

    Al termine, verificare lo stato del cluster con `crm status`:
    ```bash
    crm status
    ```

    Dovrebbe indicare che il nodo, SLES1, è configurato.

6. **Aggiungere nodi a un cluster esistente**. Aggiungere quindi il nodo SLES2 al cluster. Seguire le istruzioni nell'argomento SUSE [Adding the Second Node](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.setup.2nd-node) (Aggiunta del secondo nodo).
    
    Al termine, verificare lo stato del cluster con **crm status**. Se il secondo nodo è stato aggiunto correttamente, l'output sarà simile al seguente:
        
    ```
    2 nodes configured
    1 resource configured
    Online: [ SLES1 SLES2 ]
    Full list of resources:
    admin_addr     (ocf::heartbeat:IPaddr2):       Started SLES1
    ```

    > [!NOTE]
    > **admin_addr** è la risorsa cluster IP virtuale configurata durante l'installazione iniziale del cluster a un nodo.

7.  **Procedure di rimozione**. Se si vuole rimuovere un nodo dal cluster, usare lo script di bootstrap **ha-cluster-remove**. Per altre informazioni, vedere [Overview of the Bootstrap Scripts](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.bootstrap) (Panoramica degli script di bootstrap).  

## <a name="configure-the-cluster-resources-for-sql-server"></a>Configurare le risorse del cluster per SQL Server

I passaggi seguenti illustrano come configurare la risorsa cluster per SQL Server. Esistono due impostazioni che è necessario personalizzare.

- **Nome risorsa SQL Server**: Un nome per la risorsa cluster di SQL Server. 
- **Valore di timeout**: Il valore di timeout è la quantità di tempo che il cluster rimane in attesa mentre una risorsa viene portata online. Per SQL Server, questo è l'ora in cui si prevede di SQL Server per portare il `master` online del database. 

Aggiornare i valori dallo script seguente per l'ambiente. Eseguire in un nodo per configurare e avviare il servizio cluster.

```bash
sudo crm configure
primitive <sqlServerResourceName> ocf:mssql:fci op start timeout=<timeout_in_seconds>
colocation <constraintName> inf: <virtualIPResourceName> <sqlServerResourceName>
show
commit
exit
```

Ad esempio, lo script seguente crea una risorsa cluster di SQL Server denominata mssqlha. 

```bash
sudo crm configure
primitive mssqlha ocf:mssql:fci op start timeout=60s
colocation admin_addr_mssqlha inf: admin_addr mssqlha
show
commit
exit
```

Dopo aver eseguito il commit, la configurazione di SQL Server viene avviato nello stesso nodo della risorsa IP virtuale. 

Per altre informazioni, vedere [Configuring and Managing Cluster Resources (riga di comando)](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.manual_config). 

### <a name="verify-that-sql-server-is-started"></a>Verificare che SQL Server è stato avviato. 

Per verificare che SQL Server è stato avviato, eseguire la **crm stato** comando:

```bash
crm status
```

Negli esempi seguenti vengono illustrati i risultati quando Pacemaker avviato correttamente come risorsa cluster. 
```
2 nodes configured
2 resources configured

Online: [ SLES1 SLES2 ]

Full list of resources:

 admin_addr     (ocf::heartbeat:IPaddr2):       Started SLES1
 mssqlha        (ocf::mssql:fci):       Started SLES1
```

## <a name="managing-cluster-resources"></a>La gestione delle risorse cluster

Per gestire le risorse del cluster, vedere l'argomento SUSE seguente: [La gestione delle risorse Cluster](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.config.crm )

### <a name="manual-failover"></a>Failover manuale

Anche se le risorse sono configurate per automaticamente il failover o eseguire la migrazione da altri nodi del cluster in caso di errore hardware o software, è possibile spostare una risorsa manualmente in un altro nodo del cluster usando l'interfaccia utente grafica di Pacemaker o la riga di comando . 

Usare il comando Migra per questa attività. Ad esempio, per eseguire la migrazione della risorsa SQL a un nome di nodo SLES2 cluster eseguire: 

```bash
crm resource
migrate mssqlha SLES2
```

## <a name="additional-resources"></a>Risorse aggiuntive

[Estensione per la disponibilità elevata SUSE Enterprise Linux: Guida all'amministrazione](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html) 
