---
title: Usare SSMS per gestire SQL Server in Linux
description: ''
author: VanMSFT
ms.author: vanto
ms.date: 05/21/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: b2fcf858-21c3-462a-8d49-50c85647d092
ms.openlocfilehash: 753845d41c946d955b80a927901f827ee4643567
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68000097"
---
# <a name="use-sql-server-management-studio-on-windows-to-manage-sql-server-on-linux"></a>Usare SQL Server Management Studio in Windows per la gestione di SQL Server in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questo articolo introduce [SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md) e illustra in dettaglio un paio delle attività comuni. SQL Server Management Studio è un'applicazione Windows, utilizzare SQL Server Management Studio quando si dispone di un computer Windows che può connettersi a un'istanza remota di SQL Server in Linux.

> [!TIP]
> Se non si dispone di un computer Windows eseguire SSMS, prendere in considerazione le nuove [Studio di Azure Data](../azure-data-studio/index.md). Fornisce uno strumento grafico per la gestione di SQL Server e viene eseguito su Linux e Windows.

[SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md) fa parte di una suite di strumenti SQL che Microsoft offre gratuitamente per le esigenze di sviluppo e gestione. SSMS è un ambiente integrato per accedere, configurare, gestire, amministrare e sviluppare tutti i componenti di SQL Server. È possibile connettersi a SQL Server in esecuzione su qualsiasi piattaforma sia in locale, nei contenitori Docker e nel cloud. Consente inoltre di connettersi al Database SQL di Azure e Azure SQL Data Warehouse. SSMS integra un'ampia gamma di strumenti grafici con numerosi editor di script per fornire l'accesso a SQL Server per gli sviluppatori e amministratori di livello di competenza.

SSMS offre una vasta gamma di funzionalità di sviluppo e gestione per SQL Server, inclusi gli strumenti per:

- Configurare, monitorare e amministrare una o più istanze di SQL Server
- Distribuire, monitorare e aggiornare i componenti livello dati, ad esempio database e i data warehouse
- Backup e ripristino dei database
- Compilare ed eseguire gli script e query T-SQL e visualizzare i risultati
- Generare script T-SQL per oggetti di database
- Visualizzare e modificare dati nei database
- Progettazione visiva di query T-SQL e gli oggetti di database, ad esempio viste, tabelle e stored procedure

