---
title: Eseguire la migrazione di dati di Sybase ASE in SQL Server - database SQL di Azure | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Migrating data,Client Side Data Migration
- Migrating data,Server Side Data Migration
ms.assetid: 54a39f5e-9250-4387-a3ae-eae47c799811
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 28a07c08fd801a9d5fdcdde4206f7aa6fe7b926f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68028841"
---
# <a name="migrating-sybase-ase-data-into-sql-server---azure-sql-db--sybasetosql"></a>Migrazione dei dati di Sybase ASE in SQL Server - Azure SQL database (SybaseToSQL)
Dopo che sono stati caricati correttamente gli oggetti di database di Sybase Adaptive Server Enterprise (ASE) in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o il database SQL di Azure, è possibile migrare i dati dall'ambiente del servizio app [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o database SQL di Azure.  
  
> [!IMPORTANT]  
> Se il motore in uso è modulo di migrazione dei dati lato Server, quindi prima della migrazione dei dati, è necessario installare SSMA per Sybase ASE Extension Pack e i provider di Sybase ASE in computer in cui è in esecuzione SSMA. Il servizio SQL Server Agent deve inoltre essere in esecuzione. Per altre informazioni su come installare il pacchetto di estensione, vedere [installazione dei componenti SSMA in SQL Server (SybaseToSQL)](https://msdn.microsoft.com/5ad9e12c-2cdb-4dd2-8703-05a23242d19d)  
  
## <a name="setting-migration-options"></a>Impostazione delle opzioni di migrazione  
Prima della migrazione dei dati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL DB, esaminare le opzioni di migrazione del progetto nella **impostazioni di progetto** nella finestra di dialogo.  
  
-   Tramite questa finestra di dialogo è possibile impostare opzioni quali dimensioni di batch di migrazione, il blocco di tabella, verifica dei vincoli, la gestione dei valori null e la gestione dei valori identity. Per altre informazioni sulle impostazioni di migrazione del progetto, vedere [impostazioni progetto (migrazione) (Sybase)](https://msdn.microsoft.com/82f8857f-7ab1-4738-ab6e-b1e95ea94924).  
  
    Per ulteriori informazioni sul **esteso le impostazioni di migrazione dati**, vedere [le impostazioni di migrazione dati](data-migration-settings-sybasetosql.md)  
  
-   Il **modulo di migrazione** nel **le impostazioni del progetto** consente all'utente di eseguire il processo di migrazione usando una visualizzazione dei due tipi di motori di migrazione dei dati, finestra di dialogo.:  
  
    1.  Modulo di migrazione dei dati lato client  
  
    2.  Modulo di migrazione dei dati lato server  
  
**Migrazione dei dati lato client:**  
  
-   Per avviare la migrazione dei dati sul lato client, selezionare l'opzione **modulo di migrazione dei dati lato Client** nel **le impostazioni del progetto** nella finestra di dialogo.  
  
-   Nelle **impostazioni del progetto**, il **modulo di migrazione dei dati lato Client** opzione è impostata per impostazione predefinita.  
  
    > [!NOTE]  
    > Il modulo di migrazione dei dati lato Client si trova all'interno dell'applicazione di SSMA e, pertanto, non dipende dalla disponibilità del pacchetto di estensioni.  
  
**Migrazione dei dati lato server:**  
  
-   Durante la migrazione dei dati lato Server, il motore si trova nel database di destinazione. Viene installato tramite il pacchetto di estensione. Per altre informazioni su come installare il pacchetto di estensione, vedere [installazione dei componenti SSMA in SQL Server (SybaseToSQL)](https://msdn.microsoft.com/5ad9e12c-2cdb-4dd2-8703-05a23242d19d)  
  
-   Per avviare la migrazione sul lato server, selezionare la **modulo di migrazione dei dati lato Server** opzione il **le impostazioni del progetto** finestra di dialogo.  
  
> [!NOTE]  
> Quando si usa database SQL di Azure come database di destinazione, solo **migrazione dei dati lato Client** è consentito e migrazione dei dati lato server non è supportata.  
  
## <a name="migrating-data-to-sql-server-or-azure-sql-db"></a>La migrazione dei dati in SQL Server o database SQL di Azure  
Eseguire la migrazione dei dati sono un'operazione di caricamento bulk che sposta le righe di dati dalle tabelle di ambiente del servizio App in tabelle di SQL Server nelle transazioni. Il numero di righe caricate in SQL Server o database SQL di Azure in ogni transazione viene configurato nelle impostazioni del progetto.  
  
Per visualizzare i messaggi di migrazione, verificare che sia visibile il riquadro di Output. In caso contrario, selezionare **Output** dalle **visualizzazione** menu.  
  
**Per eseguire la migrazione dei dati**  
  
1.  Verificare quanto segue:  
  
    -   I provider di ambiente del servizio App installati nel computer in cui è in esecuzione SSMA.  
  
    -   Gli oggetti convertiti sincronizzati con il database di destinazione (SQL Server o database SQL di Azure).  
  
2.  Nel Visualizzatore metadati Sybase, selezionare gli oggetti che contengono i dati che si desidera eseguire la migrazione:  
  
    -   Per eseguire la migrazione dei dati per tutti gli schemi, selezionare la casella di controllo accanto a **schemi**.  
  
    -   Per eseguire la migrazione dei dati o omettere le singole tabelle, prima di tutto lo schema di espandere, espandere **tabelle**e quindi selezionare o deselezionare la casella di controllo accanto alla tabella.  
  
3.  Per eseguire la migrazione dei dati, si verificano due casi:  
  
    **Migrazione dei dati lato client:**  
  
    Per l'esecuzione **migrazione dei dati lato Client**, selezionare il **modulo di migrazione dei dati lato Client** opzione il **impostazioni di progetto** nella finestra di dialogo.  
  
    **Migrazione dei dati lato server:**  
  
    -   Prima di eseguire la migrazione di dati lato Server, assicurarsi che:  
  
        1.  SSMA per Sybase Extension Pack viene installato nell'istanza di SQL Server.  
  
        2.  Il servizio SQL Server Agent è in esecuzione nell'istanza di SQL Server  
  
    -   Per l'esecuzione **migrazione dei dati lato Server**, selezionare il **modulo di migrazione dei dati lato Server** opzione il **impostazioni di progetto** nella finestra di dialogo.  
  
4.  Fare doppio clic su **schemi** nel Visualizzatore metadati Sybase e quindi fare clic su **Migrate Data**. È anche possibile eseguire la migrazione dei dati per oggetti singoli o categorie di oggetti: L'oggetto o relativa cartella padre e scegliere il **Migrate Data** opzione.  
  
    > [!NOTE]  
    > Se SSMA per Sybase Extension Pack non è installato nell'istanza di SQL Server e se **modulo di migrazione dei dati lato Server** è selezionata, durante la migrazione dei dati al database di destinazione, viene rilevato l'errore seguente: ' Impossibile trovare componenti di migrazione dei dati di SSMA in SQL Server, la migrazione dei dati lato server non sarà possibile. Verificare se il pacchetto di estensione sia installato correttamente '. Fare clic su **annullare** per terminare la migrazione dei dati.  
  
5.  Nel **connettersi a Sybase ASE** della finestra di dialogo immettere le credenziali di connessione e quindi fare clic su **Connect**. Per altre informazioni sulla connessione a Sybase ASE, vedere [connettersi a Sybase &#40;SybaseToSQL&#41;](../../ssma/sybase/connect-to-sybase-sybasetosql.md)  
  
    Se il database di destinazione è SQL Server, quindi, immettere le credenziali di connessione nel **Connetti al Server SQL** finestra di dialogo e fare clic su **Connect**. Per altre informazioni sulla connessione a SQL Server, vedere [la connessione a SQL Server(SybaseToSQL)](https://msdn.microsoft.com/dd368a1a-45b0-40e9-b4d3-5cdb48c26606)  
  
    Se il database di destinazione è il database SQL di Azure, quindi immettere le credenziali di connessione nel **Connetti al database SQL di Azure** finestra di dialogo e fare clic su **Connect**. Per altre informazioni sulla connessione al database SQL di Azure, vedere [la connessione al database SQL di Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md)  
  
    Messaggio verrà visualizzato il **Output** riquadro. Quando la migrazione è completata, il **Report di migrazione dati** viene visualizzata. Se tutti i dati non è stata eseguita la migrazione, fare clic sulla riga che contiene gli errori e quindi fare clic su **dettagli**. Quando si è terminato con il report, fare clic su **Chiudi**. Per altre informazioni sul Report di migrazione dei dati, vedere [Report di migrazione dati (SSMA comuni)](https://msdn.microsoft.com/bbfb9d88-5a98-4980-8d19-c5d78bd0d241)  
  
> [!NOTE]  
> Quando SQL Express edition viene utilizzato come database di destinazione, è consentita solo migrazione di dati lato client e migrazione dei dati lato server non è supportata.  
  
## <a name="see-also"></a>Vedere anche  
[Migrazione dei database di Sybase ASE a SQL Server - Azure SQL database &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
