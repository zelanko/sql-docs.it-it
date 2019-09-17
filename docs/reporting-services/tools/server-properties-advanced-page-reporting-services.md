---
title: Proprietà server (pagina Avanzate) - Reporting Services | Microsoft Docs
author: maggiesMSFT
ms.author: maggies
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
ms.date: 01/15/2019
ms.openlocfilehash: 079565c813e0b66f09881039ea3d6509bdf6cf54
ms.sourcegitcommit: 75fe364317a518fcf31381ce6b7bb72ff6b2b93f
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 09/11/2019
ms.locfileid: "70908256"
---
# <a name="server-properties-advanced-page---reporting-services"></a>Proprietà server (pagina Avanzate) - Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

Questa pagina consente di impostare le proprietà di sistema nel server di report. Le proprietà di sistema possono essere impostate in diversi modi. Questo strumento fornisce un'interfaccia utente grafica che consente di impostare le proprietà senza dovere scrivere codice.

Per aprire questa pagina, avviare SQL Server Management Studio, connettersi a un'istanza del server di report, fare clic con il pulsante destro del mouse sul nome del server di report e scegliere **Proprietà**. Selezionare **Avanzate** per aprire la pagina.

## <a name="options"></a>Opzioni

**EnableMyReports**  
Indica se la caratteristica Report personali è abilitata. Un valore **true** indica che la caratteristica è abilitata.  

**MyReportsRole**  
Nome del ruolo utilizzato durante la creazione dei criteri di sicurezza nelle cartelle Report personali dell'utente. Il valore predefinito è **My Reports Role**.  

**EnableClientPrinting**  
Determina se il controllo ActiveX RSClientPrint è disponibile per il download dal server di report. I valori validi sono **true** e **false**. Il valore predefinito è **true**. Per altre informazioni sulle impostazioni aggiuntive necessarie per questo controllo, vedere [Abilitare e disabilitare la stampa sul lato client per Reporting Services](../../reporting-services/report-server/enable-and-disable-client-side-printing-for-reporting-services.md).  

**EnableExecutionLogging**  
Indica se la registrazione per l'esecuzione di report è attivata. Il valore predefinito è **true**. Per altre informazioni sul log di esecuzione del server di report, vedere [Vista ExecutionLog ed ExecutionLog3 del server di report](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md).  

**ExecutionLogDaysKept**  
Numero di giorni durante i quali le informazioni sulle esecuzioni dei report vengono conservate nel log di esecuzione. I valori validi per questa proprietà sono compresi tra **-1** e **2**,**147**,**483**,**647**. Se il valore è **-1** le voci non vengono eliminate dalla tabella del log di esecuzione. Il valore predefinito è **60**.  

> [!NOTE]
> Se si imposta un valore **0** vengono *eliminate* tutte le voci dal log di esecuzione. Il valore **-1** mantiene le voci del log di esecuzione e non le elimina.

Report RDLX **RDLXReportTimeout** *(report Power View in un server SharePoint)* che elabora il valore di timeout in secondi per tutti i report gestiti nello spazio dei nomi del server di report. È possibile eseguire l'override del valore a livello di report. Se questa proprietà è impostata, il server di report tenta di arrestare l'elaborazione di un report quando scade il tempo specificato. I valori validi sono compresi tra **-1** e **2**,**147**,**483**,**647**. Se il valore è **-1**durante l'elaborazione non si verifica alcun timeout dei report nello spazio dei nomi. Il valore predefinito è **1800**.

**SessionTimeout** Intervallo in secondi per il quale una sessione rimane attiva. Il valore predefinito è **600**.  

**SharePointIntegratedMode**  
Proprietà di sola lettura che indica la modalità del server. Se il valore è False, il server di report è in esecuzione in modalità nativa.  

