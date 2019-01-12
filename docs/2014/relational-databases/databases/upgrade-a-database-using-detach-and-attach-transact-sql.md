---
title: Aggiornare un database usando le operazioni di scollegamento e collegamento (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- database attaching [SQL Server]
- upgrading databases
- database upgrades [SQL Server]
- database detaching [SQL Server]
- detaching databases [SQL Server]
- attaching databases [SQL Server]
ms.assetid: 99f66ed9-3a75-4e38-ad7d-6c27cc3529a9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 290454026cc87819bf9ffcf73329bb562e3dc5a4
ms.sourcegitcommit: 78e32562f9c1fbf2e50d3be645941d4aa457e31f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/08/2019
ms.locfileid: "54100876"
---
# <a name="upgrade-a-database-using-detach-and-attach-transact-sql"></a>Aggiornamento di un database utilizzando le operazioni di scollegamento e collegamento (Transact-SQL)
  In questo argomento si illustra come utilizzare le operazioni di collegamento e scollegamento per aggiornare un database di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Dopo essere stato collegato a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], il database è immediatamente disponibile e viene aggiornato automaticamente.  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Indicazioni](#Recommendations)  
  
-   **Per aggiornare un database di SQL Server:**  
  
     [Utilizzo delle operazioni di collegamento e scollegamento](#SSMSProcedure)  
  
-   **Completamento:**  [Dopo l'aggiornamento di un database SQL Server](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   I database di sistema non possono essere collegati.  
  
-   Collegare e scollegare la disabilitazione del concatenamento della proprietà tra database per il database impostando l'opzione **cross db ownership chaining** su 0. Per informazioni su come abilitare il concatenamento, vedere [Opzione di configurazione del server cross db ownership chaining](../../database-engine/configure-windows/cross-db-ownership-chaining-server-configuration-option.md).  
  
-   Quando si collega un database replicato che è stato copiato anziché scollegato:  
  
    -   Se si collega il database a una versione aggiornata della stessa istanza del server, è necessario eseguire **sp_vupgrade_replication** per aggiornare la replica al termine dell'operazione di collegamento. Per altre informazioni, vedere [sp_vupgrade_replication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-vupgrade-replication-transact-sql).  
  
    -   Se si collega il database a un'istanza del server diversa (indipendentemente dalla versione), è necessario eseguire **sp_removedbreplication** per rimuovere la replica al termine dell'operazione di collegamento. Per altre informazioni, vedere [sp_removedbreplication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql).  
  
###  <a name="Recommendations"></a> Indicazioni  
 È consigliabile evitare di collegare o ripristinare database provenienti da origini sconosciute o non attendibili. Tali database possono contenere codice dannoso che potrebbe eseguire codice [!INCLUDE[tsql](../../includes/tsql-md.md)] indesiderato o causare errori modificando lo schema o la struttura fisica di database. Prima di utilizzare un database da un'origine sconosciuta o non attendibile, eseguire [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) sul database in un server non di produzione ed esaminare il codice contenuto nel database, ad esempio le stored procedure o altro codice definito dall'utente.  
  
##  <a name="SSMSProcedure"></a> Per aggiornare un database utilizzando le operazioni di collegamento e scollegamento  
  
1.  Scollegare il database. Per altre informazioni, vedere [Scollegare un database](detach-a-database.md).  
  
2.  Spostare facoltativamente il file o i file del database scollegato e il file o i file di log.  
  
     È consigliabile spostare i file di log insieme ai file di dati anche se si prevede di creare nuovi file di log. In alcuni casi, per il ricollegamento di un database sono necessari i file di log esistenti. Mantenere pertanto sempre tutti i file di log scollegati fino a quando il database non è stato collegato senza di essi.  
  
    > [!NOTE]  
    >  Se si tenta di collegare il database senza specificare il file di log, verrà eseguita una ricerca di tale file nella relativa posizione originale. Se in questa posizione esiste ancora la copia originale del log, verrà collegata tale copia. Per evitare di utilizzare il file di log originale, specificare il percorso del nuovo file di log oppure rimuovere la copia originale del file di log dopo averlo copiato nella nuova posizione.  
  
3.  Collegare i file copiati all'istanza di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Per altre informazioni, vedere [Attach a Database](attach-a-database.md).  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente di aggiorna una copia di un database da una versione precedente di SQL Server. Le istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] vengono eseguite in una finestra dell'editor di query connessa all'istanza del server a cui è collegata.  
  
1.  Scollegare il database eseguendo le istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] riportate di seguito:  
  
    ```  
    USE master;  
    GO  
    EXEC sp_detach_db @dbname = N'MyDatabase';  
    GO  
    ```  
  
2.  Copiare i dati e i file di log nel nuovo percorso utilizzando il metodo scelto.  
  
    > [!IMPORTANT]  
    >  Nel caso di un database di produzione, posizionare su dischi separati il database e il log delle transazioni.  
  
     Per copiare i file in rete su un disco di un computer remoto, utilizzare il nome UNC (Universal Naming Convention) della posizione remota. Il formato di un nome UNC è **\\\\**_Servername_**\\**_Sharename_**\\**_Path_**\\**_Filename_. Come per la scrittura di file nel disco rigido locale, è necessario che l'account utente utilizzato dall'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]disponga delle autorizzazioni appropriate per la lettura o la scrittura di un file nel disco remoto.  
  
3.  Collegare il database spostato e, facoltativamente, il relativo log tramite l'esecuzione dell'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] seguente:  
  
    ```  
    USE master;  
    GO  
    CREATE DATABASE MyDatabase   
        ON (FILENAME = 'C:\MySQLServer\MyDatabase.mdf'),  
        (FILENAME = 'C:\MySQLServer\Database.ldf')  
        FOR ATTACH;  
    GO  
    ```  
  
     In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]un database appena collegato non è immediatamente visibile in Esplora oggetti. Per visualizzarlo, in Esplora oggetti scegliere **Aggiorna** dal menu **Visualizza**. Quando si espande il nodo **Database** in Esplora oggetti, il database appena collegato viene visualizzato nell'elenco dei database.  
  
