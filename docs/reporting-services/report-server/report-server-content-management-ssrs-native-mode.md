---
title: Gestione contenuto del server di report (modalità nativa SSRS) | Microsoft Docs
ms.date: 06/14/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- administering Reporting Services
- published reports [Reporting Services], managing
- report servers [Reporting Services], content management
- content management [Reporting Services]
ms.assetid: 641961ac-53a5-4997-9d42-cf4ecce1f892
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: fa8579f24cbad2bdbebe3ad5198732ac7786bde9
ms.sourcegitcommit: 1bbbbb8686745a520543ac26c4d4f6abe1b167ea
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2019
ms.locfileid: "67228751"
---
# <a name="report-server-content-management-ssrs-native-mode"></a>Gestione contenuto del server di report (modalità nativa SSRS)
In [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], il concetto di gestione dei contenuti fa riferimento alla gestione degli elementi del server di report. È possibile gestire tutti gli elementi singolarmente tramite impostazioni di sicurezza e proprietà. Ogni elemento può essere spostato in una posizione diversa nello spazio dei nomi delle cartelle del server di report. Per gestire gli elementi in modo efficiente, è necessario conoscere quali attività vengono eseguite da un utente con ruolo Gestione contenuto. A partire da SQL Server 2016 Reporting Services o versione successiva (SSRS) CTP 3.2, il [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] portale web è disponibile. In questo articolo verranno esaminati il portale Web e la nuova esperienza del portale Web.  
  
> [!NOTE]  
> La gestione del contenuto è un'operazione diversa dall'amministrazione di un server di report. Per altre informazioni sulla gestione dell'ambiente in cui viene eseguito un server di report, vedere [Server di report di Reporting Services &#40;modalità nativa&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md).  
  
 Nella gestione del contenuto sono incluse le attività seguenti:  
  
-   Garantire la sicurezza degli elementi e del sito del server di report mediante l'applicazione della sicurezza basata sui ruoli disponibile in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
-   Creare una gerarchia di cartelle del server di report mediante l'aggiunta, la modifica e l'eliminazione di cartelle.  
  
-   Impostare proprietà e valori predefiniti da applicare agli elementi gestiti dal server di report. È ad esempio possibile impostare valori massimi di riferimento che determinano i criteri di archiviazione della cronologia dei report.  
  
-   Creare origini dati condivise da utilizzare al posto delle connessioni a origini dati specifiche dei report. Un utente con ruolo Pubblicazione o Gestione contenuto può selezionare un'origine dei dati diversa da quella definita originariamente per un report, ad esempio per sostituire un riferimento a un database di prova con un riferimento a un database di produzione.  
  
-   Creare pianificazioni condivise che possono essere utilizzate al posto delle pianificazioni specifiche del report e della sottoscrizione, semplificando la gestione delle informazioni sulla pianificazione nel tempo.  
  
-   Creare sottoscrizioni guidate dai dati tramite cui vengono generati elenchi di destinatari recuperando i dati da un archivio dati.  
  
-   Bilanciare le richieste di elaborazione di report inviate al server tramite la pianificazione dell'elaborazione dei report stessi e l'indicazione di quali possono essere eseguiti su richiesta e quali vengono caricati dalla cache.  
  
-   Fornire le autorizzazioni per eseguire le attività di gestione usando ruoli predefiniti, ovvero **Amministratore sistema** e **Gestione contenuto**. Per gestire in modo efficiente contenuto di un server di report, è necessario che un utente sia assegnato a entrambi ruoli.  
  
Gli strumenti per la gestione dei contenuti del server di report includono [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] e il portale Web. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] consente di impostare valori predefiniti e di abilitare funzionalità. Il portale Web consente di concedere agli utenti l'accesso a elementi e operazioni del server di report, visualizzare e usare report e altri tipi di contenuto, nonché visualizzare e usare tutti gli elementi condivisi e le funzionalità di distribuzione del report. Il portale Web è un sito aggiornato che offre gran parte delle funzionalità di Gestione report, deprecato. Per altre informazioni, vedere [Strumenti di Reporting Services](../../reporting-services/tools/reporting-services-tools.md).  
  
##  <a name="bkmk_ReportServerItems"></a> Elementi del server di report  
 Gli elementi del server di report includono report, origini dati condivise, set di dati condivisi, parti del report, risorse (elementi archiviati ma non elaborati in un server di report) e cartelle. Gli elementi possono dipendere da altri elementi, ad esempio un report può dipendere dalle origini dati condivise a cui fa riferimento. Se si sposta un elemento dipendente, le informazioni di riferimento vengono aggiornate automaticamente dal server di report.  
  
 È possibile spostare gli elementi del server di report in percorsi di cartelle diversi nella gerarchia di cartelle del server di report. Quando si sposta un elemento, tutte le proprietà, incluse le impostazioni di sicurezza, vengono spostate con l'elemento nel nuovo percorso. Quando si sposta una cartella, vengono spostati tutti gli elementi contenuti nella cartella.  
  
