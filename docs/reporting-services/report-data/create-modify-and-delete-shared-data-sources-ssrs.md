---
title: Creare, modificare ed eliminare origini dati condivise | Microsoft Docs
ms.date: 05/24/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
helpviewer_keywords:
- modifying data source properties
- shared data sources [Reporting Services]
- removing shared data sources
- roles [Reporting Services], shared data sources
- data sources [Reporting Services], shared
- data sources [Reporting Services], modifying properties
- deleting shared data sources
ms.assetid: 1e58c1c2-5ecf-4ce6-9d04-0a8acfba17be
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 3cb8f79b892b639e618143fd138920650fb5cfda
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "77081822"
---
# <a name="create-modify-and-delete-shared-data-sources-ssrs"></a>Creare, modificare ed eliminare origini dati condivise (SSRS)
  Un'origine dati condivisa è un set di proprietà di connessione dell'origine dati a cui è possibile fare riferimento in più report, modelli e sottoscrizioni guidate dai dati in esecuzione su un server di report [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  Le origini dei dati condivise rappresentano una soluzione semplice per gestire proprietà dell'origine dati soggette a frequenti modifiche. Se un account utente o una password viene modificata o se si sposta il database in un server diverso, è possibile aggiornare le informazioni di connessione da una posizione centralizzata.  
  
 Le origini dei dati condivise sono facoltative per i report e le sottoscrizioni guidate dai dati, ma obbligatorie per i modelli di report. Se si intende utilizzare modelli di report per il reporting ad hoc, è necessario creare e gestire un'origine dei dati condivisa per fornire al modello le informazioni di connessione.  
  
 Un'origine dei dati condivisa è costituita dalle seguenti parti:  
  
|Parte|Descrizione|  
|----------|-----------------|  
|Nome|Un nome che identifica l'elemento all'interno della gerarchia di cartelle del server di report.|  
|Descrizione|Una descrizione che viene visualizzata con l'elemento nel portale Web quando viene visualizzato il contenuto della cartella.|  
|Tipo di connessione|L'estensione per l'elaborazione dati utilizzata con l'origine dati. È possibile utilizzare solo estensioni per l'elaborazione dati distribuite sul server di report. Per altre informazioni sulle estensioni per l'elaborazione dati incluse in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], vedere [Origini dati supportate da Reporting Services &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md).|  
|Stringa di connessione|La stringa di connessione per il database. Per altre informazioni e per visualizzare esempi di stringhe di connessione alle origini dati più frequenti, vedere [Creare stringhe di connessione dati - Generatore report e SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md).|  
|Tipo di credenziali|Specifica in che modo vengono ottenute le credenziali per la connessione e se devono essere utilizzate quando viene stabilita la connessione. Per altre informazioni, vedere [Specificare le credenziali e le informazioni sulla connessione per le origini dati del report](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md).|  
  
 Le origini dei dati condivise non contengono informazioni sulla query utilizzata per recuperare i dati. La query viene sempre mantenuta all'interno della definizione del report.  
  
## <a name="creating-and-modifying-shared-data-sources"></a>Creazione e modifica di origini dati condivise  
 Per creare un'origine dati condivisa o modificarne le proprietà, è necessario avere le autorizzazioni **Gestione di origini dei dati** sul server di report. Se il server di report viene eseguito in modalità nativa, è possibile creare e configurare l'origine dati condivisa nel portale Web. Se il server di report viene eseguito in modalità integrata SharePoint, è possibile utilizzare le pagine dell'applicazione su un sito di SharePoint. Per qualsiasi server di report, indipendentemente dalla modalità, è possibile creare un'origine dei dati condivisa in Progettazione report e pubblicarla su un server di destinazione.  
  
 Dopo avere creato un'origine dei dati condivisa sul server di report, è possibile creare assegnazioni di ruolo per controllarne l'accesso, spostarla in un percorso diverso, rinominarla o disconnetterla per impedire l'elaborazione dei report durante l'esecuzione di operazioni di manutenzione sull'origine dati esterna. Se si rinomina un'origine dei dati condivisa o la si sposta in una posizione diversa nella gerarchia di cartelle del server di report, vengono di conseguenza aggiornate le informazioni sul percorso in tutti i report e sottoscrizioni che fanno riferimento all'origine dei dati condivisa. Se l'origine dei dati condivisa è offline, tutti i report, i modelli e le sottoscrizioni non verranno eseguite finché l'origine dati non viene nuovamente abilitata.  
  
 Per altre informazioni sul controllo dell'accesso alle origini dati condivise nella gerarchia delle cartelle del server di report, vedere [Proteggere le origini dei dati condivise](../../reporting-services/security/secure-shared-data-source-items.md).  
  
 **Per creare un'origine dati condivisa in Progettazione report**  
  
1.  Nel riquadro dei dati del report fare clic su **Nuova** nella barra degli strumenti, quindi su **Origine dati**. Verrà visualizzata la finestra di dialogo **Proprietà origine dati** .  
  
    > [!NOTE]  
    >  Se il riquadro Dati report non è visualizzato, scegliere **Dati report** dal menu **Visualizza** .  
  
2.  Nella casella di testo **Nome** digitare un nome per l'origine dati oppure accettare quello predefinito. Il nome dell'origine dati viene utilizzato internamente nell'ambito del report. Per maggiore chiarezza è consigliabile assegnare all'origine dati un nome che includa il nome del database specificato nella stringa di connessione.  
  
3.  Verificare che l'opzione **Usa riferimento a origine dei dati condivisa** sia selezionata e quindi eseguire queste operazioni.  
  
    1.  Fare clic su **Nuovo**. Nella finestra di dialogo **Proprietà origine dati condivisa** ed eseguire le operazioni descritte nei passaggi 2 e 3 per creare una nuova origine dati.  
  
    2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
         La nuova origine dati verrà visualizzata nella cartella Origini dati condivise in Esplora soluzioni.  
  
4.  Fare clic su **Credenziali**.  
  
     Specificare le credenziali da utilizzare per questa origine dati. Il tipo di credenziali supportato viene determinato dal proprietario dell'origine dati.  
  
 **Per creare un'origine dati condivisa nel portale Web**  
  
1.  Nel portale Web selezionare **Nuovo** > **Origine dati**. 
  
4.  Digitare un nome per l'elemento. Un nome deve includere almeno un carattere e deve iniziare con una lettera. È inoltre possibile utilizzare alcuni simboli, con l'esclusione degli spazi e dei caratteri ; ? : \@ & = + , $ / * < > | " /.  
  
5.  È possibile digitare facoltativamente una descrizione per offrire agli utenti informazioni sulla connessione.  
  
6.  Nell'elenco **Tipo di origine dati** specificare l'estensione per l'elaborazione dati usata per elaborare i dati dell'origine dati.  
  
7.  Per **Stringa di connessione**specificare la stringa usata dal server di report per la connessione all'origine dati. È consigliabile evitare di specificare credenziali nella stringa di connessione.  
  
     L'esempio seguente illustra una stringa di connessione usata per connettersi al database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] locale AdventureWorks2016:  
  
    ```  
    data source=<localservername>; initial catalog=AdventureWorks2016 
    ```  
  
8.  Per **Connetti tramite**specificare come verranno ottenute le credenziali quando il report è in esecuzione:  
  
    -   Se si vuole richiedere all'utente un nome di accesso e una password, fare clic su **Credenziali fornite dall'utente che esegue il report**. Per usare le credenziali immesse dall'utente come credenziali di Windows, fare clic su **Usa come credenziali di Windows per la connessione all'origine dei dati**. Se il nome utente e la password sono credenziali del database, non selezionare questa opzione.  
  
    -   Se si prevede di usare l'origine dati come origine dati condivisa con credenziali salvate gestite dal proprietario dell'origine dati o per i report che supportano le sottoscrizioni o altre operazioni pianificate, ad esempio la generazione della cronologia del report automatica, fare clic su **Credenziali archiviate in modo protetto nel server di report**. Se il server di database supporta la rappresentazione o la delega, selezionare **Rappresenta l'utente autenticato dopo che è stata stabilita una connessione all'origine dei dati**.  
  
    -   Se si vuole che le credenziali dell'utente che accede al report vengano passate dal server di report al server che ospita l'origine dati esterna, fare clic su **Sicurezza integrata di Windows**. In questo caso, all'utente non viene richiesto di digitare un nome utente o una password.  
  
    -   Se l'origine dati non usa credenziali (ad esempio, se l'origine dati è un file XML a cui si accede dal file system), fare clic su **Credenziali non necessarie**. È necessario specificare questo tipo di credenziali solo se l'operazione risulta valida per l'origine dati specifica. Se si seleziona questa opzione per un'origine dati che richiede l'autenticazione, la connessione non verrà stabilita. Se si seleziona questa opzione, assicurarsi inoltre di configurare l'account di esecuzione automatica che consente al server di report di connettersi agli altri computer per recuperare dati o file quando le credenziali utente non sono disponibili.  
  
         Per altre informazioni sulla configurazione delle credenziali, vedere [Specificare le credenziali e le informazioni sulla connessione per le origini dati del report](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md). Per altre informazioni sull'account di esecuzione automatica, vedere [Configurare l'account di esecuzione automatica &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).  
  