**SiteName**  
Nome del sito del server di report visualizzato nel titolo della pagina del portale Web. Il valore predefinito è [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Questa proprietà può essere una stringa vuota. La lunghezza massima è di 8.000 caratteri.  

**StoredParametersLifetime** Specifica il numero massimo di giorni per cui è possibile mantenere un parametro archiviato. I valori validi sono compresi tra **-1**, **+1** e **2,147,483,647**. Il valore predefinito è **180** giorni.  

**StoredParametersThreshold**  
Specifica il numero massimo di valori dei parametri che possono essere archiviati nel server di report. I valori validi sono compresi tra **-1**, **+1** e **2,147,483,647**. Il valore predefinito è **1500**.  

**UseSessionCookies**  
Indica se il server di report deve utilizzare cookie di sessione per le comunicazioni con i browser dei client. Il valore predefinito è **true**.  

**ExternalImagesTimeout**  
Determina l'intervallo di tempo consentito per il recupero di un file di immagine esterno prima del timeout della connessione. Il valore predefinito è **600** secondi.  

**SnapshotCompression** Snapshot del server di report nel momento.

**SnapshotCompression**  
Definisce come vengono compressi gli snapshot. Il valore predefinito è **SQL**. I valori validi sono i seguenti:

|Valori|Descrizione|
|---------|---------|
|**SQL**|Gli snapshot vengono compressi quando vengono archiviati nel database del server di report. Tale compressione è il comportamento corrente.|
|**Nessuno**|Gli snapshot non vengono compressi.|
|**Tutto**|Gli snapshot vengono compressi per tutte le opzioni di archiviazione, incluso il database del server di report o il file system.|

**SystemReportTimeout**  
Valore di timeout  predefinito per l'elaborazione dei report, espresso in secondi, per tutti i report gestiti nello spazio dei nomi del server di report. È possibile eseguire l'override del valore a livello di report. Se questa proprietà è impostata, il server di report tenta di arrestare l'elaborazione di un report quando scade il tempo specificato. I valori validi sono compresi tra **-1** e **2**,**147**,**483**,**647**. Se il valore è **-1**durante l'elaborazione non si verifica alcun timeout dei report nello spazio dei nomi. Il valore predefinito è **1800**.  

**SystemSnapshotLimit**  
Numero massimo di snapshot archiviati per un report. I valori validi sono compresi tra **-1** e **2**,**147**,**483**,**647**. Se il valore è **-1**, non vi sono limiti per gli snapshot.  

**AccessControlAllowCredentials**  
Indica se la risposta alla richiesta del client può essere esposta quando il flag "credenziali" è impostato su true. Il valore predefinito è **false**.

**AccessControlAllowHeaders** Elenco separato da virgole delle intestazioni consentite dal server quando un client invia una richiesta. Questa proprietà può essere una stringa vuota. Specificando * si consentono tutte le intestazioni.

**AccessControlAllowMethods** Elenco separato da virgole dei metodi HTTP consentiti dal server quando un client invia una richiesta. I valori predefiniti sono (GET, PUT, POST, PATCH, DELETE). Specificando * si consentono tutte le intestazioni.

**AccessControlAllowOrigin** Elenco separato da virgole delle origini consentite dal server quando un client invia una richiesta. Il valore predefinito è vuoto, il che impedisce tutte le richieste. Se si specifica * si consentono tutte le origini quando le credenziali non sono impostate; se vengono specificate credenziali, è necessario specificare un elenco esplicito delle origini.

**AccessControlExposeHeaders** Elenco separato da virgole delle intestazioni che il server esporrà ai client. Il valore predefinito è vuoto.

**AccessControlMaxAge** Specifica il numero di secondi durante i quali i risultati della richiesta preliminare possono essere memorizzati nella cache. Il valore predefinito è 600 (10 minuti).

**AllowedResourceExtensionsForUpload (solo Server di report di Power BI e Reporting Services 2017 e versioni successive)** Set di estensioni delle risorse che possono essere caricate nel server di report. Non è necessario includere le estensioni per i tipi di file predefiniti, ad esempio &ast;.rdl e &ast;.pbix. Il valore predefinito è "&ast;, &ast;.xml, &ast;.xsd, &ast;.xsl, &ast;.png, &ast;.gif, &ast;.jpg, &ast;.tif, &ast;.jpeg, &ast;.tiff, &ast;.bmp, &ast;.pdf, &ast;.svg, &ast;.rtf, &ast;.txt, &ast;.doc, &ast;.docx, &ast;.pps, &ast;.ppt, &ast;.pptx".

**RestrictedResourceMimeTypeForUpload** Set di tipi MIME a cui gli utenti non sono autorizzati a caricare il contenuto. Tutte le risorse già archiviate con un tipo MIME con restrizioni possono essere scaricate solo come un'applicazione o un flusso di ottetti anziché essere aperte/eseguite dal browser.  Per impostazione predefinita, nell'elenco non sono presenti elementi limitati, ma è consigliabile che le organizzazioni lo popolano per offrire l'esperienza più sicura.

**EditSessionCacheLimit**  
Consente di specificare il numero di voci della cache di dati che possono essere attive in una sessione di modifica del report. Il numero predefinito è 5.  

**EditSessionTimeout**  
Consente di specificare il numero di secondi prima del timeout di una sessione di modifica del report. Il valore predefinito è 7200 secondi (due ore).  

**EnableIntegratedSecurity**  
Determina se la sicurezza integrata è supportata per le connessioni all'origine dati del report. Il valore predefinito è **True**. I valori validi sono i seguenti:

|Valori|Descrizione|
|---------|---------|
|**True**|La sicurezza integrata di Windows è abilitata.|
|**False**|La sicurezza integrata di Windows non è abilitata. Le origini dati dei report configurate per l'uso della sicurezza integrata di Windows non verranno eseguite.|

**EnableLoadReportDefinition**  
Selezionare questa opzione per specificare se gli utenti possono eseguire un report non pianificato da un report di Generatore report. Selezionando questa opzione si imposta la proprietà **EnableLoadReportDefinition** sul server di report.  

Se si deseleziona questa opzione, la proprietà viene impostata su False. Il server di report non genererà report click-through per i report che usano un modello di report come origine dati. Qualsiasi chiamata al metodo LoadReportDefinition verrà bloccata.  

La disattivazione di questa opzione consente di attenuare i rischi di attacchi Denial of Service condotti da utenti malintenzionati tramite overload del server di report con richieste LoadReportDefinition.  

**EnableRemoteErrors**  
Include informazioni esterne sugli errori, ad esempio, informazioni sull'errore relative alle origini dati del report, nei messaggi di errore restituiti agli utenti che richiedono i report dai computer remoti. I valori validi sono **true** e **false**. Il valore predefinito è **false**. Per altre informazioni, vedere [Abilita errori remoti &#40;Reporting Services&#41;](../../reporting-services/report-server/enable-remote-errors-reporting-services.md).  

**EnableCustomVisuals** ***(solo Server di report di Power BI)*** Consente di abilitare la visualizzazione degli oggetti visivi personalizzati di Power BI. I valori consentiti sono True o False. *Il valore predefinito è True.*  

**ExecutionLogLevel** Imposta il livello log dell'esecuzione. *L'impostazione predefinita è Normal.*

**InterProcessTimeoutMinutes** Imposta il timeout del processo in minuti. *L'impostazione predefinita è 30.*

**MaxFileSizeMb** Imposta la dimensione massima del report in MB. *L'impostazione predefinita è 1000.  Il valore massimo è 2000.*

**ModelCleanupCycleminutes** Imposta il ciclo di pulizia del modello in minuti. *L'impostazione predefinita è 15.*

**OfficeAccessTokenExpirationSeconds** ***(solo Server di report di Power BI)*** Imposta la durata prima della scadenza del token di accesso di Office in secondi. *Il valore predefinito è 60.*

**OfficeOnlineDiscoveryURL** ***(solo Server di report di Power BI)*** Imposta l'indirizzo dell'istanza di Office Online Server per la visualizzazione delle cartelle di lavoro di Excel.

**RequireIntune** Richiede che Intune acceda ai report dell'organizzazione tramite l'app Power BI per dispositivi mobili. *Il valore predefinito è False.*

**ScheduleRefreshTimeoutMinutes** ***(solo Server di report di Power BI)*** Imposta il tempo desiderato per il timeout dell'aggiornamento predefinito. *Il valore predefinito è 120.*

**ShowDownloadMenu** Abilita il menu di download degli strumenti client. *Il valore predefinito è True.*

**SupportedHyperlinkSchemes** ***(solo Power BI Report Server)*** Consente di impostare un elenco delimitato da virgole degli schemi URI di cui è consentita la definizione nelle azioni dei collegamenti ipertestuali di cui è consentito il rendering, o "&ast;" per abilitare tutti gli schemi di collegamento ipertestuale. Se ad esempio si imposta "http,https", sono consentiti collegamenti ipertestuali a "https://www. contoso.com", ma i collegamenti ipertestuali a "mailto:bill@contoso.com" o a "javascript:window.open('www.contoso.com', '_blank')" vengono rimossi. Il valore predefinito è "&ast;".

**TimeInitialDelaySeconds** Imposta il ritardo iniziale desiderato in secondi. *Il valore predefinito è 60.*

**TrustedFileFormat** Imposta tutti i formati di file esterni che vengono aperti all'interno del browser nel sito del portale di Reporting Services. Per i formati di file esterni non inclusi nell'elenco viene proposto il download dell'opzione nel browser. I valori predefiniti sono jpg, jpeg, jpe, wav, bmp, pdf, img, gif, json, mp4, web, png.

**EnablePowerBIReportExportData** ***(solo Server di report di Microsoft Power BI)***  
Abilita l'esportazione di dati del Server di report di Power BI da oggetti visivi di Power BI. I valori sono True e False.  Il valore predefinito è True.  

**ScheduleRefreshTimeoutMinutes** ***(solo server di report di Microsoft Power BI)***  
Timeout in minuti per l'aggiornamento dei dati nell'aggiornamento pianificato dei report di Power BI con modelli AS incorporati. Il valore predefinito è 120 minuti.

**EnableTestConnectionDetailedErrors**  
Indica se inviare messaggi di errore dettagliati al computer client quando gli utenti verificano le connessioni all'origine dati mediante il server di report. Il valore predefinito è **true**. Se l'opzione viene impostata su **false**, vengono inviati solo messaggi di errore generici.

## <a name="see-also"></a>Vedere anche

[Impostare le proprietà di un server di report &#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md)   
[Eseguire la connessione a un server di report in Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
[Proprietà di Reporting Services](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties.md)   
[Guida sensibile al contesto del server di report in Management Studio](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
[Proprietà di sistema del server di report](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md)   
[Utilizzare script per l'esecuzione di attività di distribuzione e di amministrazione](../../reporting-services/tools/script-deployment-and-administrative-tasks.md)   
[Abilitare e disabilitare la funzionalità Report personali](../../reporting-services/report-server/enable-and-disable-my-reports.md)  

Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