> [!NOTE]  
>  Per la versione CTP 3.2, se si vuole spostare la posizione di un elemento, è necessario eseguire questa operazione nel portale Web.  
  
 Nel portale Web gli elementi che è possibile spostare sono indicati nella gerarchia di cartelle. L'immagine seguente mostra le icone di ogni elemento che è possibile spostare.  
  
  ![Icone di server di report per gli elementi spostabile](media/report-server-content-management-ssrs-native-mode/report-server-content-icons.png)

 Non tutti gli elementi possono essere spostati. Non è possibile spostare elementi associati a un report, ad esempio le sottoscrizioni o la cronologia del report. Tali elementi si spostano insieme ai report a essi associati. Analogamente, non è possibile spostare elementi disponibili all'esterno della gerarchia di cartelle, ad esempio le pianificazioni condivise. Non è possibile spostare gli elementi se non si dispone delle autorizzazioni appropriate. L'autorizzazione per lo spostamento di un elemento viene concessa a un utente selezionando le attività seguenti nell'assegnazione di ruolo dell'utente per l'elemento specifico: "Gestione di report", "Gestione di cartelle" e "Gestione di origini dei dati".  
  
##  <a name="bkmk_Folders"></a> Cartelle  
 Per fare riferimento agli elementi archiviati e gestiti da un server di report viene utilizzata una gerarchia di cartelle.  Per impostazione predefinita, la struttura di cartelle è costituita da un nodo radice denominato Home e da cartelle riservate che supportano la funzionalità facoltativa Report personali. Le cartelle aggiuntive vengono definite dall'utente. Le cartelle del server di report sono utili se si desidera concedere lo stesso livello di accesso a più elementi. Le autorizzazioni impostate per la cartella possono essere ereditate dagli elementi di tale cartella e in cartelle aggiuntive incluse in essa. È ad esempio possibile creare un set di cartelle sotto la cartella Home, assegnare autorizzazioni del team a ogni cartella, quindi consentire a membri del team di personalizzare le cartelle incluse nella cartella del team in base alle necessità.  
  
 Se si utilizza un browser per connettersi direttamente a un server di report, il nome della directory virtuale del server di report corrisponde al nome del nodo radice della struttura di cartelle. Dal nodo radice, è possibile creare, modificare ed eliminare cartelle come necessario per organizzare i contenuti del server di report. È possibile aggiungere contenuti a una cartella, spostare elementi da una cartella all'altra, modificare i nomi o i percorsi delle cartelle ed eliminare le cartelle non più necessarie.  
  
 Le cartelle sono contenitori virtuali per gli elementi pubblicati, a cui è possibile accedere tramite il portale Web o una connessione tramite browser al server di report. Le cartelle oppure i contenuti relativi non esistono effettivamente in un file system, ma sono archiviati nel database del server di report e sono accessibili tramite l'endpoint del servizio Web ReportServer. Lo spazio dei nomi delle cartelle del server di report è una gerarchia che include un nodo radice, cartelle predefinite e cartelle definite dall'utente. Lo spazio dei nomi identifica in modo univoco i report archiviati in un server di report e offre uno schema di indirizzamento per specificare gli elementi in un URL. Quando si seleziona o si individua un report, il percorso della cartella diventa parte integrante dell'URL del report.  
  
 Il tipo di operazioni di gestione delle cartelle dipende dalle attività che fanno parte dell'assegnazione di ruolo dell'utente. Se si utilizzano le impostazioni di sicurezza predefinite, le cartelle possono essere create e gestite dagli utenti con ruolo Gestione contenuto e Pubblicazione. Se si utilizzano assegnazioni di ruolo personalizzate, tali assegnazioni devono includere attività che supportano la gestione delle cartelle. Per altre informazioni sulle assegnazioni di ruolo e sulle attività, vedere [Concessione di autorizzazioni in un server di report in modalità nativa](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md) e [Attività e autorizzazioni](../../reporting-services/security/tasks-and-permissions.md).  
  
 Le cartelle del server di report possono contenere gli elementi seguenti:  
  
-   Report  
  
-   Origini dati condivise  
  
-   Set di dati condivisi  
  
-   Parti del report  
  
-   KPI  
  
