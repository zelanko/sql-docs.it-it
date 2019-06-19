---
title: Backup e ripristino - Parallel Data Warehouse | Microsoft Docs
description: Descrive come i dati di backup e ripristino funziona per Parallel Data Warehouse (PDW). Operazioni di backup e ripristino vengono usate per il ripristino di emergenza. Backup e ripristino è anche utilizzabile per copiare un database da un'appliance a un'altra appliance.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 01/19/2019
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 0b95d18eb38bbe0012235304747ca80b3dc19a79
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63200968"
---
# <a name="backup-and-restore"></a>Backup e ripristino

Descrive come i dati di backup e ripristino funziona per Parallel Data Warehouse (PDW). Operazioni di backup e ripristino vengono usate per il ripristino di emergenza. Backup e ripristino è anche utilizzabile per copiare un database da un'appliance a un'altra appliance.  
    
## <a name="BackupRestoreBasics"></a>Nozioni di base di backup e ripristino

Un PDW *backup di database* è una copia di un database dello strumento, archiviato in un formato in modo che può essere utilizzato per ripristinare il database originale in un'appliance.  
  
Viene creato un backup di database PDW con il [BACKUP DATABASE](../t-sql/statements/backup-database-parallel-data-warehouse.md) istruzione t-sql e formattati per l'uso con i [Ripristina DATABASE](../t-sql/statements/restore-database-parallel-data-warehouse.md) istruzione; è inutilizzabile per altri scopi. Il backup può essere ripristinato solo in un'appliance con lo stesso numero o un numero maggiore di nodi di calcolo.  
  
<!-- MISSING LINKS
The [master database](master-database.md) is a SMP SQL Server database. It is backed up with the BACKUP DATABASE statement. To restore master, use the [Restore the Master Database](configuration-manager-restore-master-database.md) page of the Configuration Manager tool.  
-->
  
Tecnologia di backup di SQL Server usano PDW per eseguire il backup e ripristino di database di appliance. Le opzioni di backup di SQL Server sono preconfigurate per utilizzare la compressione dei backup. Non è possibile impostare opzioni di backup come la compressione, il checksum, la dimensione blocco e il conteggio buffer.  
  
Backup di database vengono archiviati in uno o più server di backup, che esiste nella propria rete cliente.  PDW scrive i backup di database in parallelo direttamente dai nodi di calcolo in un server di backup e ripristinare un backup del database utente in parallelo direttamente dal server di backup per i nodi di calcolo.  
  
I backup vengono archiviati nel server di backup come un set di file nel file system Windows. Un backup del database PDW può essere ripristinato solo in PDW. Tuttavia, è possibile archiviare i backup di database dal server di backup in un'altra posizione usando standard processi di backup di file di Windows. Per altre informazioni sui server di backup, vedere [Acquire e configurare un server di backup](acquire-and-configure-backup-server.md).  
  
## <a name="BackupTypes"></a>Tipi di backup di database

Esistono due tipi di dati che richiedono un backup: database utente e i database di sistema (ad esempio, il database master). PDW non esegue il backup del log delle transazioni.  
  
Un backup completo del database è un backup di un intero database PDW. Questo è il tipo di backup predefinito. Un backup completo di un database utente include gli utenti del database e i ruoli del database. Un backup del database master include gli account di accesso.  
  
Un backup differenziale contiene tutte le modifiche dall'ultimo backup completo. Un backup differenziale richiede in genere meno tempo rispetto a un backup completo e può essere eseguito più di frequente. Quando più copie di backup differenziale si basano su stesso backup completo, ogni backup differenziale include tutte le modifiche nel backup differenziale precedente.  
  
Ad esempio, è possibile creare un backup completo ogni settimana e ogni giorno un backup differenziale. Per ripristinare il database utente, il backup completo e l'ultimo backup differenziale (se presente) deve essere ripristinato.  
  
Un backup differenziale è supportato solo per i database utente. Un backup del database master è sempre un backup completo.  
  
