---
title: Eseguire il backup, ripristino e spostamento del catalogo SSIS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: bf806aef-8556-48ab-aed5-e95de9a2204e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 625e090ab65eff7a912785e3ddef2de3e7d83b0a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66061269"
---
# <a name="backup-restore-and-move-the-ssis-catalog"></a>Backup, ripristino e spostamento del catalogo SSISDB
  [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] è incluso il database SSISDB. È possibile eseguire una query sulle viste nel database SSISDB per verificare oggetti, impostazioni e dati operativi archiviati nel catalogo **SSISDB** . In questo argomento vengono fornite istruzioni per l'esecuzione del backup e del ripristino del database.  
  
 Nel catalogo **SSISDB** sono archiviati i pacchetti distribuiti nel server [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Per ulteriori informazioni sul catalogo, vedere [Catalogo SSIS](catalog/ssis-catalog.md).  
  
##  <a name="backup"></a> Per eseguire il backup del database SSIS  
  
1.  Aprire [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] e connettersi a un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
2.  Eseguire il backup della chiave master per il database SSISDB tramite l'istruzione Transact-SQL BACKUP MASTER KEY. La chiave viene archiviata in un file specificato. Utilizzare una password per crittografare la chiave master nel file.  
  
     Per altre informazioni sull'istruzione, vedere [BACKUP MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-master-key-transact-sql).  
  
     Nell'esempio seguente la chiave master viene esportata nel file `c:\temp directory\RCTestInstKey`. Per crittografare la chiave master viene utilizzata la password `LS2Setup!` .  
  
    ```  
    backup master key to file = 'c:\temp\RCTestInstKey'  
           encryption by password = 'LS2Setup!'  
  
    ```  
  
3.  Eseguire il backup del database SSISDB tramite la finestra di dialogo **Backup database** in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Per altre informazioni, vedere [Procedura: Eseguire il backup del database (SQL Server Management Studio)](https://go.microsoft.com/fwlink/?LinkId=231812).  
  
4.  Generare lo script CREATE LOGIN per ##MS_SSISServerCleanupJobLogin##, effettuando le operazioni riportate di seguito. Per altre informazioni, vedere [CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql).  
  
    1.  In Esplora oggetti in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] espandere il nodo **Sicurezza**, quindi espandere il nodo **Account di accesso**.  
  
    2.  Fare clic con il pulsante destro del mouse su **##MS_SSISServerCleanupJobLogin##** , quindi fare clic su **Crea script per account di accesso** > **Genera codice per istruzione CREATE in** > **Nuova finestra editor di query**.  
  
5.  Se si ripristina il database SSISDB a un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in cui il catalogo SSISDB non è mai stato creato, generare lo script CREATE PROCEDURE per sp_ssis_startup, effettuando le operazioni riportate di seguito. Per altre informazioni, vedere [CREATE PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-procedure-transact-sql).  
  
    1.  In Esplora oggetti espandere il nodo **Database**, quindi espandere **master** > **Programmabilità** > nodo **Stored procedure**.  
  
    2.  Fare clic con il pulsante destro del mouse su **dbo.sp_ssis_startup**, quindi fare clic su **Crea script per stored procedure** > **Genera codice per istruzione CREATE in** > **Nuova finestra editor di query**.  
  
6.  Verificare che SQL Server Agent sia stato avviato.  
  
7.  Se si ripristina il database SSISDB a un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in cui il catalogo SSISDB non è mai stato creato, generare uno script per il processo di manutenzione del server SSIS, effettuando le operazioni riportate di seguito. Lo script viene creato automaticamente in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent quando viene creato il catalogo SSISDB. Il processo consente di pulire i log operazioni di pulizia al di fuori del periodo di memorizzazione e di rimuovere le versioni precedenti dei progetti.  
  
    1.  In Esplora oggetti espandere il nodo **SQL Server Agent** , quindi espandere il nodo **Processi** .  
  
    2.  Fare clic con il pulsante destro del mouse sul processo di manutenzione del server SSIS, quindi fare clic su **Crea script per processo** > **Genera codice per istruzione CREATE in** > **Nuova finestra editor di query**.  
  
### <a name="to-restore-the-ssis-database"></a>Per ripristinare il database SSIS  
  
1.  Se si ripristina il database SSISDB a un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in cui il catalogo SSISDB non è mai stato creato, abilitare Common Language Runtime (CLR) eseguendo la stored procedure sp_configure. Per altre informazioni, vedere [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) e [Opzione clr enabled](https://go.microsoft.com/fwlink/?LinkId=231855).  
  
    ```  
    use master   
           sp_configure 'clr enabled', 1  
           reconfigure  
  
    ```  
  
2.  Se si ripristina il database SSISDB a un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in cui il catalogo SSISDB non è mai stato creato, creare la chiave asimmetrica e l'accesso da quest'ultima e concedere l'autorizzazione UNSAFE all'account di accesso.  
  
    ```  
    Create Asymmetric key MS_SQLEnableSystemAssemblyLoadingKey  
           FROM Executable File = 'C:\Program Files\Microsoft SQL Server\110\DTS\Binn\Microsoft.SqlServer.IntegrationServices.Server.dll'  
  
    ```  
  
     [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] Per le stored procedure CLR è necessario concedere le autorizzazioni UNSAFE all'account di accesso, poiché per questo account è richiesto un accesso aggiuntivo alle risorse limitate, ad esempio l'API Microsoft Win32. Per altre informazioni sull'autorizzazione codice UNSAFE, vedere [Creazione di un assembly](../relational-databases/clr-integration/assemblies/creating-an-assembly.md).  
  
    ```  
    Create Login MS_SQLEnableSystemAssemblyLoadingUser  
           FROM Asymmetric key MS_SQLEnableSystemAssemblyLoadingKey   
  
           Grant unsafe Assembly to MS_SQLEnableSystemAssemblyLoadingUser  
  
    ```  
  
3.  Ripristinare il database SSISDB dal backup tramite la finestra di dialogo **Ripristina database** in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Per ulteriori informazioni, vedere gli argomenti seguenti.  
  
    -   [Ripristina database &#40;pagina Generale&#41;](general-page-of-integration-services-designers-options.md)  
  
    -   [Ripristina database &#40;pagina File&#41;](../relational-databases/backup-restore/restore-database-files-page.md)  
  
    -   [Ripristina database &#40;pagina Opzioni&#41;](../relational-databases/backup-restore/restore-database-options-page.md)  
  
4.  Eseguire gli script creati nella procedura [Per eseguire il backup del database SSIS](#backup) per ##MS_SSISServerCleanupJobLogin##, sp_ssis_startup e per il processo di manutenzione del server SSIS. Verificare che SQL Server Agent sia stato avviato.  
  
5.  Eseguire l'istruzione riportata di seguito per impostare l'esecuzione automatica della stored procedure sp_ssis_startup. Per altre informazioni, vedere [sp_procoption &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-procoption-transact-sql).  
  
    ```  
    EXEC sp_procoption N'sp_ssis_startup','startup','on'  
    ```  
  
6.  Eseguire il mapping dell'utente di SSISDB ##MS_SSISServerCleanupJobUser## (database SSISDB) a ##MS_SSISServerCleanupJobLogin## tramite la finestra di dialogo **Proprietà account di accesso** in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
7.  Ripristinare la chiave master utilizzando uno dei metodi riportati di seguito. Per ulteriori informazioni sulla crittografia e sulle chiavi master, vedere [Gerarchia di crittografia](../relational-databases/security/encryption/encryption-hierarchy.md).  
  
    -   **Metodo 1**  
  
         Usare questo metodo se si è già eseguito un backup della chiave master del database e si dispone della password usata per crittografare la chiave master.  
  
        ```  
               Restore master key from file = 'c:\temp\RCTestInstKey'  
               Decryption by password = 'LS2Setup!' -- 'Password used to encrypt the master key during SSISDB backup'  
               Encryption by password = 'LS3Setup!' -- 'New Password'  
               Force  
  
        ```  
  
        > [!NOTE]  
        >  Verificare che l'account del servizio [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] disponga delle autorizzazioni per leggere il file della chiave di backup.  
  
        > [!NOTE]  
        >  Se la chiave master del database non è stata ancora crittografata dalla chiave master del servizio, si riceverà il messaggio di avviso seguente visualizzato in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] . Ignorare il messaggio.  
        >   
        >  **Impossibile decrittografare la chiave master corrente. L'errore è stato ignorato perché è stata specificata l'opzione FORCE.**  
        >   
        >  L'argomento FORCE consente di specificare che è consigliabile che il processo di ripristino continui anche se la chiave master del database corrente non è aperta. Per il catalogo SSISDB, dal momento che la chiave master del database non è stata aperta nell'istanza in cui si esegue il ripristino del database, si visualizzerà questo messaggio.  
  
    -   **Metodo 2**  
  
         Utilizzare questo metodo se si dispone della password originale utilizzata per creare SSISDB.  
  
        ```  
        open master key decryption by password = 'LS1Setup!' --'Password used when creating SSISDB'  
               Alter Master Key Add encryption by Service Master Key  
        ```  
  
8.  Determinare se lo schema del catalogo SSISDB e i file binari di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] (assembly ISServerExec e SQLCLR) sono compatibili eseguendo [catalog.check_schema_version](/sql/integration-services/system-stored-procedures/catalog-check-schema-version).  
  
9. Per verificare il corretto ripristino del database SSISDB, effettuare delle operazioni nel catalogo SSISDB, ad esempio l'esecuzione dei pacchetti distribuiti nel server [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Per altre informazioni, vedere [Eseguire un pacchetto sul server SSIS mediante SQL Server Management Studio](run-a-package-on-the-ssis-server-using-sql-server-management-studio.md).  
  
### <a name="to-move-the-ssis-database"></a>Per spostare il database SSIS  
  
-   Seguire le istruzioni per lo spostamento di database utente. Per altre informazioni, vedere [Spostare database utente](../relational-databases/databases/move-user-databases.md).  
  
     Assicurarsi che venga eseguito il backup della chiave master per il database SSISDB e proteggere il file di backup. Per altre informazioni, vedere [Per eseguire il backup del database SSIS](#backup).  
  
     Assicurarsi che gli oggetti pertinenti a Integration Services (SSIS) vengano creati nella nuova istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in cui non è ancora stato creato il catalogo SSISDB.  
  
  