-   Report per dispositivi mobili  
  
-   Risorse, ovvero elementi archiviati ma non elaborati in un server di report  
  
-   Altre cartelle  
  
### <a name="reserved-folders"></a>Cartelle riservate  
 Le cartelle predefinite sono riservate per l'utilizzo in Reporting Services e non possono essere spostate, rinominate o eliminate. Sono cartelle definite dall'utente tutte le cartelle create dagli utenti o dagli amministratori del server di report che dispongono dell'autorizzazione per l'aggiunta di elementi a una cartella.  
  
 Nella tabella seguente vengono descritte le cartelle predefinite che definiscono la gerarchia di cartelle e rappresentano il framework per diverse funzionalità.  
  
|Cartella|Scopo|  
|------------|-------------|  
|Home|Nodo radice della gerarchia di cartelle.|  
|Utenti|Questa cartella viene visualizzata quando si abilita la funzionalità Report personali. Contiene sottocartelle per tutti gli utenti della caratteristica Report personali ed è accessibile solo agli amministratori del server di report. A ogni sottocartella viene assegnato il nome dell'utente.|  
|Report personali|Include un'area di lavoro personale per ogni utente.|  
  
### <a name="creating-folders"></a>Creazione di cartelle  
 È possibile creare una cartella in qualsiasi cartella disponibile nella gerarchia.  
  
 Se si creano cartelle con lo scopo di limitare l'accesso a report e modelli specifici, è necessario specificare assegnazioni di ruolo che consentano agli utenti di esplorare, ma non visualizzare, il contenuto di cartelle padre presenti nel percorso della cartella.  
  
### <a name="modifying-folder-properties"></a>Modifica delle proprietà delle cartelle  
 Dopo aver creato una cartella, è possibile modificarne le proprietà, ovvero rinominarla, aggiungerne o modificarne la descrizione oppure spostarla in un percorso diverso. Queste proprietà sono disponibili nella pagina delle proprietà Generale di ogni cartella. Per altre informazioni sull'impostazione di proprietà che concedono l'accesso a una cartella, vedere [Proteggere le cartelle](../../reporting-services/security/secure-folders.md).  
  
### <a name="deleting-folders-and-folder-contents"></a>Eliminazione di cartelle e del relativo contenuto  
 Quando si elimina una cartella, vengono eliminati tutti gli elementi che contiene. Prima di procedere all'eliminazione, è pertanto consigliabile verificare il contenuto della cartella per determinare se sono presenti elementi ai quali altri elementi potrebbero fare riferimento o che potrebbero essere utilizzati da altri elementi in una parte diversa della gerarchia di cartelle. Tra gli elementi a cui viene fatto riferimento da altri elementi sono comprese definizioni dei report che supportano report collegati, origini dei dati condivise e risorse.  
  
 Se si elimina un report al quale fanno riferimento uno o più report collegati, i report collegati non saranno più validi dopo l'eliminazione del report. Non è possibile determinare in anticipo quali saranno i report interessati dall'operazione di eliminazione, in quanto in un report non vengono mantenute informazioni sui report collegati basati su di esso. È tuttavia possibile esaminare le proprietà di un report collegato per verificare su quale report si basa. In un'origine dei dati condivisa vengono invece elencati tutti i report che la utilizzano e quindi è possibile determinare facilmente se sono in uso informazioni di connessione. Per altre informazioni, vedere [Creare, modificare ed eliminare origini dati condivise &#40;SSRS&#41;](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md). Le risorse utilizzate dai report, infine, non consentono di identificare tali report.  
  
 Prima di eliminare una cartella, è consigliabile valutare se è opportuno conservare la cronologia dei report che verranno eliminati o qualsiasi altra caratteristica specifica che fa parte di tali report, ad esempio una sottoscrizione guidata dai dati. Se si ritiene che tali informazioni siano necessarie in futuro, spostarle all'esterno della cartella prima di eliminarla.  
  
 La visibilità di un elemento in una cartella dipende sia dalle assegnazioni dei ruoli, ovvero l'autorizzazione per visualizzare un elemento, sia dalle opzioni di visualizzazione in uso per tale cartella. Nel portale Web è possibile impostare nella pagina Contenuto la visualizzazione di un elenco o di dettagli. È possibile che in alcuni casi un report o un elemento non siano visualizzati in visualizzazione Elenco. Prima di eliminare il contenuto di una cartella, verificare che sia attivata la visualizzazione Dettagli.  
  
