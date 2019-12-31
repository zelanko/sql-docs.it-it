---
title: Backup e ripristino
description: Viene descritto come funziona il backup e il ripristino dei dati per la data warehouse parallela (PDW). Le operazioni di backup e ripristino vengono usate per il ripristino di emergenza. È anche possibile usare backup e ripristino per copiare un database da un'appliance a un'altra appliance.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 01/19/2019
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 75399480879623a39da542c68f036389c645f6ab
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401354"
---
# <a name="backup-and-restore"></a>Backup e ripristino

Viene descritto come funziona il backup e il ripristino dei dati per la data warehouse parallela (PDW). Le operazioni di backup e ripristino vengono usate per il ripristino di emergenza. È anche possibile usare backup e ripristino per copiare un database da un'appliance a un'altra appliance.  
    
## <a name="BackupRestoreBasics"></a>Nozioni fondamentali su backup e ripristino

Un *backup del database* PDW è una copia di un database Appliance, archiviato in un formato in modo che possa essere usato per ripristinare il database originale in un'appliance.  
  
Un backup del database PDW viene creato con l'istruzione t-SQL [backup database](../t-sql/statements/backup-database-parallel-data-warehouse.md) e formattato per l'utilizzo con l'istruzione [Restore database](../t-sql/statements/restore-database-parallel-data-warehouse.md) . è inutilizzabile per altri scopi. Il backup può essere ripristinato solo in un appliance con lo stesso numero o un numero maggiore di nodi di calcolo.  
  
<!-- MISSING LINKS
The [master database](master-database.md) is a SMP SQL Server database. It is backed up with the BACKUP DATABASE statement. To restore master, use the [Restore the Master Database](configuration-manager-restore-master-database.md) page of the Configuration Manager tool.  
-->
  
PDW usa SQL Server tecnologia di backup per eseguire il backup e il ripristino dei database di appliance. SQL Server opzioni di backup sono preconfigurate per l'utilizzo della compressione dei backup. Non è possibile impostare opzioni di backup come la compressione, il checksum, la dimensione blocco e il conteggio buffer.  
  
I backup del database vengono archiviati in uno o più server di backup, che si trovano nella rete del cliente.  PDW scrive un backup di database utente in parallelo direttamente dai nodi di calcolo a un server di backup e ripristina un backup del database utente in parallelo direttamente dal server di backup ai nodi di calcolo.  
  
I backup vengono archiviati nel server di backup come un set di file nel file system di Windows. È possibile ripristinare un backup del database PDW solo in PDW. Tuttavia, è possibile archiviare i backup del database dal server di backup in un altro percorso usando i processi di backup dei file di Windows standard. Per ulteriori informazioni sui server di backup, vedere [acquisire e configurare un server di backup](acquire-and-configure-backup-server.md).  
  
## <a name="BackupTypes"></a>Tipi di backup di database

Sono disponibili due tipi di dati che richiedono un backup: database utente e database di sistema, ad esempio il database master. PDW non esegue il backup del log delle transazioni.  
  
Un backup completo del database è un backup di un intero database PDW. Questo è il tipo di backup predefinito. Un backup completo di un database utente include gli utenti del database e i ruoli del database. Un backup del database master include gli account di accesso.  
  
Un backup differenziale contiene tutte le modifiche apportate dopo l'ultimo backup completo. Un backup differenziale richiede in genere meno tempo rispetto a un backup completo e può essere eseguito più di frequente. Quando più backup differenziali si basano sullo stesso backup completo, ogni differenziale include tutte le modifiche apportate al backup differenziale precedente.  
  
Ad esempio, è possibile creare un backup completo ogni settimana e un backup differenziale ogni giorno. Per ripristinare il database utente, è necessario ripristinare il backup completo più l'ultimo differenziale (se esistente).  
  
Un backup differenziale è supportato solo per i database utente. Un backup del database master è sempre un backup completo.  
  
