---
title: Installare Analysis Services dati e progetti di esempio | Microsoft Docs
ms.date: 05/06/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2c89ee3edf9338c4f74b0738d930ee74dbec7244
ms.sourcegitcommit: bcc3b2c7474297aba17b7a63b17c103febdd0af9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/05/2019
ms.locfileid: "68794985"
---
# <a name="install-sample-data-and-multidimensional-projects"></a>Installare dati di esempio e progetti multidimensionali 
[!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)]

Utilizzare le istruzioni e i collegamenti forniti in questo articolo per installare i file di dati e di progetto utilizzati nelle esercitazioni Analysis Services. 
  
## <a name="step-1-install-prerequisites"></a>Passaggio 1: Prerequisiti di installazione 
Nelle lezioni di questa esercitazione si presuppone che siano installati i programmi software seguenti: È possibile installare tutte le funzionalità di in un singolo computer. Per installare queste funzionalità, eseguire il programma di installazione di SQL Server e selezionarle dalla pagina Selezione funzionalità.  
  
-   Motore di database di SQL Server  
  
-   SQL Server Analysis Services  (SSAS) 
  
    Analysis Services è disponibile solo in queste edizioni: Evaluation, Enterprise, Business Intelligence, standard. I modelli multidimensionali non sono supportati in Azure Analysis Services.
  
    Per impostazione predefinita, Analysis Services 2016 e versioni successive viene installato come istanza tabulare, di cui è possibile eseguire l'override scegliendo modalità server multidimensionale nella pagina Configurazione server dell'installazione guidata.
  
## <a name="step-2-download-and-install-developer-and-management-tools"></a>Passaggio 2: Scaricare e installare gli strumenti di sviluppo e gestione
SQL Server Data Tools (SSDT) per Visual Studio vengono scaricati e installati separatamente dalle altre funzionalità di SQL Server. Le finestre di progettazione e i modelli di progetto usati per creare modelli e report di business intelligence sono inclusi in SSDT per Visual Studio 2015 o come [pacchetti NuGet](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects) per visual studio 2017.  
  