##  <a name="FollowUp"></a> Completamento: Dopo l'aggiornamento di un database di SQL Server  
 Se il database include indici full-text, il processo di aggiornamento li importa, li reimposta o li ricompila, a seconda dell'impostazione della proprietà del server **upgrade_option** . Se l'opzione di aggiornamento è impostata per l'importazione (**upgrade_option** = 2) o la ricompilazione (**upgrade_option** = 0), gli indici full-text non saranno disponibili durante l'aggiornamento. A seconda della quantità di dati indicizzati, l'importazione può richiedere diverse ore, mentre la ricompilazione può risultare dieci volte più lunga. Si noti inoltre che quando l'opzione di aggiornamento è impostata sull'importazione, gli indici full-text associati vengono ricompilati se non è disponibile un catalogo full-text. Per modificare l'impostazione della proprietà del server **upgrade_option** , usare [sp_fulltext_service](/sql/relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql).  
  
### <a name="database-compatibility-level-after-upgrade"></a>Livello di compatibilità del database dopo l'aggiornamento  
 Se il livello di compatibilità di un database utente è 100 o superiore prima dell'aggiornamento, rimane invariato dopo l'aggiornamento. Se il livello di compatibilità è 90 prima dell'aggiornamento, nel database aggiornato questo valore viene impostato su 100, cioè sul livello di compatibilità inferiore supportato in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Per altre informazioni, vedere [Livello di compatibilità ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).  
  
### <a name="managing-metadata-on-the-upgraded-server-instance"></a>Gestione dei metadati nell'istanza del server aggiornata  
 Quando si collega un database a un'altra istanza del server, per garantire un sistema consistente a utenti e applicazioni, potrebbe essere necessario ricreare tutti i metadati del database o parte di essi, tra cui account di accesso, processi e autorizzazioni, nell'altra istanza del server. Per altre informazioni, vedere [Gestione dei metadati quando si rende disponibile un database in un'altra istanza del server &#40;SQL Server&#41;](manage-metadata-when-making-a-database-available-on-another-server.md).  
  
### <a name="service-master-key-and-database-master-key-encryption-changes-from-3des-to-aes"></a>Modifica della crittografia della chiave master di servizio e della chiave master di database da 3DES a AES  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e versioni successive usano l'algoritmo di crittografia AES per proteggere la chiave master del servizio (SMK) e la chiave master del database (DMK). AES è un algoritmo di crittografia più recente rispetto a 3DES utilizzato nelle versioni precedenti. Quando un database viene collegato per la prima volta a una nuova istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]o ripristinato, nel server non è ancora archiviata una copia della chiave master del database, crittografata dalla chiave master del servizio. È necessario usare l'istruzione `OPEN MASTER KEY` per decrittografare la chiave master del database (DMK). Dopo aver decrittografato la DMK, è possibile usare l'istruzione `ALTER MASTER KEY REGENERATE` per abilitare la decrittografia automatica per le operazioni successive, in modo da fornire al server una copia della DMK crittografata con la chiave master del servizio (SMK). Quando un database è stato aggiornato da una versione precedente, la DMK deve essere rigenerata per usare l'algoritmo AES più recente. Per altre informazioni sulla rigenerazione della DMK, vedere [ALTER MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-master-key-transact-sql). Il tempo richiesto per rigenerare la chiave DMK e aggiornarla ad AES dipende dal numero di oggetti protetti dalla DMK. È necessario rigenerare la chiave DMK per l'aggiornamento ad AES una sola volta e l'operazione non influenza le rigenerazioni future che fanno parte di una strategia di rotazione della chiave.  
  
  
