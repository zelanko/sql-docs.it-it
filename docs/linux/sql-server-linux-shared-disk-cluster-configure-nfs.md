---
title: Configurare l'archiviazione failover istanza del cluster NFS - SQL Server in Linux
description: ''
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 08/28/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 1088060b8f1af418f14210b7e09a6641fc3a62d8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68032361"
---
# <a name="configure-failover-cluster-instance---nfs---sql-server-on-linux"></a>Configurare cluster di failover - NFS - SQL Server in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questo articolo illustra come configurare l'archiviazione NFS per un'istanza cluster di failover (FCI) in Linux. 

NFS o network file system, è un metodo comune per la condivisione dei dischi nel mondo Linux ma non il Windows uno. Analogamente a iSCSI, NFS può essere configurato in un server o una sorta di appliance o unità di archiviazione, purché soddisfi i requisiti di archiviazione per SQL Server.

## <a name="important-nfs-server-information"></a>Importanti informazioni server NFS

L'origine hosting NFS (un server Linux o qualcos'altro) deve essere usando/conformi con la versione 4.2 o versione successiva. Le versioni precedenti non funzioneranno con SQL Server in Linux.

Quando si configurano le cartelle per essere condivise nel server di NFS, assicurarsi che seguono queste opzioni generali di linee guida:
- `rw` Per garantire che la cartella può essere letto da e scritti
- `sync` Per garantire operazioni di scrittura garantiti nella cartella
- Non usare `no_root_squash` come opzione; viene considerata un rischio per la sicurezza
- Assicurarsi che la cartella disponga di diritti completi (777) applicati

Assicurarsi che vengano applicati i propri standard di sicurezza per l'accesso. Quando si configura la cartella, assicurarsi che solo i server che fanno parte dell'istanza FCI verrà visualizzata la cartella NFS. Un esempio di un /etc/exports modificato in una soluzione basato su Linux con NFS è illustrato di seguito in cui la cartella è limitata a FCIN1 e FCIN2.

![05-nfsacl][1]

## <a name="instructions"></a>Istruzioni

1. Scegliere uno dei server che verranno incluse nella configurazione di FCI. Non importa quale di essi. 

2. Verificare che il server possa vedere il mount(s) sul server NFS.

    ```bash
    sudo showmount -e <IPAddressOfNFSServer>
    ```

    \<IPAddressOfNFSServer > è l'indirizzo IP del server NFS che si intende usare.

