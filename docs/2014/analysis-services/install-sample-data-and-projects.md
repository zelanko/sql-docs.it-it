---
title: Installare dati di esempio e progetti per l'esercitazione di modellazione multidimensionale di Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: fc475b25-cbb2-408a-901f-9299299538c5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3f0b4a69f7c1a6735fee26f1d622bc0f290e4677
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66080402"
---
# <a name="install-sample-data-and-projects-for-the-analysis-services-multidimensional-modeling-tutorial"></a>Installare dati di esempio e progetti per l'esercitazione di modellazione multidimensionale di Analysis Services
  Utilizzare le istruzioni e i collegamenti forniti in questo argomento per installare tutti i file di dati e di progetto utilizzati nelle esercitazioni su Analysis Services.  
  
## <a name="step-1-install-sql-server-software"></a>Passaggio 1: Installare il Software SQL Server  
 Nelle lezioni di questa esercitazione si presuppone che siano installati i programmi software seguenti: Tutti i programmi software indicati di seguito vengono installati tramite il supporto di installazione di SQL Server. Per semplificare la distribuzione, è possibile installare tutte le funzionalità in un solo computer. Per installare queste funzionalità, eseguire il programma di installazione di SQL Server e selezionarle dalla pagina Selezione funzionalità. Per altre informazioni, vedere [installare SQL Server 2014 dall'installazione guidata di &#40;installazione&#41;](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md).  
  
-   Motore di database  
  
-   Analysis Services  
  
     Analysis Services è disponibile solo in queste edizioni: Evaluation, Enterprise, Business Intelligence, Standard.  
  
     Si noti che le edizioni SQL Server Express non prevedono Analysis Services. [Scaricare la versione di valutazione](https://go.microsoft.com/fwlink/?LinkId=392824) se si vuole provare il software gratuitamente.  
  
     Per impostazione predefinita, Analysis Services viene installato come istanza multidimensionale, di cui si può eseguire l'override scegliendo la modalità server tabulare nella pagina di configurazione del server dell'Installazione guidata. Se si desidera eseguire entrambe le modalità server, eseguire di nuovo il programma di installazione di SQL Server nello stesso computer per installare una seconda istanza di Analysis Services nell'altra modalità.  
  
-   SQL Server Management Studio  
  
 Se si desidera è possibile installare Excel per esplorare i dati multidimensionali man mano che si prosegue con l'esercitazione. L'installazione di Excel abilita la funzionalità **Analizza in Excel** che avvia Excel usando un elenco di campi della tabella pivot connesso al cubo che viene compilato. Si consiglia di utilizzare Excel per sfogliare i dati perché è possibile compilare rapidamente un report pivot che consente di interagire con i dati.  
  
 In alternativa, è possibile esplorare i dati utilizzando la progettazione query MDX incorporata in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. La progettazione query restituisce gli stessi dati, ad eccezione di quelli presentati come un set di righe flat.  
  
## <a name="step-2-download-sql-server-data-tools---business-intelligence-for-visual-studio-2012"></a>Passaggio 2: Scaricare SQL Server Data Tools - Business Intelligence per Visual Studio 2012  
 In questa versione il download e l'installazione di SQL Server Data Tools vengono effettuati separatamente dalle altre funzionalità di SQL Server. Le finestre di progettazione e i modelli di progetto utilizzati per creare modelli e report di Business Intelligence sono ora disponibili come download Web gratuito.  
  
-   [Scaricare la versione Business Intelligence di SQL Server Data Tools](https://go.microsoft.com/fwlink/p/?LinkID=322038). Il file viene salvato nella cartella Downloads. Eseguire il programma di installazione per installare lo strumento.  
  
     Riavviare il computer per completare l'installazione.  
  
## <a name="step-3-install-databases"></a>Passaggio 3: Installare i database  
 In un modello multidimensionale di Analysis Services vengono utilizzati i dati transazionali importati da un sistema di gestione di database relazionali. Ai fini di questa esercitazione verrà utilizzato il database relazionale seguente come origine dati.  
  
-   **AdventureWorksDW2012** -si tratta di un data warehouse relazionale che viene eseguito in un'istanza del motore di Database. Fornisce i dati originali che verranno utilizzati dai progetti e dai database di Analysis Services compilati e distribuiti nel corso dell'esercitazione.  
  
     È possibile utilizzare il database di esempio con [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] e [!INCLUDE[ssSQL11](../includes/sssql11-md.md)].  
  
 Per installare il database, eseguire le operazioni seguenti:  
  
1.  Scaricare il database [AdventureWorkDW2012](https://go.microsoft.com/fwlink/p/?LinkID=221770) dalla pagina di esempi del prodotto su codeplex.  
  
     Il nome del file di database è AdvntureWorksDW2012_Data.mdf. Il file deve risiedere nella cartella Downloads del computer.  
  
2.  Copiare il file AdventureWorksDW2012_Data.mdf nella directory dei dati dell'istanza locale del motore di database di SQL Server. Per impostazione predefinita, il percorso di questo file è C:\Programmi\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Data.  
  
3.  Avviare SQL Server Management Studio e connettersi all'istanza del motore di database.  
  
4.  Fare clic con il pulsante destro del mouse su Database, quindi scegliere **Collega**.  
  
5.  Scegliere **Aggiungi**.  
  
6.  Selezionare il file del database **AdventureWorksDW2012_Data.mdf** e fare clic su **OK**. Se il file non è in elenco, assicurarsi che sia presente nella cartella C:\Programmi\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Data.  
  
7.  Nei dettagli del database rimuovere la voce File di log. Nel programma di installazione si presuppone che l'utente disponga di un file di log, ma nell'esempio non ve ne sono. Un nuovo file di log verrà creato automaticamente quando si collega il database. Selezionare il file di log e fare clic su **Rimuovi**quindi fare clic su **OK** per collegare solo il file di database primario.  
  
## <a name="step-4-grant-database-permissions"></a>Passaggio 4: Autorizzazioni per Database GRANT  
 Nei progetti di esempio vengono utilizzate impostazioni di rappresentazione dell'origine dati che specificano in quale contesto di sicurezza vengono importati o elaborati i dati. Per impostazione predefinita, le impostazioni di rappresentazione specificano l'account del servizio Analysis Services per l'accesso ai dati. Per usare questa impostazione predefinita, è necessario assicurarsi che nell'account del servizio in cui viene eseguito Analysis Services siano disponibili autorizzazioni di lettura dei dati per il database **AdventureWorksDW2012** .  
  
> [!NOTE]  
>  Ai fini dell'apprendimento, si consiglia di utilizzare l'opzione di rappresentazione dell'account del servizio predefinita e concedere autorizzazioni di lettura dei dati all'account del servizio in SQL Server. Anche se sono disponibili altre opzioni di rappresentazione, non tutte sono adatte per le operazioni di elaborazione. In particolare, l'opzione per l'utilizzo delle credenziali dell'utente corrente non è supportata per l'elaborazione.  
  
1.  Determinare l'account del servizio. È possibile utilizzare Gestione configurazione SQL Server o l'applicazione console Servizi per visualizzare le informazioni sull'account. Se Analysis Services è stato installato come istanza predefinita usando l'account predefinito, il servizio è in esecuzione come **NT Service\MSSQLServerOLAPService**.  
  
2.  In Management Studio connettersi all'istanza del motore di database.  
  
3.  Espandere la cartella Sicurezza, fare clic con il pulsante destro del mouse su Account di accesso e selezionare **Nuovo account di accesso**.  
  
4.  Nella pagina Generale in Nome account di accesso digitare **NT Service\MSSQLServerOLAPService** o un altro account usato per l'esecuzione del servizio.  
  
5.  Fare clic su **Mapping utenti**.  
  
6.  Selezionare la casella di controllo accanto al database **AdventureWorksDW2012** . L'appartenenza al ruolo deve includere automaticamente **db_datareader** e **public**. Fare clic su **OK** per accettare le impostazioni predefinite.  
  
## <a name="step-5-install-projects"></a>Passaggio 5: Installa i progetti  
 Nell'esercitazione sono inclusi progetti di esempio per consentire il confronto dei risultati rispetto a un progetto finito o l'avvio di una lezione successiva nella sequenza.  
  
 Il file di progetto per la Lezione 4 è particolarmente importante perché costituisce la base non solo di tale lezione, ma di tutte le lezioni successive. A differenza dei file di progetto precedenti, per cui i passaggi nell'esercitazione generano una copia esatta dei file di progetto completati, il progetto di esempio della Lezione 4 include informazioni sul nuovo modello che non sono presenti nel modello compilato nelle Lezioni da 1 a 3. La Lezione 4 presuppone che si inizi con un file di progetto di esempio disponibile nel download seguente.  
  
1.  Scaricare [Analysis Services Tutorial SQL Server 2012](https://go.microsoft.com/fwlink/p/?LinkID=221866) dalla pagina di esempi del prodotto su codeplex.  
  
     Le esercitazioni 2012 sono valide per la versione di [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] .  
  
     Il file "Analysis Services Tutorial SQL Server 2012.zip" verrà salvato nella cartella download nel computer.  
  
2.  Spostare il file con estensione zip in una cartella al livello immediatamente inferiore rispetto all'unità radice, ad esempio C:\Tutorial. Questo passaggio consente di ridurre l'errore "Percorso troppo lungo" che talvolta si verifica se si prova a decomprimere i file nella cartella Downloads.  
  
3.  Decomprimere i progetti di esempio: fare clic con il pulsante destro del mouse sul file e selezionare **Estrai tutto**. Dopo l'estrazione dei file, è necessario che i progetti seguenti siano installati nel computer:  
  
    -   Lezione 1 completa  
  
    -   Lezione 2 completa  
  
    -   Lezione 3 completa  
  
    -   Lezione 4 completa  
  
    -   Inizio della Lezione 4  
  
    -   Lezione 5 completa  
  
    -   Lezione 6 completa  
  
    -   Lezione 7 completa  
  
    -   Lezione 8 completa  
  
    -   Lezione 9 completa  
  
    -   Lezione 10 completa  
  
4.  Rimuovere le autorizzazioni di sola lettura per questi file. Fare clic con il pulsante destro del mouse sulla cartella padre, "Analysis Services Tutorial SQL Server 2012", selezionare **Proprietà**e quindi deselezionare la casella di controllo **Sola lettura**. Fare clic su **OK**. Applicare le modifiche a questa cartella, alle sottocartelle e ai file.  
  
5.  Avviare [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
6.  Aprire il file della soluzione (con estensione sln) che corrisponde alla lezione utilizzata. Ad esempio, nella cartella denominata "Lezione 1 completa", viene aperto il file Analysis Services Tutorial.sln.  
  
7.  Distribuire la soluzione per verificare che le autorizzazioni per il database e le informazioni di percorso del server siano impostate correttamente.  
  
     Se Analysis Services e il motore di database sono installati come istanza predefinita (MSSQLServer) e tutti i programmi software sono in esecuzione nello stesso computer, è possibile fare clic su **Distribuisci soluzione** nel menu Compila per compilare e distribuire il progetto di esempio nell'istanza locale di Analysis Services. Durante la distribuzione, i dati verranno elaborati o importati dal database **AdventureWorksDW2012** nell'istanza locale del motore di database. Verrà creato un nuovo database di Analysis Services nell'istanza di Analysis Services contenente i dati recuperati dal motore di database.  
  
     Se si rilevano errori, rivedere i passaggi precedenti relativi all'impostazione delle autorizzazioni per il database. Inoltre, potrebbe anche essere necessario modificare i nomi dei server. Il nome del server predefinito è localhost. Se i server sono installati in computer remoti o come istanze denominate, è necessario eseguire l'override del valore predefinito per utilizzare un nome di server valido per l'installazione. Inoltre, se i server si trovano in computer remoti, potrebbe essere necessario configurare Windows Firewall per consentire l'accesso ai server.  
  
     Il nome del server per la connessione al motore di database è specificato nell'oggetto di origine dati della soluzione multidimensionale (esercitazione di AdventureWorks), visibile in Esplora soluzioni.  
  
     Il nome del server per la connessione ad Analysis Services è specificato nella scheda Distribuzione delle pagine delle proprietà del progetto, visibile anche in Esplora soluzioni.  
  
8.  Avviare SQL Server Management Studio. In SQL Server Management Studio connettersi ad Analysis Services. Verificare che nel server sia in esecuzione un database denominato **Analysis Services Tutorial**.  
  
## <a name="next-step"></a>Passaggio successivo  
 È ora possibile avviare l'esercitazione. Per altre informazioni introduttive, vedere [Modellazione multidimensionale &#40;esercitazione di AdventureWorks&#41;](../analysis-services/multidimensional-modeling-adventure-works-tutorial.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Installare SQL Server 2014 dall'installazione guidata di &#40;programma di installazione&#41;](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)   
 [Configure the Windows Firewall to Allow Analysis Services Access](instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)   
 [Configurare Windows Firewall per consentire l'accesso a SQL Server](../../2014/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)  
  
  
