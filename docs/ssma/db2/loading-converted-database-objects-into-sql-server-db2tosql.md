---
title: Il caricamento di convertire gli oggetti di Database in SQL Server (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f4ea1ced-9f9f-4a9d-88ab-81dbab64adc3
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 21962c8849204db6f3e5f114b6f8f86994d53b35
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63298849"
---
# <a name="loading-converted-database-objects-into-sql-server-db2tosql"></a>Il caricamento di convertire gli oggetti di Database in SQL Server (DB2ToSQL)
Dopo aver convertito schemi DB2 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è possibile caricare gli oggetti di database risultante in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. È possibile avere SSMA creare gli oggetti, oppure è possibile creare script degli oggetti ed eseguire gli script manualmente. Inoltre, SSMA consente di aggiornare i metadati di destinazione con il contenuto effettivo della [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database.  
  
## <a name="choosing-between-synchronization-and-scripts"></a>Scelta tra sincronizzazione e gli script  
Se si desidera caricare gli oggetti di database convertiti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] senza alcuna modifica, è possibile avere SSMA creare o ricreare gli oggetti di database direttamente. Tale metodo è rapido e semplice, ma non consente la personalizzazione del [!INCLUDE[tsql](../../includes/tsql-md.md)] codice che definisce il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oggetti, diverse da stored procedure.  
  
Se si desidera modificare il [!INCLUDE[tsql](../../includes/tsql-md.md)] che viene usato per creare oggetti, se si desidera maggiore controllo sulla creazione di oggetti, l'uso di SSMA per creare script. È possibile quindi modificano tali script, creare individualmente ogni oggetto e persino utilizzare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent per pianificare la creazione di tali oggetti.  
  
## <a name="using-ssma-to-synchronize-objects-with-sql-server"></a>Uso di SSMA per sincronizzare gli oggetti con SQL Server  
Usare SSMA per creare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gli oggetti di database, si selezionano gli oggetti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Visualizzatore metadati e quindi sincronizzare gli oggetti con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], come illustrato nella procedura seguente. Per impostazione predefinita, se gli oggetti esistono già nella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], e se i metadati SSMA sono più l'oggetto nel recenti [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], SSMA modificheranno le definizioni degli oggetti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. È possibile modificare il comportamento predefinito modificando **impostazioni del progetto**.  
  
> [!NOTE]  
> È possibile selezionare esistente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gli oggetti che non sono stati convertiti dal database DB2 di database. Tuttavia, tali oggetti non verrà ricreati o sia stato manomesso SSMA.  
  
**Per sincronizzare gli oggetti con SQL Server**  
  
1.  Nelle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Visualizzatore metadati, espandere la parte superiore [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nodo, quindi espandere **database**.  
  
2.  Selezionare gli oggetti da elaborare:  
  
    -   Per sincronizzare un database completo, selezionare la casella di controllo accanto al nome del database.  
  
    -   Per sincronizzare o omettere gli oggetti singoli o categorie di oggetti, selezionare o deselezionare la casella di controllo accanto all'oggetto o una cartella.  
  
3.  Dopo avere selezionato gli oggetti da elaborare nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Visualizzatore metadati, fare doppio clic su **database**, quindi fare clic su **Sincronizza con Database**.  
  
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
  
2.  Nel **Salva con nome** finestra di dialogo casella, individuare la cartella in cui si desidera salvare lo script, immettere un nome di file nei **nome File** finestra e quindi [!INCLUDE[clickOK](../../includes/clickok-md.md)]. SSMA viene aggiunta l'estensione del nome file con estensione SQL.  
  
### <a name="modifying-scripts"></a>Modifica degli script  
Dopo aver salvato la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definizioni degli oggetti come uno o più script, è possibile usare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per visualizzare e modificare gli script.  
  
**Per modificare uno script**  
  
1.  Nel [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **File** dal menu **Open**, quindi fare clic su **File**.  
  
2.  Nel **aperto** nella finestra di dialogo selezionare il file di script e quindi fare clic su OK.
  
3.  Modificare il file di script usando l'editor di query.  
  
    Per altre informazioni sull'editor di query, vedere "Editor pratici comandi e funzionalità" in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] documentazione Online.  
  
4.  Per salvare lo script, dal menu scegliere File **salvare**.  
  
### <a name="running-scripts"></a>Esecuzione di script  
È possibile eseguire in uno script o le singole istruzioni, [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
**Per eseguire uno script**  
  
1.  Nel [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **File** dal menu **Open**, quindi fare clic su **File**.  
  
2.  Nel **aperto** finestra di dialogo, selezionare il file di script e quindi [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
3.  Per eseguire lo script completo, premere il **F5** chiave.  
  
4.  Per eseguire un set di istruzioni, selezionare le istruzioni nella finestra dell'editor di query e quindi premere il **F5** chiave.  
  
Per altre informazioni su come usare l'editor di query per eseguire gli script, vedere " [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] Query" in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] documentazione Online.  
  
È anche possibile eseguire gli script dalla riga di comando usando il **sqlcmd** utilità e dal [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente. Per altre informazioni sulle **sqlcmd**, vedere la sezione "utilità sqlcmd" in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] documentazione Online. Per altre informazioni sulle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, vedere "automatizzare le attività amministrative ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente)" in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] documentazione Online.  
  
## <a name="securing-objects-in-sql-server"></a>Protezione degli oggetti in SQL Server  
Dopo aver caricato gli oggetti di database convertiti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è possibile concedere e negare le autorizzazioni per tali oggetti. È consigliabile eseguire questa operazione prima della migrazione dei dati a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per informazioni su come proteggere gli oggetti nello [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere "Protezione considerazioni per i database e applicazioni di Database" nella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] documentazione Online.  
  
## <a name="next-step"></a>Passaggio successivo  
Il passaggio successivo del processo di migrazione consiste [eseguire la migrazione di dati DB2 a SQL Server](https://msdn.microsoft.com/86cbd39f-6dac-409a-9ce1-7dd54403f84b).  
  
## <a name="see-also"></a>Vedere anche  
[La migrazione di dati DB2 in SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-data-into-sql-server-db2tosql.md)  
  
