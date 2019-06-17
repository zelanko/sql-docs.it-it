---
title: Il caricamento di convertire gli oggetti di Database in SQL Server (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Loading Converted Database Objects
ms.assetid: 4c59256f-99a8-4351-9559-a455813dbd06
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 96e2bee47c97e85421b074e870c9dab1dd46220a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63245885"
---
# <a name="loading-converted-database-objects-into-sql-server-sybasetosql"></a>Caricamento di oggetti di database convertiti in SQL Server (SybaseToSQL)
Dopo aver convertito gli oggetti di database di Sybase Adaptive Server Enterprise (ASE) a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, è possibile caricare gli oggetti di database risultante in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure. È possibile avere SSMA creare gli oggetti, oppure è possibile creare script degli oggetti ed eseguire gli script manualmente. Inoltre, SSMA consente di aggiornare i metadati di destinazione con il contenuto effettivo della [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o database di SQL Azure.  
  
## <a name="choosing-between-synchronization-and-scripts"></a>Scelta tra sincronizzazione e gli script  
Se si desidera caricare gli oggetti di database convertiti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure senza alcuna modifica, è possibile avere SSMA creare o ricreare gli oggetti di database direttamente. Questo metodo è rapido e semplice, ma non consente la personalizzazione del [!INCLUDE[tsql](../../includes/tsql-md.md)] codice che definisce il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o oggetti di SQL Azure, diversi dalle stored procedure.  
  
Se si desidera modificare il [!INCLUDE[tsql](../../includes/tsql-md.md)] che consente di creare gli oggetti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, o se si desidera maggiore controllo su come e quando gli oggetti vengono creati nella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, usare SSMA per creare [!INCLUDE[tsql](../../includes/tsql-md.md)] script. È possibile quindi modificano tali script, creare individualmente ogni oggetto e persino utilizzare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure Agent per pianificare la creazione di tali oggetti.  
  
## <a name="using-ssma-to-load-objects-into-sql-server-or-sql-azure"></a>Uso di SSMA per caricare oggetti in SQL Server o SQL Azure  
Usare SSMA per creare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o gli oggetti di database di SQL Azure, si selezionano gli oggetti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Visualizzatore metadati di SQL Azure e quindi sincronizzare gli oggetti con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, come illustrato nella procedura seguente. Per impostazione predefinita, se gli oggetti esistono già nella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure e se i metadati SSMA ha alcune modifiche locali o gli aggiornamenti alla definizione di tali oggetti molto, in SSMA modificheranno le definizioni degli oggetti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure. È possibile modificare il comportamento predefinito modificando **impostazioni del progetto**.  
  
> [!NOTE]  
> È possibile selezionare esistente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o gli oggetti di database di SQL Azure non sono stati convertiti dal database di ambiente del servizio app. Tuttavia, tali oggetti non verrà ricreati o sia stato manomesso SSMA.  
  
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
  
**Per salvare gli oggetti degli script**  
  
1.  Dopo aver selezionato gli oggetti per salvare uno script, fare doppio clic su **database**, quindi selezionare **Salva come Script**.  
  
    È inoltre possibile generare script oggetti singoli o categorie di oggetti facendo clic su oggetto o la cartella che contiene, e quindi selezionando **Salva Script**.  
  
2.  Nel **Salva con nome** finestra di dialogo casella, individuare la cartella in cui si desidera salvare lo script, immettere un nome di file nei **nome File** casella e quindi fare clic su **OK**.  
  
    SSMA viene aggiunta l'estensione del nome file con estensione SQL.  
  
### <a name="modifying-scripts"></a>Modifica degli script  
Dopo aver salvato la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o definizioni di oggetti di SQL Azure come uno o più script, è possibile usare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per visualizzare e modificare gli script.  
  
**Per modificare uno script**  
  
1.  Nel [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **File** dal menu **Open**, quindi fare clic su **File**.  
  
2.  Nel **aperto** della finestra di dialogo passare a e selezionare il file di script e quindi fare clic su **OK**.  
  
3.  Modifica e il file di script usando l'editor di query.  
  
    Per altre informazioni sull'editor di query, vedere "Editor pratici comandi e funzionalità" in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] documentazione Online.  
  
4.  Per salvare lo script, nel menu File, selezionare **salvare**.  
  
### <a name="running-scripts"></a>Esecuzione di script  
È possibile eseguire in uno script o le singole istruzioni, [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
**Per eseguire uno script**  
  
1.  Nel [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **File** dal menu **Open**, quindi fare clic su **File**.  
  
2.  Nel **aperto** della finestra di dialogo passare a e selezionare il file di script e quindi fare clic su **OK**.  
  
3.  Per eseguire lo script completo, premere il **F5** chiave.  
  
4.  Per eseguire un set di istruzioni, selezionare le istruzioni nella finestra dell'editor di query e quindi premere il **F5** chiave.  
  
Per altre informazioni su come usare l'editor di query per eseguire gli script, vedere " [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] Query" in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] documentazione Online.  
  
È anche possibile eseguire gli script dalla riga di comando usando il **sqlcmd** utilità e da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dell'agente. Per altre informazioni sulle **sqlcmd**, vedere la sezione "utilità sqlcmd" in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] documentazione Online. Per altre informazioni sulle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, vedere "automazione delle attività amministrative ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente)" in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] documentazione Online.  
  
## <a name="securing-objects-in-sql-server"></a>Protezione degli oggetti in SQL Server  
Dopo aver caricato gli oggetti di database convertiti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è possibile concedere e negare le autorizzazioni per tali oggetti. È consigliabile eseguire questa operazione prima della migrazione dei dati a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per informazioni su come proteggere gli oggetti nello [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere "Protezione considerazioni per i database e applicazioni di Database" nella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] documentazione Online.  
  
## <a name="next-step"></a>Passaggio successivo  
Il passaggio successivo del processo di migrazione consiste [eseguire la migrazione di dati di Sybase ASE in SQL Server / SQL Azure(SybaseToSQL)](https://msdn.microsoft.com/54a39f5e-9250-4387-a3ae-eae47c799811).  
  
## <a name="see-also"></a>Vedere anche  
[Migrazione dei database di Sybase ASE a SQL Server - Azure SQL database &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
