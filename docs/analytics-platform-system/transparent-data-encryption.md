---
title: Transparent data encryption, Parallel Data Warehouse | Microsoft Docs
description: Transparent data encryption (TDE) per Parallel Data Warehouse (PDW) esegue la crittografia dei / o in tempo reale e la decrittografia dei dati e i file di log delle transazioni e i file di log speciali di PDW."
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: e9067416365e56dccf9c09f2e826c01fb3ecfa3c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63156958"
---
# <a name="transparent-data-encryption"></a>Transparent Data Encryption
Per proteggere il database è possibile adottare alcune accortezze, tra cui la progettazione di un sistema sicuro, la crittografia dei dati riservati e la compilazione di un firewall attorno ai server di database. Tuttavia, per uno scenario in cui si appropria i supporti fisici (ad esempio le unità o nastri di backup), un utente malintenzionato può semplicemente ripristinare o collegare il database ed esplorare i dati. Una soluzione per ovviare al problema consiste nel crittografare i dati sensibili nel database e proteggere con un certificato le chiavi usate per la crittografia. In questo modo si impedisce a chi è sprovvisto delle chiavi di usare i dati; tuttavia, questo tipo di protezione deve essere pianificato in anticipo.  
  
*Crittografia dati trasparente* (TDE) esegue la crittografia dei / o in tempo reale e la decrittografia dei dati e file di log file di log delle transazioni e le speciali PDW. Per la crittografia viene usata una chiave di crittografia del database (DEK), archiviata nel record di avvio del database affinché sia disponibile durante le operazioni di recupero. La chiave DEK è una chiave simmetrica protetta tramite un certificato archiviato nel database master di SQL Server PDW. TDE consente di proteggere i dati "non operativi", ovvero i file di dati e di log, e assicura la conformità a numerose leggi, normative e linee guida stabilite in vari settori. Questa funzionalità consente agli sviluppatori software di crittografare i dati usando algoritmi di crittografia AES e 3DES senza modificare le applicazioni esistenti.  
  
> [!IMPORTANT]  
> TDE non fornisce la crittografia per dati scambiati fra il client e di PDW. Per altre informazioni su come crittografare i dati tra il client e SQL Server PDW, vedere [effettuare il provisioning di un certificato](provision-certificate.md).  
>   
> TDE non crittografa i dati mentre è in movimento o in uso. Il traffico interno tra componenti PDW all'interno di SQL Server PDW non verrà crittografato. I dati temporaneamente archiviati nel buffer di memoria non vengono crittografati. Per ridurre questo rischio, controllare l'accesso fisico e le connessioni a SQL Server PDW.  
  
Una volta protetto, il database può essere ripristinato usando il certificato corretto.  
  
> [!NOTE]  
> Quando si crea un certificato per TDE, è consigliabile immediatamente eseguirne il backup, insieme alla chiave privata associata. Se il certificato non è più disponibile o se è necessario ripristinare o collegare il database a un altro server, è necessario disporre di copie di backup del certificato e della chiave privata, altrimenti non sarà possibile aprire il database. Il certificato di crittografia deve essere mantenuto anche se la funzionalità TDE non è più abilitata nel database. Anche se il database non è crittografato, è possibile che parti del log delle transazioni restino comunque protette e che il certificato sia necessario per alcune operazioni per l'esecuzione del backup completo del database. Un certificato che ha superato la data di scadenza può ancora essere usato per crittografare e decrittografare dati con TDE.  
  
La crittografia del file di database viene eseguita a livello di pagina. Le pagine di un database crittografato sono crittografate prima di essere scritte sul disco e decrittografate quando vengono lette in memoria. L'uso di TDE non comporta un aumento delle dimensioni del database crittografato.  
  
La figura seguente mostra la gerarchia delle chiavi per la crittografia TDE:  
  
![Visualizza la gerarchia](media/tde-architecture.png "TDE_Architecture")  
  
## <a name="using-tde"></a>Tramite Transparent Data Encryption  
Per usare TDE, eseguire le operazioni seguenti: I primi tre passaggi vengono eseguiti solo una volta, quando la preparazione di SQL Server PDW per il supporto di Transparent Data Encryption.  
  
