---
title: Connessione al database SQL di Azure (MySQLToSQL) | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68103188"
---
# <a name="connecting-to-azure-sql-db-mysqltosql"></a>Connessione al database SQL di Azure (MySQLToSQL)
Per eseguire la migrazione dei database MySQL in SQL Azure, è necessario connettersi all'istanza di destinazione di SQL Azure. Quando si esegue la connessione, SSMA ottiene i metadati relativi a tutti i database nell'istanza di SQL Azure e Visualizza i metadati del database in Esplora metadati SQL Azure. SSMA archivia le informazioni dell'istanza di SQL Azure si è connessi a, ma non archivia le password.  
  
La connessione a SQL Azure rimane attiva fino a quando non si chiude il progetto. Quando si riapre il progetto, è necessario riconnettersi a SQL Azure se si desidera una connessione attiva al server. È possibile lavorare offline fino a quando non si caricano oggetti di database in SQL Azure e si migrano i dati.  
  
I metadati relativi all'istanza di SQL Azure non vengono sincronizzati automaticamente. Per aggiornare i metadati in SQL Azure Metadata Explorer, è invece necessario aggiornare manualmente i metadati del SQL Azure. Per ulteriori informazioni, vedere la sezione "sincronizzazione dei metadati di SQL Azure" più avanti in questo argomento.  
  
## <a name="required-sql-azure-permissions"></a>Autorizzazioni SQL Azure richieste  
L'account utilizzato per connettersi a SQL Azure richiede autorizzazioni diverse a seconda delle azioni eseguite dall'account:  
  
-   Per convertire gli oggetti MySQL [!INCLUDE[tsql](../../includes/tsql-md.md)] in sintassi, per aggiornare i metadati da SQL Azure o per salvare la sintassi convertita in script, l'account deve disporre dell'autorizzazione per accedere all'istanza di SQL Azure.  
  
-   Per caricare gli oggetti di database in SQL Azure, il requisito di autorizzazione minimo è l'appartenenza al ruolo del database **db_owner** nel database di destinazione.  
  
## <a name="establishing-a-sql-azure-connection"></a>Creazione di una connessione SQL Azure  
Prima di convertire gli oggetti di database MySQL in SQL Azure sintassi, è necessario stabilire una connessione all'istanza di SQL Azure in cui si vuole eseguire la migrazione del database o dei database MySQL.  
  
Quando si definiscono le proprietà di connessione, è inoltre necessario specificare il database in cui verrà eseguita la migrazione degli oggetti e dei dati. È possibile personalizzare questo mapping a livello di schema MySQL dopo la connessione a SQL Azure. Per altre informazioni, vedere [mapping di database MySQL a schemi SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
> [!IMPORTANT]  
> Prima di provare a connettersi a SQL Azure, assicurarsi che l'istanza di SQL Azure sia in esecuzione e che sia in grado di accettare le connessioni.  
  
**Per connettersi a SQL Azure**  
  
1.  Scegliere **Connetti a SQL Azure** dal menu **file** . questa opzione è abilitata dopo la creazione di un progetto.  
  
    Se in precedenza si è connessi a SQL Azure, il nome del comando verrà **riconnesso SQL Azure**.  
  
2.  Nella finestra di dialogo connessione immettere o selezionare il nome del server SQL Azure.  
  
3.  Immettere, selezionare o **esplorare** il nome del database.  
  
4.  Immettere o selezionare **username**.  
  
5.  Immettere la **password**.  
  
6.  SSMA consiglia la connessione crittografata a SQL Azure.  
  
7.  Fare clic su **Connetti**.  
  
> [!IMPORTANT]  
> SSMA per MySQL non supporta la connessione al database **Master** in SQL Azure.  
  
## <a name="synchronizing-sql-azure-metadata"></a>Sincronizzazione di metadati di SQL Azure  
I metadati relativi ai database SQL Azure non vengono aggiornati automaticamente. I metadati in SQL Azure Esplora metadati sono uno snapshot dei metadati quando si è connessi per la prima volta a SQL Azure o all'ultima volta che sono stati aggiornati manualmente i metadati. È possibile aggiornare manualmente i metadati per tutti i database o per qualsiasi singolo database o oggetto di database.  
  
**Per sincronizzare i metadati**  
  
1.  Assicurarsi di essere connessi a SQL Azure.  
  
2.  In SQL Azure Esplora metadati, selezionare la casella di controllo accanto allo schema del database o del database che si desidera aggiornare.  
  
    Ad esempio, per aggiornare i metadati per tutti i database, selezionare la casella accanto a database.  
  
3.  Fare clic con il pulsante destro del mouse su database o sul database singolo o sullo schema del database, quindi scegliere **Sincronizza con database**.  
  
## <a name="next-step"></a>passaggio successivo  
Il passaggio successivo della migrazione dipende dalle esigenze del progetto:  
  
-   Per personalizzare il mapping tra gli schemi di MySQL e SQL Azure database e schemi, vedere [mapping di database MySQL a SQL Server schemi &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
-   Per personalizzare le opzioni di configurazione per i progetti, vedere [impostazione delle opzioni del progetto &#40;MySQLToSQL&#41;](../../ssma/mysql/setting-project-options-mysqltosql.md)  
  
-   Per personalizzare il mapping dei tipi di dati di origine e di destinazione, vedere [mapping di tipi di dati MySQL e SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
-   Se non è necessario eseguire alcuna di queste attività, è possibile convertire le definizioni degli oggetti di database MySQL in SQL Azure definizioni degli oggetti. Per altre informazioni, vedere [conversione di database MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>Vedere anche  
[Migrazione di database MySQL a SQL Server-database SQL di Azure &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
