---
title: Connessione al database SQL di Azure (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- instance of SQL Azure
- metadata, refreshing
- refreshing metadata
- SQL Azure
- SQL Azure, connecting
- SQL Azure, connecting to
- SQL Azure, reconnecting
- SQL Azure, synchronizing metadata
ms.assetid: 1ba0d113-dc05-4431-8689-e14a8821bafd
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 6c35168f1c77f0574b202b77da515dab497a3ec7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68006662"
---
# <a name="connecting-to-azure-sql-db-accesstosql"></a>Connessione al database SQL di Azure (AccessToSQL)
Per eseguire la migrazione dei database di Access a SQL Azure, è necessario connettersi all'istanza di destinazione di SQL Azure. Quando si esegue la connessione, SSMA ottiene i metadati relativi a tutti i database nell'istanza di SQL Azure e Visualizza i metadati del database in Esplora metadati SQL Azure. SSMA archivia informazioni sull'istanza di SQL Azure a cui si è connessi, ma non archivia le password.  
  
La connessione a SQL Azure rimane attiva fino a quando non si chiude il progetto. Quando si riapre il progetto, è necessario riconnettersi a SQL Azure se si desidera una connessione attiva al server. È possibile lavorare offline fino a quando non si caricano oggetti di database in SQL Azure e si migrano i dati.  
  
I metadati relativi all'istanza di SQL Azure non vengono sincronizzati automaticamente. Per aggiornare i metadati in SQL Azure Metadata Explorer, è invece necessario aggiornare manualmente i metadati del SQL Azure. Per ulteriori informazioni, vedere la sezione "sincronizzazione dei metadati di SQL Azure" più avanti in questo argomento.  
  
## <a name="required-sql-azure-permissions"></a>Autorizzazioni SQL Azure richieste  
L'account utilizzato per connettersi a SQL Azure richiede autorizzazioni diverse a seconda delle azioni eseguite dall'account:  
  
-   Per convertire gli oggetti di [!INCLUDE[tsql](../../includes/tsql-md.md)] accesso in sintassi, per aggiornare i metadati da SQL Azure o per salvare la sintassi convertita in script, l'account deve disporre dell'autorizzazione per accedere all'istanza di SQL Azure.  
  
-   Per caricare gli oggetti di database in SQL Azure, il requisito di autorizzazione minimo è l'appartenenza al ruolo del database **db_owner** nel database di destinazione.  
  
## <a name="establishing-a-sql-azure-connection"></a>Creazione di una connessione SQL Azure  
Prima di convertire gli oggetti di database di Access nella sintassi di SQL Azure, è necessario stabilire una connessione all'istanza di SQL Azure in cui si desidera eseguire la migrazione del database o dei database di Access.  
  
Quando si definiscono le proprietà di connessione, è inoltre necessario specificare il database in cui verrà eseguita la migrazione degli oggetti e dei dati. È possibile personalizzare questo mapping a livello di schema di accesso dopo la connessione a SQL Azure. Per ulteriori informazioni, vedere [mapping di database di Access a schemi SQL Server](mapping-source-and-target-databases-accesstosql.md)  
  
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
> SSMA per Access non supporta la connessione al database **Master** in SQL Azure.  
  
Se non sono presenti database nell'account di SQL Azure, è possibile creare il primo database usando l'opzione **Crea database di Azure** visualizzata nel pulsante **Sfoglia** .  
  
## <a name="synchronizing-sql-azure-metadata"></a>Sincronizzazione di metadati di SQL Azure  
I metadati relativi ai database SQL Azure non vengono aggiornati automaticamente. I metadati in SQL Azure Esplora metadati sono uno snapshot dei metadati quando si è connessi per la prima volta a SQL Azure o all'ultima volta che sono stati aggiornati manualmente i metadati. È possibile aggiornare manualmente i metadati per tutti i database o per qualsiasi singolo database o oggetto di database.  
  
**Per sincronizzare i metadati**  
  
1.  Assicurarsi di essere connessi a SQL Azure.  
  
2.  In SQL Azure Esplora metadati, selezionare la casella di controllo accanto allo schema del database o del database che si desidera aggiornare.  
  
    Ad esempio, per aggiornare i metadati per tutti i database, selezionare la casella accanto a database.  
  
3.  Fare clic con il pulsante destro del mouse su database o sul database singolo o sullo schema del database, quindi scegliere **Sincronizza con database**.  
  
## <a name="refreshing-sql-azure-metadata"></a>Aggiornamento dei metadati di SQL Azure  
Se SQL Azure schemi cambiano dopo la connessione, è possibile aggiornare i metadati dal server.  
  
**Per aggiornare i metadati di SQL Azure**  
  
-   In SQL Azure Esplora metadati fare clic con il pulsante destro del mouse su **database**, quindi scegliere **Aggiorna da database**.  
  
## <a name="reconnecting-to-sql-azure"></a>Riconnessione a SQL Azure  
La connessione a SQL Azure rimane attiva fino a quando non si chiude il progetto. Quando si riapre il progetto, è necessario riconnettersi a SQL Azure se si desidera una connessione attiva al server. È possibile lavorare offline fino a quando non si caricano oggetti di database in SQL Azure e si migrano i dati.  
  
La procedura per la riconnessione a SQL Azure è identica alla procedura per stabilire una connessione.  
  
## <a name="next-step"></a>passaggio successivo  
Il passaggio successivo della migrazione dipende dalle esigenze del progetto:  
  
-   Per personalizzare il mapping tra gli schemi di accesso e SQL Azure database e schemi, vedere [mapping dei database di Access a SQL Server schemi](mapping-source-and-target-databases-accesstosql.md).  
  
-   Per personalizzare le opzioni di configurazione per i progetti, vedere [impostazione delle opzioni del progetto](setting-conversion-and-migration-options-accesstosql.md).  
  
-   Per personalizzare il mapping dei tipi di dati di origine e di destinazione, vedere [mapping di tipi di dati di origine e di destinazione](mapping-source-and-target-data-types-accesstosql.md).  
  
-   Se non è necessario eseguire alcuna di queste attività, è possibile convertire le definizioni degli oggetti di database di Access in SQL Azure definizioni degli oggetti. Per ulteriori informazioni, vedere [conversione di database di Access](converting-access-database-objects-accesstosql.md)  
  
## <a name="see-also"></a>Vedere anche  
[Migrazione dei database di Access a SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