9. Fare clic sul pulsante **Test connessione** per convalidare la configurazione dell'origine dati.  
  
    > [!NOTE]  
    >  Il pulsante Test connessione non è supportato per il tipo di origine dati XML.  
  
10. Fare clic su **OK**.  
  
 **Per modificare un'origine dati condivisa nel portale Web**  
  
1.  Nel portale Web passare all'origine dati condivisa.  
  
2.  Selezionare i puntini di sospensione (...) nell'angolo superiore destro dell'origine dati condivisa > **Gestisci**.   

    Verrà visualizzata la pagina **Proprietà** .
  
3.  Modificare l'origine dati e fare clic su **Applica**.  
  
## <a name="deleting-shared-data-sources"></a>eliminazione di origini dati condivise  
 È possibile eliminare un'origine dei dati condivisa in modo analogo a quando si elimina un elemento qualsiasi dal server di report.  
  
 **Per eliminare un'origine dei dati condivisa**  
  
1. Nel portale Web passare all'origine dati condivisa.  
  
2.  Selezionare i puntini di sospensione (...) nell'angolo superiore destro dell'origine dati condivisa > **Gestisci**.    
    Verrà visualizzata la pagina **Proprietà** .
  
3. Fare clic su **Elimina**e quindi su **OK**.  
  
