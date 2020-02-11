---
title: Installazione dei componenti di SSMA in SQL Server (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 5ad9e12c-2cdb-4dd2-8703-05a23242d19d
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 1fbc3a8f74b21bd5a53bdd874b5c41ef522e29f6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68029015"
---
# <a name="installing-ssma-components-on-sql-server-sybasetosql"></a>Installazione di componenti SSMA in SQL Server (SybaseToSQL)
Oltre all'installazione di SSMA, per l'utilizzo della migrazione dei dati sul lato server, è necessario installare anche i componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]nel computer che esegue. Questi componenti includono il pacchetto di estensioni SSMA, che supporta la migrazione dei dati e i provider Sybase per abilitare la connettività da server a server.  
  
## <a name="ssma-for-sybase-extension-pack"></a>SSMA per Sybase Extension Pack  
Il pacchetto di estensione SSMA aggiunge i database **sysdb** e **ssmatesterdb_syb**all'istanza specificata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il database **sysdb** contiene le tabelle e le stored procedure necessarie per eseguire la migrazione dei dati. Il database **ssmatester_syb** contiene lo schema **ssma_sybase_utilities**, in cui vengono creati gli oggetti (tabelle, trigger, viste) usati dal componente SSMA tester.  
  
Inoltre, quando si esegue la migrazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]dei dati a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , SSMA crea processi di Agent quando viene utilizzato il motore di migrazione dei dati lato server per la migrazione dei dati.  
  
### <a name="installing-the-extension-pack"></a>Installazione del pacchetto di estensione  
È possibile installare il pacchetto di estensione in qualsiasi momento prima di eseguire [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]la migrazione dei dati a.  
  
> [!IMPORTANT]  
> Per installare il pacchetto di estensione, è necessario essere un membro del ruolo del server sysadmin nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
**Per installare il pacchetto di estensione**  
  
1.  Copiare SSMA per Sybase Extension Pack. *n*. Installare. exe, dove *n* è il numero di build, nel computer in cui è [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]in esecuzione.  
  
2.  Fare doppio clic su SSMA per Sybase Extension Pack. *n*. Installare. exe.  
  
3.  Nella pagina di benvenuto fare clic su **Avanti**.  
  
4.  Nella pagina Contratto di licenza con l'utente finale leggere il contratto di licenza. Se si accetta, selezionare la casella di controllo Accetto **i termini del contratto di licenza** , quindi fare clic su **Avanti**.  
  
5.  Nella pagina Selezione tipo di installazione fare clic su **tipico**.  
  
6.  Nella pagina pronto per l'installazione fare clic su **Installa**.  
  
7.  Nella pagina completamento del primo passaggio dell'installazione fare clic su **Avanti**.  
  
    Verrà visualizzata una nuova finestra di dialogo in cui è possibile selezionare l'istanza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di per l'installazione del pacchetto di estensione.  
  
8.  Selezionare l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui verrà eseguita la migrazione dei database dell'ambiente del servizio app e quindi fare clic su **Avanti**.  
  
    L'istanza predefinita ha lo stesso nome del computer. Le istanze denominate saranno seguite da una barra rovesciata e dal nome dell'istanza.  
  
9. Nella pagina parametri connessione selezionare il metodo di autenticazione e quindi fare clic su **Avanti**.  
  
    L'autenticazione di Windows utilizzerà le credenziali di Windows per tentare di accedere all'istanza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]di. Se si seleziona [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'autenticazione di, è necessario [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] immettere un nome di account di accesso e una password.  
  
10. Nella pagina Gestisci server selezionare **Installa database Utilities** *n*, dove *n* è il numero di versione, quindi fare clic su **Avanti**.  
  
    Viene creato il database **sysdb** e le stored procedure vengono create nel database.  
  
    Se è selezionata l'opzione **Installa database tester** , il tester **ssmatesterdb_syb** database verrà creato.  
  
11. Per installare le utilità in un'altra istanza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]di, selezionare **Torna a istanze**, quindi fare clic su **Avanti**. In alternativa, per uscire dalla procedura guidata, fare clic su **Esci**.  
  
### <a name="sql-server-database-objects"></a>Oggetti di database SQL Server  
Dopo aver installato il pacchetto di estensione, viene visualizzata una tabella **ssma_syb. bcp_migration_packages** nel database **sysdb** . Vengono inoltre visualizzate le stored procedure seguenti:  
  
-   **bcp_clean_migration_data**  
  
-   **bcp_ensure_message_table**  
  
-   **bcp_insert_new_message**  
  
-   **bcp_post_process**  
  
-   **bcp_read_new_migration_messages**  
  
-   **bcp_save_migration_package**  
  
-   **bcp_smart_truncate**  
  
-   **bcp_start_migration_process**  
  
-   **get_jobstep_info**  
  
-   **stop_agent_process**  
  
Ogni volta che si esegue la migrazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]dei dati in, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SSMA crea un processo di Agent. Questi processi sono denominati **ssma_syb pacchetto di migrazione dei dati {GUID}** e sono [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] visibili nel nodo [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] Agent di nella cartella Jobs.  
  
## <a name="sybase-providers"></a>Provider Sybase  
Quando si esegue la migrazione dei dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]dall'ambiente del servizio app a/SQL Azure, i dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]vengono migrati direttamente tra il servizio app e/SQL Azure. Non passa attraverso SSMA perché questo rallenta la migrazione dei dati.  
  
### <a name="installing-the-sybase-providers"></a>Installazione dei provider Sybase  
Le istruzioni seguenti forniscono i passaggi di installazione di base per l'installazione dei provider Sybase. Le istruzioni esatte variano a seconda della versione del programma di installazione di Sybase.  
  
> [!IMPORTANT]  
> Prima di eseguire il programma di installazione, verificare di non violare i contratti di licenza.  
  
1.  Eseguire il programma di installazione di Sybase ASE.  
  
2.  Selezionare installazione personalizzata.  
  
3.  Nella pagina Selezione funzionalità selezionare i provider di dati ODBC, OLE DB e ADO.NET.  
  
4.  Verificare le funzionalità selezionate, quindi fare clic su **fine** per installare il provider di dati.  
  
## <a name="see-also"></a>Vedere anche  
[Installazione di SSMA per Sybase client &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)  
[Migrazione dei database Sybase ASE a SQL Server-database SQL di Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
