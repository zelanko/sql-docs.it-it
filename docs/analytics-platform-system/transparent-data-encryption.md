---
title: Transparent Data Encryption
description: Transparent Data Encryption (Transparent Data Encryption) per la data warehouse parallela (PDW) esegue la crittografia e la decrittografia di i/O in tempo reale dei file di dati e di log delle transazioni e dei file di log PDW speciali ".
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: e75230ed175c6fbf1b0a2492265bbe12067060ca
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/22/2019
ms.locfileid: "74399928"
---
# <a name="transparent-data-encryption"></a>Transparent Data Encryption
È possibile adottare diverse precauzioni per proteggere il database, ad esempio la progettazione di un sistema sicuro, la crittografia di asset riservati e la creazione di un firewall che protegga i server di database. Tuttavia, per uno scenario in cui i supporti fisici (ad esempio unità o nastri di backup) vengono rubati, un malintenzionato può solo ripristinare o alleghire il database ed esplorare i dati. Una soluzione consiste nel crittografare i dati riservati nel database e proteggere con un certificato le chiavi utilizzate per crittografarli. In questo modo si impedisce a chi è sprovvisto delle chiavi di usare i dati; tuttavia, questo tipo di protezione deve essere pianificato in anticipo.  
  
*Transparent Data Encryption (Transparent Data Encryption* ) esegue la crittografia e la decrittografia di i/O in tempo reale dei file di dati e di log delle transazioni e dei file di log PDW speciali. La crittografia usa una chiave di crittografia del database (DEK) che viene archiviata nel record di avvio del database per la disponibilità durante il ripristino. La chiave di crittografia è una chiave simmetrica protetta tramite un certificato archiviato nel database master del SQL Server PDW. TDE protegge i dati inattivi, ovvero i file di dati e di log. Offre inoltre la possibilità di conformarsi a diverse leggi, normative e linee guida stabilite in vari settori. Questa funzionalità consente agli sviluppatori di software di crittografare i dati utilizzando algoritmi di crittografia AES e 3DES senza modificare le applicazioni esistenti.  
  
> [!IMPORTANT]  
> Transparent Data Encryption non fornisce la crittografia per i dati in viaggio tra il client e il PDW. Per ulteriori informazioni su come crittografare i dati tra il client e SQL Server PDW, vedere effettuare [il provisioning di un certificato](provision-certificate.md).  
>   
> Transparent Data Encryption non crittografa i dati mentre è in corso di trasferimento o in uso. Il traffico interno tra i componenti PDW all'interno del SQL Server PDW non è crittografato. I dati archiviati temporaneamente nei buffer di memoria non sono crittografati. Per attenuare questo rischio, controllare l'accesso fisico e le connessioni al SQL Server PDW.  
  
Una volta protetto, il database può essere ripristinato usando il certificato corretto.  
  
> [!NOTE]  
> Quando si crea un certificato per Transparent Data Encryption, è necessario eseguirne immediatamente il backup insieme alla chiave privata associata. Se il certificato non è più disponibile o se è necessario ripristinare o collegare il database a un altro server, è necessario disporre di copie di backup del certificato e della chiave privata, altrimenti non sarà possibile aprire il database. Il certificato di crittografia deve essere mantenuto anche se la funzionalità TDE non è più abilitata nel database. Anche se il database non è crittografato, è possibile che parti del log delle transazioni restino comunque protette e che il certificato sia necessario per alcune operazioni per l'esecuzione del backup completo del database. Un certificato che ha superato la data di scadenza può ancora essere usato per crittografare e decrittografare dati con TDE.  
  
La crittografia del file di database viene eseguita a livello di pagina. Le pagine di un database crittografato sono crittografate prima di essere scritte sul disco e decrittografate quando vengono lette in memoria. L'uso di TDE non comporta un aumento delle dimensioni del database crittografato.  
  
Nella figura seguente viene illustrata la gerarchia delle chiavi per la crittografia Transparent Data Encryption:  
  
![Visualizza la gerarchia](media/tde-architecture.png "TDE_Architecture")  
  
