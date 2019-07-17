---
title: La connessione al database SQL di Azure (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Connecting to SQL Azure, SQL Azure permissions
- Connecting to SQL Azure, synchronization
ms.assetid: d0b6f16a-1880-459d-a0c7-28b7ef15c56a
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 7fb6740681c08cb915755b3362352f139e078c4c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68103188"
---
# <a name="connecting-to-azure-sql-db-mysqltosql"></a>Connessione al database SQL di Azure (MySQLToSQL)
Per eseguire la migrazione di database MySQL a SQL Azure, è necessario connettersi all'istanza di destinazione di SQL Azure. Quando ci si connette, SSMA Ottiene i metadati relativi a tutti i database nell'istanza di SQL Azure e visualizza i metadati del database in Esplora i metadati di SQL Azure. SSMA archivia le informazioni dell'istanza di SQL Azure si è connessi a, ma non archiviano le password.  
  
La connessione a SQL Azure rimane attiva fino a quando non si chiude il progetto. Quando si riapre il progetto, è necessario riconnettersi a SQL Azure se si desidera che una connessione attiva al server. È possibile lavorare offline fino a quando non al caricamento di oggetti di database in SQL Azure e la migrazione dei dati.  
  
I metadati sull'istanza di SQL Azure non viene sincronizzato automaticamente. In alternativa, per aggiornare i metadati nel Visualizzatore metadati di SQL Azure, è necessario aggiornare manualmente i metadati di SQL Azure. Per altre informazioni, vedere la sezione "La sincronizzazione dei metadati di SQL Azure" più avanti in questo argomento.  
  
## <a name="required-sql-azure-permissions"></a>SQL Azure necessarie le autorizzazioni  
L'account utilizzato per connettersi a SQL Azure richiede autorizzazioni diverse a seconda di operazioni eseguite con l'account:  
  
-   Per convertire gli oggetti di MySQL per [!INCLUDE[tsql](../../includes/tsql-md.md)] sintassi, per aggiornare i metadati da SQL Azure o per convertire la sintassi per salvare gli script, l'account deve disporre dell'autorizzazione per accedere all'istanza di SQL Azure.  
  
-   Per caricare gli oggetti di database in SQL Azure, il requisito di autorizzazione minima necessaria è l'appartenenza di **db_owner** ruolo del database nel database di destinazione.  
  
## <a name="establishing-a-sql-azure-connection"></a>Tentativo di stabilire una SQL Azure connessione  
Prima di convertire gli oggetti di database MySQL in sintassi SQL Azure, è necessario stabilire una connessione all'istanza di SQL Azure in cui si desidera migrare i database MySQL.  
  
Quando si definiscono le proprietà di connessione, è inoltre possibile specificare il database in cui verranno migrati dati e oggetti. Dopo la connessione a SQL Azure, è possibile personalizzare il mapping al livello dello schema di MySQL. Per altre informazioni, vedere [Mapping di database MySQL a schemi SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
> [!IMPORTANT]  
> Prima di provare a connettersi a SQL Azure, assicurarsi che l'istanza di SQL Azure è in esecuzione e può accettare connessioni.  
  
**Per connettersi a SQL Azure**  
  
1.  Nel **File** dal menu **Connetti a SQL Azure** (dopo la creazione di un progetto, questa opzione è abilitata).  
  
    Se si è già connessa a SQL Azure, il nome del comando sarà **Riconnetti a SQL Azure**.  
  
2.  Nella finestra di dialogo di connessione, immettere o selezionare il nome del server di SQL Azure.  
  
3.  Inserire, selezionare o **esplorare** il nome del Database.  
  
4.  Immettere o selezionare **UserName**.  
  
5.  Immettere il **Password**.  
  
6.  SSMA consiglia connessione crittografata a SQL Azure.  
  
7.  Fare clic su **Connetti**.  
  
> [!IMPORTANT]  
> SSMA per MySQL supporta la connessione al **master** database in SQL Azure.  
  
## <a name="synchronizing-sql-azure-metadata"></a>La sincronizzazione di SQL Azure i metadati  
I metadati relativi a database di SQL Azure non viene aggiornato automaticamente. I metadati nel Visualizzatore metadati di SQL Azure sono uno snapshot dei metadati quando si è connessa a SQL Azure o l'ultima volta che si manualmente i metadati aggiornati. È possibile aggiornare manualmente i metadati per tutti i database o per qualsiasi database singolo o un oggetto di database.  
  
**Per sincronizzare i metadati**  
  
1.  Assicurarsi di essere connessi a SQL Azure.  
  
2.  Nel Visualizzatore metadati di SQL Azure, selezionare la casella di controllo accanto al database o schema di database che si desidera aggiornare.  
  
    Ad esempio, per aggiornare i metadati per tutti i database, selezionare la casella accanto al database.  
  
3.  I database, o i singoli database o lo schema del database e quindi scegliere **Sincronizza con Database**.  
  
## <a name="next-step"></a>Passaggio successivo  
Il passaggio successivo nel processo di migrazione dipende dalle esigenze del progetto:  
  
-   Per personalizzare il mapping tra gli schemi di MySQL e database SQL Azure e schemi, vedere [i database MySQL di Mapping a schemi SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
-   Per personalizzare le opzioni di configurazione per i progetti, vedere [impostazione delle opzioni progetto &#40;MySQLToSQL&#41;](../../ssma/mysql/setting-project-options-mysqltosql.md)  
  
-   Per personalizzare il mapping dei tipi di dati di origine e di destinazione, vedere [Mapping di MySQL e SQL Server Data Types &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
-   Se non è necessario eseguire nessuna di queste attività, è possibile convertire le definizioni degli oggetti di database MySQL in definizioni di oggetti di SQL Azure. Per altre informazioni, vedere [conversione di database MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>Vedere anche  
[Database di migrazione da MySQL a SQL Server - Azure SQL database &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
