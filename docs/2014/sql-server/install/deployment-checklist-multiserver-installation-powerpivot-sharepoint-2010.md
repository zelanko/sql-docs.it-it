---
title: 'Elenco di controllo per la distribuzione: installazione multiserver di PowerPivot per SharePoint 2010 | Microsoft Docs'
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 4380040a-1368-4a47-8930-47c65a192e59
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: ed0cd8bad3a99c7f1f59b5121aafb06ccdee63b2
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952237"
---
# <a name="deployment-checklist-multi-server-installation-of-powerpivot-for-sharepoint-2010"></a>Elenco di controllo per la distribuzione: installazione multiserver di PowerPivot per SharePoint 2010
  In questo elenco di controllo vengono illustrati i passaggi per aggiungere [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint a una farm di SharePoint 2010 a tre livelli compilata da zero. In una farm a tre livelli sono inclusi i livelli database, applicazione e Web. Per aggiungere [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] a questa topologia, è necessario eseguire SQL Server programma di installazione per installare [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] a livello di applicazione. I file di programma PowerPivot vengono aggiunti al livello Web, ma solo come attività post-installazione durante la distribuzione della soluzione applicazione Web. Anche se sono disponibili passaggi relativi alla distribuzione, non è necessario eseguire alcun passaggio di installazione separato nel livello Web o nel livello dati. L'unico passaggio di installazione che è necessario eseguire è l'installazione di [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] nei server applicazioni.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2010|  
  
  
  
## <a name="prerequisites"></a>Prerequisites  
 Per installare SQL Server e SharePoint 2010, è necessario essere un amministratore locale.  
  
 La persona che installa SharePoint deve configurare anche la farm. A tal fine, è necessario disporre di un account di accesso di SQL Server sul server di database. All'account di accesso devono essere assegnati i ruoli seguenti: `dbcreator`, `securityadmin` e `public`.  
  
 È necessario disporre della Enterprise o Enterprise Evaluation Edition di SharePoint Server 2010.  
  
 Il computer deve fare parte di un dominio.  
  
 È necessario conoscere gli account che verranno utilizzati per eseguire il motore di database, i servizi nella farm in uso e Analysis Services in modalità integrata SharePoint. Sebbene sia possibile modificare questi account in un secondo momento, verranno specificati per la prima volta durante l'installazione.  
  
 Gli account del servizio specificati durante l'installazione devono essere account utente di dominio.  
  
 Prima di iniziare l'installazione, controllare le impostazioni del browser per verificare che si disponga di una connessione Internet. Mediante il programma di installazione essenziale viene aperta una connessione Internet per scaricare il software obbligatorio. Per assicurarsi di ottenere il software obbligatorio completo, è necessario apportare le modifiche seguenti:  
  
-   In Server Manager disabilitare temporaneamente Sicurezza avanzata di Internet Explorer per consentire i download nel server. Ai fini del download del software obbligatorio, è possibile disabilitare Sicurezza avanzata di Internet Explorer solo per gli amministratori.  
  
-   In Internet Explorer potrebbe essere necessario configurare anche il browser per ignorare un server proxy in modo da consentire l'accesso tramite localhost a URL Internet.  
  
    1.  In Internet Explorer scegliere Opzioni Internet dal menu Strumenti.  
  
    2.  Nell'area Impostazioni rete locale (LAN) della scheda Connessioni fare clic su Impostazioni LAN.  
  
    3.  Nell'area Configurazione automatica deselezionare la casella di controllo Rileva automaticamente impostazioni.  
  
    4.  Nell'area Server proxy selezionare la casella di controllo Utilizza un server proxy per le connessioni LAN.  
  
    5.  Digitare l'indirizzo del server proxy nella casella Indirizzo.  
  
    6.  Digitare il numero di porta del server proxy nella casella Porta.  
  
    7.  Selezionare la casella di controllo Ignora server proxy per indirizzi locali.  
  
    8.  Fare clic su OK per chiudere la finestra di dialogo Impostazioni rete locale (LAN).  
  
    9. Fare clic su OK per chiudere la finestra di dialogo Opzioni Internet.  
  
##  <a name="installdb"></a>Installare un server di database  
 In questo argomento si presuppone che la topologia della farm sia basata su quella descritta nell'articolo [relativo a più server per una farm a tre livelli](https://go.microsoft.com/fwlink/?LinkId=182771). Se si dispone già di una farm operativa, procedere con l' [installazione PowerPivot per SharePoint](#installppapp).  
  
 Se si è all'inizio dell'avvio della topologia, cominciare installando un motore di database di SQL Server. Queste istruzioni consentono di generare un server di database al quale è possibile accedere dai server SharePoint nella farm.  
  
1.  Nel computer in uso per il server di database, eseguire SQL Server programma di installazione per installare SQL Server motore di database (vedere [install SQL Server 2014 from the Installation &#40;Wizard&#41;Setup](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)).  
  
     Quando si selezionano le funzionalità da installare, scegliere gli elementi seguenti:  
  
    -   Servizi motore di database  
  
    -   Connettività strumenti client  
  
    -   Strumenti di gestione - Completa (la versione Di base verrà inclusa automaticamente)  
  
2.  Dopo avere installato il motore di database, abilitare TCP/IP per le connessioni remote e riavviare il servizio:  
  
    1.  Avviare Gestione configurazione SQL Server.  
  
    2.  Aprire Configurazione di rete SQL Server.  
  
    3.  Selezionare **Protocolli per MSSQLSERVER**.  
  
    4.  Fare clic con il pulsante destro del mouse su **TCP/IP** e selezionare **Abilita**.  
  
    5.  Fare clic su **SQL Server Services**.  
  
    6.  Fare clic con il pulsante destro del mouse su **SQL Server (MSSQLSERVER)** , quindi scegliere **Riavvia**.  
  
3.  Abilitare l'accesso in entrata al server di database tramite Windows Firewall. In questo modo, i server SharePoint nella farm possono connettersi ai database di SharePoint. Per altre informazioni, vedere [Configurare Windows Firewall per consentire l'accesso a SQL Server](../../../2014/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
    1.  In strumenti di amministrazione nel pannello di controllo di Windows fare clic su **Windows Firewall con sicurezza avanzata**.  
  
    2.  Fare clic su **Regole connessioni in ingresso**.  
  
    3.  Fare clic su **nuova regola**.  
  
    4.  In tipo di regola fare clic su **personalizzata**.  
  
    5.  Scegliere **Avanti**.  
  
    6.  In programma, nella sezione servizi, fare clic su **Personalizza**.  
  
    7.  Fare clic su **applica a questo servizio**.  
  
    8.  Selezionare **SQL Server (MSSQLSERVER)** se è stato installato SQL Server come istanza predefinita, quindi fare clic su **OK**.  
  
    9. Scegliere **Avanti**.  
  
    10. In protocollo e porte accettare le impostazioni predefinite e fare clic su **Avanti**.  
  
    11. In ambito accettare le impostazioni predefinite e fare clic su **Avanti**.  
  
    12. In azione accettare le impostazioni predefinite e fare clic su **Avanti**.  
  
    13. In profilo deselezionare le caselle di controllo per **privato** e **pubblico**, quindi fare clic su **Avanti**.  
  
    14. In nome digitare un nome descrittivo per la regola in ingresso, ad esempio **SQL Server**.  
  
    15. Fare clic su **Fine**.  
  
##  <a name="installsp"></a>Installare e configurare una farm di SharePoint 2010 a tre livelli  
 Nei computer utilizzati come server SharePoint, eseguire il programma di installazione essenziale di SharePoint su ognuno, seguito dal programma di installazione del server SharePoint.  
  
 Utilizzare le istruzioni seguenti nella documentazione di SharePoint 2010 per installare e configurare una farm di SharePoint 2010 che include due server Web e un server applicazioni:  
  
 [Più server per una farm a tre livelli (SharePoint Server 2010)](https://go.microsoft.com/fwlink/?LinkId=182771)  
  
 Quando viene richiesto di specificare un server di database, indicare il server di database installato in precedenza.  
  
 Nelle procedure riportate di seguito si presuppone che la farm sia stata configurata utilizzando le istruzioni fornite per l'installazione della farm a tre livelli. Nella farm devono essere inclusi i servizi e le funzionalità seguenti:  
  
-   Excel Services, servizio di ricerca e servizio di archiviazione sicura  
  
-   Applicazione Web e raccolta siti  
  
-   Raccolta dati di utilizzo e integrità  
  
-   Registrazione diagnostica  
  
##  <a name="installppapp"></a>Installare PowerPivot per SharePoint in un server applicazioni  
 Eseguire il programma di installazione di SQL Server per aggiungere PowerPivot per SharePoint a una farm di SharePoint. Se la farm è costituita da più server SharePoint, è necessario eseguire il programma di installazione di SQL Server in un server applicazioni per il quale è già stato creato un join alla farm.  
  
 Installare sempre PowerPivot per SharePoint in un server applicazioni. Anche se i server front-end Web eseguono i componenti server PowerPivot per SharePoint, i componenti eseguiti nel front-end Web vengono installati durante il passaggio di configurazione di PowerPivot per SharePoint, quando si distribuiscono soluzioni nella farm. Per ulteriori informazioni sul programma di installazione, vedere [Install PowerPivot per SharePoint 2010](../../../2014/sql-server/install/install-powerpivot-for-sharepoint-2010.md).  
  
 Se la topologia di distribuzione richiede due istanze di PowerPivot per SharePoint, eseguire il programma di installazione di SQL Server su ogni server applicazioni. In un computer può essere presente una sola istanza di PowerPivot per SharePoint. Se sono richieste più istanze, è necessario utilizzare server aggiuntivi. Per ulteriori informazioni sull'aggiunta di più server PowerPivot per SharePoint alla stessa farm, vedere [elenco di controllo per la distribuzione: scalabilità orizzontale mediante l'aggiunta di server PowerPivot a una farm di SharePoint 2010](../../../2014/sql-server/install/deployment-checklist-scale-out-adding-powerpivot-servers-sharepoint-2010-farm.md).  
  
##  <a name="installclientlib"></a>Installare Analysis Services librerie client nei server applicazioni di SharePoint che non dispongono di un'installazione di PowerPivot per SharePoint  
 Per una topologia farm contenente un server front-end Web o un server applicazioni che esegue le applicazioni riportate di seguito, senza un'installazione di PowerPivot per SharePoint nello stesso computer, sarà necessario un software aggiuntivo per supportare le funzionalità e l'acceso ai dati PowerPivot:  
  
-   Excel Services o PerformancePoint Services  
  
-   Amministrazione centrale in esecuzione come applicazione autonoma nel proprio server  
  
 Sia per Excel Services sia per PerformancePoint Services è necessaria una versione più recente del provider OLE DB per Analysis Services per supportare l'accesso ai dati PowerPivot. Se si esegue una delle due applicazioni in un computer in cui non è disponibile il provider OLE DB più recente, è necessario installare quest'ultimo manualmente. Per ulteriori informazioni, vedere [Install the provider OLE DB Analysis Services on SharePoint Servers](../../../2014/sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md)  
  
 Analogamente, per un computer in cui è installato solo Amministrazione centrale, senza PowerPivot per SharePoint, sarà necessaria la libreria client ADOMD.NET. Questa libreria viene utilizzata dal dashboard di gestione PowerPivot per accedere ai dati interni utilizzati per popolare il dashboard. Per altre informazioni, vedere [Install ADOMD.NET on Web Front-End Servers Running Central Administration](../../../2014/sql-server/install/install-adomd-net-on-web-front-end-servers-running-central-administration.md).  
  
##  <a name="configsrvr"></a>Configurare il server  
 Utilizzare lo strumento di configurazione PowerPivot per configurare PowerPivot per SharePoint. Lo strumento analizzerà la configurazione esistente della farm e fornirà le opzioni per l'installazione o l'attivazione delle funzionalità di SharePoint necessarie per PowerPivot per SharePoint. Durante questo passaggio verrà avviato Claims to Windows Token Service. Inoltre, se altre funzionalità di SharePoint richieste non sono ancora abilitate, queste verranno aggiunte all'elenco e verranno incluse le azioni per l'abilitazione della funzionalità.  
  
 Per ulteriori informazioni, vedere [configurare o ripristinare PowerPivot per SharePoint strumento &#40;&#41;di configurazione PowerPivot 2010](../../../2014/analysis-services/configure-repair-powerpivot-sharepoint-2010.md).  
  
##  <a name="AAM"></a>Configurare il mapping di accesso alternativo per i server front-end Web  
 Per assicurarsi che le richieste di accesso ai dati PowerPivot o di aggiornamento dati vengano gestite da ogni server front-end Web, è necessario eseguire il mapping di URL diversi di ogni server alla stessa applicazione Web.  
  
1.  In Gestione applicazioni di amministrazione centrale fare clic su **Configura mapping di accesso alternativo**.  
  
2.  In Raccolta di mapping di accesso alternativo selezionare l'applicazione Web in uso.  
  
3.  Fare clic su **Aggiungi URL interno**.  
  
4.  Specificare l'URL del primo server front-end Web.  
  
5.  Ripetere i passaggi precedenti per aggiungere l'URL del secondo server front-end Web.  
  
##  <a name="activatePP"></a>Attivare l'integrazione delle funzionalità di PowerPivot per le raccolte siti  
 L'attivazione di funzionalità a livello di raccolta siti rende disponibile pagine e modelli dell'applicazione nei siti in uso, incluse le pagine di configurazione per l'aggiornamento dati pianificato e le pagine dell'applicazione per la raccolta PowerPivot e le librerie di feed di dati.  
  
 Lo strumento di configurazione PowerPivot attiva l'integrazione delle funzionalità per la raccolta siti specificata. È possibile eseguire lo strumento più volte per selezionare raccolte siti aggiuntive. In alternativa, gli amministratori del sito possono configurare l'attivazione della funzionalità da SharePoint. Per ulteriori informazioni, vedere [attivazione dell'integrazione delle funzionalità di PowerPivot per le raccolte siti in Amministrazione centrale](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/activate-power-pivot-integration-for-site-collections-in-ca).  
  
##  <a name="verify"></a>Verificare l'integrazione e la disponibilità del server  
 L'elaborazione di query PowerPivot si verifica nella farm quando un utente o un'applicazione apre una cartella di lavoro di Excel che contiene dati PowerPivot. Come minimo, è possibile controllare le pagine sui siti di SharePoint per verificare che le funzionalità PowerPivot siano disponibili. Tuttavia, per verificare completamente un'installazione, è necessario disporre di una cartella di lavoro di PowerPivot pubblicabile in SharePoint e accessibile da una raccolta. A scopo di test, è possibile pubblicare una cartella di lavoro di esempio contenente già dati PowerPivot e utilizzarla per confermare la corretta configurazione dell'integrazione SharePoint.  
  
 Per verificare l'integrazione di PowerPivot con un sito di SharePoint, effettuare le operazioni seguenti:  
  
1.  In un browser aprire l'applicazione Web creata. Se sono stati usati valori predefiniti, è possibile specificare http://\<il nome del computer > nell'indirizzo URL.  
  
2.  Verificare che le funzionalità di elaborazione e di accesso ai dati PowerPivot siano disponibili nell'applicazione. È possibile effettuare questa operazione verificando la presenza di modelli di libreria forniti da PowerPivot:  
  
    1.  In azioni sito fare clic su **altre opzioni.** ..  
  
    2.  Nelle librerie dovrebbero essere visualizzate la **libreria di feed di dati** e la **raccolta PowerPivot**. Questi modelli di raccolta vengono forniti dalla funzionalità PowerPivot e saranno visibili nell'elenco delle raccolte se la funzionalità è integrata correttamente.  
  
 Per verificare l'accesso ai dati PowerPivot nel server, effettuare le operazioni seguenti:  
  
1.  [Scaricare](https://go.microsoft.com/fwlink/?LinkID=219108) i dati di esempio Picnic forniti con l'esercitazione Reporting Services. La cartella di lavoro di esempio contenuta in questo download sarà utilizzata per verificare l'accesso ai dati PowerPivot. Estrarre i file.  
  
2.  Caricare una cartella di lavoro di PowerPivot in Raccolta PowerPivot o in qualsiasi raccolta SharePoint.  
  
3.  Fare clic sul documento per aprirlo dalla raccolta.  
  
4.  Fare clic su un filtro dei dati o filtrare i dati per avviare una query PowerPivot. I dati PowerPivot verranno caricati in background e verranno restituiti i risultati. Nel passaggio successivo verrà effettuata la connessione al server per verificare che i dati vengano caricati e memorizzati nella cache.  
  
5.  Avviare SQL Server Management Studio dal gruppo di programmi Microsoft SQL Server 2008 R2 nel menu Start. Se questo strumento non è installato nel server, è possibile ignorare l'ultimo passaggio per confermare la presenza di file memorizzati nella cache.  
  
6.  In Tipo di server selezionare **Analysis Services**.  
  
7.  In nome server immettere **\<nome-server > \powerpivot**, dove **\<nome-server >** è il nome del computer in cui è presente l'installazione di PowerPivot per SharePoint.  
  
8.  Fare clic su **Connetti**.  
  
9. In Esplora oggetti fare clic su **database** per visualizzare l'elenco dei file di dati PowerPivot caricati.  
  
10. Nel file system del computer, controllare la cartella seguente per determinare se i file vengono memorizzati nella cache su disco. La presenza di file memorizzati nella cache è un'ulteriore verifica che la distribuzione è operativa. Per visualizzare la cache dei file, spostarsi nella cartella \Programmi\Microsoft SQL Server\MSAS10_50.POWERPIVOT\OLAP\Backup.  
  
##  <a name="nextsteps"></a>Passaggi successivi all'installazione  
 Dopo aver verificato l'installazione, terminare la configurazione del servizio creando una raccolta PowerPivot oppure ottimizzando le singole impostazioni di configurazione. Per sfruttare al meglio i componenti server appena installati, è possibile scaricare [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] per creare e pubblicare la prima cartella di lavoro di PowerPivot.  
  
####  <a name="bkmk_disk"></a>Imposta i limiti massimi sull'utilizzo dello spazio su disco  
 È possibile impostare un limite massimo sulla quantità di spazio su disco che è possibile utilizzare per i file di dati PowerPivot memorizzati nella cache su disco. Per impostazione predefinita, viene utilizzato tutto lo spazio su disco disponibile. Per istruzioni su come limitare l'utilizzo dello spazio su disco, vedere [configurare l' &#40;utilizzo&#41;dello spazio su disco PowerPivot per SharePoint](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/configure-disk-space-usage-power-pivot-for-sharepoint).  
  
####  <a name="Upload"></a>Aumentare le dimensioni massime di caricamento file per le applicazioni Web di SharePoint  
 Poiché le cartelle di lavoro di PowerPivot possono essere di grandi dimensioni, è possibile aumentare le dimensioni massime di caricamento dei file. Possono essere configurate due impostazioni relative alle dimensioni dei file: Dimensioni massime caricamento per l'applicazione Web e Dimensioni massime cartella di lavoro in Excel Services. Le dimensioni massime dei file devono essere impostate sullo stesso valore in entrambe le applicazioni. Per istruzioni, vedere [configurare le dimensioni &#40;massime di&#41;caricamento dei file PowerPivot per SharePoint](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/configure-maximum-file-upload-size-power-pivot-for-sharepoint).  
  
#### <a name="grant-sharepoint-permissions-to-workbook-users"></a>Concedere autorizzazioni di SharePoint agli utenti delle cartelle di lavoro  
 Gli utenti devono disporre delle autorizzazioni di SharePoint per pubblicare o visualizzare cartelle di lavoro. Assicurarsi di concedere le autorizzazioni di **visualizzazione** agli utenti che devono visualizzare le cartelle di lavoro pubblicate e le autorizzazioni di **collaborazione** agli utenti che pubblicano o gestiscono le cartelle di lavoro. Per concedere le autorizzazioni, è necessario disporre dei privilegi di amministratore della raccolta siti.  
  
1.  Nel sito, fare clic su **Azioni sito**.  
  
2.  Fare clic su **autorizzazioni sito**.  
  
3.  Selezionare la casella di controllo per il gruppo **membri** raccolta siti.  
  
4.  Sulla barra multifunzione fare clic su **Concedi autorizzazioni**.  
  
5.  Immettere gli account gruppo o utente di dominio di Windows che dispongono delle autorizzazioni per aggiungere o rimuovere documenti.  
  
6.  Scegliere **OK**.  
  
7.  Selezionare la casella di controllo per il gruppo **visitatori** raccolta siti.  
  
8.  Sulla barra multifunzione fare clic su **Concedi autorizzazioni**.  
  
9. Immettere gli account gruppo o utente di dominio di Windows che dispongono delle autorizzazioni per visualizzare documenti. Come in precedenza, non usare indirizzi di posta elettronica o gruppi di distribuzione se l'applicazione è configurata per l'autenticazione classica.  
  
10. Scegliere **OK**.  
  
#### <a name="install-adonet-data-services-35-sp1"></a>Installare ADO.NET Data Services 3.5 SP1  
 ADO.NET Data Services è necessario per un'esportazione dei feed di dati di elenchi SharePoint. SharePoint 2010 non include questo componente nel programma PrerequisiteInstaller, pertanto è necessario installarlo manualmente. Per altre informazioni su come installare ADO.NET Data Services, vedere [installare ADO.NET Data Services per supportare esportazioni di feed di dati di elenchi SharePoint](../../../2014/sql-server/install/install-ado-net-data-services-to-support-data-feed-exports-of-sharepoint-lists.md).  
  
#### <a name="install-data-providers-used-in-data-refresh-and-check-user-permissions"></a>Installare provider di dati usati per l'aggiornamento dati e verificare le autorizzazioni utente  
 L'aggiornamento dati lato server consente agli utenti di reimportare dati aggiornati nelle cartelle di lavoro in modalità automatica. Affinché l'aggiornamento dati riesca, il server deve disporre dello stesso provider di dati usato per importare i dati inizialmente. Inoltre, per l'account utente con il quale viene eseguito l'aggiornamento dati vengono spesso richieste autorizzazioni di lettura sulle origini dati esterne. Verificare i requisiti per l'abilitazione e la configurazione dell'aggiornamento dati per assicurarsi un risultato positivo. Per ulteriori informazioni, vedere [aggiornamento dati PowerPivot con SharePoint 2010](../../../2014/analysis-services/powerpivot-data-refresh-with-sharepoint-2010.md).  
  
#### <a name="create-a-powerpivot-gallery"></a>Creare una Raccolta PowerPivot  
 Raccolta PowerPivot include opzioni di anteprima e presentazione per la visualizzazione delle cartelle di lavoro di PowerPivot su un sito di SharePoint. L'utilizzo di Raccolta PowerPivot per pubblicare e visualizzare le cartelle di lavoro di PowerPivot è consigliato per la sua funzionalità di anteprima. Inoltre, se Reporting Services è stato distribuito nello stesso server SharePoint, Raccolta PowerPivot semplifica le procedure di creazione di report. È possibile avviare Generatore report dall'interno di Raccolta PowerPivot per basare un nuovo report su una cartella di lavoro di PowerPivot pubblicata. Per ulteriori informazioni sulla creazione e sull'utilizzo della libreria, vedere [creare e personalizzare la raccolta PowerPivot](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/create-and-customize-power-pivot-gallery) e [utilizzare la raccolta PowerPivot](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/use-power-pivot-gallery).  
  
#### <a name="tune-configuration-settings"></a>Ottimizzare le impostazioni di configurazione  
 Un'applicazione di servizio PowerPivot viene creata utilizzando valori e proprietà predefiniti. È possibile modificare le impostazioni di configurazione per singole applicazioni di servizio per modificare la metodologia di allocazione delle richieste, impostare timeout del server, modificare le soglie per gli eventi del report di risposta alle query o specificare il periodo di conservazione dei dati di utilizzo. Per ulteriori informazioni sulla configurazione in Amministrazione centrale o sull'utilizzo delle funzionalità PowerPivot nelle applicazioni Web di SharePoint, vedere [amministrazione e configurazione del server PowerPivot in Amministrazione centrale](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration).  
  
## <a name="see-also"></a>Vedere anche  
 [Funzionalità supportate dalle edizioni di SQL Server 2012](https://go.microsoft.com/fwlink/?linkid=232473)   
 [Installare PowerPivot per SharePoint 2010](../../../2014/sql-server/install/install-powerpivot-for-sharepoint-2010.md)   
 [Elenco di controllo per la distribuzione: scalabilità orizzontale mediante l'aggiunta di server PowerPivot a una farm di SharePoint 2010](../../../2014/sql-server/install/deployment-checklist-scale-out-adding-powerpivot-servers-sharepoint-2010-farm.md)  
  
  