## <a name="using-tde"></a>Uso della crittografia trasparente dei dati  
Per usare TDE, eseguire le operazioni seguenti: I primi tre passaggi vengono eseguiti solo una volta, quando si prepara SQL Server PDW per il supporto di Transparent Data Encryption.  
  
1.  Creare una chiave master nel database master.  
  
2.  Usare **sp_pdw_database_encryption** per abilitare Transparent Data encryption nel SQL Server PDW. Questa operazione modifica i database temporanei per garantire la protezione dei dati temporanei futuri e avrà esito negativo se viene eseguito un tentativo quando sono presenti sessioni attive con tabelle temporanee. **sp_pdw_database_encryption** attiva la maschera dati utente nei log di sistema PDW. Per ulteriori informazioni sulla maschera dati utente nei log di sistema PDW, vedere [sp_pdw_log_user_data_masking](../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md).  
  
3.  Utilizzare [sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) per creare una credenziale in grado di autenticare e scrivere nella condivisione in cui verrà archiviato il backup del certificato. Se una credenziale esiste già per il server di archiviazione previsto, è possibile usare le credenziali esistenti.  
  
4.  Nel database master creare un certificato protetto dalla chiave master.  
  
5.  Eseguire il backup del certificato nella condivisione di archiviazione.  
  
6.  Nel database utente creare una chiave di crittografia del database e proteggerla dal certificato archiviato nel database master.  
  
7.  Utilizzare l' `ALTER DATABASE` istruzione per crittografare il database tramite Transparent Data Encryption.  
  
Nell'esempio seguente viene illustrata la crittografia `AdventureWorksPDW2012` del database utilizzando un certificato `MyServerCert`denominato, creato in SQL Server PDW.  
  
**Primo: abilitare Transparent Data Encryption sul SQL Server PDW.** Questa azione è necessaria solo una volta.  
  
```sql  
USE master;  
GO  
  
-- Create a database master key in the master database  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<UseStrongPasswordHere>';  
GO  
  
-- Enable encryption for PDW  
EXEC sp_pdw_database_encryption 1;  
GO  
  
-- Add a credential that can write to the share  
-- A credential created for a backup can be used if you wish  
EXEC sp_pdw_add_network_credentials 'SECURE_SERVER', '<domain>\<Windows_user>', '<password>';  
```  
  
**Secondo: creare ed eseguire il backup di un certificato nel database master.** Questa azione è necessaria solo una volta. È possibile disporre di un certificato separato per ogni database (scelta consigliata) oppure è possibile proteggere più database con un solo certificato.  
  
```sql  
-- Create certificate in master  
CREATE CERTIFICATE MyServerCert WITH SUBJECT = 'My DEK Certificate';  
GO  
  
-- Back up the certificate with private key  
BACKUP CERTIFICATE MyServerCert   
    TO FILE = '\\SECURE_SERVER\cert\MyServerCert.cer'  
    WITH PRIVATE KEY   
    (   
        FILE = '\\SECURE_SERVER\cert\MyServerCert.key',  
        ENCRYPTION BY PASSWORD = '<UseStrongPasswordHere>'   
    )   
GO  
```  
  
**Last: creare la chiave di crittografia e usare ALTER DATABASE per crittografare un database utente.** Questa azione viene ripetuta per ogni database protetto da Transparent Data Encryption.  
  
```sql  
USE AdventureWorksPDW2012;  
GO  
  
CREATE DATABASE ENCRYPTION KEY  
WITH ALGORITHM = AES_128  
ENCRYPTION BY SERVER CERTIFICATE MyServerCert;  
GO  
  
ALTER DATABASE AdventureWorksPDW2012 SET ENCRYPTION ON;  
GO  
```  
  
Le operazioni di crittografia e decrittografia sono pianificate sui thread in background per SQL Server. È possibile visualizzare lo stato di queste operazioni usando le viste del catalogo e le viste a gestione dinamica nell'elenco visualizzato più avanti in questo articolo.  
  