1.  Creare una chiave master nel database master.  
  
2.  Uso **sp_pdw_database_encryption** per abilitare TDE in SQL Server PDW. Questa operazione modifica i database temporanei per garantire la protezione dei dati temporanei future e avrà esito negativo se si tenta la presenza di eventuali sessioni attive che hanno tabelle temporanee. **sp_pdw_database_encryption** accende il mascheramento dei dati utente nei registri di sistema PDW. (Per ulteriori informazioni sulla maschera di dati utente nei registri di sistema PDW, vedere [sp_pdw_log_user_data_masking](../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md).)  
  
3.  Uso [sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) per creare una credenziale che può eseguire l'autenticazione e scrittura per la condivisione in cui verrà archiviato il backup del certificato. Se esiste già una credenziale per il server di archiviazione è prevista, è possibile usare le credenziali esistenti.  
  
4.  Nel database master, creare un certificato protetto dalla chiave master.  
  
5.  Eseguire il backup del certificato per la condivisione di archiviazione.  
  
6.  Nel database utente, creare una chiave di crittografia del database e proteggerla mediante il certificato viene archiviato nel database master.  
  
7.  Usare il `ALTER DATABASE` istruzione per crittografare il database tramite TDE.  
  
L'esempio seguente illustra la crittografia di `AdventureWorksPDW2012` il database con un certificato denominato `MyServerCert`, creato in SQL Server PDW.  
  
**Prima: Abilitare Transparent Data Encryption in SQL Server PDW.** Questa azione è necessaria solo una volta.  
  
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
  
**Secondo: Creare ed eseguire il backup di un certificato nel database master.** Questa azione è solo obbligatorio una sola volta. È possibile avere un certificato separato per ogni database (scelta consigliata) oppure è possibile proteggere più database con un certificato.  
  
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
  
**Ultimo: Creare la chiave DEK e usare ALTER DATABASE per crittografare un database utente.** Questa azione viene ripetuta per ogni database protetto con TDE.  
  
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
  
Le operazioni di crittografia e decrittografia sono pianificate sui thread in background da SQL Server. È possibile visualizzare lo stato di queste operazioni tramite le viste del catalogo e viste a gestione dinamica nell'elenco riportato più avanti in questo articolo.  
  
> [!CAUTION]  
> I file di backup dei database in cui è abilitata la funzionalità TDE vengono crittografati anche tramite la chiave di crittografia del database. Di conseguenza, quando questi backup vengono ripristinati, è necessario disporre del certificato che protegge la chiave di crittografia del database. Pertanto, oltre ad eseguire il backup del database, è necessario assicurarsi di conservare un backup dei certificati server per impedire la perdita di dati. Se il certificato non è più disponibile, si verificherà la perdita di dati.  
  
## <a name="commands-and-functions"></a>Comandi e funzioni  
Affinché vengano accettati dalle istruzioni indicate di seguito, è necessario che i certificati TDE siano crittografati mediante la chiave master del database.  
  
Nella tabella seguente sono inclusi collegamenti e spiegazioni delle funzioni e dei comandi correlati a TDE.  
  
|Comando o funzione|Scopo|  
|-----------------------|-----------|  
|[CREARE UNA CHIAVE DI CRITTOGRAFIA DEL DATABASE](../t-sql/statements/create-database-encryption-key-transact-sql.md)|Consente di creare una chiave usata per crittografare un database.|  
|[ALTER DATABASE ENCRYPTION KEY](../t-sql/statements/alter-database-encryption-key-transact-sql.md)|Consente di modificare la chiave usata per crittografare un database.|  
|[DROP DATABASE ENCRYPTION KEY](../t-sql/statements/drop-database-encryption-key-transact-sql.md)|Consente di rimuovere la chiave usata per crittografare un database.|  
|[ALTER DATABASE](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)|Descrive l'opzione **ALTER DATABASE** , usata per abilitare TDE.|  
  
## <a name="catalog-views-and-dynamic-management-views"></a>Viste del catalogo e viste a gestione dinamica  
Nella tabella seguente vengono illustrate le viste del catalogo e le viste a gestione dinamica di TDE.  
  
