---
title: Transparent Data Encryption con il database SQL di Azure | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- TDE, SQL Database
- Transparent Data Encryption, SQL Database
- encryption (SQL Database) TDE
ms.assetid: 0bf7e8ff-1416-4923-9c4c-49341e208c62
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 4ae4437e6beb842d1df7bf2e2d96db8334b208f9
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028684"
---
# <a name="transparent-data-encryption-with-azure-sql-database"></a>Transparent Data Encryption con il database SQL di Azure
  Transparent Data Encryption (anteprima) per il [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)] contribuisce alla protezione dalle minacce di attività dannose eseguendo la crittografia e decrittografia in tempo reale del database, dei backup associati e dei file di log delle transazioni inattivi, senza richiedere modifiche all'applicazione.  
  
 Transparent Data Encryption crittografa l'archivio di un intero database utilizzando una chiave simmetrica denominata chiave di crittografia del database. Nel [!INCLUDE[ssSDS](../includes/sssds-md.md)] la chiave di crittografia del database è protetta con un certificato server predefinito. Il certificato server predefinito è univoco per ogni server del [!INCLUDE[ssSDS](../includes/sssds-md.md)] . Se un database fa parte di una relazione GeoDR, è protetto da una chiave diversa in ogni server. Se due database sono connessi allo stesso server, condividono lo stesso certificato predefinito. [!INCLUDE[msCoName](../includes/msconame-md.md)] ruota automaticamente questi certificati almeno ogni 90 giorni. Per una descrizione generale di TDE, vedere [Transparent Data Encryption &#40;TDE&#41;](../relational-databases/security/encryption/transparent-data-encryption.md).  
  
 [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)] non supporta l'integrazione dell'insieme di credenziali delle chiavi di Azure con TDE. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in esecuzione in una macchina virtuale di Azure può usare una chiave asimmetrica dall'insieme di credenziali delle chiavi. Per ulteriori informazioni, vedere [l'esempio A: Transparent Data Encryption utilizzando una chiave asimmetrica del Key Vault](../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md#ExampleA).  
  
||  
|-|  
|**Si applica a**: [!INCLUDE[sqldbesa](../includes/sqldbesa-md.md)]([Anteprima in alcune aree](https://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag)).|  
  
> [!IMPORTANT]  
>  Si tratta attualmente di una funzionalità di anteprima. L'utente dichiara di essere a conoscenza e di accettare che l'implementazione di Transparent Data Encryption del [!INCLUDE[ssSDS](../includes/sssds-md.md)] nei database è soggetta alle condizioni per l'anteprima indicate nel contratto di licenza, ad esempio il Contratto Enterprise, il Contratto di Microsoft Azure o il Contratto di Sottoscrizione Microsoft Online, oltre a eventuali [Condizioni Supplementari per l'Utilizzo delle Anteprime di Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).  
  
 L'anteprima dello stato di TDE si applica anche nel subset di aree geografiche in cui la famiglia della versione V12 del [!INCLUDE[ssSDS](../includes/sssds-md.md)] è stata annunciata in stato di disponibilità generale. TDE per [!INCLUDE[ssSDS](../includes/sssds-md.md)] non potrà essere usato nei database di produzione finché [!INCLUDE[msCoName](../includes/msconame-md.md)] non ne annuncia il passaggio dalla versione di anteprima a quella di disponibilità generale. Per altre informazioni sul [!INCLUDE[ssSDS](../includes/sssds-md.md)] V12, vedere l'articolo relativo alle [novità del database SQL di Azure](https://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/).  
  
##  <a name="Permissions"></a> Autorizzazioni  
 Per iscriversi per l'anteprima e configurare Transparent Data Encryption tramite il portale di Azure usando l'API REST o PowerShell, è necessario essere connessi come proprietario, collaboratore o Gestore Sicurezza SQL di Azure.  
  
 Per configurare Transparent Data Encryption tramite [!INCLUDE[tsql](../includes/tsql-md.md)] è necessario soddisfare le condizioni seguenti:  
  
-   Si deve essere già registrati per l'anteprima di Transparent Data Encryption.  
  
-   Per creare la chiave di crittografia del database, è necessario essere un amministratore di [!INCLUDE[ssSDS](../includes/sssds-md.md)] oppure un membro del ruolo **dbmanager** nel database master e disporre dell'autorizzazione di **CONTROLLO** sul database.  
  
-   Per eseguire l'istruzione ALTER DATABASE con l'opzione SET, è richiesta solo l'appartenenza al ruolo **dbmanager** .  
  
##  <a name="Preview"></a>Iscriversi per l'anteprima di Transparent Data Encryption e abilitare la crittografia transparent in un database  
  
1.  Visitare il portale di Azure [https://portal.azure.com](https://portal.azure.com) all'indirizzo e accedere con l'account di amministratore o collaboratore di Azure.  
  
2.  Nel banner sinistro fare clic su **SFOGLIA**e quindi su **Database SQL**.  
  
3.  Con la voce **Database SQL** selezionata nel riquadro sinistro fare clic sul proprio database utente.  
  
4.  Nel pannello del database fare clic su **Tutte le impostazioni**.  
  
5.  Nel pannello **Impostazioni** fare clic su **Transparent Data Encryption (anteprima)** per aprire il pannello **Transparent Data Encryption ANTEPRIMA** . Se non si è già iscritti per l'anteprima di Transparent Data Encryption, le impostazioni di crittografia dei dati saranno disabilitate finché non si completa l'iscrizione.  
  
6.  Fare clic su **CONDIZIONI PER L'ANTEPRIMA**.  
  
7.  Leggere le condizioni della versione di anteprima e, se si accettano le condizioni, selezionare la casella di controllo **condizioni di EncryptionPreview dati trasparenti** , quindi fare clic su **OK** nella parte inferiore della pagina. Tornare al pannello **dati encryptionPREVIEW** , in cui il pulsante **crittografia dati** dovrebbe ora essere abilitato.  
  
8.  Nel pannello **Crittografia dati ANTEPRIMA** spostare lo stato attivo del pulsante **Crittografia dati** su **Attivato**e quindi fare clic su **Salva** (in alto nella pagina) per applicare l'impostazione. Il valore di **Stato crittografia** indicherà approssimativamente lo stato di avanzamento di Transparent Data Encryption.  
  
     ![SQLDB_TDE_TermsNewUI](../../2014/database-engine/media/sqldb-tde-termsnewui.png "SQLDB_TDE_TermsNewUI")  
  
     È anche possibile monitorare lo stato di avanzamento della crittografia connettendosi al [!INCLUDE[ssSDS](../includes/sssds-md.md)] con uno strumento di query quale [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] come utente del database con l'autorizzazione di **VISUALIZZAZIONE STATO DEL DATABASE** . Eseguire una `encryption_state` query sulla colonna della vista [sys. dm _database_encryption_keys](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql) .  
  
##  <a name="Encrypt"></a> Abilitazione di TDE nel [!INCLUDE[ssSDS](../includes/sssds-md.md)] tramite Transact-SQL  
 I passaggi seguenti presuppongono che sia già stata effettuata l'iscrizione per l'anteprima.  
  
###  <a name="TsqlProcedure"></a>  
  
1.  Connettersi al database con un account di accesso come amministratore o membro del ruolo **dbmanager** nel database master.  
  
2.  Eseguire le istruzioni seguenti per creare una chiave di crittografia del database e crittografare il database.  
  
    ```  
    -- Create the database encryption key that will be used for TDE.  
    CREATE DATABASE ENCRYPTION KEY   
    WITH ALGORITHM = AES_256   
    ENCRYPTION BY SERVER CERTIFICATE ##MS_TdeCertificate##;  
  
    -- Enable encryption  
    ALTER DATABASE [AdventureWorks] SET ENCRYPTION ON;  
    GO  
    ```  
  
3.  Per monitorare lo stato di avanzamento della [!INCLUDE[ssSDS](../includes/sssds-md.md)]crittografia in, gli utenti del database con l'autorizzazione **View database state** possono eseguire una query sulla `encryption_state` colonna della vista [sys. dm _database_encryption_keys](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql) .  
  
## <a name="enabling-tde-on-sql-database-by-using-powershell"></a>Abilitazione di Transparent Data Encryption nel database SQL tramite PowerShell  
 Con Azure PowerShell è possibile eseguire il comando seguente per attivare o disattivare TDE. Prima di eseguire il comando, è necessario connettere l'account alla finestra di PowerShell. I passaggi seguenti presuppongono che sia già stata effettuata l'iscrizione per l'anteprima. Per altre informazioni su PowerShell, vedere [Come installare e configurare Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).  
  
1.  Per abilitare Transparent Data Encryption, tornare al relativo stato e visualizzare l'attività di crittografia.  
  
    ```  
    PS C:\> Switch-AzureMode -Name AzureResourceManager  
  
    PS C:\> Set-AzureSqlDatabaseTransparentDataEncryption -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1" -State "Enabled"  
  
    PS C:\> Get-AzureSqlDatabaseTransparentDataEncryption -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1"  
  
    PS C:\> Get-AzureSqlDatabaseTransparentDataEncryptionActivity -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1"  
  
    ```  
  
2.  Per disabilitare TDE:  
  
    ```  
    PS C:\> Set-AzureSqlDatabaseTransparentDataEncryption -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1" -State "Disabled"  
  
    PS C:\> Switch-AzureMode -Name AzureServiceManagement  
    ```  
  
##  <a name="Decrypt"></a> Decrittografia di un database protetto con TDE nel [!INCLUDE[ssSDS](../includes/sssds-md.md)]  
  
#### <a name="to-disable-tde-by-using-the-azure-portal"></a>Per disabilitare TDE tramite il portale di Azure  
  
1.  Visitare il portale di Azure [https://portal.azure.com](https://portal.azure.com) all'indirizzo e accedere con l'account di amministratore o collaboratore di Azure.  
  
2.  Nel banner sinistro fare clic su **SFOGLIA**e quindi su **Database SQL**.  
  
3.  Con la voce **Database SQL** selezionata nel riquadro sinistro fare clic sul proprio database utente.  
  
4.  Nel pannello del database fare clic su **Tutte le impostazioni**.  
  
5.  Nel pannello **Impostazioni** fare clic su **Transparent Data Encryption (anteprima)** per aprire il pannello **Transparent Data Encryption ANTEPRIMA** .  
  
6.  Nel pannello **Transparent Data Encryption ANTEPRIMA** spostare lo stato attivo del pulsante **Crittografia dati** su **Attivato**e quindi fare clic su **Salva** (in alto nella pagina) per applicare l'impostazione. Il valore di **Stato crittografia** indicherà approssimativamente lo stato di avanzamento della decrittografia trasparente dei dati.  
  
     È anche possibile monitorare lo stato di avanzamento della decrittografia connettendosi al [!INCLUDE[ssSDS](../includes/sssds-md.md)] con uno strumento di query quale [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] come utente del database con l'autorizzazione di **VISUALIZZAZIONE STATO DEL DATABASE** . Eseguire una `encryption_state` query sulla colonna della vista [sys. dm _database_encryption_keys](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql).  
  
#### <a name="to-disable-tde-by-using-transact-sql"></a>Per disabilitare TDE tramite Transact-SQL  
  
1.  Connettersi al database con un account di accesso come amministratore o membro del ruolo **dbmanager** nel database master.  
  
2.  Eseguire le istruzioni seguenti per decrittografare il database.  
  
    ```  
    -- Enable encryption  
    ALTER DATABASE [AdventureWorks] SET ENCRYPTION OFF;  
    GO  
    ```  
  
3.  Per monitorare lo stato di avanzamento della [!INCLUDE[ssSDS](../includes/sssds-md.md)]crittografia in, gli utenti del database con l'autorizzazione **View database state** possono eseguire una query sulla `encryption_state` colonna della vista [sys. dm _database_encryption_keys](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql) .  
  
##  <a name="Working"></a>Uso dei database protetti con Transparent Data Encryption in[!INCLUDE[ssSDS](../includes/sssds-md.md)]  
 Non è necessario decrittografare i database per eseguire operazioni all'interno di Azure. Le impostazioni di Transparent Data Encryption nel database di origine o nel database primario vengono ereditate in modo trasparente nel database di destinazione. Sono incluse le operazioni che prevedono le attività seguenti:  
  
-   Ripristino geografico  
  
-   Ripristino temporizzato self-service  
  
-   Ripristino di un database eliminato  
  
-   Replica a livello geografico attiva  
  
-   Creazione di una copia del database  
  
##  <a name="Moving"></a>Trasferimento di un database protetto da Transparent Data Encryption in utilizzando. File BACPAC  
 Quando si esporta un database protetto con TDE tramite la funzione Esporta Database nel portale del [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)] o tramite l'Importazione/Esportazione guidata [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], il contenuto del database non è crittografato. Il contenuto viene archiviato in file BACPAC che non sono crittografati.  Assicurarsi di proteggere i file BACPAC nel modo appropriato e abilitare TDE al termine dell'importazione del nuovo database.  
  
## <a name="related-sql-server-topic"></a>Argomento correlato a SQL Server  
 [Abilitare TDE usando EKM](../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Transparent Data Encryption &#40;TDE&#41;](../relational-databases/security/encryption/transparent-data-encryption.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-credential-transact-sql)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-asymmetric-key-transact-sql)   
 [CREATE DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-database-encryption-key-transact-sql)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [Opzioni ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)  
  
  