3. Per i database di sistema o tutti gli elementi archiviati nel percorso dati predefinito, seguire questa procedura. In caso contrario, andare al passaggio 4.
 
   * Verificare che SQL Server è arrestato nel server che si sta lavorando.

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```
   * Opzione completamente da essere l'utente con privilegi avanzati. Non riceverà alcun acknowledgement se ha esito positivo.

    ```bash
    sudo -i
    ```

   * Passa a corrispondere all'utente mssql. Non riceverà alcun acknowledgement se ha esito positivo.

    ```bash
    su mssql
    ```

   * Creare una directory temporanea per archiviare i dati di SQL Server e i file di log. Non riceverà alcun acknowledgement se ha esito positivo.

    ```bash
    mkdir <TempDir>
    ```

    \<TempDir > è il nome della cartella. L'esempio seguente crea una cartella denominata /var/opt/mssql/tmp.

    ```bash
    mkdir /var/opt/mssql/tmp
    ```

   * Copiare i file di dati e di log di SQL Server per la directory temporanea. Non riceverà alcun acknowledgement se ha esito positivo.
    
    ```bash
    cp /var/opt/mssql/data/* <TempDir>
    ```

    \<TempDir > è il nome della cartella nel passaggio precedente.

   * Verificare che i file sono nella directory.

    ```bash
    ls TempDir
    ```

    \<TempDir > è il nome della cartella dal passaggio d.

   * Eliminare i file dalla directory di dati di SQL Server esistente. Non riceverà alcun acknowledgement se ha esito positivo.

    ```bash
    rm - f /var/opt/mssql/data/*
    ```

   * Verificare che i file siano stati eliminati. 

    ```bash
    ls /var/opt/mssql/data
    ```
    
   * Tipo di uscita per tornare all'utente radice.

   * Montare la condivisione NFS nella cartella dati SQL Server. Non riceverà alcun acknowledgement se ha esito positivo.

    ```bash
    mount -t nfs4 <IPAddressOfNFSServer>:<FolderOnNFSServer> /var/opt/mssql/data -o nfsvers=4.2,timeo=14,intr
    ```

    \<IPAddressOfNFSServer > è l'indirizzo IP del server NFS che si intende usare 

    \<FolderOnNFSServer > è il nome della condivisione NFS. La sintassi di esempio seguente corrisponde alle informazioni di NFS dal passaggio 2.

    ```bash
    mount -t nfs4 200.201.202.63:/var/nfs/fci1 /var/opt/mssql/data -o nfsvers=4.2,timeo=14,intr
    ```

   * Verificare che il montaggio ha esito negativo generando montaggio senza opzioni.

    ```bash
    mount
    ```

    ![10-mountnoswitches][2]

   * Passare all'utente mssql. Non riceverà alcun acknowledgement se ha esito positivo.

    ```bash
    su mssql
    ```

   * Copiare i file da /var/opt/mssql/data la directory temporanea. Non riceverà alcun acknowledgement se ha esito positivo.

    ```bash
    cp /var/opt/mssql/tmp/* /var/opt/mssqldata
    ```

   * Verificare che i file siano presenti.

    ```bash
    ls /var/opt/mssql/data
    ```

   * Immettere l'uscita per non essere mssql 
    
   * Immettere l'uscita per non essere radice

   * Avviare SQL Server. Se tutto ciò che è stato copiato correttamente e sicurezza applicata correttamente, SQL Server dovrebbe risultare avviato.

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    ```
    
   * Creare un database per verificare che la protezione è impostata correttamente. L'esempio seguente mostra che viene eseguita tramite codice Transact-SQL è possibile tramite SSMS.
 
    ![CreateTestdatabase][3]

   * Arresto di SQL Server e verificare che sia arrestato.

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```

   * Se non si intende creare tutti gli altri punti di montaggio di NFS, smontare la condivisione. Se si è, non smontare.

    ```bash
    sudo umount <IPAddressOfNFSServer>:<FolderOnNFSServer> <FolderToMountIn>
    ```

    \<IPAddressOfNFSServer > è l'indirizzo IP del server NFS che si intende usare

    \<FolderOnNFSServer > è il nome della condivisione NFS

    \<FolderMountedIn > è la cartella creata nel passaggio precedente. 

4. Per scopi diversi da database di sistema, ad esempio i database utente o i backup, seguire questa procedura. Se solo utilizzando il percorso predefinito, andare al passaggio 5.

   * Commutatore sia l'utente con privilegi avanzati. Non riceverà alcun acknowledgement se ha esito positivo.

    ```bash
    sudo -i
    ```

   * Creare una cartella che verrà usata da SQL Server. 

    ```bash
    mkdir <FolderName>
    ```

    \<Nomecartella > è il nome della cartella. Percorso completo della cartella deve essere specificata se non sono in posizione corretta. L'esempio seguente crea una cartella denominata /var/opt/mssql/userdata.

    ```bash
    mkdir /var/opt/mssql/userdata
    ```

   * Montare la condivisione NFS nella cartella creata nel passaggio precedente. Non riceverà alcun acknowledgement se ha esito positivo.

    ```bash
    Mount -t nfs4 <IPAddressOfNFSServer>:<FolderOnNFSServer> <FolderToMountIn> -o nfsvers=4.2,timeo=14,intr
    ```

    \<IPAddressOfNFSServer > è l'indirizzo IP del server NFS che si intende usare

    \<FolderOnNFSServer > è il nome della condivisione NFS

    \<FolderToMountIn > è la cartella creata nel passaggio precedente. Di seguito è riportato un esempio. 

    ```bash
    mount -t nfs4 200.201.202.63:/var/nfs/fci2 /var/opt/mssql/userdata -o nfsvers=4.2,timeo=14,intr
    ```

   * Verificare che il montaggio ha esito negativo generando montaggio senza opzioni.
  
   * Uscita di tipo che non rappresenta più l'utente con privilegi avanzati.

   * Per eseguire il test, creare un database in tale cartella. L'esempio seguente usa sqlcmd per creare un database, passare a esso, verificare i file esistono a livello di sistema operativo e quindi Elimina il percorso temporaneo. È possibile usare SQL Server Management Studio.

    ![15-createtestdatabase][4]
 
   * Smontare la condivisione 

    ```bash
    sudo umount <IPAddressOfNFSServer>:<FolderOnNFSServer> <FolderToMountIn>
    ```

    \<IPAddressOfNFSServer > è l'indirizzo IP del server NFS che si intende usare
    
    \<FolderOnNFSServer > è il nome della condivisione NFS

    \<FolderMountedIn > è la cartella creata nel passaggio precedente. Di seguito è riportato un esempio. 
 
5. Ripetere i passaggi in altri nodi.


## <a name="next-steps"></a>Passaggi successivi

[Configurare l'istanza del cluster di failover: SQL Server in Linux](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
[1]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/05-nfsacl.png
[2]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/10-mountnoswitches.png
[3]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/20-createtestdatabase.png
[4]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/15-createtestdatabase.png
