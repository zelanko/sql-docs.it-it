---
title: Configura failover cluster istanza archiviazione iSCSI - SQL Server in Linux
description: ''
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
manager: jroth
ms.date: 08/28/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 89a72a7390b3b782781c4849d69f81065544e991
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2019
ms.locfileid: "67833196"
---
# <a name="configure-failover-cluster-instance---iscsi---sql-server-on-linux"></a>Configurare l'istanza del cluster di failover SQL Server in Linux - iSCSI:

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questo articolo illustra come configurare l'archiviazione iSCSI per un'istanza cluster di failover (FCI) in Linux. 

## <a name="configure-iscsi"></a>Configurare iSCSI 
iSCSI utilizza funzionalità di rete per presentare i dischi da un server noto come una destinazione per i server. Il server ci si connette alla destinazione iSCSI richiedono che un iniziatore iSCSI sia configurato. I dischi nella destinazione vengono concesse autorizzazioni specifiche in modo che solo gli iniziatori che devono essere in grado di accedere a tali possono eseguire questa operazione. La destinazione stessa deve essere affidabile e a disponibilità elevata.

### <a name="important-iscsi-target-information"></a>Informazioni di destinazione iSCSI importanti
Sebbene questa sezione non illustra come configurare una destinazione iSCSI, poiché è specifico per il tipo di origine che verrà usato, assicurarsi che la sicurezza per i dischi che verranno usati dai nodi del cluster sia configurata.  

La destinazione non deve essere configurata in uno qualsiasi dei nodi di FCI mai se si usa una destinazione iSCSI basate su Linux. Per la disponibilità e prestazioni, iSCSI reti devono essere separate da quelle utilizzate da normale traffico di rete di origine sia i server client. Le reti usate per iSCSI devono essere veloci. Tenere presente che tale rete usano alcuni larghezza di banda del processore, pertanto, pianificare di conseguenza se si usa un normale server.
È la cosa più importante per garantire completata nella destinazione è che i dischi che vengono creati sono assegnati le autorizzazioni appropriate in modo che solo i server che fanno parte dell'istanza FCI possano accedervi. Seguito è riportato un esempio di destinazione iSCSI Microsoft in cui linuxnodes1 è il nome creato e in questo caso, gli indirizzi IP dei nodi vengono assegnati in modo che venga visualizzato NewFCIDisk1.vhdx ad essi.

![Initiator][1]

### <a name="instructions"></a>Istruzioni

Questa sezione illustra come configurare un iniziatore iSCSI nel server che fungono da nodi per l'istanza FCI. Le istruzioni funzionerà così com'è in Ubuntu e RHEL.

