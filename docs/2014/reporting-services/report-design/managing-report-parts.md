---
title: Gestione di parti di report | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 41947b4c-8ecf-4e4f-b30e-66e1d6692b74
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f7564a37766972782a5c118ced64298b7f4ce076
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63209278"
---
# <a name="managing-report-parts"></a>Gestione di parti di report
  A partire [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], parti del report possono essere pubblicate nei server di report e riutilizzate in altri report e da altri utenti se hanno le autorizzazioni appropriate.  
  
 Le parti del report possono essere inoltre riutilizzate da più utenti e in più report. Gli utenti possono cercare le parti del report nel server e aggiungerle a un report.  Possono inoltre essere informati sugli aggiornamenti apportati alla parte del report nel server e ripubblicare nuove versioni di una parte del report. Queste azioni di creazione di report possono essere interessate e controllate dalle autorizzazioni di sicurezza di Reporting Services.  In questo argomento vengono illustrate le proprietà delle parti del report e viene descritto il comportamento delle parti del report presenti nel server.  
  
## <a name="managing-report-parts"></a>Gestione di parti di report  
 Per gestire le parti del report, è possibile utilizzare Gestione report per un server di report in modalità nativa o le pagine dell'applicazione per un server di report in modalità integrata SharePoint.  
  
### <a name="server-side-interaction-and-search"></a>Interazione e ricerca sul lato server  
 Le parti del report possono essere pubblicate in un server di report in modalità nativa o in modalità integrata SharePoint. Gli utenti possono trovare e aggiungere parti del report ai report in uso tramite la funzionalità di raccolta delle parti del report in un'applicazione di creazione di report, ad esempio Generatore report di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Quando un utente cerca una parte del report, la ricerca viene effettuata nel catalogo del server di report indipendentemente dalla modalità di installazione del server.  
  
 Quando le parti del report vengono pubblicate da un'applicazione di creazione di report come Generatore report in un server di report in modalità integrata SharePoint, viene aggiornato anche il catalogo del server di report e vengono eseguite ricerche nella raccolta per riflettere in maniera accurata la parte del report nuova o aggiornata.  
  
#### <a name="directly-uploading-report-parts-to-a-sharepoint-folder"></a>Caricamento diretto di parti del report in una cartella di SharePoint  
 Se una parte del report viene caricata direttamente in una cartella di documenti di SharePoint anziché essere pubblicata da un'applicazione di creazione di report, il catalogo del server di report non viene aggiornato. La parte del report caricata non verrà pertanto trovata mediante le ricerche eseguite nella raccolta di parti del report. Per garantire la sincronizzazione delle cartelle di SharePoint e del catalogo del server di report, è possibile attivare la caratteristica di sincronizzazione dei file di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nel server SharePoint. Per altre informazioni, vedere [Attivare la funzionalità Sincronizzazione file server di report in Amministrazione centrale SharePoint](../activate-report-server-file-sync-feature-sharepoint-central-administration.md).  
  
 È inoltre possibile sincronizzare i file mediante la chiamata di alcune API di gestione di Reporting Services, ad esempio GetProperties e SetProperties.  
  
### <a name="organizing-and-moving-report-parts"></a>Organizzazione e spostamento di parti del report  
 È opportuno considerare e pianificare in anticipo la modalità di utilizzo e organizzazione da parte del team di parti del report, origini dati e set di dati condivisi. Sebbene sia possibile spostare successivamente tali elementi, tale operazione potrebbe creare problemi.  
  
#### <a name="native-mode-report-server"></a>Server di report in modalità nativa  
 Lo spostamento di una parte del report presente in un server di report in modalità nativa in un'altra cartella nello stesso server non influisce sulla possibilità delle applicazioni di creazione di report di eseguire ricerche o scaricare aggiornamenti della parte del report, poiché il server si basa sull'elemento univoco ComponentID. Se tuttavia la parte del report viene spostata in una cartella per la quale un utente non dispone di autorizzazioni, non sarà possibile trovarla mediante le ricerche e ai report relativi non verranno notificati gli aggiornamenti apportati alla parte del report stessa.  
  
#### <a name="report-server-in-sharepoint-integrated-mode"></a>Server di report in modalità integrata SharePoint  
 Lo spostamento di parti del report in una raccolta documenti o in una cartella diversa equivale al caricamento diretto in un server SharePoint. Il catalogo del server di report non sarà sincronizzato. Per evitare questa situazione, attivare la caratteristica Sincronizzazione file server di report nel server SharePoint.  
  
 Le sottocartelle costituiscono un'eccezione, poiché la ricerca viene sempre eseguita all'interno di queste ultime e di conseguenza, se la si sposta manualmente in una sottocartella, una parte di report verrà comunque trovata durante una ricerca in una raccolta di parti di report .  
  
### <a name="report-server-catalog-properties"></a>Proprietà del catalogo del server di report  
 Nella tabella seguente vengono illustrate le correlazioni dei campi del catalogo del server di report esistenti a una parte del report e ai nuovi campi aggiunti al catalogo per le parti del report. Questi sono esposti in Gestione report, nelle raccolte di SharePoint e nelle applicazioni di creazione di report, ad esempio Generatore report.  
  
 (*) indica un elemento introdotto in questa versione.  
  
