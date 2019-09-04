---
title: 'Avvio rapido: Backup e ripristino di SQL Server nel servizio Archiviazione BLOB di Azure| Microsoft Docs'
ms.custom: ''
ms.date: 04/09/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 9e1d94ce-2c93-45d1-ae2a-2a7d1fa094c4
author: rothja
ms.author: jroth
ms.openlocfilehash: ae4d9cd9333e8dd42582f972a0d19260b2c9a3ee
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155705"
---
# <a name="quickstart-sql-server-backup-and-restore-to-azure-blob-storage-service"></a>Avvio rapido: Backup e ripristino di SQL Server nel servizio di archiviazione BLOB di Azure
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Questa guida di avvio rapido contiene nozioni utili sulla scrittura di backup nel servizio Archiviazione BLOB di Azure e sul ripristino dallo stesso.  Questa guida di avvio rapido illustra come creare un contenitore BLOB di Azure e le credenziali per l'accesso all'account di archiviazione, la scrittura di un backup nel servizio BLOB e l'esecuzione di un ripristino semplice.
  
### <a name="prerequisites"></a>Prerequisites  
Per completare questa guida di avvio rapido è necessario conoscere i concetti di backup e ripristino di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e la sintassi T-SQL. Per usare questa guida di avvio rapido sono necessari un account di archiviazione di Azure, SQL Server Management Studio (SSMS), l'accesso a un server che esegue SQL Server e un database AdventureWorks. Inoltre, l'account utente usato per eseguire i comandi BACKUP e RESTORE deve essere incluso nel ruolo del database **db_backup operator** con autorizzazioni **Modifica qualsiasi credenziale**. 