Per eseguire il backup dell'intera Appliance, è necessario eseguire un backup di tutti i database utente e di un backup del database master.  
  
## <a name="BackupProc"></a>Processo di backup del database

Il diagramma seguente illustra il flusso di dati durante un backup del database.  
  
![Processo di backup PDW](media/backup-process.png "Processo di backup PDW")  
  
Il processo di backup funziona nel modo seguente:  
  
1.  L'utente invia un'istruzione BACKUP DATABASE TSQL al nodo di controllo.  
  
    -   Il backup è un backup completo o differenziale.  
  
2.  Per i database utente, il nodo di controllo (motore MPP) crea un piano di query distribuite per eseguire un backup del database parallelo.  
  
3.  Ogni nodo che partecipa al backup copia il file di backup nel server di backup utilizzando SQL Server funzionalità di backup.  
  
    -   Ogni nodo che ha richiesto copia un file di backup nel server di backup.  
  
    -   Il backup del database utente (completo o differenziale) include un backup della parte del database archiviato in ogni nodo di calcolo e un backup degli utenti del database e dei ruoli del database.  
  
4.  Il dispositivo esegue il backup in parallelo usando la rete InfiniBand.  
  
    -   PDW esegue ogni backup completo e differenziale in parallelo. Tuttavia, non vengono eseguiti simultaneamente più backup di database. Ogni richiesta di backup deve attendere il completamento dei backup inviati in precedenza.  
  
    -   Un backup del database master esegue solo il backup dei dati dal nodo di controllo. Questo tipo di backup viene eseguito in modo seriale.  
  
5.  Un backup del database PDW è un gruppo di file archiviati in una directory che risiede fuori dal dispositivo. Il nome della directory viene specificato come un percorso di rete e un nome di directory. La directory non può essere un percorso locale e non può trovarsi nell'appliance.  
  
6.  Al termine del backup, è possibile usare il file system di Windows per copiare la directory di backup in un altro percorso, se necessario.  
  
    -   Un backup può essere ripristinato solo in un'appliance PDW con un numero uguale o maggiore di nodi di calcolo.  
  
    -   Non è possibile modificare il nome del backup prima di eseguire un ripristino. Il nome della directory di backup deve corrispondere al nome del nome originale del backup. Il nome originale del backup si trova nel file backup. XML all'interno della directory di backup. Per ripristinare un database con un nome diverso, è possibile specificare il nuovo nome nel comando Restore. Ad esempio: `RESTORE DATABASE MyDB1 FROM DISK = ꞌ\\10.192.10.10\backups\MyDB2ꞌ`.  
  
## <a name="RestoreModes"></a>Modalità di ripristino del database

Un ripristino completo del database ricrea il database PDW usando i dati nel backup del database. Il ripristino del database viene eseguito ripristinando prima un backup completo e quindi eventualmente ripristinando un backup differenziale. Il ripristino del database include gli utenti del database e i ruoli del database.  
  
Un'intestazione Restore Restore restituisce le informazioni di intestazione per un database. Non ripristina i dati nel dispositivo.  
  
Il ripristino di un dispositivo è un ripristino dell'intero dispositivo. Ciò include il ripristino di tutti i database utente e del database master.  
  
## <a name="RestoreProc"></a>Processo di ripristino

Il diagramma seguente illustra il flusso di dati durante il ripristino di un database.  
  
![Processo di ripristino](media/restore-process.png "Processo di ripristino")  
  
## <a name="restoring-to-an-appliance-with-the-same-number-of-compute-nodes"></a>Ripristino in un appliance con lo stesso numero di nodi di calcolo * *  
  
Quando si ripristinano i dati, l'appliance rileva il numero di nodi di calcolo nell'appliance di origine e nell'appliance di destinazione. Se entrambe le appliance hanno un numero uguale di nodi di calcolo, il processo di ripristino funziona nel modo seguente:  
  