Quando si elimina un'origine dati condivisa, vengono disattivati tutti i report, i modelli o le sottoscrizioni guidate dai dati in cui viene usata. In assenza delle informazioni sulla connessione all'origine dati, gli elementi non verranno più eseguiti. Per attivare tali elementi, è necessario aprirli singolarmente ed eseguire le seguenti operazioni:  
  
-   Per i report e le sottoscrizioni guidate dai dati che fanno riferimento all'origine dei dati condivisa, è possibile specificare le informazioni sulla connessione all'origine dati nelle proprietà del report o nella sottoscrizione. In alternativa, è possibile selezionare una nuova origine dei dati condivisa che include i valori che si desidera utilizzare.  
  
-   Per i modelli e i report di Generatore report che utilizzano tale modello, è necessario specificare una nuova origine dei dati condivisa. I modelli ottengono le informazioni sulla connessione all'origine dati solo tramite origini dei dati condivise.  
  
 Non è prevista alcuna operazione di annullamento per l'eliminazione di un'origine dei dati condivisa. Se tuttavia si elimina accidentalmente un'origine dei dati condivisa, è possibile crearne una nuova utilizzando gli stessi valori di proprietà di quella eliminata. Sarà necessario aprire i singoli report, modelli e sottoscrizioni guidate dai dati per riassociare l'origine dei dati condivisa all'elemento in cui viene utilizzata, ma i report, i modelli e le sottoscrizioni continueranno a funzionare come in precedenza purché le proprietà dell'origine dati siano identiche a quelle precedenti.  
  
## <a name="importing-shared-data-sources"></a>Importazione di origini dati condivise  

**Per importare un'origine dati esistente in Progettazione report**  
  
1.  In Esplora soluzioni fare clic con il pulsante destro del mouse sulla cartella **Origini dati condivise** nel progetto del server report e quindi scegliere **Aggiungi elemento esistente**. Verrà visualizzata la finestra di dialogo **Aggiungi elemento esistente** .  
  