|Vista del catalogo e vista a gestione dinamica|Scopo|  
|-------------------------------------------|-----------|  
|[sys.databases](../relational-databases/system-catalog-views/sys-databases-transact-sql.md)|Vista del catalogo che consente di visualizzare le informazioni del database.|  
|[sys.certificates](../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)|Vista del catalogo che consente di visualizzare i certificati di un database.|  
|[sys.dm_pdw_nodes_database_encryption_keys](../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-database-encryption-keys-transact-sql.md)|Vista a gestione dinamica che fornisce informazioni per ogni nodo, sulle chiavi di crittografia utilizzato in un database e lo stato della crittografia di un database.|  
  
## <a name="permissions"></a>Permissions  
Ogni funzionalità e comando di TDE ha requisiti specifici relativi alle autorizzazioni, descritti nelle tabelle precedenti.  
  
Visualizzare i metadati interessati da TDE richiede il `CONTROL SERVER` l'autorizzazione.  
  
## <a name="considerations"></a>Considerazioni  
Durante un'analisi di una nuova crittografia di un database, le operazioni di manutenzione per il database sono disabilitate.  
  
È possibile trovare lo stato della crittografia del database utilizzando la **sys.dm_pdw_nodes_database_encryption_keys** vista a gestione dinamica. Per altre informazioni, vedere la *viste del catalogo e viste a gestione dinamica* sezione più indietro in questo articolo.  
  
### <a name="restrictions"></a>Restrictions  
Le operazioni seguenti non sono consentite durante la `CREATE DATABASE ENCRYPTION KEY`, `ALTER DATABASE ENCRYPTION KEY`, `DROP DATABASE ENCRYPTION KEY`, o `ALTER DATABASE...SET ENCRYPTION` istruzioni.  
  
-   Eliminazione del database.  
  
-   Usando un `ALTER DATABASE` comando.  
  
-   Avvio di un backup del database.  
  
-   Avvio di un ripristino del database.  
  
Le seguenti operazioni o condizioni impedirà il `CREATE DATABASE ENCRYPTION KEY`, `ALTER DATABASE ENCRYPTION KEY`, `DROP DATABASE ENCRYPTION KEY`, o `ALTER DATABASE...SET ENCRYPTION` istruzioni.  
  
-   Un `ALTER DATABASE` comando è in esecuzione.  
  
-   Un backup dei dati è in corso di esecuzione.  
  
Durante la creazione dei file di database, l'inizializzazione immediata dei file non è disponibile se è abilitata la crittografia TDE.  
  
### <a name="areas-not-protected-by-tde"></a>Aree non è protette da TDE  
TDE non protegge le tabelle esterne.  
  
TDE non protegge le sessioni di diagnostica. Gli utenti devono prestare attenzione non alle query con parametri sensibili anche se sessioni di diagnostica sono in uso. Sessioni di diagnostica che rivelano informazioni sensibili devono essere eliminate non appena non sono più necessari.  
  
I dati protetti con TDE viene decrittografati quando viene inserita nella memoria di SQL Server PDW. I dump di memoria vengono creati quando si verificano determinati problemi nell'appliance. Scarica i file rappresentano il contenuto della memoria al momento dell'aspetto problema e può contenere dati sensibili in un formato non crittografato. Il contenuto del dump della memoria deve essere rivisti prima vengono condivise con altri utenti.  
  
Il database master non è protetto da TDE. Anche se il database master non contiene dati utente, contiene informazioni quali nomi account di accesso.  
  
