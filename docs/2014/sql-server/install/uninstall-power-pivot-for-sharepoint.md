---
title: Disinstallare PowerPivot per SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 3941a2f0-0d0c-4d1a-8618-7a6a7751beac
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 9397dd268d767fd8c4bad9056455c21b9be65398
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52769773"
---
# <a name="uninstall-powerpivot-for-sharepoint"></a>Disinstallare PowerPivot per SharePoint
  La disinstallazione di [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] è un'operazione che prevede più passaggi, tra cui la preparazione per la disinstallazione e la rimozione di funzionalità e soluzioni dalla farm, nonché di file di programma e impostazioni del Registro di sistema.  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2013 | SharePoint 2010  
  
 **Contenuto dell'argomento:**  
  
-   [Prerequisiti](#prereq)  
  
-   [Passaggio 1: Elenco di controllo per la pre-disinstallazione](#bkmk_before)  
  
-   [Passaggio 2: Rimuovere funzionalità e soluzioni da SharePoint](#bkmk_remove)  
  
-   [Passaggio 3: Eseguire il programma di installazione SQL Server per rimuovere programmi dal Computer locale](#bkmk_uninstall)  
  
-   [Passaggio 4: Disinstallare PowerPivot per componente aggiuntivo per SharePoint](#bkmk_addin)  
  
-   [Passaggio 5: Verificare la disinstallazione](#verify)  
  
-   [Passaggio 6: Elenco di controllo per la post-disinstallazione](#bkmk_post)  
  
##  <a name="prereq"></a> Prerequisiti  
  
-   È necessario essere un amministratore della farm di SharePoint o dell'applicazione di servizio per disinstallare le funzionalità e le soluzioni della farm.  
  
-   È necessario essere amministratore di sistema di SQL Server e membro del gruppo Administrators locale se si disinstalla anche il motore di database.  
  
-   È necessario essere amministratore di sistema di Analysis Services e membro del gruppo Administrators locale per disinstallare Analysis Services e [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)].  
  
##  <a name="bkmk_before"></a> Passaggio 1: Elenco di controllo per la pre-disinstallazione  
 L'accesso ai dati PowerPivot verrà disabilitato dopo la rimozione dalla farm del software che supporta l'elaborazione di dati e query. È innanzitutto necessario eliminare in modalità preemptive i file e le librerie che non saranno più operativi. In questo modo, sarà possibile affrontare eventuali problemi relativi a dati mancanti prima della disinstallazione del software.  
  
1.  Eliminare le librerie, i documenti e le cartelle di lavoro di PowerPivot associati a un'installazione di PowerPivot per SharePoint. Né le librerie, né i documenti funzioneranno dopo la disinstallazione del software.  
  
    -   [Eliminare la raccolta PowerPivot](../../analysis-services/power-pivot-sharepoint/delete-power-pivot-gallery.md)  
  
    -   [Eliminare una libreria di feed di dati PowerPivot](../../analysis-services/power-pivot-sharepoint/delete-a-power-pivot-data-feed-library.md)  
  
2.  Eliminare le cartelle di lavoro di Excel o i report di Reporting Services in altre librerie che contengono o fanno riferimento a dati PowerPivot.  
  
3.  Rimuovere eventuali web part in un dashboard di PerformancePoint che fanno riferimento a dati PowerPivot.  
  
4.  Rivedere le autorizzazioni di SharePoint per librerie e siti esistenti per determinare se è necessario apportarvi modifiche. Alcuni scenari di accesso ai dati PowerPivot, in particolare l'accesso ai dati secondario attraverso una stringa di connessione URL ai dati PowerPivot di un'altra cartella di lavoro, richiedono autorizzazioni di lettura superiori alle autorizzazioni di visualizzazione che vengono in genere assegnate agli utenti di SharePoint che visitano un sito. Se non sono più necessarie le autorizzazioni di lettura, è possibile ridurre le autorizzazioni di conseguenza.  
  
5.  Facoltativamente, arrestare i servizi e attendere alcuni giorni prima di disinstallare il software. Questo passaggio non è necessario per la disinstallazione, tuttavia consente di riprendere temporaneamente il servizio mentre si tenta di risolvere i problemi di sostituzione della tecnologia e di migrazione dei dati non ancora affrontati.  
  
##  <a name="bkmk_remove"></a> Passaggio 2: Rimuovere funzionalità e soluzioni da SharePoint  
 Utilizzare lo strumento di configurazione PowerPivot per rimuovere i servizi e le applicazioni PowerPivot da SharePoint.  
  
-   È necessario essere amministratore di farm, amministratore del server nell'istanza di Analysis Services e **db_owner** nel database di configurazione della farm.  
  
-   Utilizzare la versione dello strumento di configurazione appropriata per la versione di SharePoint. Non utilizzarlo con installazioni di [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] .  
  
-   Verificare che il servizio Amministrazione SharePoint sia in esecuzione.  
  
1.  **Eseguire lo strumento di configurazione:** Gli strumenti di configurazione sono elencati solo quando [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] è installato nel server locale. Nel **avviare** dal menu **tutti i programmi**, fare clic su [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], fare clic su **strumenti di configurazione**e quindi fare clic su uno dei seguenti:  
  
    -   **PowerPivot per SharePoint 2013**  
  
    -   **Strumento di configurazione PowerPivot**  
  
2.  Selezionare **Rimuovi funzionalità, servizi, applicazioni e soluzioni** , quindi fare clic su **OK**.  
  
3.  È possibile espandere completamente la finestra. Nella parte inferiore della finestra dovrebbe essere disponibile una barra contenente i comandi **Convalida**, **Esegui**ed **Esci** .  
  
4.  Esaminare ogni azione nell'elenco attività per capirne lo scopo.  
  
     In **Rimuovere le applicazioni del servizio PowerPivot**è disponibile l'opzione per eliminare i dati applicazione associati all'applicazione del servizio. I dati applicazione sono un database di SQL Server creato con l'applicazione del servizio allo scopo di archiviare le pianificazioni dell'aggiornamento dati, le informazioni dell'istanza di database, i dati di utilizzo e altri dati utilizzati da PowerPivot per SharePoint. Non vengono archiviati i file utente, ad esempio le cartelle di lavoro di PowerPivot. A meno che non sia necessario mantenere i dati dell'applicazione (ad esempio se vengono applicati criteri di memorizzazione dei dati correlati al loro aggiornamento o accesso), è possibile eliminare il database dell'applicazione senza rimuovere i file creati o salvati dagli utenti di SharePoint.  
  
     Per eliminare il database, selezionare **Rimuovere le applicazioni del servizio PowerPivot** , quindi selezionare **Eliminare i dati dell'applicazione associati a questa applicazione del servizio**.  
  
5.  È possibile esaminare le informazioni dettagliate nella scheda **Output** o **Script** .  
  
     Nella scheda Output viene fornito un riepilogo delle azioni che saranno eseguite dallo strumento. Queste informazioni vengono salvate in file di log nel percorso:  
  
     `C:\Program Files\Microsoft SQL Server\120\Tools\PowerPivotTools\SPAddinConfiguration\Log`  
  
     Nella scheda Script sono visualizzati i cmdlet di PowerShell o i riferimenti ai file di script di PowerShell che verranno eseguiti dallo strumento.  
  
6.  Fare clic su **Convalida** per controllare la validità di ogni azione. Se **Convalida** non è disponibile, significa che tutte le azioni sono valide per il sistema.  
  
7.  Fare clic su **Esegui** per eseguire tutte le azioni valide per questa attività. L'opzione**Esegui** è disponibile solo dopo il superamento del controllo di convalida. Quando fa clic su **eseguire**, viene visualizzato l'avviso seguente, in cui si ricorda che le azioni vengono elaborate in modalità batch: "Tutte le impostazioni di configurazione contrassegnate come valide nello strumento verranno applicate alla farm di SharePoint. Continuare?"  
  
8.  Per continuare, scegliere **Sì** .  
  
 **Risoluzione degli errori:**  
  
 Nello strumento di configurazione è possibile visualizzare informazioni sull'errore nel riquadro dei parametri per ciascuna azione. Per i problemi correlati alla distribuzione o al ritiro della soluzione, verificare che il servizio Amministrazione SharePoint sia avviato. Tramite questo servizio vengono eseguiti i processi timer che attivano le modifiche della configurazione in una farm. Se il servizio non è in esecuzione, la distribuzione o il ritiro della soluzione avrà esito negativo. Gli errori persistenti indicano che un processo di distribuzione o ritiro esistente è già in coda e blocca ulteriori azioni da parte dello strumento di configurazione. È possibile utilizzare il comando PowerShell seguente per verificare che il servizio sia in esecuzione:  
  
```  
Get-Service | where {$_.displayname -like "*sharepoint* administration*"}  
```  
  
 Per trovare e rimuovere un processo di distribuzione o ritiro già in coda, effettuare le operazioni seguenti:  
  
1.  Per tutti gli altri errori, controllare i log ULS. Per altre informazioni, vedere [configurare e visualizzare i file di Log di SharePoint e la registrazione diagnostica &#40;PowerPivot per SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/configure-and-view-sharepoint-and-diagnostic-logging.md).  
  
2.  Avviare la shell di gestione SharePoint come amministratore, quindi eseguire il comando indicato di seguito per visualizzare i processi in coda:  
  
    ```  
    Stsadm -o enumdeployments  
    ```  
  
3.  Esaminare le distribuzioni esistenti per le informazioni seguenti: **Tipo di** è Retraction o Deployment, **File** è powerpivotwebapp. wsp o powerpivotfarm. wsp.  
  
4.  Per le distribuzioni o i ritiri correlati alle soluzioni PowerPivot, copiare il valore GUID per **JobId** e quindi incollarlo nel comando seguente (utilizzare i comandi Contrassegna, copia e Incolla nel menu Modifica della Shell per copiare il GUID):  
  
    ```  
    Stsadm -o canceldeployment -id "<GUID>"  
    ```  
  
5.  Riprovare l'attività nello strumento di configurazione facendo clic su **Convalida** , quindi su **Esegui**.  
  
 In alternativa, è possibile utilizzare PowerShell per rimuovere funzionalità e soluzioni dalla farm. Per altre informazioni, vedere [informazioni di riferimento di PowerShell per PowerPivot per SharePoint](/sql/analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint).  
  
##  <a name="bkmk_uninstall"></a> Passaggio 3: Eseguire il programma di installazione SQL Server per rimuovere programmi dal Computer locale  
 L'eliminazione dei file di programma richiede l'esecuzione del programma di installazione di SQL Server per disinstallare il software. La disinstallazione consente di rimuovere sia file sia le voci del Registro di sistema creati dal programma di installazione. È possibile utilizzare la pagina Programmi e funzionalità per disinstallare il software. Un'installazione di [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] fa parte di un'installazione di SQL Server.  
  
 È possibile disinstallare parte dell'installazione senza conseguenze per le altre istanze di SQL Server (o funzionalità nella stessa istanza) già installate. È ad esempio possibile disinstallare PowerPivot per SharePoint lasciando installati altri componenti come [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o il motore di database.  
  
1.  Selezionare **Microsoft SQL Server 2014 (64 bit)** nell'elenco dei programmi.  
  
2.  Fare clic su **Disinstalla/Cambia**.  
  
3.  Scegliere **Rimuovi**. Verrà avviato il programma di installazione di SQL Server.  
  
     Nel programma di installazione è possibile selezionare l'istanza di **PowerPivot** , quindi scegliere **Analysis Services** e **Integrazione Analysis Services SharePoint** per rimuovere solo quella funzionalità, senza toccare il resto.  
  
##  <a name="bkmk_addin"></a> Passaggio 4: Disinstallare PowerPivot per componente aggiuntivo per SharePoint  
 Se la distribuzione di [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] dispone di due o più server ed è stato installato il componente aggiuntivo [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] , disinstallare il componente aggiuntivo [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] da ogni server in cui è stato installato per disinstallare completamente tutti i file di [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] . Per altre informazioni, vedere [installare o disinstallare PowerPivot per SharePoint Add-in &#40;SharePoint 2013&#41;](../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md).  
  
##  <a name="verify"></a> Passaggio 5: Verificare la disinstallazione  
  
1.  In **Gestisci servizi nel server**di Amministrazione centrale connettersi al server da cui è stato disinstallato PowerPivot per SharePoint.  
  
2.  -   Se è stato disinstallato [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013, verificare che **Servizio di sistema SQL Server PowerPivot** non sia più presente nell'elenco.  
  
    -   Se è stato disinstallato [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010, verificare che **SQL Server Analysis Services** e **Servizio di sistema SQL Server PowerPivot** non siano più presenti nell'elenco.  
  
3.  Dopo la disinstallazione dell'ultimo server PowerPivot per SharePoint nella farm, effettuare le operazioni seguenti:  
  
    1.  In Gestione applicazioni verificare in **Gestisci applicazioni di servizio**che l'applicazione del servizio PowerPivot non sia più presente nell'elenco.  
  
    2.  In Impostazioni sistema, verificare in **Gestisci funzionalità farm**che Funzionalità di integrazione PowerPivot non sia più presente nella pagina. In **Gestisci soluzioni farm**verificare che le soluzioni PowerPivot non siano più presenti nella pagina.  
  
    3.  In **Configura registrazione diagnostica** e **Configura raccolta dati di utilizzo e integrità**di Monitoraggio verificare che gli eventi e le categorie di eventi PowerPivot non siano più visualizzati.  
  
    4.  In Impostazioni generali applicazione verificare che **Dashboard di gestione PowerPivot** non sia più presente nella pagina.  
  
##  <a name="bkmk_post"></a> Passaggio 6: Elenco di controllo per la post-disinstallazione  
 Utilizzare l'elenco seguente per rimuovere il software e i file che non sono stati eliminati durante la disinstallazione.  
  
1.  Eliminare tutti i file di dati e le sottocartelle da `C:\Program Files\Microsoft SQL Server\MSAS12.PowerPivot`, quindi eliminare la cartella. Durante questo passaggio vengono anche eliminati i file precedentemente memorizzati nella cache nella directory DATA.  
  
2.  Eliminare le librerie, i documenti e le cartelle di lavoro di PowerPivot se non è ancora stato fatto.  
  
    -   [Eliminare la raccolta PowerPivot](../../analysis-services/power-pivot-sharepoint/delete-power-pivot-gallery.md)  
  
    -   [Eliminare una libreria di feed di dati PowerPivot](../../analysis-services/power-pivot-sharepoint/delete-a-power-pivot-data-feed-library.md)  
  
3.  Nel servizio di archiviazione sicura eliminare eventuali applicazioni di destinazione contenenti le credenziali archiviate utilizzate da PowerPivot per SharePoint. Alcune voci, ma non tutte, del servizio di archiviazione sicura vengono eliminate quando si disinstalla PowerPivot per SharePoint. Le applicazioni di destinazione create per l'account di aggiornamento dati automatico PowerPivot, più eventuali applicazioni di destinazione create per l'aggiornamento dati sono ancora presenti ed è quindi necessario eliminarle manualmente.  
  
     Al contrario, le singole applicazioni di destinazione generate automaticamente dal servizio di sistema PowerPivot vengono eliminate automaticamente alla disinstallazione di PowerPivot.  
  
4.  Nel Pannello di controllo fare clic su **Programmi**, quindi scegliere **Disinstalla un programma** . Disinstallare eventuali librerie client di Analysis Services non più utilizzate. Analysis Services ADOMD.NET e Microsoft SQL Server Analysis Management Objects non vengono rimossi quando si disinstalla PowerPivot per SharePoint. Poiché le librerie potrebbero essere utilizzate da altri programmi in cui sono utilizzati i dati Analysis Services, non vengono disinstallate automaticamente. È necessario disinstallare le librerie client singolarmente se non sono più necessarie.  
  
     Non disinstallare il componente aggiuntivo SQL Server Reporting Services per Prodotti SharePoint 2010 a meno che non si stiano seguendo le istruzioni relative all'installazione o alla risoluzione dei problemi seguenti in cui viene esplicitamente indicato di disinstallarlo. Il componente aggiuntivo Reporting Services viene utilizzato da Access Services. Viene installato dall'Utilità preparazione prodotti SharePoint e deve essere presente nel sistema per garantire il supporto delle funzionalità richieste da SharePoint.  
  
     Non disinstallare il provider OLE DB di Analysis Services. Il provider OLE DB viene installato come prerequisito delle cartelle di lavoro di Excel tramite cui viene effettuata la connessione ai database di Analysis Services. [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] viene installata una nuova versione compatibile con le versioni precedenti, pertanto è necessario lasciarla nel sistema per evitare futuri problemi di connessione dati.  
  
## <a name="see-also"></a>Vedere anche  
 [Installare o disinstallare PowerPivot per il componente aggiuntivo SharePoint &#40;SharePoint 2013&#41;](../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)   
 [Strumenti di configurazione PowerPivot](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md)  
  
  