2.  Passare a un file relativo all'origine dati condivisa della definizione del report (con estensione rds) esistente e quindi fare clic su **Apri**.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="shared-data-sources-in-sharepoint"></a>Origini dati condivise in SharePoint  
 Quando si esegue un report da una raccolta di SharePoint, le informazioni di connessione possono essere definite all'interno del report o in un file esterno collegato al report. Se le informazioni di connessione sono incorporate nel report, si parlerà di origine dati personalizzata. Se le informazioni di connessione sono definite in un file esterno, si parlerà di origine dati condivisa. Il file esterno può essere un file dell'origine dei dati del server di report (con estensione rsds) o un file di connessione dati (con estensione odc).  
  
 Un file rsds è simile a un file rds, ma dispone di uno schema diverso. Per creare un file rsds, è possibile pubblicare un file rds da Progettazione report o Progettazione modelli in una raccolta di SharePoint. Dal file rds originale verrà creato un nuovo file rsds. In alternativa, è possibile creare un nuovo file nella raccolta di un sito di SharePoint.  
  
 Dopo avere creato o pubblicato un'origine dei dati condivisa, è possibile modificare le proprietà di connessione o eliminare il file nel caso non venga più utilizzato. Prima di eliminare un'origine dei dati condivisa, è necessario verificare se viene utilizzata da report e modelli di report. A tale scopo, visualizzare gli elementi dipendenti che fanno riferimento all'origine dei dati condivisa.  
  
 L'elenco degli elementi dipendenti, tuttavia, indica se viene fatto riferimento all'origine dei dati condivisa, ma non se quest'ultima viene utilizzata attivamente. Per determinare se l'origine dati condivisa o il modello viene utilizzato attivamente, è possibile esaminare i file di registro sul server di report. Se non si dispone dell'accesso ai file di log o se tali file non contengono le informazioni desiderate, provare a spostare il report in una cartella inaccessibile mentre se ne determina lo stato effettivo.  
  
 **Per creare un'origine dati condivisa (file RSDS) (SharePoint 2010)**  
  
1.  Nella barra multifunzione della libreria fare clic sulla scheda **Documenti** .  
  
2.  Scegliere **Origine dati report** dal menu **Nuovo documento**.  
  
    > [!NOTE]  
    >  Se la voce **Origine dati report** non compare nel menu, il tipo di contenuto dell'origine dati del report non è stato abilitato. Per altre informazioni, vedere [Aggiungere i tipi di contenuto di Reporting Services a una raccolta di SharePoint](../../reporting-services/report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md).  
  
3.  In **Nome**immettere un nome descrittivo per il file con estensione rsds.  
  
4.  Scegliere il tipo di origine dati dall'elenco **Tipo di origine dati**. Per altre informazioni, vedere [Origini dati supportate da Reporting Services &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md).  
  
5.  In **Stringa di connessione**specificare un puntatore all'origine dati e qualsiasi altra impostazione necessaria per stabilire una connessione all'origine dati esterna. La sintassi della stringa di connessione è determinata dal tipo di origine dei dati che si sta utilizzando. Per altre informazioni ed esempi, vedere [Creare stringhe di connessione dati - Generatore report e SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md).  
  
6.  In **Credenziali**specificare la modalità con cui il server di report ottiene le credenziali per l'accesso all'origine dati esterna. Le credenziali possono essere archiviate, richieste al momento dell'esecuzione, integrate o configurate per l'elaborazione automatica del report.  
  
    -   Selezionare **Autenticazione di Windows (integrata)** se si vuole accedere ai dati usando le credenziali dell'utente che ha aperto il report. Non selezionare questa opzione se il sito o la farm di SharePoint utilizza l'autenticazione basata su form o si connette al server di report tramite un account attendibile. Non selezionare questa opzione se si desidera pianificare una sottoscrizione o l'elaborazione di dati per il report. È consigliabile utilizzare questa opzione quando per il dominio è abilitata l'autenticazione Kerberos oppure quando l'origine dei dati si trova nello stesso computer del server di report. Se l'autenticazione Kerberos non è attivata, le credenziali di Windows possono essere passate a un solo altro computer. Ciò significa che se l'origine dei dati esterna è in un altro computer, e richiede pertanto una connessione aggiuntiva, al posto dei previsti verrà restituito un errore.  
  
    -   Selezionare **Richiedi credenziali** se si vuole che l'utente immetta le proprie credenziali ogni volta che esegue il report. Non selezionare questa opzione se si desidera pianificare una sottoscrizione o l'elaborazione di dati per il report.  
  
    -   Selezionare **Credenziali archiviate** se si preferisce accedere ai dati usando un unico set di credenziali. Le credenziali vengono crittografate prima dell'archiviazione. È possibile selezionare opzioni che determinano la modalità di autenticazione delle credenziali archiviate. Selezionare Usa come credenziali di Windows se le credenziali archiviate appartengono all'account utente di Windows. Selezionare **Imposta contesto di esecuzione sull'account seguente** se si vuole impostare il contesto di esecuzione sul server di database. Nei database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] questa opzione consente di impostare la funzione SETUSER. Per altre informazioni, vedere [SETUSER &#40;Transact-SQL&#41;](../../t-sql/statements/setuser-transact-sql.md).  
  
    -   Selezionare **Credenziali non necessarie** se si preferisce specificare le credenziali nella stringa di connessione o eseguire il report usando un account con privilegi minimi configurato nel server di report. Se questo account non è configurato nel server di report, verrà visualizzato un messaggio di richiesta delle credenziali ed eventuali operazioni pianificate definite per il report non verranno eseguite.  
  