### <a name="transparent-data-encryption-and-transaction-logs"></a>Crittografia trasparente dei dati e log delle transazioni  
L'abilitazione di un database da usare TDE ha l'effetto di azzeramento la parte rimanente del log delle transazioni virtuale per forzare il log delle transazioni virtuale successivo. Ciò garantisce che non rimanga alcun testo non crittografato nei log delle transazioni dopo che il database viene impostato per la crittografia. È possibile trovare lo stato della crittografia del file di log in ogni nodo PDW, vedere la `encryption_state` colonna il `sys.dm_pdw_nodes_database_encryption_keys` visualizzazione, come nel seguente esempio:  
  
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
SQL Server PDW gestisce un set di log previsto per la risoluzione dei problemi. Si noti, non si tratta del log delle transazioni, il log degli errori di SQL Server o nel registro eventi di Windows. Questi log attività PDW possono contenere istruzioni complete in testo non crittografato, alcuni dei quali può contenere i dati dell'utente. Sono esempi tipici **inserire** e **UPDATE** istruzioni. Mascheramento dei dati utente possa essere esplicitamente attivato o disattivato tramite **sp_pdw_log_user_data_masking**. Abilitazione della crittografia in SQL Server PDW automaticamente attiva il mascheramento dei dati utente nei log attività PDW per proteggerli. **sp_pdw_log_user_data_masking** è anche utilizzabile per mascherare le istruzioni quando non si usa TDE, ma che non è consigliato perché riduce in modo significativo la capacità del Team di supporto Microsoft di analizzare i problemi.  
  
### <a name="transparent-data-encryption-and-the-tempdb-system-database"></a>Transparent Data Encryption e database di sistema tempdb  
Il database di sistema tempdb viene crittografato quando è abilitata la crittografia usando [sp_pdw_database_encryption](../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md). Ciò è necessario prima di qualsiasi database può usare Transparent Data Encryption. Ciò potrebbe avere un effetto sulle prestazioni per database non crittografati presenti nella stessa istanza di SQL Server PDW.  
  
## <a name="key-management"></a>Gestione chiavi  
La chiave di crittografia del database (DEK) è protetto per i certificati archiviati nel database master. Questi certificati sono protette dalla chiave master del database (DMK) del database master. La DMK deve essere protetto dalla chiave master del servizio (SMK) per poter essere usato per TDE.  
  
Il sistema può accedere alle chiavi senza richiedere intervento umano (ad esempio, fornire una password). Se il certificato non è disponibile, il sistema restituirà un errore per segnalare che non può essere decrittografata la chiave DEK fino a quando non è disponibile il certificato appropriato.  
  
