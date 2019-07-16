---
title: Il caricamento di convertire gli oggetti di Database in SQL Server (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access databases, loading converted objects into SQL Azure
- Access databases, loading converted objects into SQL Server
- data, securing
- loading objects into SQL Azure
- loading objects into SQL Server
- migrating objects into SQL Azure
- migrating objects into SQL Server
- moving objects into SQL Azure
- moving objects into SQL Server
- schemas, loading into SQL Azure
- schemas, loading into SQL Server
- scripting converted objects
- securing data
- SQL Azure, loading objects into
- SQL Server, loading objects into
- synchronizing metadata with SQL Azure
- synchronizing metadata with SQL Server
- uploading objects into SQL Azure
- uploading objects into SQL Server
ms.assetid: 4e854eee-b10c-4f0b-9d9e-d92416e6f2ba
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 7effaa973b7a39df6fc0b9385a5cfde4fdad18d4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67986317"
---
# <a name="loading-converted-database-objects-into-sql-server-accesstosql"></a>Il caricamento di convertire gli oggetti di Database in SQL Server (AccessToSQL)
Dopo aver convertito oggetti di database di Access da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, è possibile caricare gli oggetti di database risultante in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure. È possibile avere SSMA creare gli oggetti, oppure è possibile creare script degli oggetti ed eseguire gli script manualmente. Inoltre, SSMA consente di aggiornare i metadati di destinazione con il contenuto effettivo della [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o database di SQL Azure.  
  
## <a name="choosing-between-synchronization-and-scripts"></a>Scelta tra sincronizzazione e gli script  
Se si desidera caricare gli oggetti di database convertiti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure senza alcuna modifica, è possibile avere SSMA creare o ricreare gli oggetti di database direttamente. Tale metodo è rapido e semplice, ma non consente la personalizzazione del [!INCLUDE[tsql](../../includes/tsql-md.md)] codice che definisce il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o oggetti di SQL Azure, diversi dalle stored procedure.  
  
Se si desidera modificare il [!INCLUDE[tsql](../../includes/tsql-md.md)] che viene usato per creare oggetti, se si desidera maggiore controllo sulla creazione di oggetti, l'uso di SSMA per creare script. È possibile quindi modificano tali script, creare individualmente ogni oggetto e persino utilizzare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent per pianificare la creazione di tali oggetti.  
  
## <a name="using-ssma-to-synchronize-objects-with-sql-server"></a>Uso di SSMA per sincronizzare gli oggetti con SQL Server  
Usare SSMA per creare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o gli oggetti di database di SQL Azure, si selezionano gli oggetti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Visualizzatore metadati di SQL Azure e quindi sincronizzare gli oggetti con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, come illustrato nella procedura seguente. Per impostazione predefinita, se gli oggetti esistono già nella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure e se i metadati SSMA ha alcune modifiche locali o gli aggiornamenti alla definizione di tali oggetti molto, in SSMA modificheranno le definizioni degli oggetti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure. È possibile modificare il comportamento predefinito modificando **impostazioni del progetto**.  
  
> [!NOTE]  
> È possibile selezionare esistente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o gli oggetti di database di SQL Azure non sono stati convertiti dal database di Access. Tuttavia, SSMA non ricreare o modificare tali oggetti.  
  
**Per sincronizzare gli oggetti con SQL Server o SQL Azure**  
  
1.  Nella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure i metadati Explorer, espandere la parte superiore [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o un nodo di SQL Azure, quindi espandere **database**.  
  
2.  Selezionare gli oggetti da elaborare:  
  
    -   Per sincronizzare un database completo, selezionare la casella di controllo accanto al nome del database.  
  
    -   Per sincronizzare o omettere gli oggetti singoli o categorie di oggetti, selezionare o deselezionare la casella di controllo accanto all'oggetto o una cartella.  
  
3.  Dopo avere selezionato gli oggetti da elaborare nella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Visualizzatore metadati di SQL Azure, fare doppio clic su **database**, quindi fare clic su **Sincronizza con Database**.  
  
    È inoltre possibile sincronizzare singoli oggetti o le categorie di oggetti facendo clic su oggetto o relativa cartella padre, e quindi scegliendo **Sincronizza con Database**.  
  
    Successivamente, verrà visualizzato SSMA il **Sincronizza con Database** finestra di dialogo in cui è possibile visualizzare due gruppi di elementi. Sul lato sinistro, SSMA viene rappresentati in un albero di oggetti di database selezionati. Sul lato destro, è possibile visualizzare una struttura ad albero che rappresentano gli stessi oggetti nei metadati SSMA. È possibile espandere l'albero, fare clic a destra o sinistra pulsante ' +'. La direzione di sincronizzazione viene visualizzata nella colonna azione inserita tra le due strutture ad albero.  
  
    Un segno di azione può trovarsi in tre stati:  
  
    -   Una freccia a sinistra indica che verrà salvato il contenuto dei metadati del database (predefinito).  
  
    -   Una freccia a destra significa contenuto del database verrà sovrascritti i metadati SSMA.  
  
    -   Un segnale di cross, che non verrà eseguita alcuna azione.  
  
    Fare clic sul segno azione di modifica dello stato. Viene eseguita la sincronizzazione effettiva quando si fa clic **OK** pulsante delle **Sincronizza con Database** finestra di dialogo.  
  
## <a name="scripting-objects"></a>Oggetti di scripting  
Se si desidera salvare [!INCLUDE[tsql](../../includes/tsql-md.md)] definizioni di oggetti di database convertiti, o si desidera modificare le definizioni degli oggetti e generare script per eseguire manualmente, è possibile salvare le definizioni degli oggetti per il database convertito [!INCLUDE[tsql](../../includes/tsql-md.md)] script.  
  
**Per salvare uno o più oggetti in uno script**  
  
1.  Nelle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Visualizzatore metadati, espandere il nodo principale (il nome del server) e quindi espandere **database**.  
  
2.  Eseguire una o più delle seguenti operazioni:  
  
    -   Per creare uno script un database completo, selezionare la casella di controllo accanto al nome del database.  
  
    -   Per creare uno script o omettere singole viste, espandere il database, espandere **viste**e quindi selezionare o deselezionare la casella di controllo accanto alla visualizzazione.  
  
    -   Per creare uno script o omettere le singole tabelle, espandere il database, espandere **tabelle**e quindi selezionare o deselezionare la casella di controllo accanto alla tabella.  
  
    -   Per creare uno script o omettere singoli indici per una tabella, espandere la tabella, espandere **indici**e quindi selezionare o deselezionare l'indice.  
  
3.  Fare doppio clic su **database** e selezionare **Salva come Script**.  
  
    È anche possibile creare script singoli oggetti. Per creare uno script un oggetto, indipendentemente dal fatto che siano selezionati gli oggetti, fare doppio clic su oggetto e selezionare **Salva con nome Script**.  
  
4.  Nel **Salva con nome** finestra di dialogo casella, individuare la cartella in cui si desidera salvare lo script, immettere un nome di file nei **nome File** casella e quindi fare clic su **OK**.  
  
    SSMA viene aggiunta l'estensione del nome file con estensione SQL.  
  
### <a name="modifying-scripts"></a>Modifica degli script  
Dopo aver salvato la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o definizioni di oggetti di SQL Azure come uno script, è possibile usare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per modificare lo script.  
  
**Per modificare uno script**  
  
1.  Nel [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] **File** dal menu **Open**, quindi fare clic su **File**.  
  
2.  Nel **aperto** finestra di dialogo, individuare e selezionare il file di script e quindi fare clic su **OK**.  
  
3.  Modificare il file di script usando l'editor di query.  
  
    Per altre informazioni sull'editor di query, vedere "Editor pratici comandi e funzionalità" in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] documentazione Online.  
  
4.  Per salvare lo script, nel menu File, selezionare **salvare**.  
  
### <a name="running-scripts"></a>Esecuzione di script  
È possibile eseguire in uno script o le singole istruzioni, [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
**Per eseguire uno script**  
  
1.  Nel [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **File** dal menu **Open** e quindi fare clic su **File**.  
  
2.  Nel **aperto** finestra di dialogo, individuare e selezionare il file di script e quindi fare clic su **OK**.  
  
3.  Per eseguire lo script completo, premere il **F5** chiave.  
  
4.  Per eseguire un set di istruzioni, selezionare le istruzioni nella finestra dell'editor di query e quindi premere il **F5** chiave.  
  
Per altre informazioni su come usare l'editor di query per eseguire gli script, vedere " [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] Query" in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] documentazione Online.  
  
È anche possibile eseguire gli script dalla riga di comando usando il **sqlcmd** utilità e da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dell'agente. Per altre informazioni sulle **sqlcmd**, vedere la sezione "utilità sqlcmd" in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] documentazione Online. Per altre informazioni sulle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, vedere "automatizzare le attività amministrative ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente)" in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] documentazione Online.  
  
## <a name="securing-objects-in-sql-server"></a>Protezione degli oggetti in SQL Server  
Dopo aver caricato gli oggetti di database convertiti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è possibile concedere e negare le autorizzazioni per tali oggetti. È consigliabile eseguire questa operazione prima della migrazione dei dati a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per informazioni su come proteggere gli oggetti nello [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere "Protezione considerazioni per i database e applicazioni di Database" nella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] documentazione Online.  
  
## <a name="next-step"></a>Passaggio successivo  
Il passaggio successivo del processo di migrazione consiste [eseguire la migrazione dei dati in SQL Server](migrating-access-data-into-sql-server-azure-sql-db-accesstosql.md).  
  
## <a name="see-also"></a>Vedere anche  
[Migrazione dei database di Access a SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