> [!CAUTION]  
> I file di backup dei database in cui è abilitata la funzionalità TDE vengono crittografati anche tramite la chiave di crittografia del database. Di conseguenza, quando questi backup vengono ripristinati, è necessario disporre del certificato che protegge la chiave di crittografia del database. Pertanto, oltre ad eseguire il backup del database, è necessario assicurarsi di conservare un backup dei certificati server per impedire la perdita di dati. Se il certificato non è più disponibile, si verificherà la perdita di dati.  
  
## <a name="commands-and-functions"></a>Comandi e funzioni  
Affinché vengano accettati dalle istruzioni indicate di seguito, è necessario che i certificati TDE siano crittografati mediante la chiave master del database.  
  
Nella tabella seguente sono inclusi collegamenti e spiegazioni delle funzioni e dei comandi correlati a TDE.  
  
|Comando o funzione|Scopo|  
|-----------------------|-----------|  
|[CREA CHIAVE DI CRITTOGRAFIA DEL DATABASE](../t-sql/statements/create-database-encryption-key-transact-sql.md)|Consente di creare una chiave usata per crittografare un database.|  
|[ALTER DATABASE ENCRYPTION KEY](../t-sql/statements/alter-database-encryption-key-transact-sql.md)|Consente di modificare la chiave usata per crittografare un database.|  
|[ELIMINA CHIAVE DI CRITTOGRAFIA DEL DATABASE](../t-sql/statements/drop-database-encryption-key-transact-sql.md)|Consente di rimuovere la chiave usata per crittografare un database.|  
|[ALTER DATABASE](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)|Descrive l'opzione **ALTER DATABASE** , usata per abilitare TDE.|  
  
## <a name="catalog-views-and-dynamic-management-views"></a>Viste del catalogo e viste a gestione dinamica  
Nella tabella seguente vengono illustrate le viste del catalogo e le viste a gestione dinamica di TDE.  
  
|Vista del catalogo e vista a gestione dinamica|Scopo|  
|-------------------------------------------|-----------|  
|[sys. databases](../relational-databases/system-catalog-views/sys-databases-transact-sql.md)|Vista del catalogo che consente di visualizzare le informazioni del database.|  
|[sys. Certificates](../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)|Vista del catalogo che consente di visualizzare i certificati di un database.|  
|[sys. dm_pdw_nodes_database_encryption_keys](../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-database-encryption-keys-transact-sql.md)|Vista a gestione dinamica che fornisce informazioni per ogni nodo, informazioni sulle chiavi di crittografia utilizzate in un database e lo stato della crittografia di un database.|  
  
## <a name="permissions"></a>Autorizzazioni  
Ogni funzionalità e comando di TDE ha requisiti specifici relativi alle autorizzazioni, descritti nelle tabelle precedenti.  
  
Per visualizzare i metadati implicati con Transparent Data Encryption è necessaria l' `CONTROL SERVER` autorizzazione.  
  
## <a name="considerations"></a>Considerazioni  
Durante un'analisi di una nuova crittografia di un database, le operazioni di manutenzione per il database sono disabilitate.  
  
È possibile trovare lo stato della crittografia del database utilizzando la vista a gestione dinamica **sys. dm_pdw_nodes_database_encryption_keys** . Per altre informazioni, vedere la sezione *viste del catalogo e viste a gestione dinamica* più indietro in questo articolo.  
  
### <a name="restrictions"></a>Restrizioni  
Le operazioni seguenti non sono consentite `CREATE DATABASE ENCRYPTION KEY`durante `ALTER DATABASE ENCRYPTION KEY`le `DROP DATABASE ENCRYPTION KEY`istruzioni, `ALTER DATABASE...SET ENCRYPTION` , o.  
  
-   Eliminazione del database.  
  
-   Utilizzando un `ALTER DATABASE` comando.  
  
-   Avvio di un backup del database.  
  
-   Avvio di un ripristino del database.  
  