Quando si sposta un database da un'appliance a un'altra, il certificato usato per proteggere la ' chiave DEK devono essere ripristinati prima di tutto nel server di destinazione. Il database può essere ripristinato come di consueto. Per altre informazioni, vedere la documentazione di SQL Server standard, all'indirizzo [spostare un Database protetto con TDE in un altro Server SQL](https://technet.microsoft.com/library/ff773063.aspx).  
  
I certificati usati per crittografare DEK devono essere conservati fino a quando non esistono backup di database che li utilizzano. Backup del certificato deve includere la chiave privata del certificato, perché senza la chiave privata non può essere utilizzato un certificato per il ripristino di database. Questi backup chiave privata del certificato vengono archiviati in un file separato, protetto da una password che deve essere fornita per il ripristino di certificato.  
  
## <a name="restoring-the-master-database"></a>Ripristino del Database master  
Il database master può essere ripristinato utilizzando **DWConfig**, come parte del ripristino di emergenza.  
  
-   Se il nodo di controllo non è stato modificato, ovvero che se viene ripristinato il database master nell'appliance stessa e invariato da cui è stato eseguito il backup del database master, la DMK e tutti i certificati possono essere lette senza ulteriori interventi.  
  
-   Se il database master viene ripristinato in un dispositivo diverso o se il nodo di controllo è stato modificato dopo il backup del database master, saranno necessario per rigenerare la DMK passaggi aggiuntivi.  
  
    1.  Aprire la DMK:  
  
        ```sql  
        OPEN MASTER KEY DECRYPTION BY PASSWORD = '<password>';  
        ```  
  
    2.  Aggiungere la crittografia dalla chiave SMK:  
  
        ```sql  
        ALTER MASTER KEY   
            ADD ENCRYPTION BY SERVICE MASTER KEY;  
        ```  
  
    3.  Riavviare l'appliance.  
  
## <a name="upgrade-and-replacing-virtual-machines"></a>Aggiornamento e sostituzione di macchine virtuali  
Se è presente una DMK nell'appliance in cui è stata eseguita l'aggiornamento o sostituire una macchina virtuale, è necessario specificare password DMK come parametro.  
  
Esempio di azione di aggiornamento. Sostituire `**********` con la password DMK.  
  
`setup.exe /Action=ProvisionUpgrade ... DMKPassword='**********'`  
  
Esempio di azione per sostituire una macchina virtuale.  
  
`setup.exe /Action=ReplaceVM ... DMKPassword='**********'`  
  
Durante l'aggiornamento, se un database utente è crittografato e la password DMK non viene specificata, l'azione di aggiornamento avrà esito negativo. Durante la sostituzione, se la password corretta non è disponibile quando è presente una DMK, l'operazione ignorerà il passaggio di recupero DMK. Tutti gli altri passaggi verranno completati al termine dell'azione di sostituzione della macchina virtuale, ma l'azione segnala un errore alla fine per indicare che sono necessari passaggi aggiuntivi. Nei log del programma di installazione (che si trova **\ProgramData\Microsoft\Microsoft SQL Server Parallel Data Warehouse\100\Logs\Setup\\\Detail-Setup < timestamp >**), verrà visualizzato l'avviso seguente verso la fine.  
  
`*** WARNING \*\*\* DMK is detected in master database, but could not be recovered automatically! The DMK password was either not provided or is incorrect!`
  
Eseguire manualmente queste istruzione in PDW e riavviare l'appliance in seguito per eseguire il ripristino DMK:  
  
```sql
OPEN MASTER KEY DECRYPTION BY PASSWORD = '<DMK password>';  
ALTER MASTER KEY ADD ENCRYPTION BY SERVICE MASTER KEY;  
```
  
Usare la procedura descritta nel **ripristino del Database master** di paragrafo per ripristinare il database e quindi riavviare l'appliance.  
  
Se la DMK esistenti prima, ma non è stata recuperata dopo l'azione, verrà generato il messaggio di errore seguente quando viene eseguita una query di un database.  
  
```sql
Msg 110806;  
A distributed query failed: Database '<db_name>' cannot be opened due to inaccessible files or insufficient memory or disk space. See the SQL Server errorlog for details.
```  
  
## <a name="performance-impact"></a>Impatto sulle prestazioni  
L'impatto sulle prestazioni della funzionalità TDE varia con il tipo di dati che disponibili, come viene archiviato e il tipo di attività del carico di lavoro in SQL Server PDW. Quando protetto da TDE, il / o di lettura e quindi la decrittografia dei dati o la crittografia e quindi la scrittura dei dati è un'attività a elevato utilizzo di CPU e avrà impatto maggiore quando vengono eseguite altre attività con utilizzo intensivo della CPU nello stesso momento. Poiché Transparent Data Encryption crittografa `tempdb`, Transparent Data Encryption possono influenzare le prestazioni dei database che non vengono crittografati. Per ottenere un'idea precisa delle prestazioni, è consigliabile testare l'intero sistema con l'attività i dati e query.  
  
## <a name="related-content"></a>Contenuto correlato  
I collegamenti seguenti contengono informazioni generali sul modo in cui SQL Server gestisce la crittografia. Questi articoli consentono di comprendere la crittografia di SQL Server, ma questi articoli non dispongono di informazioni specifiche di SQL Server PDW e vengono illustrate le funzionalità che non sono presenti in SQL Server PDW.  
  
-   [Crittografia di SQL Server](../relational-databases/security/encryption/sql-server-encryption.md)  
  
-   [Gerarchia di crittografia](../relational-databases/security/encryption/encryption-hierarchy.md)  
  
-   [Chiavi di crittografia del database e di SQL Server](../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)  

  
## <a name="see-also"></a>Vedere anche  
[ALTER DATABASE](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)  
[CREATE MASTER KEY](../t-sql/statements/create-master-key-transact-sql.md)  
[CREARE UNA CHIAVE DI CRITTOGRAFIA DEL DATABASE](../t-sql/statements/create-database-encryption-key-transact-sql.md)  
[BACKUP CERTIFICATE](../t-sql/statements/backup-certificate-transact-sql.md)  
[sp_pdw_database_encryption](../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)  
[sp_pdw_database_encryption_regenerate_system_keys](../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)  
[sp_pdw_log_user_data_masking](../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md)  
[sys.certificates](../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)  
[sys.dm_pdw_nodes_database_encryption_keys](../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-database-encryption-keys-transact-sql.md)  
  