Per eseguire il backup dell'intera appliance, è necessario eseguire un backup di tutti i database utente e un backup del database master.  
  
## <a name="BackupProc"></a>Processo di backup del database

Il diagramma seguente mostra il flusso di dati durante un backup del database.  
  
![Processo di backup PDW](media/backup-process.png "processo di backup di PDW")  
  
Il processo di backup funziona nel modo seguente:  
  
1.  Utente invia un'istruzione tsql BACKUP DATABASE per il nodo di controllo.  
  
    -   Il backup è un backup completo o differenziale.  
  
2.  Per i database utente, il nodo di controllo (motore MPP) crea un piano di query distribuite per eseguire un backup del database parallelo.  
  
3.  Ogni nodo coinvolta in copie di backup il file di backup nel server di backup usando la funzionalità backup di SQL Server.  
  
    -   Ogni nodo coinvolta copia un file di backup nel server di backup.  
  
    -   Il backup del database utente (completo o differenziale) include un backup della parte del database archiviato in ogni nodo di calcolo e un backup degli utenti di database e dei ruoli predefiniti del database.  
  
4.  L'appliance esegue il backup in parallelo usando la rete InfiniBand.  
  
    -   PDW esegue ogni backup completi e differenziali in parallelo. Tuttavia, più backup del database non vengono eseguiti contemporaneamente. Ogni richiesta di backup deve attendere i backup inviati in precedenza terminare.  
  
    -   Un backup del database master esegue solo il backup dei dati dal nodo di controllo. Questo tipo di backup viene eseguito in modo seriale.  
  
5.  Un backup del database PDW è un gruppo di file archiviati in una directory che risiede fuori dal dispositivo. Il nome della directory è specificato come un nome di percorso e la directory di rete. La directory non può essere un percorso locale e non può essere nell'appliance.  
  
6.  Una volta completato il backup, è possibile utilizzare il file system di Windows per copiare la directory di backup in un altro percorso, se lo si desidera.  
  
    -   Un backup può essere ripristinato solo su un'appliance PDW con un numero uguale o maggiore di nodi di calcolo.  
  
    -   Prima di eseguire un ripristino, è possibile modificare il nome del backup. Il nome della directory di backup deve corrispondere al nome il nome originale del backup. Il nome originale del backup si trova nel file di backup. XML all'interno della directory di backup. Per ripristinare un database a un nome diverso, è possibile specificare il nuovo nome nel comando restore. Ad esempio: `RESTORE DATABASE MyDB1 FROM DISK = ꞌ\\10.192.10.10\backups\MyDB2ꞌ`.  
  
## <a name="RestoreModes"></a>Modalità di ripristino del database

Ripristino completo del database crea nuovamente il database PDW con i dati nel backup del database. Il ripristino di database viene eseguito prima di tutto ripristinare un backup completo e quindi, facoltativamente, il ripristino di un backup differenziale. Ripristino del database include gli utenti di database e i ruoli del database.  
  
Un ripristino solo di intestazione restituite le informazioni di intestazione per un database. Non verranno ripristinati i dati per l'appliance.  
  
Un ripristino appliance viene eseguito un ripristino dell'intera appliance. Ciò include il ripristino di tutti i database utente e il database master.  
  
## <a name="RestoreProc"></a>Processo di ripristino

Il diagramma seguente mostra il flusso di dati durante il ripristino del database.  
  
![Processo di ripristino](media/restore-process.png "processo di ripristino")  
  
## <a name="restoring-to-an-appliance-with-the-same-number-of-compute-nodes"></a>Il ripristino in un'Appliance con lo stesso numero di nodi di calcolo * *  
  
Quando si ripristinano i dati, l'appliance rileva il numero di nodi di calcolo dell'appliance di origine e l'appliance di destinazione. Se entrambi i dispositivi hanno un numero uguale di nodi di calcolo, il processo di ripristino funziona nel modo seguente:  
  
