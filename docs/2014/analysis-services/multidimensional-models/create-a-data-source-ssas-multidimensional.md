---
title: Creare un'origine dati (SSAS multidimensionale) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.datasourcedesigner.f1
- sql12.asvs.sqlserverstudio.impersonationinfo.f1
- sql12.asvs.connectionmanager.f1
helpviewer_keywords:
- impersonation [Analysis Services]
- data sources [Analysis Services], creating
- security [Analysis Services], data source connections
ms.assetid: 9fab8298-10dc-45a9-9a91-0c8e6d947468
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d224c58651601bd18baf8e4aa79ece34a653d8c4
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2019
ms.locfileid: "70152902"
---
# <a name="create-a-data-source-ssas-multidimensional"></a>Crea un' origine dati (SSAS multidimensionale)
  In un modello multidimensionale di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] un oggetto di origine dati rappresenta una connessione all'origine dati dalla quale si elaborano o si importano dati. Un modello multidimensionale deve contenere almeno un oggetto di origine dati, tuttavia è possibile aggiungerne altri per combinare dati provenienti da diversi data warehouse. Utilizzare le istruzioni in questo argomento per creare un oggetto di origine dati per il modello. Per altre informazioni sull'impostazione delle proprietà per questo oggetto, vedere [Impostare le proprietà dell'origine dati &#40;SSAS multidimensionale&#41;](set-data-source-properties-ssas-multidimensional.md).  
  
 In questo argomento sono contenute le sezioni seguenti:  
  
 [Scegliere un provider di dati](#bkmk_provider)  
  
 [Impostare credenziali e opzioni di rappresentazione](#bkmk_impersonation)  
  
 [Visualizzare o modificare proprietà di connessione](#bkmk_ConnectionString)  
  
 [Creare un'origine dati con la Creazione guidata origine dati](#bkmk_steps)  
  
 [Creare un'origine dati utilizzando una connessione esistente](#bkmk_connection)  
  
 [Aggiungere più origini dati in un modello](#bkmk_multipleDS)  
  
##  <a name="bkmk_provider"></a> Scegliere un provider di dati  
 È possibile connettersi tramite un provider OLE DB nativo o [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework gestito. Il provider di dati consigliato per le origini dati SQL Server è SQL Server Native Client perché è quello che offre in genere le prestazioni migliori.  
  
 Per Oracle e altre origini dati di terze parti, verificare se viene offerto un provider OLE DB nativo e provarlo prima. Se si verificano errori, provare uno degli altri provider di dati .NET o i provider OLE DB nativi elencati in Gestione connessione. Assicurarsi che qualsiasi provider di dati utilizzato sia installato in tutti i computer utilizzati per sviluppare ed eseguire la soluzione [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
##  <a name="bkmk_impersonation"></a> Impostare credenziali e opzioni di rappresentazione  
 In una connessione all'origine dati può talvolta essere utilizzata l'autenticazione di Windows o un servizio di autenticazione fornito dal sistema di gestione di database, ad esempio l'autenticazione di SQL Server per la connessione ai database di SQL Azure. È necessario che l'account specificato disponga dell'accesso al server di database remoto e delle autorizzazioni di lettura sul database esterno.  
  
### <a name="windows-authentication"></a>Autenticazione di Windows  
 Le connessioni che usano l'autenticazione di Windows vengono specificate nella scheda **Impostazioni di rappresentazione** di Progettazione origine dati. Utilizzare questa scheda per scegliere l'opzione di rappresentazione che consente di specificare l'account utilizzato per l'esecuzione di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] durante la connessione all'origine dati esterna. Non tutte le opzioni possono essere utilizzare in tutti gli scenari. Per altre informazioni su queste opzioni e quando usarle, vedere [Impostare opzioni di rappresentazione &#40;SSAS - Multidimensionale&#41;](set-impersonation-options-ssas-multidimensional.md).  
  
### <a name="database-authentication"></a>Autenticazione del database  
 In alternativa all'autenticazione di Windows, è possibile specificare una connessione in cui si utilizza un servizio di autenticazione fornito dal sistema di gestione di database. In alcuni casi, è richiesto l'uso dell'autenticazione del database. Gli scenari che richiedono l'uso dell'autenticazione del database includono l'uso di SQL Server autenticazione per connettersi a un database SQL di Azure o l'accesso a un'origine dati relazionale in esecuzione in un sistema operativo diverso o in un dominio non trusted.  
  
 Per un'origine dati in cui si utilizza l'autenticazione del database, il nome utente e la password di un account di accesso al database vengono specificati nella stringa di connessione. Le credenziali vengono aggiunte alla stringa di connessione quando si inserisce un nome utente e una password in Gestione connessione durante l'impostazione della connessione all'origine dati nel modello di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Ricordarsi di specificare un'identità utente che disponga di autorizzazioni di lettura sui dati.  
  
 Durante il recupero dei dati, mediante la libreria client con cui si stabilisce la connessione viene formulata una richiesta di connessione per l'inclusione delle credenziali nella stringa di connessione. Le opzioni delle credenziali di autenticazione di Windows nella scheda Impostazioni di rappresentazione non vengono utilizzate nella connessione, ma possono essere usate per altre operazioni, ad esempio l'accesso a risorse sul computer locale. Per altre informazioni, vedere [Impostare opzioni di rappresentazione &#40;SSAS - Multidimensionale&#41;](set-impersonation-options-ssas-multidimensional.md).  
  
 Dopo il salvataggio dell'oggetto di origine dati nel modello, la stringa di connessione e la password vengono crittografate.  Per motivi di sicurezza, tutte le tracce visibili della password vengono rimosse dalla stringa di connessione quando viene successivamente visualizzata in strumenti, script o codice.  
  
> [!NOTE]  
>  Per impostazione predefinita, le password non vengono salvate da [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] con la stringa di connessione. Se la password non viene salvata, in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ne verrà richiesta l'immissione quando necessaria. Se si sceglie di salvare la password, questa viene archiviata in formato crittografato nella stringa di connessione dati. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] consente di crittografare le informazioni sulla password per le origini dati usando la chiave di crittografia del database che contiene l'origine dati. In presenza di informazioni di connessione crittografate, è necessario usare Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per modificare la password o l'account di servizio di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . In caso contrario, le informazioni crittografate non potranno essere recuperate. Per altre informazioni, vedere [Gestione configurazione SQL Server](../../relational-databases/sql-server-configuration-manager.md).  
  
### <a name="defining-impersonation-information-for-data-mining-objects"></a>Definizione delle impostazioni di rappresentazione per gli oggetti di data mining  
 Le query di data mining possono essere eseguite sia nel contesto dell'account di servizio di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] che nel contesto dell'utente che ha inviato la query o di un utente specificato. Il contesto in cui una query viene eseguita può influire sui risultati della query. Per operazioni di data mining di tipo `OPENQUERY`, può essere opportuno eseguire la query di data mining nel contesto dell'utente corrente o di un utente specificato (indipendentemente dall'utente che ha eseguito la query), anziché nel contesto dell'account di servizio. Ciò consente di eseguire la query con credenziali di sicurezza limitate. Per fare in modo che [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] rappresenti l'utente corrente o un utente specificato, selezionare l'opzione **Usa nome utente e password specifici** o **Usa credenziali dell'utente corrente** .  
  
##  <a name="bkmk_steps"></a> Creare un'origine dati con la Creazione guidata origine dati  
  
1.  In [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]aprire il progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o connettersi al database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in cui si desidera definire l'origine dei dati.  
  
2.  In **Esplora soluzioni**fare clic con il pulsante destro del mouse sulla cartella **Origini dati** e quindi scegliere **Nuova origine dati** per avviare la **Creazione guidata origine dati**.  
  
3.  Nella pagina **Selezione metodo di definizione connessione** fare clic su **Crea un'origine dati basata su una connessione nuova o esistente** e quindi fare clic su **Nuova** per aprire **Gestione connessione**.  
  
     Le nuove connessioni vengono create tramite Gestione connessione. In Gestione connessione è possibile selezionare un provider, quindi specificare le proprietà della stringa di connessione utilizzata per la connessione del provider ai dati sottostanti. Le informazioni esattamente necessarie dipendono dal provider selezionato, ma in genere includono un'istanza del server o del servizio, i dati per l'accesso a tale istanza, il nome di un database o un file e altre impostazioni specifiche del provider. Per la parte restante di questa procedura, si presuppone una connessione di database SQL Server.  
  
4.  Selezionare [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework o il provider OLE DB nativo da utilizzare per la connessione.  
  
     Il provider predefinito per una nuova connessione è il provider OLE DB nativo\\[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Questo provider viene usato per connettersi a un'istanza del motore di database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tramite OLE DB. Per le connessioni a un database relazionale SQL Server, l'utilizzo di OLE DB nativo\SQL Server Native Client 11.0 è spesso più veloce dell'utilizzo di provider alternativi.  
  
     È possibile scegliere un provider diverso per accedere ad altre origini dati. Per un elenco dei provider e dei database relazionali supportati da [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], vedere [Data Sources &#40;supported&#41;SSAS](supported-data-sources-ssas-multidimensional.md)Multidimensional.  
  
5.  Immettere le informazioni richieste dal provider selezionato per la connessione all'origine dei dati sottostante. In caso di selezione del provider **OLE DB nativo\SQL Server Native Client** , immettere le informazioni seguenti:  
  
    1.  **Nome server** è il nome di rete dell'istanza del motore di database. Può essere specificato come l'indirizzo IP, il nome NETBIOS del computer, o un nome di dominio completo. Se il server è installato come istanza denominata, è necessario includere il nome dell'istanza (ad esempio, \<nomecomputer >\\< NomeIstanza\>).  
  
    2.  **Accesso al server** specifica la modalità di autenticazione della connessione. **Usa autenticazione di Windows** consente di usare l'autenticazione di Windows. **Usa autenticazione SQL Server** specifica un account di accesso utente del database per un database SQL di Azure o un'istanza di SQL Server che supporta l'autenticazione in modalità mista.  
  
        > [!IMPORTANT]  
        >  La gestione connessione include una casella di controllo **Salva password** per le connessioni che usano l'autenticazione di SQL Server. Anche se la casella di controllo è sempre visibile, non viene sempre utilizzata.  
        >   
        >  Le condizioni in base alle quali in Analysis Services non viene utilizzata questa casella di controllo includono l'aggiornamento o l'elaborazione dei dati relazionali di SQL Server utilizzati in un database di Analysis Services attivo. Indipendentemente dal fatto che la casella di controllo **Salva password**venga selezionata o deselezionata, la password verrà sempre crittografata e salvata da Analysis Services. La password viene crittografata e archiviata nei file di dati e abf. Questo comportamento è dovuto al fatto che Analysis Services non supporta l'archiviazione nel server di password basate su sessione.  
        >   
        >  Questo comportamento riguarda unicamente i database che a) vengono resi persistenti in un'istanza del server Analysis Services e b) utilizzano l'autenticazione di SQL Server per aggiornare o elaborare i dati relazionali. Non si applica alle connessioni all'origine dati impostate in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] utilizzate unicamente per la durata di una sessione. Sebbene non sia in alcun modo possibile rimuovere una password già archiviata, è possibile utilizzare credenziali diverse o l'autenticazione di Windows per sovrascrivere le informazioni utente attualmente archiviate con il database.  
  
    3.  Per specificare il database viene usata l'opzione**Selezionare o immettere un nome di database** o **Associa file di database** .  
  
    4.  Sul lato sinistro della finestra di dialogo fare clic su **Tutte** per visualizzare le impostazioni aggiuntive per la connessione, incluse tutte le impostazioni predefinite del provider corrente.  
  
    5.  Modificare le impostazioni nel modo appropriato per l'ambiente in uso e quindi fare clic su **OK**.  
  
         La nuova connessione verrà visualizzata nel riquadro **Connessioni dati** della pagina **Selezione metodo di definizione connessione** della Creazione guidata origine dati.  
  
6.  Fare clic su **Avanti**.  
  
7.  In **Impostazioni di rappresentazione**specificare le credenziali di Windows o l'identità utente usata da Analysis Services al momento della connessione all'origine dati esterna. Se si utilizza l'autenticazione del database, queste impostazioni verranno ignorate ai fini della connessione.  
  
     Le linee guida per la scelta di un'opzione di rappresentazione variano a seconda della modalità di utilizzo dell'origine dati. Per le attività di elaborazione, al momento della connessione a un'origine dati è necessario che il servizio [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] venga eseguito nel contesto di sicurezza del relativo account di servizio o di un account utente specificato.  
  
    -   **Usa nome utente e password specifici di Windows** consente di specificare un set univoco di credenziali con privilegi minimi.  
  
    -   **Usa account del servizio** consente di elaborare i dati usando l'identità del servizio.  
  
     L'account specificato deve disporre delle autorizzazioni di lettura per l'origine dati.  
  
8.  Fare clic su **Avanti**.  In **Completamento procedura guidata**immettere il nome di un'origine dati o usare il nome predefinito. Il nome predefinito corrisponde a quello del database specificato nella connessione. Nel riquadro **Anteprima** verrà visualizzata la stringa di connessione per la nuova origine dati.  
  
9. Scegliere **Fine**.  La nuova origine dati verrà visualizzata nella cartella **Origini dati** in Esplora soluzioni.  
  
##  <a name="bkmk_connection"></a> Creare un'origine dati utilizzando una connessione esistente  
 In un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] l'origine dati può essere basata su un'origine dei dati esistente nella soluzione oppure su un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Nella Creazione guidata origine dati sono disponibili diverse opzioni per la creazione dell'oggetto di origine dati, incluso l'utilizzo di una connessione esistente nello stesso progetto.  
  
-   La creazione di un'origine dei dati basata su un'origine dei dati esistente nella soluzione consente di definire un'origine dei dati sincronizzata con l'origine dei dati esistente. Quando viene compilato il progetto contenente la nuova origine dei dati, vengono utilizzate le impostazioni dell'origine dei dati sottostante.  
  
-   La creazione di un'origine dati basata su un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] consente di fare riferimento a un altro progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] nella soluzione del progetto corrente. La nuova origine dei dati utilizza il provider MSOLAP con la relativa proprietà `Data Source` e la proprietà `Initial Catalog` acquisita dalle proprietà `TargetServer` e `TargetDatabase` del progetto selezionato. Questa funzionalità è utile nelle soluzioni in cui si utilizzano più progetti di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per gestire partizioni remote, in quanto i database di origine e di destinazione di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] richiedono le origini dei dati reciproche per supportare l'archiviazione e l'elaborazione delle partizioni remote.  
  
 Quando si fa riferimento a un oggetto di origine dei dati, è possibile modificare tale oggetto soltanto nel progetto o nell'oggetto di riferimento. Non è possibile modificare le informazioni di connessione nell'oggetto di origine dei dati contenente il riferimento. Le modifiche apportate alle informazioni di connessione nel progetto o nell'oggetto di riferimento vengono applicate alla nuova origine dei dati al momento della relativa compilazione. Le informazioni della stringa di connessione contenute nel file dell'origine dei dati ( con estensione ds) del progetto vengono sincronizzate quando si compila il progetto o quando si cancella il riferimento in Progettazione origine dati.  
  
##  <a name="bkmk_ConnectionString"></a> Visualizzare o modificare proprietà di connessione  
 La stringa di connessione viene formulata in base alle proprietà selezionate in Progettazione origine dati o nella nuova Creazione guidata origine dati. È possibile visualizzare la stringa di connessione e altre proprietà in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
 **Per modificare la stringa di connessione**  
  
1.  In [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]fare doppio clic sull'oggetto origine dati in Esplora soluzioni.  
  
2.  Nel pannello di navigazione sinistro fare clic su **Modifica**e quindi su **Tutto** .  
  
3.  Verrà visualizzata la griglia delle proprietà contenente le proprietà disponibili per il provider di dati in uso. Per ulteriori informazioni su tali proprietà, vedere la documentazione del prodotto relativa al provider.  Per SQL Server Native Client, vedere [Uso delle parole chiave delle stringhe di connessione con SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 Se si dispone di più oggetti origine dati nella soluzione e si preferisce mantenere la stringa di connessione in un posto, l'origine dati corrente può essere configurata in modo da fare riferimento all'altro oggetto di origine dati.  
  
 Un *riferimento all'origine dati* è un'associazione a un altro progetto o un'altra origine dati di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] nella stessa soluzione. I riferimenti consentono la sincronizzazione delle origini dei dati tra oggetti diversi di una soluzione. Le informazioni sulla stringa di connessione sono sincronizzate quando si compila il progetto. Per modificare la stringa di connessione per un'origine dati che fa riferimento a un altro oggetto, è necessario modificare la stringa di connessione dell'oggetto di riferimento.  
  
 È possibile rimuovere il riferimento deselezionando la casella di controllo. Questa operazione consente di interrompere la sincronizzazione tra oggetti e di modificare la stringa di connessione dell'origine dati.  
  
##  <a name="bkmk_multipleDS"></a> Aggiungere più origini dati in un modello  
 È possibile creare più di un oggetto di origine dati per supportare le connessioni a origini dati aggiuntive. Ogni origine dati deve disporre di colonne che sia possibile utilizzare per creare relazioni.  
  
> [!NOTE]  
>  Se vengono definite più origini dati e viene eseguita una singola query su dati di più origini, ad esempio per una dimensione con schema a fiocco di neve, è necessario definire un'origine dati in grado di supportare query remote tramite `OpenRowset`. Si tratterà in genere di un'origine dati di Microsoft SQL Server.  
  
 Tra i requisiti per l'utilizzo di più origini dati sono inclusi i seguenti:  
  
-   Impostare un'origine dati come origine dati primaria, ovvero quella che viene utilizzata per creare una vista origine dati.  
  
-   Un'origine dati primaria deve supportare la funzione `OpenRowset`.  Per altre informazioni su questa funzione in SQL Server, vedere <xref:Microsoft.SqlServer.TransactSql.ScriptDom.TSqlTokenType.OpenRowSet>.  
  
 Per combinare dati da più origini dati, utilizzare l'approccio seguente:  
  
1.  Creare l'origine dati nel modello.  
  
2.  Creare una vista origine dati utilizzando un database relazionale di SQL Server come origine dati. Questa è l'origine dati primaria.  
  
3.  Usando la vista origine dati creata in Progettazione vista origine dati, fare clic con il pulsante destro del mouse in un punto qualsiasi dell'area di lavoro e scegliere **Aggiungi/Rimuovi tabelle**.  
  
4.  Scegliere la seconda origine dati, quindi selezionare le tabelle che si desidera aggiungere.  
  
5.  Individuare e selezionare la tabella aggiunta. Fare clic con il pulsante destro del mouse sulla tabella e scegliere **Nuova relazione**. Scegliere le colonne di origine o di destinazione che contengono dati corrispondenti.  
  
## <a name="see-also"></a>Vedere anche  
 [Origini dati supportate &#40;SSAS Multidimensional&#41;](supported-data-sources-ssas-multidimensional.md)   
 [Viste origine dati in modelli multidimensionali](data-source-views-in-multidimensional-models.md)  
  
  