Le operazioni o condizioni seguenti impediranno l' `CREATE DATABASE ENCRYPTION KEY`esecuzione `ALTER DATABASE ENCRYPTION KEY`delle `DROP DATABASE ENCRYPTION KEY`istruzioni, `ALTER DATABASE...SET ENCRYPTION` , o.  
  
-   È `ALTER DATABASE` in corso l'esecuzione di un comando.  
  
-   Un backup dei dati è in corso di esecuzione.  
  
Durante la creazione dei file di database, l'inizializzazione immediata dei file non è disponibile se è abilitata la crittografia TDE.  
  
### <a name="areas-not-protected-by-tde"></a>Aree non protette da Transparent Data Encryption  
Transparent Data Encryption non protegge le tabelle esterne.  
  
Transparent Data Encryption non protegge le sessioni di diagnostica. Gli utenti devono prestare attenzione a non eseguire query con parametri sensibili mentre sono in uso sessioni di diagnostica. Le sessioni di diagnostica che rivelano informazioni riservate devono essere eliminate non appena non sono più necessarie.  
  
I dati protetti da Transparent Data Encryption vengono decrittografati quando vengono inseriti nella memoria SQL Server PDW. I dump della memoria vengono creati quando si verificano determinati problemi nell'appliance. I file dump rappresentano il contenuto della memoria al momento dell'aspetto del problema e possono contenere dati sensibili in un formato non crittografato. Il contenuto dei dump della memoria deve essere esaminato prima di essere condiviso con altri.  
  
Il database master non è protetto da Transparent Data Encryption. Sebbene il database master non contenga dati utente, contiene informazioni quali i nomi di accesso.  
  
### <a name="transparent-data-encryption-and-transaction-logs"></a>Crittografia trasparente dei dati e log delle transazioni  
L'abilitazione di un database per l'utilizzo di Transparent Data Encryption comporta l'azzeramento della parte rimanente del log delle transazioni virtuale per forzare il log delle transazioni virtuale successivo. Ciò garantisce che non rimanga alcun testo non crittografato nei log delle transazioni dopo che il database viene impostato per la crittografia. È possibile trovare lo stato della crittografia del file di log in ogni nodo PDW visualizzando la `encryption_state` colonna nella `sys.dm_pdw_nodes_database_encryption_keys` vista, come nell'esempio seguente:  
  
```sql  
WITH dek_encryption_state AS   
(  
    SELECT ISNULL(db_map.database_id, dek.database_id) AS database_id, encryption_state  
    FROM sys.dm_pdw_nodes_database_encryption_keys AS dek  
        INNER JOIN sys.pdw_nodes_pdw_physical_databases AS node_db_map  
           ON dek.database_id = node_db_map.database_id AND dek.pdw_node_id = node_db_map.pdw_node_id  
        LEFT JOIN sys.pdw_database_mappings AS db_map  
            ON node_db_map .physical_name = db_map.physical_name  
        INNER JOIN sys.dm_pdw_nodes AS nodes  
            ON nodes.pdw_node_id = dek.pdw_node_id  
    WHERE dek.encryptor_thumbprint <> 0x  
)  
SELECT TOP 1 encryption_state  
       FROM dek_encryption_state  
       WHERE dek_encryption_state.database_id = DB_ID('AdventureWorksPDW2012 ')  
       ORDER BY (CASE encryption_state WHEN 3 THEN -1 ELSE encryption_state END) DESC;  
```  
  
Tutti i dati scritti nel log delle transazioni prima di una modifica della chiave di crittografia del database saranno crittografati usando la chiave di crittografia del database precedente.  
  
### <a name="pdw-activity-logs"></a>Log attività PDW  
SQL Server PDW gestisce un set di log destinati alla risoluzione dei problemi. Si noti che questo non è il log delle transazioni, il log degli errori di SQL Server o il registro eventi di Windows. Questi log attività PDW possono contenere istruzioni complete in testo non crittografato, alcune delle quali possono contenere dati utente. Esempi tipici sono le istruzioni **Insert** e **Update** . La maschera dei dati utente può essere attivata o disattivata in modo esplicito tramite **sp_pdw_log_user_data_masking**. L'abilitazione della crittografia su SQL Server PDW attiva automaticamente la maschera dei dati utente nei log attività PDW per poterli proteggere. **sp_pdw_log_user_data_masking** può essere utilizzato anche per mascherare le istruzioni quando non si utilizza Transparent Data Encryption, ma questa operazione non è consigliata perché riduce significativamente la capacità del Team di supporto tecnico Microsoft di analizzare i problemi.  
  