|Proprietà|Descrizione|Parte del report<br /><br /> Criteri di ricerca nella raccolta|  
|--------------|-----------------|---------------------------------------------|  
|nome|Uno dei criteri in base al quale un utente può eseguire la ricerca nella raccolta di parti del report.|Yes|  
|Descrizione|Può essere necessario organizzare i nomi delle parti del report in modo da semplificare la ricerca nella raccolta. Ad esempio, è possibile cercare la descrizione che inizia con "Vendite>>" per trovare tutte le parti di report in cui sono presenti dati e presentazioni relativi alle vendite.|Yes|  
|CreatedBy|ID dell'utente che ha aggiunto la parte del report al database del server di report. Il formato esatto dipende dal metodo di autenticazione. Alcuni metodi di autenticazione, ad esempio, consentono di visualizzare il nome di dominio\utente completo nei campi CreatedBy e ModifiedBy.|Yes|  
|CreationDate|Data in cui è stata originariamente creata la parte del report.<br /><br /> Uno dei criteri in base al quale un utente può eseguire la ricerca nella raccolta di parti del report.|Yes|  
|ModifiedBy|ModifiedBy è l'ID dell'ultimo utente che ha modificato la parte del report.|Yes|  
|ModifiedDate|Data dell'ultima modifica della parte del report nel server.<br /><br /> Questo campo viene utilizzato come parte della logica per determinare quando vengono apportati aggiornamenti a una parte del report sul lato server. Per ulteriori informazioni, vedere la descrizione di ComponentID più avanti in questa tabella.|Yes|  
|SubType (*)|SubType è una stringa che indica il tipo di parte del report da cercare, ad esempio "Tablix" o "Grafico".|Yes|  
|ComponentID (*)|ComponentID è un identificatore univoco della parte del report. Si tratta di uno dei nuovi campi aggiunti al catalogo ed è visibile sia sul lato server sia nelle applicazioni di creazione di report, ad esempio Generatore report.<br /><br /> Questo campo viene utilizzato dalle applicazioni client durante la verifica degli aggiornamenti di una parte del report nel server. L'applicazione client esegue la ricerca nel server degli elementi ComponentID presenti nel report corrente sul lato client. Quando viene rilevata una corrispondenza, il valore del campo ModifiedDate viene confrontato con il valore del campo SyncDate dell'elemento del report sul lato client.|N0|  
  
## <a name="controlling-access-to-report-parts"></a>Controllo dell'accesso alle parti del report  
 Nelle tabelle seguenti vengono descritte le assegnazioni di ruolo predefinite e il modo in cui consentono di eseguire diverse operazioni. I nomi delle assegnazione di ruolo sono diversi a seconda del tipo di server di report utilizzato.  
  
### <a name="server-in-native-mode"></a>Server in modalità nativa  
  
|Azioni|Ruoli|  
|-------------|-----------|  
|Aggiunta, eliminazione, modifica delle proprietà dell'elemento, gestione della sicurezza e download di parti del report|Gestione contenuto<br /><br /> Report personali|  
|Aggiunta, eliminazione e download di parti del report|Server di pubblicazione|  
|Esecuzione di ricerche e riutilizzo|Browser<br /><br /> Generatore report|  
  
### <a name="server-in-sharepoint-integrated-mode"></a>Server in modalità integrata SharePoint  
  
|Azioni|Role|  
|-------------|----------|  
|Aggiunta, eliminazione, modifica delle proprietà dell'elemento, gestione della sicurezza e download di parti del report|Controllo completo|  
|Aggiunta, eliminazione, modifica delle proprietà dell'elemento e download di parti del report|Progettazione<br /><br /> Collaborazione|  
|Esecuzione di ricerche e riutilizzo|lettura<br /><br /> Solo visualizzazione|  
  
### <a name="security-considerations"></a>Considerazioni sulla sicurezza  
  
-   Quando vengono riutilizzate in un report, le definizioni delle parti del report vengono copiate completamente nella definizione del report insieme all'elemento ComponentID di identificazione. Se una parte del report viene aggiornata nel server, gli utenti possono scegliere di scaricare la parte del report aggiornata nel report in uso. Gli aggiornamenti sono inoltre copie complete della parte del report, poiché sostituiscono la versione esistente della parte del report presente nel report in uso.  
  
    > [!IMPORTANT]  
    >  In ognuno di questi passaggi, verificare che le parti del report riutilizzate nei report provengano da percorsi e utenti attendibili.  
  
-   Le parti di report usano gli stessi criteri di autorizzazione del tipo di elemento risorsa esistente. Dal punto di vista dell'ereditarietà della sicurezza, all'interno di una cartella non esiste alcuna differenza tra gli elementi risorsa tradizionali e le parti di report. La parte del report eredita gli stessi criteri di autorizzazione delle immagini presenti nella stessa cartella. Quando occorre fare distinzione, è possibile configurare la sicurezza a livello di elemento per le parti del report desiderate. In alternativa, le parti del report devono essere posizionate in cartelle separate con le autorizzazioni desiderate configurate.  
  
## <a name="see-also"></a>Vedere anche  
 [Parti del report e set di dati in Generatore report](../report-data/report-parts-and-datasets-in-report-builder.md)   
 [Pagina delle proprietà generale, parti del Report &#40;gestione Report&#41;](../general-properties-page-report-parts-report-manager.md)   
 [Spostamento degli elementi &#40;gestione Report&#41;](../move-items-page-report-manager.md)   
 [Gestione contenuto del server di report &#40;modalità nativa SSRS&#41;](../report-server/report-server-content-management-ssrs-native-mode.md)   
 [Risolvere i problemi di parti del Report &#40;Report e SSRS&#41;](../report-parts-report-builder-and-ssrs.md)   
 [Parti del report in Progettazione report &#40;SSRS&#41;](report-parts-in-report-designer-ssrs.md)  
  
  
