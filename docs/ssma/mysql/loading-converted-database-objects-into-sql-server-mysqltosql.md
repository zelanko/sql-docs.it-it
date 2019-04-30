---
title: Il caricamento di convertire gli oggetti di Database in SQL Server (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: ac993a6d-0283-4823-8793-6b217677dfa3
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: b2e58eb534088482493e6f36c3841f36644183af
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63187235"
---
# <a name="loading-converted-database-objects-into-sql-server-mysqltosql"></a>Caricamento di oggetti di database convertiti in SQL Server (MySQLToSQL)
Dopo aver convertito i database MySQL al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, è possibile caricare gli oggetti di database risultante in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure. È possibile avere SSMA creare gli oggetti, oppure è possibile creare script degli oggetti ed eseguire gli script manualmente. Inoltre, SSMA consente di aggiornare i metadati di destinazione con il contenuto effettivo della [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o database di SQL Azure.  
  
## <a name="choosing-between-synchronization-and-scripts"></a>Scelta tra sincronizzazione e gli script  
Se si desidera caricare gli oggetti di database convertiti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure senza alcuna modifica, è possibile avere SSMA creare o ricreare gli oggetti di database direttamente. Che metodo è rapido e semplice, ma non consente la personalizzazione del codice Transact-SQL che definisce il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o gli oggetti di SQL Azure.  
  
Se si desidera modificare Transact-SQL che consente di creare oggetti o se si desidera maggiore controllo sulla creazione di oggetti, utilizzare SSMA consente di creare script. Si può quindi modificare questi script, creare individualmente ogni oggetto e anche usare SQL Server Agent per pianificare la creazione di questi oggetti.  
  
## <a name="using-ssma-to-synchronize-objects-with-sql-server"></a>Uso di SSMA per sincronizzare gli oggetti con SQL Server  
Per l'uso di SSMA per creare gli oggetti di database di SQL Server o SQL Azure, si seleziona gli oggetti nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Esplora risorse di SQL Azure i metadati e quindi sincronizzare gli oggetti con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, come illustrato nella procedura seguente. Per impostazione predefinita, se gli oggetti esistono già nella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure e se i metadati SSMA ha alcune modifiche locali o gli aggiornamenti alla definizione di tali oggetti molto, in SSMA modificheranno le definizioni degli oggetti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure. È possibile modificare il comportamento predefinito modificando **impostazioni del progetto**.  
  
> [!NOTE]  
> È possibile selezionare esistente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o gli oggetti di database di SQL Azure non sono stati convertiti dal database MySQL. Tuttavia, questi oggetti non verrà ricreati o sia stato manomesso SSMA.  
  
##### <a name="to-synchronize-objects-with-sql-server-or-sql-azure"></a>Per sincronizzare gli oggetti con SQL Server o SQL Azure  
  
1.  Nella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure i metadati Explorer, espandere la parte superiore [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o un nodo di SQL Azure, quindi espandere **database**.  
  
2.  Selezionare gli oggetti da elaborare:  
  
    -   Per sincronizzare un database completo, selezionare la casella di controllo accanto al nome del database.  
  
    -   Per sincronizzare o omettere gli oggetti singoli o categorie di oggetti, selezionare o deselezionare la casella di controllo accanto all'oggetto o una cartella.  
  
3.  Dopo aver selezionato gli oggetti da elaborare in SQL Server o SQL Azure i metadati Explorer, fare doppio clic su **database**, quindi fare clic su **Sincronizza con Database**.  
  
    È inoltre possibile sincronizzare singoli oggetti o le categorie di oggetti facendo clic su oggetto o relativa cartella padre, e quindi scegliendo **Sincronizza con Database**.  
  
    Successivamente, verrà visualizzato SSMA il **Sincronizza con Database** finestra di dialogo in cui è possibile visualizzare due gruppi di elementi. Sul lato sinistro, SSMA viene rappresentati in un albero di oggetti di database selezionati. Sul lato destro, è possibile visualizzare una struttura ad albero che rappresentano gli stessi oggetti nei metadati SSMA. È possibile espandere l'albero, fare clic a destra o sinistra pulsante ' +'. La direzione di sincronizzazione viene visualizzata nella colonna azione inserita tra le due strutture ad albero.  
  
    Un segno di azione può trovarsi in tre stati seguenti:  
  
    -   Una freccia a sinistra indica che verrà salvato il contenuto dei metadati del database (predefinito).  
  
    -   Una freccia a destra significa contenuto del database verrà sovrascritti i metadati SSMA.  
  
    -   Un segnale di cross, che non verrà eseguita alcuna azione.  
  
    -   Fare clic sul segno azione di modifica dello stato. Viene eseguita la sincronizzazione effettiva quando si fa clic **OK** pulsante delle **Sincronizza con Database** finestra di dialogo.  
  
## <a name="scripting-objects"></a>Oggetti di scripting  
Per salvare [!INCLUDE[tsql](../../includes/tsql-md.md)] le definizioni degli oggetti di database convertiti, o per modificare le definizioni degli oggetti ed eseguire gli script manualmente, è possibile salvare il database convertito le definizioni degli oggetti a [!INCLUDE[tsql](../../includes/tsql-md.md)] script.  
  
**Per salvare gli oggetti degli script**  
  
1.  Dopo aver selezionato gli oggetti per salvare uno script, fare doppio clic su **database**, quindi fare clic su **Salva come Script**.  
  
    È inoltre possibile generare script oggetti singoli o categorie di oggetti facendo clic su oggetto o relativa cartella padre, e quindi scegliendo **Salva con nome Script**.  
  
2.  Nel **Salva con nome** finestra di dialogo casella, individuare la cartella in cui si desidera salvare lo script, immettere un nome di file nei **nome File** finestra e quindi [!INCLUDE[clickOK](../../includes/clickok-md.md)] SSMA aggiungerà l'estensione del nome file con estensione SQL.  
  
### <a name="modifying-scripts"></a>Modifica degli script  
Dopo aver salvato il Server SQL o le definizioni degli oggetti di SQL Azure come uno script, è possibile usare SQL Server Management Studio per modificare lo script.  
  
**Per modificare uno script**  
  
1.  In Management Studio **File** dal menu **Open**, quindi fare clic su **File**.  
  
2.  Nella finestra di dialogo Apri, individuare e selezionare il file di script e quindi fare clic su **OK**.  
  
3.  Modificare il file di script usando l'editor di query. Per altre informazioni sull'editor di query, vedere "Editor pratici comandi e funzionalità" nella documentazione Online di SQL Server.  
  
4.  Per salvare lo script, nel menu File, selezionare **salvare**.  
  
### <a name="running-scripts"></a>Esecuzione di script  
È possibile eseguire uno script o le singole istruzioni, in SQL Server Management Studio.  
  
**Per eseguire uno script**  
  
1.  In SQL Server Management Studio **File** dal menu **Open** e quindi fare clic su **File**.  
  
2.  Nella finestra di dialogo Apri, individuare e selezionare il file di script e quindi fare clic su **OK**.  
  
3.  Per eseguire lo script completo, premere il **F5** chiave.  
  
4.  Per eseguire un set di istruzioni, selezionare le istruzioni nella finestra dell'editor di query e quindi premere il **F5** chiave.  
  
5.  Per altre informazioni su come usare l'editor di query per eseguire gli script, vedere "SQL Server Management Studio Query Transact-SQL" nella documentazione Online di SQL Server.  
  
6.  È anche possibile eseguire gli script dalla riga di comando usando il **sqlcmd** utility e da SQL Server Agent. Per altre informazioni sulle **sqlcmd**, vedere "utilità sqlcmd" nella documentazione Online di SQL Server. Per altre informazioni su SQL Server Agent, vedere "Automatizzare attività amministrative (SQL Server Agent)" nella documentazione Online di SQL Server.  
  
## <a name="securing-objects-in-sql-server"></a>Protezione degli oggetti in SQL Server  
Dopo aver caricato gli oggetti di database convertiti in SQL Server, è possibile concedere e negare le autorizzazioni per tali oggetti. È consigliabile eseguire questa operazione prima della migrazione dei dati a SQL Server. Per informazioni su come migliorare la protezione di oggetti in SQL Server, vedere "Protezione considerazioni per i database e applicazioni di Database" nella documentazione Online di SQL Server.  
  
## <a name="next-step"></a>Passaggio successivo  
Il passaggio successivo del processo di migrazione consiste [eseguire la migrazione di dati di MySQL in SQL Server - database SQL di Azure &#40;MySQLToSQL&#41;](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
  
## <a name="see-also"></a>Vedere anche  
[Database di migrazione da MySQL a SQL Server - Azure SQL database &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