- Ottenere un [account Azure](https://azure.microsoft.com/offers/ms-azr-0044p/) gratuito.
- Creare un [account di archiviazione di Azure](https://docs.microsoft.com/azure/storage/common/storage-quickstart-create-account?tabs=portal).
- Installare [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
- Installare [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads).
- Assegnare l'account utente al ruolo [db_backupoperator](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/database-level-roles) e concedere le autorizzazioni [Modifica qualsiasi credenziale](https://docs.microsoft.com/sql/t-sql/statements/alter-credential-transact-sql). 


## <a name="create-azure-blob-container"></a>Creare un contenitore BLOB di Azure
Un contenitore fornisce un raggruppamento di un set di BLOB. Tutti i BLOB devono essere inclusi in un contenitore. Un account può contenere un numero illimitato di contenitori, tuttavia ne deve contenere almeno uno. In un contenitore è possibile archiviare un numero illimitato di BLOB. 

[!INCLUDE[freshInclude](../includes/paragraph-content/fresh-note-steps-feedback.md)]

Per creare un contenitore, seguire questa procedura:

1. Aprire il portale di Azure. 
1. Passare all'account di archiviazione. 
1. Selezionare l'account di archiviazione e scorrere verso il basso fino a **Servizi BLOB**.
1. Selezionare **BLOB** e quindi selezionare +**Contenitore** per aggiungere un nuovo contenitore. 
1. Immettere il nome del contenitore e prendere nota del nome specificato. Queste informazioni vengono usate nell'URL (percorso del file di backup) nelle istruzioni T-SQL più avanti in questa guida di avvio rapido. 
1. Fare clic su **OK**. 
    
    ![Nuovo contenitore](media/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service/new-container.png)


  > [!NOTE]
  > L'autenticazione per l'account di archiviazione è obbligatoria per il backup e il ripristino di SQL Server anche se si sceglie di creare un contenitore pubblico. È anche possibile creare un contenitore a livello di programmazione tramite le API REST. Per altre informazioni, vedere [Create container](https://docs.microsoft.com/rest/api/storageservices/Create-Container) (Crea contenitore)

## <a name="create-a-test-database"></a>Creare un database di test 

1. Avviare [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md) e connettersi all'istanza di SQL Server.
1. Aprire una finestra **Nuova query**. 
1. Eseguire il codice Transact-SQL (T-SQL) seguente per creare il database di test. Aggiornare il nodo **Database** in **Esplora oggetti** per vedere il nuovo database. 

```sql
USE [master]
GO

CREATE DATABASE [SQLTestDB]
GO

USE [SQLTestDB]
GO
CREATE TABLE SQLTest (
    ID INT NOT NULL PRIMARY KEY,
    c1 VARCHAR(100) NOT NULL,
    dt1 DATETIME NOT NULL DEFAULT getdate()
)
GO


USE [SQLTestDB]
GO

INSERT INTO SQLTest (ID, c1) VALUES (1, 'test1')
INSERT INTO SQLTest (ID, c1) VALUES (2, 'test2')
INSERT INTO SQLTest (ID, c1) VALUES (3, 'test3')
INSERT INTO SQLTest (ID, c1) VALUES (4, 'test4')
INSERT INTO SQLTest (ID, c1) VALUES (5, 'test5')
GO

SELECT * FROM SQLTest
GO
```


## <a name="create-a-sql-server-credential"></a>Creare le credenziali di SQL Server
Una credenziale di SQL Server è un oggetto utilizzato per archiviare le informazioni di autenticazione necessarie per connettersi a una risorsa all'esterno di SQL Server. In questo caso, nei processi di backup e ripristino di SQL Server le credenziali vengono usate per l'autenticazione per il servizio Archiviazione BLOB di Azure. Nelle credenziali vengono archiviati il nome dell'account di archiviazione e i relativi valori della **chiave di accesso** . Una volta create, le credenziali devono essere specificate nell'opzione WITH CREDENTIAL durante l'esecuzione delle istruzioni BACKUP/RESTORE. Per altre informazioni sulle credenziali, vedere [Credenziali](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/credentials-database-engine). 

  > [!IMPORTANT]
  > I requisiti per la creazione delle credenziali di SQL Server descritti di seguito sono specifici per i processi di backup di SQL Server ([Backup di SQL Server nell'URL](backup-restore/sql-server-backup-to-url.md)e [Backup gestito di SQL Server in Microsoft Azure](backup-restore/sql-server-managed-backup-to-microsoft-azure.md)). SQL Server usa il nome dell'account di archiviazione e le informazioni sulla chiave di accesso per accedere all'archiviazione di Azure per scrivere e leggere i backup.

### <a name="access-keys"></a>Chiavi di accesso
Per creare le credenziali, sono necessarie le chiavi di accesso per l'account di archiviazione. 

1. Passare ad **Account di archiviazione** nel portale di Azure. 
1. Selezionare **Chiavi di accesso** in **Impostazioni**. 
1. Salvare sia la chiave che la stringa di connessione per usarle più avanti in questa guida di avvio rapido. 

   ![Chiavi di accesso](media/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service/access-keys.png)

### <a name="create-a-sql-server-credential"></a>Creare le credenziali di SQL Server
Usare la chiave di accesso salvata per creare le credenziali di SQL Server seguendo questa procedura. 

1. Connettersi all'istanza di SQL Server usando SQL Server Management Studio. 
1. Selezionare il database **SQLTestDB** e aprire una finestra **Nuova query**. 
1. Copiare, incollare ed eseguire l'esempio seguente nella finestra Query modificandolo in base alle esigenze: 

   ```sql
   CREATE CREDENTIAL mycredential   
   WITH IDENTITY= 'msftutorialstorage', -- this is the name of the storage account you specified when creating a storage account   
   SECRET = '<storage account access key>' -- this should be either the Primary or Secondary Access Key for the storage account 
   ```

1. Eseguire l'istruzione per creare le credenziali. 

## <a name="back-up-database-to-the-azure-blob-storage-service"></a>Eseguire il backup del database nel servizio Archiviazione BLOB di Azure
In questa sezione si userà un'istruzione T-SQL per eseguire un backup completo del database nel servizio Archiviazione BLOB di Azure. 

1. Connettersi all'istanza di SQL Server usando SQL Server Management Studio. 
1. Selezionare il database **SQLTestDB** e aprire una finestra **Nuova query**. 
1. Copiare e incollare l'esempio seguente nella finestra Query modificandolo se necessario: 

     ```sql
     BACKUP DATABASE [SQLTestDB] 
     TO URL = 'https://msftutorialstorage.blob.core.windows.net/sql-backup/SQLTestDB.bak' 
     /* URL includes the endpoint for the BLOB service, followed by the container name, and the name of the backup file*/ 
     WITH CREDENTIAL = 'mycredential';
     /* name of the credential you created in the previous step */ 
     GO
     ```

1. Eseguire l'istruzione per il backup del database SQLTestDB nell'URL. 

 
## <a name="restore-database-from-azure-blob-storage-service"></a>Ripristinare il database dal servizio Archiviazione BLOB di Azure
In questa sezione verrà usata un'istruzione T-SQL per ripristinare il backup di database completo. 

1. Connettersi all'istanza di SQL Server usando SQL Server Management Studio. 
1. Aprire una finestra **Nuova query**. 
1. Copiare e incollare l'esempio seguente nella finestra Query modificandolo se necessario: 

 ```sql
 RESTORE DATABASE [SQLTestDB] 
 FROM URL = 'https://msftutorialstorage.blob.core.windows.net/sql-backup/SQLTestDB.bak' 
 WITH CREDENTIAL = 'mycredential',
 STATS = 5 -- use this to see monitor the progress
 GO
 ``` 

## <a name="see-also"></a>Vedere anche 
Di seguito sono indicate alcune letture suggerite per comprendere i concetti e le procedure consigliate quando si usa il servizio Archiviazione BLOB di Azure per i backup di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
-   [Backup e ripristino di SQL Server con il servizio di archiviazione BLOB di Microsoft Azure](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)   
-   [Procedure consigliate e risoluzione dei problemi per il backup di SQL Server nell'URL](../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
  