1.  Il backup del database da ripristinare è disponibile in una condivisione file di Windows in un server di backup di non appliance. Per prestazioni ottimali, questo server è connesso alla rete InfiniBand appliance.  
  
2.  Utente invia un' [RESTORE DATABASE](../t-sql/statements/restore-database-parallel-data-warehouse.md) istruzione tsql per il nodo di controllo.  
  
    -   Il ripristino non è un ripristino completo o un ripristino dell'intestazione. Il ripristino completo consente di ripristinare un backup completo e, facoltativamente, un backup differenziale.  
  
3.  Il nodo di controllo (motore MPP) crea un piano di query distribuite per eseguire un ripristino del database parallelo.  
  
    -   ServerPDW SQL esegue il ripristino di un database utente in parallelo. Tuttavia, più backup del database e i ripristini non vengono eseguiti contemporaneamente. Il motore MPP inserisce ogni istruzione restore in una coda. deve attendere per il backup inviato in precedenza e richieste al fine di ripristino.  
  
    -   Un ripristino del database master consente di ripristinare solo i dati sul nodo di controllo. il ripristino viene eseguito in modo seriale.  
  
    -   Un ripristino delle informazioni di intestazione è un'operazione rapida e non ripristina tutti i dati ai nodi di calcolo o un controllo. Al contrario, il nodo di controllo restituisce i risultati come output della query.  
  
4.  I file di backup copiati nei nodi di calcolo corretti in parallelo, in genere tramite la rete InfiniBand di appliance.  
  
5.  Ogni nodo di calcolo consente di ripristinare la parte del database utente. Se uno qualsiasi dei ripristini non completata correttamente, tutti i database rimossi e il ripristino non viene completato correttamente.  
  
## <a name="restoring-to-an-appliance-with-a-larger-number-of-compute-nodes"></a>Ripristino in un'appliance con un numero maggiore di nodi di calcolo  
  
Il ripristino di un backup in un'appliance con un numero maggiore di nodi di calcolo aumenta la dimensione allocata al database proporzionalmente al numero di nodi di calcolo.  
  
Ad esempio, quando si ripristina un database da 60 GB da un'appliance di 2 nodi (30 GB per nodo) in un'appliance di 6 nodi, SQL Server PDW crea un database di 180 GB (6 nodi con 30 GB per ogni nodo) nell'appliance di 6 nodi. SQL Server PDW inizialmente Ripristina il database in 2 nodi, in modo che corrisponda alla configurazione di origine e quindi ridistribuisce i dati in tutti i 6 nodi.  
  
Dopo la ridistribuzione, ogni nodo di calcolo contiene meno dati effettivi e più spazio libero rispetto a ogni nodo di calcolo nell'appliance di origine più piccoli. Usare lo spazio aggiuntivo per l'aggiunta di altri dati al database. Se le dimensioni del database ripristinato sono maggiori del necessario, è possibile usare [ALTER DATABASE](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw) per compattare le dimensioni dei file di database.  
  
## <a name="related-tasks"></a>Attività correlate  
  
|Backup e attività di ripristino|Descrizione|  
|---------------------------|---------------|  
|Preparare un server come server di backup.|[Acquisire e configurare un server di backup](acquire-and-configure-backup-server.md)|  
|Backup di un database.|[BACKUP DEL DATABASE](../t-sql/statements/backup-database-parallel-data-warehouse.md)|  
|Ripristinare un database.|[RESTORE DATABASE](../t-sql/statements/restore-database-parallel-data-warehouse.md)|    

<!-- MISSING LINKS

|Create a disaster recovery plan.|[Create a Disaster Recovery Plan](create-disaster-recovery-plan.md)|
|Restore the master database.|To restore the master database, use the [Restore the master database](configuration-manager-restore-master-database.md) page in the Configuration Manager tool.| 
|Copy a database from one appliance to another appliance.|[Copy a PDW database to another appliance](copy-pdw-database-to-another-appliance.md).|  
|Monitor backups and restores.|[Monitor backups and restores](monitor-backup-and-restore.md)|  

-->