Per altre informazioni sull'iniziatore iSCSI per le distribuzioni supportate, consultare i collegamenti seguenti:
- [Red Hat](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Storage_Administration_Guide/iscsi-api.html)
- [SUSE](https://www.suse.com/documentation/sles11/stor_admin/data/sec_inst_system_iscsi_initiator.html) 
- [Ubuntu](https://help.ubuntu.com/lts/serverguide/iscsi-initiator.html)

1.  Scegliere uno dei server che verranno incluse nella configurazione di FCI. Non importa quale di essi. iSCSI deve trovarsi in una rete dedicata, quindi l'opzione configure iSCSI per riconoscere e usare tale rete. Eseguire `sudo iscsiadm -m iface -I <iSCSIIfaceName> -o new` in cui `<iSCSIIfaceName>` è il nome descrittivo o univoco per la rete. L'esempio seguente usa `iSCSINIC`:
   
    ```bash
    sudo iscsiadm -m iface -I iSCSINIC -o new
    ```
    ![7-setiscsinetwork][6]
 
2.  Modifica `/var/lib/iscsi/ifaces/iSCSIIfaceName`. Assicurarsi di avere a che disposizione i seguenti valori compilati completamente:

    - iface.net_ifacename è il nome della scheda di rete, come illustrato nel sistema operativo.
    - iface.hwaddress è l'indirizzo MAC del nome univoco che verrà creato per questa interfaccia riportato di seguito.
    - iface.ipaddress
    - iface.subnet_Mask 

    Vedere l'esempio seguente:

    ![iSCSITargetSettings][2]

3.  Trovare la destinazione iSCSI.

    ```bash
    sudo iscsiadm -m discovery -t sendtargets -I <iSCSINetName> -p <TargetIPAddress>:<TargetPort>
    ```

     \<iSCSINetName > è il nome univoco/adatto per la rete, \<TargetIPAddress > è l'indirizzo IP di destinazione iSCSI, e \<TargetPort > è la porta di destinazione iSCSI. 

    ![iSCSITargetResults][3]

 
4.  Accedere a destinazione

    ```bash
    sudo iscsiadm -m node -I <iSCSIIfaceName> -p TargetIPAddress -l
    ```

    \<iSCSIIfaceName > è il nome univoco/adatto per la rete e \<TargetIPAddress > è l'indirizzo IP di destinazione iSCSI.

    ![iSCSITargetLogin][4]

5.  Verificare che sia disponibile una connessione alla destinazione iSCSI.

    ```bash
    sudo iscsiadm -m session
    ```

    ![iSCSIVerify][5]

 
6.  Controllare i dischi collegati iSCSI

    ```bash
    sudo grep "Attached SCSI" /var/log/messages
    ```
    ![30-iSCSIattachedDisks][7]

7.  Creare un volume fisico sul disco iSCSI.

    ```bash
    sudo pvcreate /dev/<devicename>
    ```

    \<DeviceName > è il nome del dispositivo nel passaggio precedente. 

 
8.  Creare un gruppo di volumi nel disco iSCSI. I dischi assegnati a un singolo gruppo di volumi vengono interpretati come un pool o una raccolta. 

    ```bash
    sudo vgcreate <VolumeGroupName> /dev/devicename
    ```

    \<VolumeGroupName > è il nome del gruppo di volumi e \<devicename > è il nome del dispositivo dal passaggio 6. 
 
9.  Creare e verificare il volume logico per il disco.

    ```bash
    sudo lvcreate -Lsize -n <LogicalVolumeName> <VolumeGroupName>
    ```
    
    \<dimensioni > è la dimensione del volume per la creazione e possono essere specificati con G (GB), T (terabyte) e così via\<LogicalVolumeName > è il nome del volume logico, e \<VolumeGroupName > è il nome del gruppo di volumi dal passaggio precedente. 

    L'esempio seguente crea un volume di 25GB.
 
    ![Create25GBVol][10]

10. Eseguire `sudo lvs` per visualizzare la LVM che è stato creato.
 
11. Formattare il volume logico con un file System supportato. Per EXT4, usare l'esempio seguente:

    ```bash
    sudo mkfs.ext4 /dev/<VolumeGroupName>/<LogicalVolumeName>
    ```

    \<VolumeGroupName > è il nome del gruppo di volumi nel passaggio precedente. \<LogicalVolumeName > è il nome del volume logico nel passaggio precedente.  

12. Per i database di sistema o tutti gli elementi archiviati nel percorso dati predefinito, seguire questa procedura. In caso contrario, andare al passaggio 13.

   *    Verificare che SQL Server è arrestato nel server che si sta lavorando.

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```

   *    Opzione completamente da essere l'utente con privilegi avanzati. Non riceverà alcun acknowledgement se ha esito positivo.

    ```bash
    sudo -i
    ```

   *    Passa a corrispondere all'utente mssql. Non riceverà alcun acknowledgement se ha esito positivo.

    ```bash
    su mssql
    ```

   *    Creare una directory temporanea per archiviare i dati di SQL Server e i file di log. Non riceverà alcun acknowledgement se ha esito positivo.

    ```bash
    mkdir <TempDir>
    ```

    \<TempDir > è il nome della cartella. L'esempio seguente crea una cartella denominata /var/opt/mssql/TempDir.

    ```bash
    mkdir /var/opt/mssql/TempDir
    ```
    
   *    Copiare i file di dati e di log di SQL Server per la directory temporanea. Non riceverà alcun acknowledgement se ha esito positivo.

    ```bash
    cp /var/opt/mssql/data/* <TempDir>
    ```

    \<TempDir > è il nome della cartella nel passaggio precedente.
    
   *    Verificare che i file sono nella directory.

    ```bash
    ls \<TempDir>
    ```
    \<TempDir > è il nome della cartella dal passaggio d.

   *    Eliminare i file dalla directory di dati di SQL Server esistente. Non riceverà alcun acknowledgement se ha esito positivo.

    ```bash
    rm - f /var/opt/mssql/data/*
    ```

   *    Verificare che i file siano stati eliminati. L'immagine seguente mostra un esempio dell'intera sequenza da c a h.

    ```bash
    ls /var/opt/mssql/data
    ```

    ![45-CopyMove][8]
 
   *    Tipo `exit` per tornare all'utente radice.

   *    Montare il volume logico iSCSI nella cartella dati SQL Server. Non riceverà alcun acknowledgement se ha esito positivo.

    ```bash
    mount /dev/<VolumeGroupName>/<LogicalVolumeName> /var/opt/mssql/data
    ``` 

    \<VolumeGroupName > è il nome del gruppo di volumi e \<LogicalVolumeName > è il nome del volume logico che è stato creato. La sintassi di esempio seguente corrisponde al gruppo di volumi e volumi logici dal comando precedente.

    ```bash
    mount /dev/FCIDataVG1/FCIDataLV1 /var/opt/mssql/data
    ``` 

   *    Modificare il proprietario del montaggio a mssql. Non riceverà alcun acknowledgement se ha esito positivo.

    ```bash
    chown mssql /var/opt/mssql/data
    ```

   *    Modificare la proprietà del gruppo del montaggio in mssql. Non riceverà alcun acknowledgement se ha esito positivo.

    ```bash
    chgrp mssql /var/opt/mssql/data
    ``` 

   *    Passare all'utente mssql. Non riceverà alcun acknowledgement se ha esito positivo.

    ```bash
    su mssql
    ``` 

   *    Copiare i file da /var/opt/mssql/data la directory temporanea. Non riceverà alcun acknowledgement se ha esito positivo.

    ```bash
    cp /var/opt/mssql/TempDir/* /var/opt/mssql/data
    ``` 

   *    Verificare che i file siano presenti.

    ```bash
    ls /var/opt/mssql/data
    ``` 
 
   *    Immettere `exit` a non essere mssql.
    
   *    Immettere `exit` a non essere radice.

   *    Avviare SQL Server. Se tutto ciò che è stato copiato correttamente e sicurezza applicata correttamente, SQL Server dovrebbe risultare avviato.

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    ``` 
 
   *    Arresto di SQL Server e verificare che sia arrestato.

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ``` 

13. Per scopi diversi da database di sistema, ad esempio i database utente o i backup, seguire questa procedura. Se solo utilizzando il percorso predefinito, andare al passaggio 14.

   *    Commutatore sia l'utente con privilegi avanzati. Non riceverà alcun acknowledgement se ha esito positivo.

    ```bash
    sudo -i
    ```

   *    Creare una cartella che verrà usata da SQL Server. 

    ```bash
    mkdir <FolderName>
    ```

    \<Nomecartella > è il nome della cartella. Percorso completo della cartella deve essere specificata se non sono in posizione corretta. L'esempio seguente crea una cartella denominata /var/opt/mssql/userdata.

    ```bash
    mkdir /var/opt/mssql/userdata
    ```

   *    Montare il volume logico iSCSI nella cartella creata nel passaggio precedente. Non riceverà alcun acknowledgement se ha esito positivo.
    
    ```bash
    mount /dev/<VolumeGroupName>/<LogicalVolumeName> <FolderName>
    ```

    \<VolumeGroupName > è il nome del gruppo di volumi, \<LogicalVolumeName > è il nome del volume logico che è stato creato, e \<nomecartella > è il nome della cartella. Sintassi di esempio è illustrata di seguito.

    ```bash
    mount /dev/FCIDataVG2/FCIDataLV2 /var/opt/mssql/userdata 
    ```

   *    Modificare la proprietà della cartella creata per mssql. Non riceverà alcun acknowledgement se ha esito positivo.

    ```bash
    chown mssql <FolderName>
    ```

    \<Nomecartella > è il nome della cartella in cui è stato creato. Di seguito è riportato un esempio.

    ```bash
    chown mssql /var/opt/mssql/userdata
    ```
  
   *    Modificare il gruppo della cartella creata per mssql. Non riceverà alcun acknowledgement se ha esito positivo.

    ```bash
    chown mssql <FolderName>
    ```

    \<Nomecartella > è il nome della cartella in cui è stato creato. Di seguito è riportato un esempio.

    ```bash
    chown mssql /var/opt/mssql/userdata
    ```

   *    Tipo `exit` a non essere più l'utente con privilegi avanzati.

   *    Per eseguire il test, creare un database in tale cartella. L'esempio illustrato di seguito Usa sqlcmd per creare un database, passare a esso, verificare i file esistono a livello di sistema operativo e quindi Elimina il percorso temporaneo. È possibile usare SQL Server Management Studio.
  
    ![50-ExampleCreateSSMS][9]

   *    Smontare la condivisione 

    ```bash
    sudo umount /dev/<VolumeGroupName>/<LogicalVolumeName> <FolderName>
    ```

    \<VolumeGroupName > è il nome del gruppo di volumi, \<LogicalVolumeName > è il nome del volume logico che è stato creato, e \<nomecartella > è il nome della cartella. Sintassi di esempio è illustrata di seguito.

    ```bash
    sudo umount /dev/FCIDataVG2/FCIDataLV2 /var/opt/mssql/userdata 
    ```

14. Configurare il server in modo che solo Pacemaker può attivare il gruppo di volumi.

    ```bash
    sudo lvmconf --enable-halvm --services -startstopservices
    ```
 
15. Generare un elenco dei gruppi di volumi nel server. Tutti gli elementi elencati non il disco iSCSI viene utilizzato dal sistema, ad esempio per il disco del sistema operativo.

    ```bash
    sudo vgs
    ```

16. Modificare la sezione di configurazione di attivazione di /etc/lvm/lvm.conf il file. Configurare la riga seguente:

    ```bash
    volume_list = [ <ListOfVGsNotUsedByPacemaker> ]
    ```

    \<ListOfVGsNotUsedByPacemaker > è l'elenco dei gruppi di volumi dall'output del passaggio 20 che non verrà utilizzato dall'istanza FCI. Inserire ognuno racchiuso tra virgolette e separati da una virgola. Di seguito è riportato un esempio.

    ![55-ListOfVGs][11]
 
 
17. Quando viene avviato Linux, esegue il montaggio di file system. Per garantire che solo Pacemaker poter montare il disco iSCSI, ricompilare l'immagine del file System radice. 

    Eseguire il comando seguente dell'operazione potrebbe richiedere qualche istante per completare. Non si riceverà alcun messaggio nuovamente se ha esito positivo.

    ```bash
    sudo dracut -H -f /boot/initramfs-$(uname -r).img $(uname -r)
    ```

18. Riavviare il server.

19. In un altro server che farà parte dell'istanza FCI, eseguire i passaggi da 1 - 6. Verrà visualizzata la destinazione iSCSI a SQL Server. 
 
20. Generare un elenco dei gruppi di volumi nel server. Dovrebbe visualizzare il gruppo di volumi creato in precedenza. 

    ```bash
    sudo vgs
    ``` 
23. Avviare SQL Server e verificare di che poter essere avviato su questo server.

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    ```

24. Arrestare SQL Server e verificare che sia arrestata.

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```
25. Ripetere i passaggi da 1 a 6 su altri server che farà parte dell'istanza FCI.

A questo punto si è pronti configurare l'infrastruttura di classificazione file.

|Distribuzione |Argomento 
|----- |-----
|**Red Hat Enterprise Linux con il componente aggiuntivo a disponibilità elevata** |[Configurare](sql-server-linux-shared-disk-cluster-configure.md)<br/>[Gestire](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
|**SUSE Linux Enterprise Server con il componente aggiuntivo a disponibilità elevata** |[Configurare](sql-server-linux-shared-disk-cluster-sles-configure.md)

## <a name="next-steps"></a>Passaggi successivi

[Configurare l'istanza del cluster di failover: SQL Server in Linux](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
[1]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/05-initiator.png
[2]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/10-iscsiTargetSettings.png
[3]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/15-iSCSITargetResults.png
[4]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/20-iSCSITargetLogin.png
[5]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/25-iSCSIVerify.png
[6]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/7-setiscsinetwork.png
[7]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/30-iSCSIattachedDisks.png
[8]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/45-CopyMove.png
[9]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/50-ExampleCreateSSMS.png
[10]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/40-Create25GBVol.png
[11]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/55-ListOfVGs.png
