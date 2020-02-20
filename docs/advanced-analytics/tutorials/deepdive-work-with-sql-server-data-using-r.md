---
title: Database per le esercitazioni su RevoScaleR
description: 'Esercitazione di RevoScaleR 1: Come creare un database di SQL Server per le esercitazioni su R.'
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ae2fd2d200b6a231dd76f04556d6d221df00809f
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "74947209"
---
# <a name="create-a-database-and-permissions-sql-server-and-revoscaler-tutorial"></a>Creare un database e le autorizzazioni (esercitazioni su SQL Server e RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questa è l'esercitazione 1 della [serie di esercitazioni per RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) dedicate all'uso delle [funzioni di RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

In questa esercitazione viene descritto come creare un database di SQL Server e impostare le autorizzazioni necessarie per completare le altre esercitazioni di questa serie. Usare [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) o a un altro editor di query per completare le attività seguenti:

> [!div class="checklist"]
> * Creare un nuovo database in cui archiviare i dati per il training e l'assegnazione dei punteggi di due modelli R
> * Creare un account di accesso per un database con autorizzazioni per la creazione e l'utilizzo di oggetti di database
  
## <a name="create-the-database"></a>Creare il database

Per questa esercitazione è necessario un database per l'archiviazione di dati e codice. Se non si dispone dei diritti di amministratore, chiedere all'amministratore dei database di creare il database e impostare un account di accesso. Saranno necessarie le autorizzazioni per scrivere e leggere i dati e per eseguire script R.

1. In SQL Server Management Studio connettersi a un'istanza di database con supporto per R.

2. Fare clic con il pulsante destro del mouse su **Database** e scegliere **Nuovo database**.
  
2. Digitare un nome per il nuovo database: RevoDeepDive.
  
## <a name="create-a-login"></a>Crea un accesso
  
1. Selezionare **Nuova query**e modificare il contesto del database sul database master.
  
2. Nella nuova finestra **Query** , eseguire i comandi seguenti per creare gli account utente e assegnarli al database usato in questa esercitazione. Assicurarsi di modificare il nome del database, se necessario.

3. Per verificare che l'account di accesso sia stato creato, espandere **Sicurezza** e quindi **Utenti**.
  
**utente di Windows**
  
```sql
 -- Create server user based on Windows account
USE master
GO
CREATE LOGIN [<DOMAIN>\<user_name>] FROM WINDOWS WITH DEFAULT_DATABASE=[RevoDeepDive]

 --Add the new user to tutorial database
USE [RevoDeepDive]
GO
CREATE USER [<user_name>] FOR LOGIN [<DOMAIN>\<user_name>] WITH DEFAULT_SCHEMA=[db_datareader]
```

**Account di accesso SQL**

```sql
-- Create new SQL login
USE master
GO
CREATE LOGIN [DDUser01] WITH PASSWORD='<type password here>', CHECK_EXPIRATION=OFF, CHECK_POLICY=OFF;

-- Add the new SQL login to tutorial database
USE RevoDeepDive
GO
CREATE USER [DDUser01] FOR LOGIN [DDUser01] WITH DEFAULT_SCHEMA=[db_datareader]
```

## <a name="assign-permissions"></a>Assegnare le autorizzazioni

Questa esercitazione illustra lo script R e le operazioni DDL, tra cui la creazione e l'eliminazione di tabelle e stored procedure e l'esecuzione di uno script R in un processo esterno di SQL Server. In questo passaggio vengono assegnate le autorizzazioni necessarie per poter eseguire queste attività.

Questo esempio presuppone che sia stato creato un account di accesso SQL (DDUser01), ma se è stato creato un account di accesso Windows, usare quest'ultimo.

```sql
USE RevoDeepDive
GO

EXEC sp_addrolemember 'db_owner', 'DDUser01'
GRANT EXECUTE ANY EXTERNAL SCRIPT TO DDUser01
GO
```

## <a name="troubleshoot-connections"></a>Risolvere i problemi delle connessioni

In questa sezione sono elencati alcuni problemi comuni che possono verificarsi durante l'impostazione del database.

- **Come è possibile verificare la connettività del database e controllare le query SQL?**
  
    È possibile che, prima di eseguire il codice R tramite il server, si voglia controllare che il database sia raggiungibile dall'ambiente di sviluppo R. Entrambi [Esplora Server di Visual Studio](https://docs.microsoft.com/previous-versions/x603htbk(v=vs.140)) e [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md) sono strumenti gratuiti con connettività di database e funzionalità di gestione molto efficienti.
  
    Se non si vogliono installare altri strumenti di gestione del database, è possibile creare una connessione di test per l'istanza di SQL Server usando l' [Amministrazione origine dati ODBC](https://docs.microsoft.com/sql/odbc/admin/odbc-data-source-administrator?view=sql-server-2017) in Pannello di controllo. Se il database è configurato correttamente e il nome utente e la password specificati sono corretti, sarà possibile visualizzare il database appena creato e selezionarlo come database predefinito.
  
    Gli errori di connessione si verificano solitamente se le connessioni remote non sono abilitate per il server o se il protocollo Named Pipes non è abilitato. Per altri suggerimenti sulla risoluzione dei problemi, vedere questo articolo: [Risolvere i problemi di connessione al motore di database di SQL Server](https://docs.microsoft.com/sql/database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine).
  
- **Il nome della tabella datareader è preceduto dal prefisso it. Perché?**
  
    Se si specifica che lo schema predefinito per questo utente è **db_datareader**, tutte le tabelle e gli altri nuovi oggetti creati da questo utente saranno preceduti da un prefisso costituito da questo nome di *schema*. Uno schema è una sorta di cartella. Può essere aggiunto a un database per organizzare gli oggetti. Lo schema definisce anche i privilegi dell'utente all'interno del database.
  
    Se lo schema è associato a un nome utente specifico, l'utente diventa il _proprietario dello schema_. Ogni volta che si crea un oggetto, l'oggetto sarà sempre creato in base al proprio schema, a meno che non si chieda specificatamente di crearlo in un altro schema.
  
    Ad esempio, se si crea una tabella con il nome **TestData** e lo schema predefinito è **db_datareader**, la tabella verrà creata con il nome `<database_name>.db_datareader.TestData`.
  
    Per questo motivo, un database può contenere più tabelle con lo stesso nome, purché le tabelle appartengano a schemi diversi.
   
    Se si cerca una tabella senza specificare uno schema, il server di database cercherà uno schema di cui si è proprietari. Non è pertanto necessario specificare il nome dello schema quando si accede a tabelle di uno schema associato al proprio account di accesso.
  
- **Non ho privilegi DLL. Posso comunque seguire l'esercitazione**?
  
    Sì, ma è necessario chiedere a un altro utente di precaricare i dati nelle tabelle di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e passare direttamente all'esercitazione successiva. In questa esercitazione le funzioni che richiedono privilegi DDL sono espressamente indicate (laddove possibile).

    Chiedere inoltre all'amministratore di ricevere l'autorizzazione EXECUTE ANY EXTERNAL SCRIPT, necessaria per l'esecuzione dello script R, in remoto o tramite `sp_execute_external_script`.

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Creare oggetti dati di SQL Server usando RxSqlServerData](../../advanced-analytics/tutorials/deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)