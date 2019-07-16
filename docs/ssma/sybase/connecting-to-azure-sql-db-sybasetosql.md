---
title: La connessione al database SQL di Azure (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9e77e4b0-40c0-455c-8431-ca5d43849aa7
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 2a322f7769db5b1f2ee0de4e4e35839d63ed43b8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67948567"
---
# <a name="connecting-to-azure-sql-db-sybasetosql"></a>Connessione al database SQL di Azure (SybaseToSQL)
Per eseguire la migrazione dei database Sybase a database SQL di Azure, è necessario connettersi all'istanza di destinazione di database SQL di Azure. Quando ci si connette, SSMA Ottiene i metadati relativi a tutti i database nell'istanza di database SQL di Azure e visualizza i metadati del database in Azure SQL DB metadati Explorer. SSMA archivia le informazioni dell'istanza di database SQL di Azure si è connessi a, ma non archiviano le password.  
  
La connessione al database SQL di Azure rimane attiva fino a quando non si chiude il progetto. Quando si riapre il progetto, è necessario riconnettersi al database SQL di Azure se si desidera che una connessione attiva al server. È possibile lavorare offline finché non si caricherà gli oggetti di database nel database SQL di Azure e la migrazione dei dati.  
  
I metadati sull'istanza di database SQL di Azure non viene sincronizzato automaticamente. In alternativa, per aggiornare i metadati nel Visualizzatore metadati di Azure SQL DB, è necessario aggiornare manualmente i metadati del database SQL di Azure. Per altre informazioni, vedere la sezione "La sincronizzazione di Azure SQL DB Metadata" più avanti in questo argomento.  
  
## <a name="required-azure-sql-db-permissions"></a>Autorizzazioni di database SQL di Azure necessarie  
L'account utilizzato per connettersi al database SQL di Azure richiede autorizzazioni diverse a seconda di operazioni eseguite con l'account:  
  
1.  Per convertire gli oggetti di Sybase a [!INCLUDE[tsql](../../includes/tsql-md.md)] sintassi, per aggiornare i metadati dal database SQL di Azure o per convertire la sintassi per salvare gli script, l'account deve disporre dell'autorizzazione per accedere all'istanza di database SQL di Azure.  
  
2.  Per caricare gli oggetti di database nel database SQL di Azure, il requisito di autorizzazione minima necessaria è l'appartenenza al **db_owner** ruolo del database nel database di destinazione.  
  
## <a name="establishing-a-azure-sql-db-connection"></a>Stabilire una connessione di database SQL di Azure  
Prima di convertire gli oggetti di database di Sybase alla sintassi del database SQL di Azure, è necessario stabilire una connessione all'istanza di database SQL di Azure in cui si desidera migrare i database di Sybase.  
  
Quando si definiscono le proprietà di connessione, è inoltre possibile specificare il database in cui verranno migrati dati e oggetti. È possibile personalizzare il mapping a livello di schema Sybase dopo la connessione al database SQL di Azure. Per altre informazioni, vedere [Mapping di schemi di ASE Sybase a schemi SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md)  
  
> [!WARNING]  
> Prima di provare a connettersi al database SQL di Azure, assicurarsi che l'istanza di database SQL di Azure è in esecuzione e può accettare connessioni.  
  
**Per connettersi al database SQL di Azure**  
  
1.  Nel **File** dal menu **Connetti al database SQL di Azure**(dopo la creazione di un progetto, questa opzione è abilitata).  
  
    Se è già connessi al database SQL di Azure, il nome del comando sarà **riconnessione al database SQL di Azure**  
  
2.  Nella finestra di dialogo di connessione, immettere o selezionare il nome del server di database SQL di Azure.  
  
3.  Inserire, selezionare o **esplorare** il nome del Database.  
  
4.  Immettere o selezionare **UserName**.  
  
5.  Immettere il **Password**.  
  
6.  SSMA consiglia connessione crittografata al database SQL di Azure.  
  
7.  Fare clic su **Connetti**.  
  
> [!IMPORTANT]  
> Non supporta la connessione a SSMA per Sybase **master** database nel database SQL di Azure.  
  
## <a name="synchronizing-azure-sql-db-metadata"></a>La sincronizzazione dei metadati di database SQL di Azure  
I metadati relativi a database SQL di Azure non viene aggiornato automaticamente. I metadati in Azure SQL DB metadati Explorer sono uno snapshot dei metadati quando si è connessi prima al database SQL di Azure o l'ultima volta che aggiornato manualmente i metadati. È possibile aggiornare manualmente i metadati per tutti i database o per qualsiasi database singolo o un oggetto di database.  
  
**Per sincronizzare i metadati**  
  
1.  Assicurarsi di essere connessi al database SQL di Azure.  
  
2.  Nel Visualizzatore metadati di database SQL di Azure, selezionare la casella di controllo accanto al database o schema di database che si desidera aggiornare.  
  
    Ad esempio, per aggiornare i metadati per tutti i database, selezionare la casella accanto al database.  
  
3.  I database, o i singoli database o lo schema del database e quindi scegliere **Sincronizza con Database**.  
  
## <a name="next-step"></a>Passaggio successivo  
Il passaggio successivo nel processo di migrazione dipende dalle esigenze del progetto:  
  
-   Per personalizzare il mapping tra gli schemi di Sybase e i database di database SQL di Azure e gli schemi, vedere [gli schemi di Mapping Sybase ASE a schemi SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md)  
  
-   Per personalizzare le opzioni di configurazione per i progetti, vedere [impostazione delle opzioni progetto &#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md)  
  
-   Per personalizzare il mapping dei tipi di dati di origine e di destinazione, vedere [Mapping di Sybase ASE e SQL Server Data Types &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md)  
  
-   Se non è necessario eseguire nessuna di queste attività, è possibile convertire le definizioni degli oggetti di database Sybase in definizioni di oggetti di database SQL di Azure. Per altre informazioni, vedere [convertire gli oggetti di Database di Sybase ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md)  
  
## <a name="see-also"></a>Vedere anche  
[Migrazione dei database di Sybase ASE a SQL Server - Azure SQL database &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
