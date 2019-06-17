---
title: 'Creare un database e le autorizzazioni per RevoScaleR esercitazioni: SQL Server Machine Learning'
description: Procedura dettagliata su come creare un database di SQL Server per le esercitazioni di R...
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 2ed5d6e7ef3b0d6e8ac5ebaa3533c6bebce5e856
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62641094"
---
# <a name="create-a-database-and-permissions-sql-server-and-revoscaler-tutorial"></a>Creare un database e autorizzazioni (esercitazione di RevoScaleR e SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

In questa lezione fa parte il [esercitazione RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) su come usare [funzioni RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

Lezione uno è sull'impostazione di un database di SQL Server e le autorizzazioni necessarie per completare questa esercitazione. Uso [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) o un altro editor di query per completare le attività seguenti:

> [!div class="checklist"]
> * Creare un nuovo database per archiviare i dati per il training e valutazione dei due modelli R
> * Creare un account di accesso utente con autorizzazioni per la creazione e utilizzo di oggetti di database
  
## <a name="create-the-database"></a>Creare il database

Questa esercitazione richiede un database per l'archiviazione dei dati e il codice. Se non si è amministratore, richiedere l'amministratore del database per creare il database e account di accesso per te. Sono necessarie autorizzazioni per scrivere e leggere i dati e per eseguire gli script R.

1. In SQL Server Management Studio, connettersi a un'istanza di database abilitato per R.

2. Fare doppio clic su **database**e selezionare **nuovo database**.
  
2. Digitare un nome per il nuovo database: RevoDeepDive.
  

## <a name="create-a-login"></a>Crea un accesso
  
1. Selezionare **Nuova query**e modificare il contesto del database sul database master.
  
2. Nella nuova finestra **Query** , eseguire i comandi seguenti per creare gli account utente e assegnarli al database usato in questa esercitazione. Assicurarsi di modificare il nome del database, se necessario.

3. Per verificare l'account di accesso, selezionare il nuovo database, espandere **sicurezza**, espandere **utenti**.
  
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

Questa esercitazione viene illustrato lo script R e le operazioni DDL, inclusa la creazione e l'eliminazione di tabelle e stored procedure e l'esecuzione di script R in un processo esterno in SQL Server. In questo passaggio, assegnare autorizzazioni per consentire queste attività.

In questo esempio si presuppone che un account di accesso SQL (DDUser01), ma se è stato creato un account di accesso di Windows, utilizzarla.

```sql
USE RevoDeepDive
GO

EXEC sp_addrolemember 'db_owner', 'DDUser01'
GRANT EXECUTE ANY EXTERNAL SCRIPT TO DDUser01
GO
```

## <a name="troubleshoot-connections"></a>Risolvere i problemi di connessioni

In questa sezione sono elencati alcuni problemi comuni che possono verificarsi durante l'impostazione del database.

- **Come è possibile verificare la connettività del database e controllare le query SQL?**
  
    È possibile che, prima di eseguire il codice R tramite il server, si voglia controllare che il database sia raggiungibile dall'ambiente di sviluppo R. Entrambi [Esplora Server di Visual Studio](https://docs.microsoft.com/previous-versions/x603htbk(v=vs.140)) e [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md) sono strumenti gratuiti con connettività di database e funzionalità di gestione molto efficienti.
  
    Se non si vogliono installare altri strumenti di gestione del database, è possibile creare una connessione di test per l'istanza di SQL Server usando l' [Amministrazione origine dati ODBC](https://docs.microsoft.com/sql/odbc/admin/odbc-data-source-administrator?view=sql-server-2017) in Pannello di controllo. Se il database è configurato correttamente e il nome utente e la password specificati sono corretti, sarà possibile visualizzare il database appena creato e selezionarlo come database predefinito.
  
    Cause comuni degli errori di connessione includono remota connessioni non sono abilitate per il server e il protocollo Named Pipes non è abilitato. In questo articolo, è possibile trovare altri suggerimenti sulla risoluzione dei problemi: [Risolvere i problemi di connessione al motore di Database di SQL Server](https://docs.microsoft.com/sql/database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine).
  
- **Il nome della tabella datareader è preceduto dal prefisso it. Perché?**
  
    Quando si specifica lo schema predefinito per questo utente come **db_datareader**, tutte le tabelle e altri nuovi oggetti creati da questo utente hanno come prefisso il *schema* nome. Uno schema è una sorta di cartella. Può essere aggiunto a un database per organizzare gli oggetti. Lo schema definisce anche i privilegi dell'utente all'interno del database.
  
    Quando lo schema è associato un nome utente specifico, l'utente è il _proprietario dello schema_. Ogni volta che si crea un oggetto, l'oggetto sarà sempre creato in base al proprio schema, a meno che non si chieda specificatamente di crearlo in un altro schema.
  
    Ad esempio, se si crea una tabella con il nome **TestData**, e lo schema predefinito è **db_datareader**, la tabella viene creata con il nome `<database_name>.db_datareader.TestData`.
  
    Per questo motivo, un database può contenere più tabelle con lo stesso nome, purché le tabelle appartengano a schemi diversi.
   
    Se si sta cercando una tabella e non si specifica uno schema, il server di database cercherà uno schema che si è proprietari. Non è pertanto necessario specificare il nome dello schema quando si accede a tabelle di uno schema associato al proprio account di accesso.
  
- **Non ho privilegi DLL. Posso comunque seguire l'esercitazione**?
  
    Sì, ma si deve chiedere a un utente di pre-caricare i dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabelle e andare direttamente alla lezione successiva. Le funzioni che richiedono privilegi DDL sono indicate nell'esercitazione laddove possibile.

    Inoltre, chiedere all'amministratore di concedere l'autorizzazione EXECUTE ANY EXTERNAL SCRIPT. È necessario per l'esecuzione di script R, se è remoto oppure usando `sp_execute_external_script`.

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Creare oggetti dati di SQL Server usando RxSqlServerData](../../advanced-analytics/tutorials/deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)