Visualizzare [che cos'è SSMS?](../ssms/sql-server-management-studio-ssms.md) per altre informazioni su SQL Server Management Studio.

## <a name="install-the-newest-version-of-sql-server-management-studio-ssms"></a>Installare la versione più recente di SQL Server Management Studio (SSMS)

Quando si lavora con SQL Server, è consigliabile usare sempre la versione più recente di SQL Server Management Studio (SSMS). La versione più recente di SSMS viene continuamente aggiornata e ottimizzata e attualmente funziona con SQL Server in Linux. Per scaricare e installare la versione più recente, vedere [scaricare SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md). Per mantenersi aggiornata, la versione più recente di SSMS chiede di quando è disponibile una nuova versione disponibile per il download.

> [!NOTE]
> Prima di usare SSMS per gestire Linux, vedere la [problemi noti](sql-server-linux-release-notes.md) per SQL Server Management Studio in Linux.

## <a name="connect-to-sql-server-on-linux"></a>Connettersi a SQL Server in Linux

Usare i seguenti passaggi di base per la connessione:

1. Avviare SSMS digitare **Microsoft SQL Server Management Studio** in Windows la casella di ricerca e quindi fare clic sull'app desktop.

    ![SQL Server Management Studio](./media/sql-server-linux-manage-ssms/ssms.png)

1. Nel **Connetti al Server** finestra, immettere le informazioni seguenti (se SSMS è già in esecuzione, fare clic su **Connetti > motore di Database** per aprire il **Connetti al Server** finestra):

   | Impostazione | Descrizione |
   |-----|-----|
   | **Tipo server** | Il valore predefinito è il motore di database; non modificare questo valore. |
   | **Nome server** | Immettere il nome del computer Linux di SQL Server di destinazione o il relativo indirizzo IP. |
   | **Autenticazione** | Per SQL Server in Linux, usare **autenticazione di SQL Server**. |
   | **Account di accesso** | Immettere il nome di un utente con accesso a un database nel server (ad esempio, il valore predefinito **SA** account creato durante l'installazione). |
   | **Password** | Immettere la password per l'utente specificato (per il **SA** account, si ha creato questo durante l'installazione). |

    ![SQL Server Management Studio: Connettersi al Database di SQL server](./media/sql-server-linux-manage-ssms/connect.png)

1. Fare clic su **Connetti**.

    > [!TIP]
    > Se si verifica un errore di connessione, provare a diagnosticare il problema dal messaggio di errore. Rivedere poi i [consigli per la risoluzione dei problemi di connessione](sql-server-linux-troubleshooting-guide.md#connection).
 
1. Dopo aver stabilito la connessione a SQL Server **Esplora oggetti** verrà aperto e sarà possibile accedere al database per eseguire attività amministrative o eseguire query sui dati.

## <a name="run-transact-sql-queries"></a>Eseguire query Transact-SQL

Dopo la connessione al server, è possibile connettersi a un database ed eseguire query Transact-SQL. Query Transact-SQL possono essere utilizzate per quasi tutte le attività del database.

1. Nelle **Esplora oggetti**, passare al database di destinazione nel server. Ad esempio, espandere **database di sistema** per lavorare con i **master** database.

1. Il database e quindi scegliere **nuova Query**.

1. Nella finestra di query, scrivere una query Transact-SQL per selezionare restituiscono i nomi di tutti i database nel server.

   ```sql
   SELECT [Name]
   FROM sys.Databases
   ```

   Se si ha familiarità con la scrittura di query, vedere [scrittura di istruzioni Transact-SQL](../t-sql/tutorial-writing-transact-sql-statements.md).

1. Scegliere il **Execute** pulsante per eseguire la query e visualizzare i risultati.

   ![Esito positivo. Connettersi al Database di SQL server: SQL Server Management Studio](./media/sql-server-linux-manage-ssms/execute-query.png)

Sebbene sia possibile eseguire quasi qualsiasi attività di gestione con le query Transact-SQL, SQL Server Management Studio è uno strumento grafico che rende più facile da gestire SQL Server. Le sezioni seguenti forniscono alcuni esempi di tramite l'interfaccia utente grafica.

## <a name="create-and-manage-databases"></a>Creare e gestire i database

Durante la connessione con il *master* database, è possibile creare i database nel server e modificare o eliminare database esistenti. I passaggi seguenti descrivono come eseguire diverse comuni attività di gestione di database tramite Management Studio. Per eseguire queste attività, assicurarsi che si è connessi al *master* database con l'account di accesso dell'entità a livello di server che è stato creato quando si configura SQL Server in Linux.

### <a name="create-a-new-database"></a>Creare un nuovo database

1. Avviare SSMS e connettersi al server in SQL Server in Linux

2. In Esplora oggetti fare clic sui *database* cartella e quindi fare clic su * Nuovo Database... "

3. Nel *Nuovo Database* finestra di dialogo immettere un nome per il nuovo database e quindi fare clic su *OK*

Il nuovo database è stato creato nel server. Se si preferisce creare un nuovo database usando T-SQL, vedere [CREATE DATABASE (SQL Server Transact-SQL)](../t-sql/statements/create-database-sql-server-transact-sql.md).

### <a name="drop-a-database"></a>Eliminare un database

1. Avviare SSMS e connettersi al server in SQL Server in Linux

2. In Esplora oggetti espandere il *database* cartella per visualizzare un elenco di tutti i database nel server.

3. In Esplora oggetti fare clic sul database di cui si desidera eliminare e quindi fare clic su *Delete*

4. Nel *Elimina oggetto* finestra di dialogo, check *Chiudi connessioni esistenti* e quindi fare clic su *OK*

Il database viene eliminato correttamente dal server. Se si preferisce eliminare un database usando T-SQL, vedere [DROP DATABASE (SQL Server Transact-SQL)](../t-sql/statements/drop-database-transact-sql.md).

## <a name="use-activity-monitor-to-see-information-about-sql-server-activity"></a>Utilizzare Monitoraggio attività per visualizzare informazioni sulle attività di SQL Server

Il [Monitoraggio attività](../relational-databases/performance-monitor/activity-monitor.md) strumento viene compilato in SQL Server Management Studio (SSMS) e visualizza le informazioni sui processi di SQL Server e come questi processi influiscono sull'istanza corrente di SQL Server.

1. Avviare SSMS e connettersi al server in SQL Server in Linux

1. In Esplora oggetti fare doppio clic il *server* nodo e quindi fare clic su *Monitoraggio attività*

Monitoraggio attività Mostra i riquadri espandibili e comprimibili, con le informazioni seguenti:

- Panoramica
- Processi
- Attese risorse
- I/o File di dati
- Query recenti con costo elevato
- Query attive con costo elevato

Quando un riquadro è espanso, Monitoraggio attività esegue una query di istanza per ottenere informazioni. Quando un riquadro è compresso, significa che tutte le relative attività di query sono arrestate. È possibile espandere uno o più riquadri contemporaneamente per visualizzare diversi tipi di attività nell'istanza.

## <a name="see-also"></a>Vedere anche
- [Che cos'è SSMS?](../ssms/sql-server-management-studio-ssms.md)
- [Esportare e importare un database con SSMS](sql-server-linux-migrate-ssms.md)
- [Esercitazione: SQL Server Management Studio](../ssms/tutorials/tutorial-sql-server-management-studio.md)
- [Esercitazione: Scrittura di istruzioni Transact-SQL](../t-sql/tutorial-writing-transact-sql-statements.md)
- [Monitoraggio delle prestazioni e dell'attività del server](../relational-databases/performance/server-performance-and-activity-monitoring.md)
