---
title: Configura archivio cluster di failover istanza SMB - SQL Server in Linux | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/28/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 7a8df4121fa71580af9596c855e0f0d6199fca46
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66712862"
---
# <a name="configure-failover-cluster-instance---smb---sql-server-on-linux"></a>Configurare cluster di failover - SMB - SQL Server in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questo articolo illustra come configurare l'archiviazione SMB per un'istanza cluster di failover (FCI) in Linux. 
 
Nel mondo non Windows, SMB è spesso definita per la condivisione come Common Internet File System (CIFS) e implementata tramite Samba. L'accesso a una condivisione SMB del mondo di Windows, viene eseguita in questo modo: \\SERVERNAME\SHARENAME. Per le installazioni di SQL Server basata su Linux, è necessario montare la condivisione SMB come cartella.

## <a name="important-source-and-server-information"></a>Importanti informazioni di origine e di server

Ecco alcuni suggerimenti e le note per correttamente usando SMB:
- La condivisione SMB può essere in Windows, Linux, o anche da un dispositivo come fino a quando Usa SMB 3.0 o versione successiva. Per altre informazioni su Samba e SMB 3.0, vedere [SMB 3.0](https://wiki.samba.org/index.php/Samba3/SMB2#SMB_3.0) per verificare se l'implementazione Samba è compatibile con SMB 3.0.
- La condivisione SMB deve essere a disponibilità elevata.
- Sicurezza deve essere impostata in modo corretto nella condivisione SMB. Di seguito è riportato un esempio da /etc/samba/smb.conf, dove SQLData1 è il nome della condivisione.

![05 smbsource][1]

## <a name="instructions"></a>Istruzioni

1. Scegliere uno dei server che verranno incluse nella configurazione di FCI. Non importa quale di essi.
   
1. Ottenere informazioni relative all'utente mssql.
   
   ```bash
    sudo id mssql
   ```
   
   Si noti l'uid, gid e gruppi. 
   
1. Eseguire `sudo smbclient -L //NameOrIP/ShareName -U User`.
   
   \<NameOrIP > è il nome DNS o indirizzo IP del server che ospita la condivisione SMB.
   
   \<ShareName > è il nome della condivisione SMB. 
   
1. Sistema database o tutti gli elementi archiviati nel percorso dati predefinito seguire questi passaggi. In caso contrario, andare al passaggio 5. 
   
   1. Verificare che SQL Server è arrestato nel server che si sta lavorando.
      ```bash
      sudo systemctl stop mssql-server
      sudo systemctl status mssql-server
      ```
      
   1. Opzione completamente da essere l'utente con privilegi avanzati. Non riceverà alcun acknowledgement se ha esito positivo.
      
      ```bash
      sudo -i
      ```
      
   1. Passa a corrispondere all'utente mssql. Non riceverà alcun acknowledgement se ha esito positivo.
      
      ```bash
      su mssql
      ```
      
   1. Creare una directory temporanea per archiviare i dati di SQL Server e i file di log. Non riceverà alcun acknowledgement se ha esito positivo.
      
      ```bash
      mkdir <TempDir>
      ```
      
      \<TempDir > è il nome della cartella. L'esempio seguente crea una cartella denominata /var/opt/mssql/tmp.
      
      ```bash
      mkdir /var/opt/mssql/tmp
      ```
      
   1. Copiare i file di dati e di log di SQL Server per la directory temporanea. Non riceverà alcun acknowledgement se ha esito positivo.
      
      ```bash
      cp /var/opt/mssql/data/* <TempDir>
      ```
      
      \<TempDir > è il nome della cartella nel passaggio precedente.
      
   1. Verificare che i file sono nella directory.
      
      ```bash
      ls <TempDir>
      ```
      
      \<TempDir > è il nome della cartella dal passaggio d.
      
   1. Eliminare i file dalla directory di dati di SQL Server esistente. Non riceverà alcun acknowledgement se ha esito positivo.
      
      ```bash
      rm - f /var/opt/mssql/data/*
      ```
      
   1. Verificare che i file siano stati eliminati. 
      
      ```bash
      ls /var/opt/mssql/data
      ```
      
   1. Tipo di uscita per tornare all'utente radice.
      
   1. Montare la condivisione SMB nella cartella dati SQL Server. Non riceverà alcun acknowledgement se ha esito positivo. In questo esempio viene illustrata la sintassi per la connessione a una condivisione SMB 3.0 basato su Windows Server.
      
      ```bash
      Mount -t cifs //<ServerName>/<ShareName> /var/opt/mssql/data -o vers=3.0,username=<UserName>,password=<Password>,domain=<domain>,uid=<mssqlUID>,gid=<mssqlGID>,file_mode=0777,dir_mode=0777
      ```
      
      \<ServerName > è il nome del server con la condivisione SMB
      
      \<ShareName > è il nome della condivisione
      
      \<Nome utente > è il nome dell'utente per accedere alla condivisione
      
      \<Password > è la password per l'utente
      
      \<dominio > è il nome di Active Directory
      
      \<mssqlUID > è l'UID dell'utente mssql 
      
      \<mssqlGID > è il GID dell'utente mssql
      
   1. Verificare che il montaggio ha esito negativo generando montaggio senza opzioni.
      
      ```bash
      mount
      ```
      
   1. Passare all'utente mssql. Non riceverà alcun acknowledgement se ha esito positivo.
      
      ```bash
      su mssql
      ```
      
   1. Copiare i file da /var/opt/mssql/data la directory temporanea. Non riceverà alcun acknowledgement se ha esito positivo.
      
      ```bash
      cp /var/opt/mssql/tmp/* /var/opt/mssql/data
      ```
      
   1. Verificare che i file siano presenti.
      
      ```bash
      ls /var/opt/mssql/data
      ```
      
   1. Immettere l'uscita per non essere mssql 
      
   1. Immettere l'uscita per non essere radice
   
   1. Avviare SQL Server. Se tutto ciò che è stato copiato correttamente e sicurezza applicata correttamente, SQL Server dovrebbe risultare avviato.
      
      ```bash
      sudo systemctl start mssql-server
      sudo systemctl status mssql-server
      ```
      
   1. Per testare ulteriormente, creare un database per garantire che le autorizzazioni sono corrette. L'esempio seguente Usa codice Transact-SQL è possibile usare SQL Server Management Studio.
      
      ![10_testcreatedb][2] 
      
   1. Arresto di SQL Server e verificare che sia arrestato. Se si intende aggiungere o test di altri dischi, non arrestare SQL Server fino a quando questi vengono aggiunti e testati.
      
      ```bash
      sudo systemctl stop mssql-server
      sudo systemctl status mssql-server
      ```
      
   1. Solo se è stato completato, smontare la condivisione. In caso contrario, smontare dopo il completamento della verifica/aggiunta di eventuali altri dischi.
      
      ```bash
      sudo umount //<IPAddressorServerName>/<ShareName /<FolderMountedIn>
      ```
      
      \<IPAddressOrServerName > è l'indirizzo IP o nome dell'host SMB
      
      \<ShareName > è il nome della condivisione
      
      \<FolderMountedIn > è il nome della cartella in cui è montato SMB
      
5. Per scopi diversi da database di sistema, ad esempio i database utente o i backup, seguire questa procedura. Se solo utilizzando il percorso predefinito, andare al passaggio 14.
   
   1. Commutatore sia l'utente con privilegi avanzati. Non riceverà alcun acknowledgement se ha esito positivo.
      
      ```bash
      sudo -i
      ```
      
   1. Creare una cartella che verrà usata da SQL Server. 
      
      ```bash
      mkdir <FolderName>
      ```
      
      \<Nomecartella > è il nome della cartella. Percorso completo della cartella deve essere specificata se non sono in posizione corretta. L'esempio seguente crea una cartella denominata /var/opt/mssql/userdata.
      
      ```bash
      mkdir /var/opt/mssql/userdata
      ```
      
   1. Montare la condivisione SMB nella cartella dati SQL Server. Non riceverà alcun acknowledgement se ha esito positivo. In questo esempio viene illustrata la sintassi per la connessione a una condivisione Samba basato su SMB 3.0.
      
      ```bash
      Mount -t cifs //<ServerName>/<ShareName> <FolderName> -o vers=3.0,username=<UserName>,password=<Password>,uid=<mssqlUID>,gid=<mssqlGID>,file_mode=0777,dir_mode=0777
      ```
      
      \<ServerName > è il nome del server con la condivisione SMB
      
      \<ShareName > è il nome della condivisione
      
      \<Nomecartella > è il nome della cartella creata nel passaggio precedente  
      
      \<Nome utente > è il nome dell'utente per accedere alla condivisione
      
      \<Password > è la password per l'utente
      
      \<mssqlUID > è l'UID dell'utente mssql
      
      \<mssqlGID > è il GID dell'utente mssql.
      
   1. Verificare che il montaggio ha esito negativo generando montaggio senza opzioni.
   
   1. Uscita di tipo che non rappresenta più l'utente con privilegi avanzati.
   
   1. Per eseguire il test, creare un database in tale cartella. L'esempio seguente usa sqlcmd per creare un database, passare a esso, verificare i file esistono a livello di sistema operativo e quindi Elimina il percorso temporaneo. È possibile usare SQL Server Management Studio.
   
   1. Smontare la condivisione 
      
      ```bash
      sudo umount //<IPAddressorServerName>/<ShareName> /<FolderMountedIn>
      ```
      
      \<IPAddressOrServerName > è l'indirizzo IP o nome dell'host SMB
      
      \<ShareName > è il nome della condivisione
      
      \<FolderMountedIn > è il nome della cartella in cui è montato SMB.
   
1. Ripetere i passaggi in altri nodi.

A questo punto si è pronti configurare l'infrastruttura di classificazione file.

## <a name="next-steps"></a>Passaggi successivi

[Configurare l'istanza del cluster di failover: SQL Server in Linux](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
[1]: ./media/sql-server-linux-shared-disk-cluster-configure-smb/05-smbsource.png 
[2]: ./media/sql-server-linux-shared-disk-cluster-configure-smb/10-testcreatedb.png 