[Scaricare SQL Server Data Tools (SSDT)](http://go.microsoft.com/fwlink/?LinkID=827542).   

SQL Server Management Studio (SSMS) viene scaricato e installato separatamente dalle altre funzionalità di SQL Server.  

[Scaricare SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md)  

Se si desidera è possibile installare Excel per esplorare i dati multidimensionali man mano che si prosegue con l'esercitazione. L'installazione di Excel abilita la funzionalità **Analizza in Excel** che avvia Excel usando un elenco di campi della tabella pivot connesso al cubo che viene compilato. Si consiglia di utilizzare Excel per sfogliare i dati perché è possibile compilare rapidamente un report pivot che consente di interagire con i dati.  
  
In alternativa, è possibile esplorare i dati utilizzando la progettazione query MDX incorporata in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. La progettazione query restituisce gli stessi dati, ad eccezione di quelli presentati come un set di righe flat.  
  
## <a name="step-3-install-databases"></a>Passaggio 3: Installare i database  
In un modello multidimensionale di Analysis Services vengono utilizzati i dati transazionali importati da un sistema di gestione di database relazionali. Ai fini di questa esercitazione, viene utilizzato il database relazionale seguente come origine dati.  
  
-   **AdventureWorksDW2012 o versione successiva** : si tratta di un data warehouse relazionale eseguito in un'istanza di motore di database. Fornisce i dati originali usati dai database e dai progetti di Analysis Services compilati e distribuiti durante l'esercitazione. L'esercitazione presuppone che si usi AdventureWorksDW2012, tuttavia, le versioni successive funzionano.
  
    È possibile utilizzare questo database di esempio [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] con e versioni successive. In generale, è consigliabile usare la versione del database di esempio corrispondente alla versione del motore di database.
  
Per installare il database, eseguire le operazioni seguenti:  
  
1.  Scaricare un backup del database [AdventureWorksDW](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) da GitHub.  
  
2.  Copiare il file di backup nella directory dei dati dell'istanza locale di motore di database SQL Server.
  
3.  Avviare SQL Server Management Studio e connettersi all'istanza del motore di database.  
  
4.  Ripristinare il database.  
  
## <a name="step-4-grant-database-permissions"></a>Passaggio 4: GRANT-autorizzazioni per database  
Nei progetti di esempio vengono utilizzate impostazioni di rappresentazione dell'origine dati che specificano in quale contesto di sicurezza vengono importati o elaborati i dati. Per impostazione predefinita, le impostazioni di rappresentazione specificano l'account del servizio Analysis Services per l'accesso ai dati. Per usare questa impostazione predefinita, è necessario verificare che l'account di servizio con cui viene eseguito Analysis Services disponga delle autorizzazioni di lettura dati per il database **AdventureWorksDW** .  
  
> [!NOTE]  
> Ai fini dell'apprendimento, si consiglia di utilizzare l'opzione di rappresentazione dell'account del servizio predefinita e concedere autorizzazioni di lettura dei dati all'account del servizio in SQL Server. Anche se sono disponibili altre opzioni di rappresentazione, non tutte sono adatte per le operazioni di elaborazione. In particolare, l'opzione per l'utilizzo delle credenziali dell'utente corrente non è supportata per l'elaborazione.  
  
1.  Determinare l'account del servizio. È possibile utilizzare Gestione configurazione SQL Server o l'applicazione console Servizi per visualizzare le informazioni sull'account. Se Analysis Services è stato installato come istanza predefinita usando l'account predefinito, il servizio è in esecuzione come **NT Service\MSSQLServerOLAPService**.  
  
2.  In Management Studio connettersi all'istanza del motore di database.  
  
3.  Espandere la cartella Sicurezza, fare clic con il pulsante destro del mouse su Account di accesso e selezionare **Nuovo account di accesso**.  
  
4.  Nella pagina Generale in Nome account di accesso digitare **NT Service\MSSQLServerOLAPService** o un altro account usato per l'esecuzione del servizio.  
  
5.  Fare clic su **Mapping utenti**.  
  
6.  Selezionare la casella di controllo accanto al database **AdventureWorksDW** . L'appartenenza al ruolo deve includere automaticamente **db_datareader** e **public**. Fare clic su **OK** per accettare le impostazioni predefinite.  
  
## <a name="step-5-install-projects"></a>Passaggio 5: Installare i progetti  

Nell'esercitazione sono inclusi progetti di esempio per consentire il confronto dei risultati rispetto a un progetto finito o l'avvio di una lezione successiva nella sequenza.  
  
1.  Scaricare [Adventure-Works-Multidimensional-tutorial-Projects. zip](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks-analysis-services) dalla pagina di esempi di Adventure works per Analysis Services su GitHub.  
  
    I progetti dell'esercitazione funzionano [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] per e versioni successive.  
  
2.  Spostare il file con estensione zip in una cartella al livello immediatamente inferiore rispetto all'unità radice, ad esempio C:\Tutorial. Questo passaggio attenua l'errore "percorso troppo lungo" che talvolta si verifica se si tenta di decomprimere i file nella cartella Downloads.  
  
3.  Decomprimere i progetti di esempio: fare clic con il pulsante destro del mouse sul file e selezionare **Estrai tutto**. Dopo l'estrazione dei file, è necessario disporre delle cartelle lezione 1, 2, 3, 5, 6, 7, 8, 9, 10 completate e inizio lezione 4. 
  
4.  Rimuovere le autorizzazioni di sola lettura per questi file. Fare clic con il pulsante destro del mouse sulla cartella padre, scegliere **Proprietà**e deselezionare la casella di controllo di sola **lettura**. Fare clic su **OK**. Applicare le modifiche a questa cartella, alle sottocartelle e ai file.  

5.  Aprire il file di soluzione (con estensione sln) che corrisponde alla lezione in corso. Ad esempio, nella cartella denominata "Lezione 1 completa", viene aperto il file Analysis Services Tutorial.sln.  
  
6.  Distribuire la soluzione per verificare che le autorizzazioni del database e le informazioni sul percorso del server siano impostate correttamente.  
  
    Se Analysis Services e il motore di database sono installati come istanza predefinita (MSSQLServer) e tutti i programmi software sono in esecuzione nello stesso computer, è possibile fare clic su **Distribuisci soluzione** nel menu Compila per compilare e distribuire il progetto di esempio nell'istanza locale di Analysis Services. Durante la distribuzione, i dati vengono elaborati (o importati) dal database **AdventureWorksDW** nell'istanza di motore di database locale. Viene creato un nuovo Analysis Services database nell'istanza Analysis Services contenente i dati recuperati dal motore di database.  
  
    Se si rilevano errori, rivedere i passaggi precedenti relativi all'impostazione delle autorizzazioni per il database. Inoltre, potrebbe anche essere necessario modificare i nomi dei server. Il nome del server predefinito è localhost. Se i server sono installati in computer remoti o come istanze denominate, è necessario eseguire l'override del valore predefinito per utilizzare un nome di server valido per l'installazione. Inoltre, se i server si trovano in computer remoti, potrebbe essere necessario configurare Windows Firewall per consentire l'accesso ai server.  
  
    Il nome del server per la connessione al motore di database è specificato nell'oggetto di origine dati della soluzione multidimensionale (esercitazione di AdventureWorks), visibile in Esplora soluzioni.  
  
    Il nome del server per la connessione ad Analysis Services è specificato nella scheda Distribuzione delle pagine delle proprietà del progetto, visibile anche in Esplora soluzioni.  
  
7.  In SQL Server Management Studio connettersi ad Analysis Services. Verificare che nel server sia in esecuzione il database denominato **Analysis Services Tutorial** .  
  
## <a name="next-step"></a>Passaggio successivo  
È ora possibile avviare l'esercitazione. Per altre informazioni introduttive, vedere [Modellazione multidimensionale &#40;esercitazione di AdventureWorks&#41;](multidimensional-modeling-adventure-works-tutorial.md).  
  
## <a name="see-also"></a>Vedere anche  
[Configurare Windows Firewall per consentire l'accesso ad Analysis Services](../instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)  
[Configurare Windows Firewall per consentire l'accesso a SQL Server](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)  
  
  