1.  Il backup del database da ripristinare è disponibile in una condivisione file di Windows in un server di backup non Appliance. Per prestazioni ottimali, questo server è connesso alla rete InfiniBand dell'appliance.  
  
2.  L'utente invia un'istruzione [Restore database](../t-sql/statements/restore-database-parallel-data-warehouse.md) TSQL al nodo di controllo.  
  
    -   Il ripristino può essere un ripristino completo o un'intestazione. Il ripristino completo ripristina un backup completo e, facoltativamente, ripristina un backup differenziale.  
  
3.  Il nodo di controllo (motore MPP) crea un piano di query distribuite per eseguire un ripristino parallelo del database.  
  
    -   SQL ServerPDW esegue il ripristino di un database utente in parallelo. Tuttavia, i backup e i ripristini di più database non vengono eseguiti contemporaneamente. Il motore MPP inserisce ogni istruzione RESTORE in una coda. deve attendere il completamento delle richieste di backup e ripristino inviate in precedenza.  
  
    -   Il ripristino del database master ripristina solo i dati nel nodo di controllo; il ripristino viene eseguito in modo seriale.  
  
    -   Un ripristino delle informazioni di intestazione è un'operazione rapida e non consente di ripristinare i dati nei nodi di calcolo o di controllo. Al contrario, il nodo di controllo restituisce i risultati come output della query.  
  
4.  I file di backup vengono copiati nei nodi di calcolo corretti in parallelo, in genere sulla rete InfiniBand dell'appliance.  
  
5.  Ogni nodo di calcolo ripristina la parte del database utente. Se uno dei ripristini non viene completato correttamente, tutti i database vengono rimossi e il ripristino non viene completato correttamente.  
  
## <a name="restoring-to-an-appliance-with-a-larger-number-of-compute-nodes"></a>Ripristino in un'appliance con un numero maggiore di nodi di calcolo  
  
Il ripristino di un backup in un'appliance con un numero maggiore di nodi di calcolo aumenta la dimensione allocata al database proporzionalmente al numero di nodi di calcolo.  
  
Ad esempio, quando si ripristina un database di 60 GB da un'appliance a 2 nodi (30 GB per nodo) a un dispositivo a 6 nodi, SQL Server PDW crea un database da 180 GB (6 nodi con 30 GB per nodo) nell'appliance a 6 nodi. SQL Server PDW Ripristina inizialmente il database a 2 nodi in modo che corrispondano alla configurazione di origine, quindi ridistribuisce i dati in tutti i 6 nodi.  
  
Dopo la ridistribuzione, ogni nodo di calcolo conterrà dati meno effettivi e più spazio libero rispetto a ogni nodo di calcolo dell'appliance di origine più piccola. Usare lo spazio aggiuntivo per l'aggiunta di altri dati al database. Se le dimensioni del database ripristinato sono maggiori del necessario, è possibile utilizzare [ALTER database](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw) per compattare le dimensioni dei file di database.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Attività di backup e ripristino|Description|  
|---------------------------|---------------|  
|Preparare un server come server di backup.|[Acquisire e configurare un server di backup](acquire-and-configure-backup-server.md)|  
|Eseguire il backup di un database.|[BACKUP DATABASE](../t-sql/statements/backup-database-parallel-data-warehouse.md)|  
|Ripristinare un database.|[RESTORE DATABASE](../t-sql/statements/restore-database-parallel-data-warehouse.md)|    

<!-- MISSING LINKS

|Create a disaster recovery plan.|[Create a Disaster Recovery Plan](create-disaster-recovery-plan.md)|
|Restore the master database.|To restore the master database, use the [Restore the master database](configuration-manager-restore-master-database.md) page in the Configuration Manager tool.| 
|Copy a database from one appliance to another appliance.|[Copy a PDW database to another appliance](copy-pdw-database-to-another-appliance.md).|  
|Monitor backups and restores.|[Monitor backups and restores](monitor-backup-and-restore.md)|  

-->
