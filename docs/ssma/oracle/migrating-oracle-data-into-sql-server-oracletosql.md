---
title: Migrazione di dati Oracle a SQL Server (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Oracle Data Migration, Client-Side Migration
- Oracle Data Migration,Server-Side Migration
ms.assetid: e23c5268-41ed-4e55-9fe7-a11376202a13
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: ad944432b2a00acb923732863624a69dcbaf227f
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52418292"
---
# <a name="migrating-oracle-data-into-sql-server-oracletosql"></a>Migrazione di dati Oracle a SQL Server (OracleToSQL)
Dopo aver sincronizzato gli oggetti convertiti con correttamente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è possibile migrare i dati da Oracle a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
> Se il motore in uso è modulo di migrazione dei dati lato Server, quindi, prima di migrare i dati, è necessario installare SSMA per Oracle Extension Pack e i provider Oracle nel computer che esegue SSMA. Il servizio SQL Server Agent deve inoltre essere in esecuzione. Per altre informazioni su come installare il pacchetto di estensione, vedere [installazione dei componenti Server (OracleToSQL)](https://msdn.microsoft.com/33070e5f-4e39-4b70-ae81-b8af6e4983c5)  
  
## <a name="setting-migration-options"></a>Impostazione delle opzioni di migrazione  
Prima della migrazione dei dati per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esaminare le opzioni di migrazione del progetto nella **impostazioni di progetto** nella finestra di dialogo.  
  
-   Tramite questa finestra di dialogo è possibile impostare opzioni quali dimensioni di batch di migrazione, il blocco di tabella, verifica dei vincoli, la gestione dei valori null e la gestione dei valori identity. Per altre informazioni sulle impostazioni di migrazione del progetto, vedere [impostazioni progetto (migrazione) (OracleToSQL)](https://msdn.microsoft.com/fcd6b988-633b-4b2b-9f36-6368b5e86b60).  
  
-   Il **modulo di migrazione** nel **le impostazioni del progetto** della finestra di dialogo consente all'utente di eseguire il processo di migrazione utilizzando due tipi di motori di migrazione dei dati:  
  
    1.  Modulo di migrazione dei dati lato client  
  
    2.  Modulo di migrazione dei dati lato server  
  
**Migrazione dei dati lato client:**  
  
-   Per avviare la migrazione dei dati sul lato client, selezionare la **modulo di migrazione dei dati lato Client** opzione il **le impostazioni del progetto** nella finestra di dialogo.  
  
-   Nelle **impostazioni del progetto**, il **modulo di migrazione dei dati lato Client** opzione è impostata.  
  
    > [!NOTE]  
    > Il **modulo di migrazione dei dati lato Client** si trova all'interno dell'applicazione SSMA e, pertanto, non dipende dalla disponibilità del pacchetto di estensioni.  
  
**Migrazione dei dati lato server:**  
  
-   Durante la migrazione dei dati lato Server, il motore si trova nel database di destinazione. Viene installato tramite il pacchetto di estensione. Per altre informazioni su come installare il pacchetto di estensione, vedere [installazione dei componenti Server in SQL Server](installing-ssma-components-on-sql-server-oracletosql.md)  
  
-   Per avviare la migrazione sul lato server, selezionare la **modulo di migrazione dei dati lato Server** opzione il **le impostazioni del progetto** nella finestra di dialogo.  
  
## <a name="migrating-data-to-sql-server"></a>La migrazione dei dati a SQL Server  
Eseguire la migrazione dei dati sono un'operazione di caricamento bulk che sposta le righe di dati dalle tabelle di Oracle in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabelle nelle transazioni. Numero di righe caricate in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in ogni transazione viene configurata nelle impostazioni del progetto.  
  
Per visualizzare i messaggi di migrazione, verificare che sia visibile il riquadro di Output. In caso contrario, dal **View** dal menu **Output**.  
  
**Per eseguire la migrazione dei dati**  
  
1.  Verificare gli elementi seguenti:  
  
    -   Il provider Oracle vengono installati nel computer che esegue SSMA.  
  
    -   Aver sincronizzato gli oggetti convertiti con la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database.  
  
2.  Nel Visualizzatore metadati Oracle, selezionare gli oggetti che contengono i dati che si desidera eseguire la migrazione:  
  
    -   Per eseguire la migrazione dei dati per tutti gli schemi, selezionare la casella di controllo accanto a **schemi**.  
  
    -   Per eseguire la migrazione dei dati o omettere le singole tabelle, prima di tutto lo schema di espandere, espandere **tabelle**e quindi selezionare o deselezionare la casella di controllo accanto alla tabella.  
  
3.  Per eseguire la migrazione dei dati, si verificano due casi:  
  
    **Migrazione dei dati lato client:**  
  
    -   Per l'esecuzione **migrazione dei dati lato Client**, selezionare il **modulo di migrazione dei dati lato Client** opzione il **impostazioni di progetto** nella finestra di dialogo.  
  
    **Migrazione dei dati lato server:**  
  
    -   Prima di eseguire la migrazione dei dati sul lato server, assicurarsi che:  
  
        1.  SSMA per Oracle Extension Pack viene installato nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
        2.  Il servizio SQL Server Agent è in esecuzione nell'istanza di SQL Server.  
  
    -   Per l'esecuzione **migrazione dei dati lato Server**, selezionare il **modulo di migrazione dei dati lato Server** opzione il **impostazioni di progetto** nella finestra di dialogo.  
  
4.  Fare doppio clic su **schemi** nel Visualizzatore metadati Oracle e quindi fare clic su **Migrate Data**. È anche possibile eseguire la migrazione dei dati per oggetti singoli o categorie di oggetti: Fare doppio clic dell'oggetto o la cartella padre. Selezionare il **Migrate Data** opzione.  
  
    > [!NOTE]  
    > Se SSMA per Oracle Extension Pack non è installato nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e se **modulo di migrazione dei dati lato Server** è selezionata, durante la migrazione dei dati al database di destinazione, viene rilevato l'errore seguente: ' Impossibile trovare componenti di migrazione dei dati di SSMA in SQL Server, la migrazione dei dati lato server non sarà possibile. Verificare se il pacchetto di estensione sia installato correttamente '. Fare clic su **annullare** per terminare la migrazione dei dati.  
  
5.  Nel **Connetti a Oracle** della finestra di dialogo immettere le credenziali di connessione e quindi fare clic su **Connect**. Per altre informazioni sulla connessione a Oracle, vedere [connettersi a Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/connect-to-oracle-oracletosql.md)  
  
    Per la connessione al database di destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], immettere le credenziali di connessione nel **Connetti al Server SQL** nella finestra di dialogo e fare clic su **Connect**. Per altre informazioni sulla connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Connetti a SQL Server](https://msdn.microsoft.com/bb8c4bde-cfc2-4636-92ae-5dd24abe9536)  
  
    Messaggio verrà visualizzato il **Output** riquadro. Quando la migrazione è completata, il **Report di migrazione dati** viene visualizzata. Se tutti i dati non è stata eseguita la migrazione, fare clic sulla riga che contiene gli errori e quindi fare clic su **dettagli**. Quando si è terminato con il report, fare clic su **Chiudi**. Per altre informazioni sul Report di migrazione dei dati, vedere [Report di migrazione dati (SSMA comuni)](https://msdn.microsoft.com/bbfb9d88-5a98-4980-8d19-c5d78bd0d241)  
  
> [!NOTE]  
> Quando SQL Express edition viene utilizzato come database di destinazione, è consentita solo migrazione di dati lato client e migrazione dei dati lato server non è supportata.  
  
## <a name="see-also"></a>Vedere anche  
[La migrazione da Oracle database in SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
