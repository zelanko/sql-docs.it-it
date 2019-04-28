---
title: Il caricamento di convertire gli oggetti di Database in SQL Server (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Synchronization, Securing Objects in SQL Server
- Synchronization,Scripting Objects
ms.assetid: a8ae33b2-1883-4785-922b-ea0e31c0b37a
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 57d66d48591304d5481cb86c7418ed0ac27051db
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62818926"
---
# <a name="loading-converted-database-objects-into-sql-server-oracletosql"></a>Caricamento di oggetti di database convertiti in SQL Server (OracleToSQL)
Dopo aver convertito schemi Oracle a SQL Server, è possibile caricare gli oggetti di database risultante in SQL Server. È possibile avere SSMA creare gli oggetti, oppure è possibile creare script degli oggetti ed eseguire gli script manualmente. SSMA consente inoltre di aggiornare i metadati di destinazione con il contenuto effettivo del database di SQL Server.  
  
## <a name="choosing-between-synchronization-and-scripts"></a>Scelta tra sincronizzazione e gli script  
Se si desidera caricare gli oggetti di database convertiti in SQL Server senza alcuna modifica, è possibile avere SSMA creare o ricreare gli oggetti di database direttamente. Che metodo è rapido e semplice, ma non consente la personalizzazione del [!INCLUDE[tsql](../../includes/tsql-md.md)] codice che definisce gli oggetti di SQL Server, diverse da stored procedure.  
  
Se si desidera modificare il [!INCLUDE[tsql](../../includes/tsql-md.md)] che viene usato per creare oggetti, se si desidera maggiore controllo sulla creazione di oggetti, l'uso di SSMA per creare script. Si può quindi modificare gli script, creare individualmente ogni oggetto e anche usare SQL Server Agent per pianificare la creazione di tali oggetti.  
  
## <a name="using-ssma-to-synchronize-objects-with-sql-server"></a>Uso di SSMA per sincronizzare gli oggetti con SQL Server  
Per l'uso di SSMA per creare oggetti di database di SQL Server, selezionare gli oggetti in Esplora i metadati di SQL Server e quindi sincronizzare gli oggetti con SQL Server, come illustrato nella procedura seguente. Per impostazione predefinita, se gli oggetti già presenti in SQL Server e se i metadati SSMA sono più recenti rispetto all'oggetto di SQL Server, SSMA modificheranno le definizioni degli oggetti in SQL Server. È possibile modificare il comportamento predefinito modificando **impostazioni del progetto**.  
  
> [!NOTE]  
> È possibile selezionare oggetti di database di SQL Server esistenti che non sono stati convertiti dal database Oracle. Tuttavia, tali oggetti non verrà ricreati o sia stato manomesso SSMA.  
  
**Per sincronizzare gli oggetti con SQL Server**  
  
1.  In Esplora i metadati di SQL Server, espandere il nodo principale di SQL Server e quindi espandere **database**.  
  
2.  Selezionare gli oggetti da elaborare:  
  
    -   Per sincronizzare un database completo, selezionare la casella di controllo accanto al nome del database.  
  
    -   Per sincronizzare o omettere gli oggetti singoli o categorie di oggetti, selezionare o deselezionare la casella di controllo accanto all'oggetto o una cartella.  
  
3.  Dopo aver selezionato gli oggetti da elaborare in Visualizzatore metadati di SQL Server, fare doppio clic su **database**, quindi fare clic su **Sincronizza con Database**.  
  
    È inoltre possibile sincronizzare singoli oggetti o le categorie di oggetti facendo clic su oggetto o relativa cartella padre, e quindi scegliendo **Sincronizza con Database**.  
  
    Successivamente, verrà visualizzato SSMA il **Sincronizza con Database** finestra di dialogo in cui è possibile visualizzare due gruppi di elementi. Sul lato sinistro, SSMA viene rappresentati in un albero di oggetti di database selezionati. Sul lato destro, è possibile visualizzare una struttura ad albero che rappresentano gli stessi oggetti nei metadati SSMA. È possibile espandere l'albero, fare clic a destra o sinistra pulsante ' +'. La direzione di sincronizzazione viene visualizzata nella colonna azione inserita tra le due strutture ad albero.  
  
    Un segno di azione può trovarsi in tre stati:  
  
    -   Una freccia a sinistra indica che verrà salvato il contenuto dei metadati del database (predefinito).  
  
    -   Una freccia a destra significa contenuto del database verrà sovrascritti i metadati SSMA.  
  
    -   Un segnale di cross, che non verrà eseguita alcuna azione.  
  
Fare clic sul segno azione di modifica dello stato. Viene eseguita la sincronizzazione effettiva quando si fa clic **OK** pulsante delle **Sincronizza con Database** finestra di dialogo.  
  
## <a name="scripting-objects"></a>Oggetti di scripting  
Per salvare [!INCLUDE[tsql](../../includes/tsql-md.md)] le definizioni degli oggetti di database convertiti, o per modificare le definizioni degli oggetti ed eseguire gli script manualmente, è possibile salvare il database convertito le definizioni degli oggetti a [!INCLUDE[tsql](../../includes/tsql-md.md)] script.  
  
**Per salvare gli oggetti degli script**  
  
1.  Dopo aver selezionato gli oggetti per salvare uno script, fare doppio clic su **database**, quindi fare clic su **Salva come Script**.  
  
    È inoltre possibile generare script oggetti singoli o categorie di oggetti facendo clic su oggetto o relativa cartella padre, e quindi scegliendo **Salva con nome Script**.  
  
2.  Nel **Salva con nome** finestra di dialogo casella, individuare la cartella in cui si desidera salvare lo script, immettere un nome di file nei **nome File** casella e quindi fare clic su OK SSMA aggiungerà l'estensione del nome file con estensione SQL.  
  
### <a name="modifying-scripts"></a>Modifica degli script  
Dopo aver salvato le definizioni degli oggetti di SQL Server come uno o più script, è possibile usare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per visualizzare e modificare gli script.  
  
**Per modificare uno script**  
  
1.  Nel [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **File** dal menu **Open**, quindi fare clic su **File**.  
  
2.  Nel **aperto** nella finestra di dialogo selezionare il file di script, quindi fare clic su OK.
  
3.  Modificare il file di script usando l'editor di query.  
  
    Per altre informazioni sull'editor di query, vedere "Editor pratici comandi e funzionalità" nella documentazione Online di SQL Server.  
  
4.  Per salvare lo script, dal menu scegliere File **salvare**.  
  
### <a name="running-scripts"></a>Esecuzione di script  
È possibile eseguire in uno script o le singole istruzioni, [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
**Per eseguire uno script**  
  
1.  Nel [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **File** dal menu **Open**, quindi fare clic su **File**.  
  
2.  Nel **aperto** nella finestra di dialogo selezionare il file di script e quindi fare clic su OK  
  
3.  Per eseguire lo script completo, premere il **F5** chiave.  
  
4.  Per eseguire un set di istruzioni, selezionare le istruzioni nella finestra dell'editor di query e quindi premere il **F5** chiave.  
  
Per altre informazioni su come usare l'editor di query per eseguire gli script, vedere " [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] Query" nella documentazione Online di SQL Server.  
  
È anche possibile eseguire gli script dalla riga di comando usando il **sqlcmd** utility e da SQL Server Agent. Per altre informazioni sulle **sqlcmd**, vedere "utilità sqlcmd" nella documentazione Online di SQL Server. Per altre informazioni su SQL Server Agent, vedere "Automatizzare attività amministrative (SQL Server Agent)" nella documentazione Online di SQL Server.  
  
## <a name="securing-objects-in-sql-server"></a>Protezione degli oggetti in SQL Server  
Dopo aver caricato gli oggetti di database convertiti in SQL Server, è possibile concedere e negare le autorizzazioni per tali oggetti. È consigliabile eseguire questa operazione prima della migrazione dei dati a SQL Server. Per informazioni su come migliorare la protezione di oggetti in SQL Server, vedere "Protezione considerazioni per i database e applicazioni di Database" nella documentazione Online di SQL Server.  
  
## <a name="next-step"></a>Passaggio successivo  
Il passaggio successivo del processo di migrazione consiste [eseguire la migrazione dei dati in SQL Server](migrating-oracle-data-into-sql-server-oracletosql.md).  
  
## <a name="see-also"></a>Vedere anche  
[La migrazione da Oracle database in SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
