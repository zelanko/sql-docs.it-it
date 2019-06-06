---
title: Configurare condivisioni cartella snapshot della replica di SQL Server in Linux | Microsoft Docs
description: Questo articolo descrive come configurare la replica di SQL Server condivisioni cartella snapshot in Linux.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 09/24/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 7569eaf92484038e998595405df42dd1f2d31b3d
ms.sourcegitcommit: fc341b2e08937fdd07ea5f4d74a90677fcdac354
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66718161"
---
# <a name="configure-replication-snapshot-folder-with-shares"></a>Configura la cartella snapshot della replica con le condivisioni

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

La cartella snapshot è una directory che è stata definita come una condivisione di; gli agenti di lettura e scrittura a questa cartella devono disporre delle autorizzazioni sufficienti per accedervi.

![diagramma di replica][1]

### <a name="replication-snapshot-folder-share-explained"></a>Condivisione cartella Snapshot della replica illustrata

Prima di esempi, di seguito viene illustrato come SQL Server Usa condivisioni samba nella replica. Di seguito è un esempio di base del funzionamento.

1. Condivisioni Samba configurate che i file scritti `/local/path1` della replica gli agenti nei server di pubblicazione possono essere osservati dal sottoscrittore
2. SQL Server è configurato per usare i percorsi di condivisione quando si configura il server di pubblicazione nel server di distribuzione in modo che tutte le istanze sarebbe simile al `//share/path`
3. SQL Server consente di trovare il percorso locale dal `//share/path` sapere dove cercare i file
4. SQL Server legge/scrive i percorsi locali supportati da una condivisione samba


## <a name="configure-a-samba-share-for-the-snapshot-folder"></a>Configurare una condivisione samba per la cartella snapshot 

Gli agenti di replica saranno necessaria una directory condivisa tra gli host di replica per accedere alle cartelle di snapshot in altri computer. Ad esempio, nella replica pull transazionali, l'agente di distribuzione si trova nel Sottoscrittore, che richiede l'accesso al server di distribuzione per ottenere gli articoli. In questa sezione verrà esaminato un esempio di come configurare una condivisione samba in due host di replica.


## <a name="steps"></a>Passaggi

Ad esempio, una cartella snapshot verrà configurato su Host 1 (il server di distribuzione) devono essere condivisi con Host 2 (sottoscrittore) usando Samba. 

### <a name="install-and-start-samba-on-both-machines"></a>Installare e avviare Samba in entrambi i computer 

In Ubuntu:

```bash
sudo apt-get -y install samba
sudo service smbd restart
```

In RHEL:

```bash
sudo yum install samba
sudo service smb start
sudo service smb status
```

### <a name="on-host-1-distributor-set-up-the-samba-share"></a>Operazioni di configurazione Host 1 (database di distribuzione) la condivisione Samba 

1. Errore di impostazione utente e password per samba:

  ```bash
  sudo smbpasswd -a mssql 
  ```

1. Modificare il `/etc/samba/smb.conf` per includere la voce seguente e inserire il *nome_condivisione* e *percorso* campi
 ```bash
  <[share_name]>
  path = </local/path/on/host/1>
  writable = yes
  create mask = 770
  directory mask 
  valid users = mssql 
  ```

  **Esempio**

  ```bash
  [mssql_data]    <- Name of the shared directory
  path = /var/opt/mssql/repldata <- location of directory we wish to share
  writable = yes  <- determines if the share is writable from other hosts
  create mask = 770  <- Linux permissions for files created 
  directory mask = 770 <- Linux permissions for directories created
  valid users = mssql   <- list of users who can login to this share
  ```

### <a name="on-host-2-subscriber--mount-the-samba-share"></a>Montare la condivisione Samba nell'Host 2 (sottoscrittore)

Modificare il comando con i percorsi corretti ed eseguire il comando seguente in machine2:

  ```bash
  sudo mount //<name_of_host_1>/<share_name> </local/path/on/host/2> -o user=mssql,uid=mssql,gid=mssql
  ```

  **Esempio**

  ```bash
  mount //host1/mssql_data /var/opt/mssql/repldata_shared -o user=mssql,uid=mssql,gid=mssql

  user=mssql <- sets the login name for samba
  uid=mssql   <- makes the mssql user as the owner of the mounted directory
  gid=mssql   <- sets the mssql group as the owner of the mounted directory
  ```

### <a name="on-both-hosts--configure-sql-server-on-linux-instances-to-use-snapshot-share"></a>In entrambi gli host configura SQL Server nelle istanze di Linux per usare Snapshot di condivisione

Aggiungere la seguente sezione a `mssql.conf` su entrambi i computer. Usare ovunque condivisione samba per il / / / percorso di condivisione. In questo esempio, sarebbe `//host1/mssql_data`

  ```bash
  [uncmapping]
  //share/path = /local/path/on/hosts/
  ```

  **Esempio**

  In host1:

  ```bash
  [uncmapping]
  //host1/mssql_data = /local/path/on/hosts/1
  ```

  In host2:
  
  ```bash
  [uncmapping]
  //host1/mssql_data = /local/path/on/hosts/2
  ```

### <a name="configuring-publisher-with-shared-paths"></a>Configura server di pubblicazione con i percorsi condivisi

* Quando si configura la replica, usare il percorso di condivisioni (ad esempio `//host1/mssql_data`
* Mappa `//host1/mssql_data` a una directory locale e sul mapping aggiunto a `mssql.conf`.

## <a name="next-steps"></a>Passaggi successivi

[Concetti: Replica di SQL Server in Linux](sql-server-linux-replication.md)

[Stored procedure di replica](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md).

[1]: ./media/sql-server-linux-replication-snapshot-shares/image1.png