### <a name="transparent-data-encryption-and-the-tempdb-system-database"></a>Transparent Data Encryption e database di sistema tempdb  
Il database di sistema tempdb viene crittografato quando la crittografia viene abilitata utilizzando [sp_pdw_database_encryption](../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md). Questa operazione è necessaria prima che qualsiasi database possa utilizzare Transparent Data Encryption. Questo potrebbe avere un effetto sulle prestazioni per i database non crittografati nella stessa istanza di SQL Server PDW.  
  
## <a name="key-management"></a>Gestione della chiave  
La chiave di crittografia del database è protetta dai certificati archiviati nel database master. Questi certificati sono protetti dalla chiave master del database (DMK) del database master. Per poter essere usata per Transparent Data Encryption, è necessario che la DMK sia protetta dalla chiave master del servizio (SMK).  
  
Il sistema può accedere alle chiavi senza richiedere l'intervento dell'uomo (ad esempio, fornire una password). Se il certificato non è disponibile, il sistema restituirà un errore che indica che non è possibile decrittografare la chiave di crittografia finché non è disponibile il certificato appropriato.  
  
Quando si trasferisce un database da un appliance a un altro, il certificato utilizzato per proteggere la relativa chiave di crittografia deve essere ripristinato per primo nel server di destinazione. Il database può quindi essere ripristinato come di consueto. Per ulteriori informazioni, vedere la documentazione di SQL Server standard, in [spostare un database protetto con Transparent Data Encryption in un'altra SQL Server](https://technet.microsoft.com/library/ff773063.aspx).  
  
I certificati usati per crittografare chiavi DEK devono essere conservati finché sono presenti backup del database che li usano. I backup dei certificati devono includere la chiave privata del certificato, perché senza la chiave privata non è possibile usare un certificato per il ripristino del database. Tali backup della chiave privata del certificato vengono archiviati in un file separato, protetto da una password che è necessario fornire per il ripristino del certificato.  
  
## <a name="restoring-the-master-database"></a>Ripristino del database master  
Il database master può essere ripristinato usando **DWConfig**, come parte del ripristino di emergenza.  
  
-   Se il nodo di controllo non è stato modificato, ovvero se il database master viene ripristinato nello stesso dispositivo e non modificato da cui è stato effettuato il backup del database master, la DMK e tutti i certificati saranno leggibili senza ulteriori azioni.  
  
-   Se il database master viene ripristinato in un dispositivo diverso o se il nodo di controllo è stato modificato dopo il backup del database master, saranno necessari ulteriori passaggi per rigenerare la DMK.  
  
    1.  Aprire la DMK:  
  
        ```sql  
        OPEN MASTER KEY DECRYPTION BY PASSWORD = '<password>';  
        ```  
  
    2.  Aggiungere la crittografia per SMK:  
  
        ```sql  
        ALTER MASTER KEY   
            ADD ENCRYPTION BY SERVICE MASTER KEY;  
        ```  
  
    3.  Riavviare l'appliance.  
  
## <a name="upgrade-and-replacing-virtual-machines"></a>Aggiornare e sostituire macchine virtuali  
Se è presente una DMK nel dispositivo in cui è stato eseguito l'aggiornamento o la sostituzione della macchina virtuale, è necessario specificare la password DMK come parametro.  
  
Esempio di azione di aggiornamento. Sostituire `**********` con la password DMK.  
  
`setup.exe /Action=ProvisionUpgrade ... DMKPassword='**********'`  
  
Esempio di azione per sostituire una macchina virtuale.  
  
`setup.exe /Action=ReplaceVM ... DMKPassword='**********'`  
  
Durante l'aggiornamento, se un database utente è crittografato e la password DMK non viene specificata, l'operazione di aggiornamento avrà esito negativo. Durante la sostituzione, se non viene fornita la password corretta quando è presente una DMK, l'operazione ignorerà il passaggio di ripristino DMK. Tutti gli altri passaggi verranno completati alla fine dell'azione Sostituisci macchina virtuale. Tuttavia, l'azione segnalerà un errore alla fine per indicare che sono necessari ulteriori passaggi. Nei log del programma di installazione (che si trovano in **\ProgramData\Microsoft\Microsoft\\ SQL Server Parallel Data Warehouse\100\Logs\Setup<time-stamp> \Detail-Setup**), verrà visualizzato l'avviso seguente in prossimità della fine.  
  
`*** WARNING \*\*\* DMK is detected in master database, but could not be recovered automatically! The DMK password was either not provided or is incorrect!`
  
Eseguire manualmente queste istruzioni in PDW e riavviare Appliance per ripristinare la DMK:  
  
```sql
OPEN MASTER KEY DECRYPTION BY PASSWORD = '<DMK password>';  
ALTER MASTER KEY ADD ENCRYPTION BY SERVICE MASTER KEY;  
```
  
Usare i passaggi descritti nel paragrafo **ripristino del database master** per ripristinare il database e quindi riavviare l'appliance.  
  
Se la DMK esisteva prima, ma non è stata recuperata dopo l'azione, verrà generato il messaggio di errore seguente quando viene eseguita una query su un database.  
  
```sql
Msg 110806;  
A distributed query failed: Database '<db_name>' cannot be opened due to inaccessible files or insufficient memory or disk space. See the SQL Server errorlog for details.
```  
  
## <a name="performance-impact"></a>Impatto sulle prestazioni  
L'effetto sulle prestazioni di Transparent Data Encryption varia a seconda del tipo di dati, della modalità di archiviazione e del tipo di attività del carico di lavoro nel SQL Server PDW. Se protetto da Transparent Data Encryption, l'i/O di lettura e di decrittografia dei dati o la crittografia e la scrittura dei dati è un'attività con utilizzo intensivo della CPU e avrà un maggiore effetto quando si verificano contemporaneamente altre attività con utilizzo intensivo della CPU. Poiché crittografia Transparent Data Encryption `tempdb`, Transparent Data Encryption può influire sulle prestazioni dei database non crittografati. Per ottenere un'idea accurata delle prestazioni, è consigliabile testare l'intero sistema con i dati e l'attività di query.  
  
## <a name="related-content"></a>Contenuti correlati  
I collegamenti seguenti contengono informazioni generali sul modo in cui SQL Server gestisce la crittografia. Questi articoli consentono di comprendere SQL Server crittografia, ma questi articoli non contengono informazioni specifiche per SQL Server PDW e discutono delle funzionalità non presenti in SQL Server PDW.  
  
-   [Crittografia SQL Server](../relational-databases/security/encryption/sql-server-encryption.md)  
  
-   [Gerarchia di crittografia](../relational-databases/security/encryption/encryption-hierarchy.md)  
  
-   [Chiavi di crittografia del database e di SQL Server](../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)  

  
## <a name="see-also"></a>Vedere anche  
[ALTER DATABASE](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)  
[CREA CHIAVE MASTER](../t-sql/statements/create-master-key-transact-sql.md)  
[CREA CHIAVE DI CRITTOGRAFIA DEL DATABASE](../t-sql/statements/create-database-encryption-key-transact-sql.md)  
[CERTIFICATO DI BACKUP](../t-sql/statements/backup-certificate-transact-sql.md)  
[sp_pdw_database_encryption](../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)  
[sp_pdw_database_encryption_regenerate_system_keys](../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)  
[sp_pdw_log_user_data_masking](../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md)  
[sys. Certificates](../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)  
[sys. dm_pdw_nodes_database_encryption_keys](../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-database-encryption-keys-transact-sql.md)  
  