7.  Selezionare **Abilita questa origine dati** se si vuole che l'origine dati sia attiva. Se l'origine dati è configurata, ma non attiva, verrà visualizzato un messaggio di errore quando si tenta di utilizzare un report basato sull'origine dati.  
  
8.  Fare clic sul pulsante **Test connessione** per convalidare la configurazione dell'origine dati.  
  
    > [!NOTE]  
    >  Il pulsante Test connessione non è supportato per il tipo di origine dati XML.  
  
9. Fare clic su **OK** per salvare l'origine dati condivisa.  
  
 **Per eliminare il file rsds dell'origine dei dati condivisa**  
  
1.  Aprire la raccolta che contiene il file rsds.  
  
2.  Posizionare il puntatore del mouse sull'origine dei dati condivisa.  
  
3.  Fare clic per visualizzare una freccia verso il basso e quindi selezionare **Elimina**.  
  
 Se si elimina accidentalmente un'origine dei dati condivisa che invece si desidera conservare, è possibile crearne una nuova contenente le stesse informazioni di connessione. Dopo avere ricreato l'origine dati condivisa, è necessario aprire tutti i report e i modelli che la utilizzano, quindi selezionarla. Il nome, le credenziali o la sintassi della stringa di connessione della nuova origine dati possono essere diversi da quelli dell'origine dati eliminata. Le proprietà dell'origine dati possono avere valori diversi da quelli originali, purché la connessione venga risolta nella stessa origine dati.  
  
 Quando si elimina un modello di report è necessario prestare molta attenzione. Se si elimina un modello, non sarà più possibile aprire e modificare in Generatore report alcun report basato su tale modello. Se si elimina accidentalmente un modello utilizzato da report esistenti, sarà necessario rigenerare il modello, ricreare e salvare tutti i report che utilizzano il modello, quindi specificare di nuovo le impostazioni di sicurezza di tutti gli elementi del modello che si desidera utilizzare. Non è possibile rigenerare semplicemente il modello e collegarlo a un report esistente.  
  
## <a name="dependent-items"></a>Elementi dipendenti  
 Per visualizzare un elenco di report e modelli che utilizzano l'origine dati, aprire la pagina Elementi dipendenti relativa all'origine dei dati condivisa. È possibile accedere a questa pagina quando si apre l'origine dati nel portale Web o in una pagina dell'applicazione di SharePoint. Si noti che nella pagina Elementi dipendenti non vengono visualizzate le sottoscrizioni guidate dai dati. Se un'origine dei dati condivisa viene utilizzata da una sottoscrizione, questa non sarà inclusa nell'elenco degli elementi dipendenti.  
  
 **Per visualizzare elementi dipendenti in SharePoint**  
  
1.  Aprire la raccolta che contiene il file rsds.  
  
2.  Posizionare il puntatore del mouse sull'origine dei dati condivisa.  
  
3.  Fare clic per visualizzare una freccia verso il basso e quindi selezionare **Visualizza elementi dipendenti**.  
  
     Per i modelli di report, nell'elenco degli elementi dipendenti sono visualizzati i report creati in Generatore report. L'elenco degli elementi dipendenti relativo alle origini dei dati condivise può includere sia i report che i modelli di report.  
  
## <a name="see-also"></a>Vedere anche  
 [Creare stringhe di connessione dati - Generatore report e SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)   
 [Gestire origini dati dei report](../../reporting-services/report-data/manage-report-data-sources.md)   
 [Configurare le proprietà delle origini dati per un report](../../reporting-services/report-data/configure-data-source-properties-for-a-report-report-manager.md)  
  
  
