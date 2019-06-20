---
title: La migrazione dei dati di MySQL in SQL Server - Azure SQL database (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Data Migration, server side data migration
- Data Migration,client side data migration
ms.assetid: a6a7f4d6-68aa-4a38-93bf-53eba0d7dc82
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 1e5c4c996a7dea9da3eccb24da2b6021a13d2590
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63312004"
---
# <a name="migrating-mysql-data-into-sql-server---azure-sql-db-mysqltosql"></a>La migrazione dei dati di MySQL in SQL Server - Azure SQL database (MySQLToSQL)
Dopo aver sincronizzato gli oggetti convertiti con correttamente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, è possibile migrare i dati da MySQL a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure.  
  
> [!IMPORTANT]  
> Se il motore in uso è modulo di migrazione dei dati lato Server, quindi, prima della migrazione dei dati, è necessario installare SSMA per MySQL Extension Pack e i provider di MySQL nel computer che esegue SSMA. Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servizio dell'agente deve anche essere in esecuzione. Per altre informazioni su come installare il pacchetto di estensione, vedere [installazione dei componenti SSMA in SQL Server (MySQL a SQL)](https://msdn.microsoft.com/6772d0c5-258f-4d7b-afb0-b5f810e71af1)  
  
## <a name="setting-migration-options"></a>Impostazione delle opzioni di migrazione  
Prima della migrazione dei dati per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, esaminare le opzioni di migrazione del progetto nella **le impostazioni del progetto** nella finestra di dialogo.  
  
-   Tramite questa finestra di dialogo è possibile impostare opzioni quali dimensioni di batch di migrazione, il blocco di tabella, verifica dei vincoli, la gestione dei valori null e gestione dei valori identity. Per altre informazioni sulle impostazioni di migrazione del progetto, vedere [impostazioni progetto (migrazione)](https://msdn.microsoft.com/2a3cba9e-cd54-4a8b-b858-8fc4cf2580d9).  
  
    Per ulteriori informazioni sul **esteso le impostazioni di migrazione dati**, vedere [le impostazioni di migrazione dati](data-migration-settings-mysqltosql.md)  
  
-   Il **modulo di migrazione** nel **le impostazioni del progetto** della finestra di dialogo consente all'utente di eseguire il processo di migrazione utilizzando due tipi di motori di migrazione dei dati:  
  
    1.  Modulo di migrazione dei dati lato client  
  
    2.  Modulo di migrazione dei dati lato server  
  
**Migrazione dei dati lato client:**  
  
-   Per avviare la migrazione dei dati sul lato client, selezionare la **modulo di migrazione dei dati lato Client** opzione il **le impostazioni del progetto** nella finestra di dialogo.  
  
-   Nelle **impostazioni del progetto**, il **modulo di migrazione dei dati lato Client** opzione è impostata.  
  
    > [!NOTE]  
    > Il **modulo di migrazione dei dati lato Client** si trova all'interno dell'applicazione SSMA e, pertanto, non dipende dalla disponibilità del pacchetto di estensioni.  
  
**Migrazione dei dati lato server:**  
  
-   Durante la migrazione dei dati lato Server, il motore si trova nel database di destinazione. Viene installato tramite il pacchetto di estensione. Per altre informazioni su come installare il pacchetto di estensione, vedere [installazione dei componenti SSMA in SQL Server (MySQL a SQL)](https://msdn.microsoft.com/6772d0c5-258f-4d7b-afb0-b5f810e71af1)  
  
-   Per avviare la migrazione sul lato server, selezionare la **modulo di migrazione dei dati lato Server** opzione il **le impostazioni del progetto** nella finestra di dialogo.  
  
> [!IMPORTANT]  
> **Migrazione dei dati lato client** opzione è solo disponibile per SQL Azure.  
  
## <a name="migrating-data-to-sql-server-or-sql-azure"></a>La migrazione dei dati in SQL Server o SQL Azure  
Eseguire la migrazione dei dati sono un'operazione di caricamento bulk che sposta le righe di dati dalle tabelle di MySQL in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o tabelle di SQL Azure nelle transazioni. Numero di righe caricate in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in ogni transazione viene configurata nelle impostazioni del progetto.  
  
Per visualizzare i messaggi di migrazione, verificare che sia visibile il riquadro di Output. In caso contrario, dal **View** dal menu **Output**.  
  
**Per eseguire la migrazione dei dati**  
  
1.  Verificare gli elementi seguenti:  
  
    -   I provider di MySQL sono installati nel computer che esegue SSMA.  
  
    -   Gli oggetti convertiti sincronizzati con il database di destinazione (SQL Server / SQL Azure).  
  
2.  Nel Visualizzatore metadati di MySQL, selezionare gli oggetti che contengono i dati che si desidera eseguire la migrazione:  
  
    -   Per eseguire la migrazione dei dati per tutti gli schemi, selezionare la casella di controllo accanto a **schemi**.  
  
    -   Per eseguire la migrazione dei dati o omettere le singole tabelle, prima di tutto lo schema di espandere, espandere **tabelle**e quindi selezionare o deselezionare la casella di controllo accanto alla tabella.  
  
3.  Per eseguire la migrazione dei dati, si verificano due casi:  
  
    **Migrazione dei dati lato client:**  
  
    -   Per l'esecuzione **migrazione dei dati lato Client**, selezionare il **modulo di migrazione dei dati lato Client** opzione il **impostazioni di progetto** nella finestra di dialogo.  
  
    **Migrazione dei dati lato server:**  
  
    -   Prima di eseguire la migrazione dei dati sul lato server, assicurarsi che:  
  
        1.  SSMA per MySQL Extension Pack viene installato nell'istanza di SQL Server.  
  
        2.  Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servizio dell'agente è in esecuzione nell'istanza di SQL Server  
  
    -   Per l'esecuzione **migrazione dei dati lato Server**, selezionare il **modulo di migrazione dei dati lato Server** opzione il **impostazioni di progetto** nella finestra di dialogo.  
  
4.  Fare doppio clic su **schemi** nel Visualizzatore metadati MySQL e quindi fare clic su **Migrate Data**. È anche possibile eseguire la migrazione dei dati per oggetti singoli o categorie di oggetti: Fare doppio clic dell'oggetto o la cartella padre. Selezionare il **Migrate Data** opzione.  
  
    > [!NOTE]  
    > Se SSMA per MySQL Extension Pack non è installato nell'istanza di SQL Server e se **modulo di migrazione dei dati lato Server** è selezionata, durante la migrazione dei dati al database di destinazione, viene rilevato l'errore seguente: ' Impossibile trovare componenti di migrazione dei dati di SSMA in SQL Server, la migrazione dei dati lato server non sarà possibile. Verificare se il pacchetto di estensione sia installato correttamente '. Fare clic su **annullare** per terminare la migrazione dei dati.  
  
5.  Nel **connettersi a MySQL** della finestra di dialogo immettere le credenziali di connessione e quindi fare clic su **Connect**. Per altre informazioni sulla connessione a MySQL, vedere [connettersi a MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connect-to-mysql-mysqltosql.md)  
  
    Se il database di destinazione è SQL Server, quindi, immettere le credenziali di connessione nel **Connetti al Server SQL** finestra di dialogo e fare clic su **Connect**. Per altre informazioni sulla connessione a SQL Server, vedere [Connetti a SQL Server](https://msdn.microsoft.com/bb8c4bde-cfc2-4636-92ae-5dd24abe9536)  
  
    Se il database di destinazione è SQL Azure, quindi immettere le credenziali di connessione nel **Connetti a SQL Azure** finestra di dialogo e fare clic su **Connect**. Per altre informazioni sulla connessione a SQL Azure, vedere [Connetti al database SQL di Azure &#40;MySQLToSQL&#41;](../../ssma/mysql/connect-to-azure-sql-db-mysqltosql.md)  
  
    Messaggio verrà visualizzato il **Output** riquadro. Quando la migrazione è completata, il **Report di migrazione dati** viene visualizzata. Se tutti i dati non è stata eseguita la migrazione, fare clic sulla riga che contiene gli errori e quindi fare clic su **dettagli**. Quando si è terminato con il report, fare clic su **Chiudi**. Per altre informazioni sul Report di migrazione dei dati, vedere [Report di migrazione dati (SSMA comuni)](https://msdn.microsoft.com/bbfb9d88-5a98-4980-8d19-c5d78bd0d241)  
  
> [!NOTE]  
> Quando SQL Express edition viene utilizzato come database di destinazione, è consentita solo migrazione di dati lato client e migrazione dei dati lato server non è supportata.  
  
## <a name="see-also"></a>Vedere anche  
[Database di migrazione da MySQL a SQL Server - Azure SQL database &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