##  <a name="bkmk_Resources"></a> Risorse  
 Una risorsa è un elemento gestito che viene archiviato, ma non elaborato, in un server di report. In genere, una risorsa fornisce contenuto esterno per gli utenti dei report. Esempi di risorsa sono un'immagine in un file con estensione jpg, un file di forma ESRI contenente dati spaziali o un file HTML che descrive le regole business utilizzate in un report. Il file in formato JPG, SHP o HTML viene archiviato nel server di report, che tuttavia lo invia direttamente browser anziché elaborarlo. Per altre informazioni, vedere [Immagini &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/images-report-builder-and-ssrs.md) e la sezione "Aggiunta di dati a una mappa" in [Mappe &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/maps-report-builder-and-ssrs.md).  
  
### <a name="adding-and-viewing-a-resource"></a>Aggiunta e visualizzazione di una risorsa  
 Per aggiungere una risorsa a un server di report, caricare o pubblicare un file:  
  
|Operazione|Tipo di file|  
|---------------|---------------|  
|Caricamento|Per caricare una risorsa, è necessario usare il portale Web se il server di report è in esecuzione in modalità nativa o una pagina di applicazione in un sito di SharePoint se il server è in esecuzione in modalità integrata SharePoint. Per altre informazioni, vedere [Caricare un file o un report nel server di report](../../reporting-services/reports/upload-a-file-or-report-report-manager.md) o [Caricare documenti in una raccolta di SharePoint &#40;Reporting Services in modalità SharePoint&#41;](../../reporting-services/report-server-sharepoint/upload-documents-to-a-sharepoint-library-reporting-services-in-sharepoint-mode.md).|  
|Pubblicazione|Tutti i file in un progetto che non sono report, parti del report, origini dati o set di dati, vengono caricati come risorse. Per pubblicare una risorsa, aggiungere un elemento esistente a un progetto in Progettazione report, quindi pubblicare il progetto in un server di report.|  
  
 Tutte le risorse provengono da file presenti nel file system, caricati successivamente in un server di report. Ad eccezione dei limiti per le dimensioni del file predefinite di 4 MB imposte da ASP.NET, non sono presenti restrizioni sui tipi di file che è possibile caricare. Alcuni tipi di file risultano tuttavia più adatti di altri con tipo MIME equivalente per la pubblicazione in un server di report come risorse. Ad esempio, le risorse basate su file HTML e JPG vengono aperte in una finestra del browser quando l'utente fa clic sulla risorsa. In tal modo i file HTML vengono visualizzati come pagine Web e i file JPG come immagini visibili all'utente. Al contrario le risorse con tipi MIME non equivalenti, ad esempio file di applicazioni desktop, non vengono visualizzate in alcun modo nella finestra del browser.  
  
 Il fatto che una risorsa risulti visibile agli utenti di un report dipende dalle funzionalità del browser in uso. Poiché le risorse non vengono elaborate dal server di report, il browser deve fornire la funzionalità di visualizzazione per eseguire il rendering di un tipo MIME specifico. Se il browser non è in grado di eseguire il rendering del contenuto, gli utenti che visualizzeranno la risorsa ne vedranno esclusivamente le proprietà generali.  
  
### <a name="securing-and-managing-a-resource"></a>Sicurezza e gestione di una risorsa  
 Le risorse sono presenti come elementi denominati nella gerarchia delle cartelle del server di report insieme ai report, alle origini dati condivise, alle pianificazioni condivise e alle cartelle. È possibile ricercare, visualizzare, proteggere impostare proprietà relative alle risorse analogamente a qualsiasi altro elemento presente in un server di report. Per visualizzare o gestire una risorsa, è necessario disporre delle attività Visualizzazione di risorse o Gestione di risorse nella propria assegnazione di ruolo.  
  
### <a name="referencing-an-image-resource-from-a-report"></a>Riferimento a una risorsa immagine da un report  
 Le risorse possono contenere un'immagine cui si fa riferimento in un report. Se i requisiti del report includono l'utilizzo di immagini esterne, considerare i vantaggi seguenti relativi all'archiviazione di un'immagine come risorsa:  
  
-   Archiviazione centralizzata nel database del server di report. Se il database del server di report e il relativo contenuto vengono spostati in un altro computer, l'immagine esterna rimane con il report. Non è necessario tenere traccia di file di immagine archiviato su disco in computer diversi.  
  
-   sicurezza garantita dalle assegnazioni di ruolo anziché a livello di file system. Le stesse autorizzazioni utilizzate per visualizzare un report possono essere applicate alla risorsa. Al contrario, se si archivia l'immagine su disco, è necessario verificare che l'account utente anonimo o l'account di esecuzione automatica disponga delle autorizzazioni per accedere al file.  
  
 Per utilizzare una risorsa immagine in un report, aggiungere il file di immagine al progetto e pubblicarlo insieme al report. Dopo la pubblicazione, è possibile aggiornare il riferimento all'immagine nel report in modo che punti alla risorsa nel server di report e successivamente ripubblicare il report per salvare le modifiche. È possibile a questo punto aggiornare l'immagine in modo indipendente dal report ripubblicando la risorsa. Nel report viene utilizzata la versione più recente dell'immagine disponibile nel server di report.  
  
 Per altre informazioni, vedere [aggiornamento di una risorsa (portale web)](../../reporting-services/report-server/update-a-resource-report-manager.md).  
  
##  <a name="bkmk_MyReports"></a> Report personali  
 La cartella Report personali è un'area di lavoro personale specifica di ogni utente che accede a un server di report con un account di dominio valido. Questa cartella speciale può essere utilizzata per archiviare report non ancora definitivi, report che non saranno soggetti a un'ampia distribuzione o report che sono stati modificati per rispondere a esigenze specifiche. Non è possibile limitare la quantità né le dimensioni degli elementi che possono essere archiviati in una cartella Report personali, né è possibile configurare una cartella Report personali per la condivisione tra più utenti.  
  
 Tecnicamente, la funzionalità Report personali esegue il mapping tra il nome di una cartella virtuale visualizzata da ogni utente (Report personali) e una sottocartella univoca (il cui nome si basa sul nome dell'utente) della cartella Cartelle utenti generale. Quando un utente accede alla propria cartella Report personali, viene in realtà reindirizzato alla propria sottocartella di Cartelle utenti. In ogni sottocartella vengono archiviati i report e gli elementi che un utente aggiunge alla propria cartella Report personali. Nel portale Web non verrà visualizzato Report personali a livello di radice. Sarà necessario esaminare Cartelle utenti.  
  
 Durante l'installazione del server di report, viene creata la cartella Cartelle utenti. In seguito, quando un utente apre la cartella Report personali per la prima volta, ad esempio facendo clic su Report personali nel portale Web, viene creata la sottocartella specifica dell'utente. Ogni nome di cartella è nel formato seguente:  
  
```  
/Users Folders/<username>/My Reports  
```  
  
 Solo agli utenti con account di sistema validi vengono assegnate cartelle. Se un nome utente contiene caratteri speciali, per il nome della cartella vengono utilizzati i caratteri di escape equivalenti. Nella tabella seguente vengono indicate le corrispondenze tra caratteri speciali e caratteri di escape.  
  
|Carattere|Valore di escape|Esempio|  
|---------------|------------------|-------------|  
|(spazio)|[ ]|*Firstname Lastname* diventa *Firstname[ ]Lastname*|  
|\ (barra rovesciata)|Sostituito con uno spazio|*DomainName\Username* diventa *DomainName Username*|  
|@ (simbolo di chiocciola)|[at]|*username*@hotmail.com diventa *username*[at]hotmail.com|  
|& (e commerciale)|[amp]|*username*@*company*&*company.com* diventa *username*[at]*company*[amp]*company.com*|  
|$ (segno di dollaro)|[dollar]|*User* $*Name* diventa *User*[ ][dollar]*Name*|  
  
 La funzionalità Report personali è facoltativa. Quando si installa un server di report, la funzionalità Report personali è disabilitata per impostazione predefinita. Per altre informazioni sull'abilitazione di questa funzionalità, vedere [Abilitare e disabilitare la funzionalità Report personali](../../reporting-services/report-server/enable-and-disable-my-reports.md). Per altre informazioni, vedere [Proteggere i report personali](../../reporting-services/security/secure-my-reports.md).  
  
## <a name="tasks"></a>Attività  
 [Caricare file in una cartella](../../reporting-services/report-server/upload-files-to-a-folder.md)  
 [Creare, eliminare o modificare una cartella (portale Web)](../../reporting-services/report-server/create-delete-or-modify-a-folder-web-portal.md)  
 [Aggiornare una risorsa (portale web)](../../reporting-services/report-server/update-a-resource-report-manager.md)  
 [Caricare file in una cartella](../../reporting-services/report-server/upload-files-to-a-folder.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Strumenti di Reporting Services](../../reporting-services/tools/reporting-services-tools.md)   
 [Ruoli e autorizzazioni &#40;Reporting Services&#41;](../../reporting-services/security/roles-and-permissions-reporting-services.md)   
 [Report di Reporting Services &#40;SSRS&#41;](../../reporting-services/reports/reporting-services-reports-ssrs.md)  
  