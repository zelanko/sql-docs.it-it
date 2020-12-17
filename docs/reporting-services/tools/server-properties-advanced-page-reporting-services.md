---
title: Pagina Proprietà server - Avanzate | Microsoft Docs
description: Usare la pagina Proprietà server - Avanzate per impostare le proprietà di sistema nel server di report. Questo strumento offre un'interfaccia utente grafica che consente di impostare le proprietà senza dovere scrivere codice.
author: maggiesMSFT
ms.author: maggies
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
ms.date: 10/19/2020
monikerRange: '>=sql-server-2016'
ms.openlocfilehash: ed31e889e195cffb828f5e04e131ffd2cb71fa84
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97466662"
---
# <a name="server-properties-advanced-page---power-bi-report-server--reporting-services"></a>Pagina Proprietà server - Avanzate - Server di report di Power BI e Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

Questa pagina consente di impostare le proprietà di sistema nel server di report. Le proprietà di sistema possono essere impostate in diversi modi. Questo strumento fornisce un'interfaccia utente grafica che consente di impostare le proprietà senza dovere scrivere codice.

Per aprire questa pagina, avviare SQL Server Management Studio, connettersi a un'istanza del server di report, fare clic con il pulsante destro del mouse sul nome del server di report e scegliere **Proprietà**. Selezionare **Avanzate** per aprire la pagina.

## <a name="options"></a>Opzioni

### <a name="accesscontrolallowcredentials"></a>AccessControlAllowCredentials
(Solo Server di report di Power BI, Reporting Services 2017 e versioni successive) Indica se la risposta alla richiesta del client può essere esposta quando il flag `credentials` è impostato su true. Il valore predefinito è **false**.

### <a name="accesscontrolallowheaders"></a>AccessControlAllowHeaders
(Solo Server di report di Power BI, Reporting Services 2017 e versioni successive) Elenco di intestazioni delimitate da virgole che il server consente quando un client invia una richiesta. Questa proprietà può essere una stringa vuota. Specificando * si consentono tutte le intestazioni.

### <a name="accesscontrolallowmethods"></a>AccessControlAllowMethods
(Solo Server di report di Power BI, Reporting Services 2017 e versioni successive) Elenco di metodi HTTP delimitati da virgole che il server consente quando un client invia una richiesta. I valori predefiniti sono (GET, PUT, POST, PATCH, DELETE). Specificando * si consentono tutte le intestazioni.

### <a name="accesscontrolalloworigin"></a>AccessControlAllowOrigin
(Solo Server di report di Power BI, Reporting Services 2017 e versioni successive) Elenco di origini delimitate da virgole che il server consente quando un client invia una richiesta. Il valore predefinito è vuoto, il che impedisce tutte le richieste. Se si specifica * si consentono tutte le origini quando le credenziali non sono impostate; se vengono specificate credenziali, è necessario specificare un elenco esplicito delle origini.

### <a name="accesscontrolexposeheaders"></a>AccessControlExposeHeaders
(Solo Server di report di Power BI, Reporting Services 2017 e versioni successive) Elenco di intestazioni delimitate da virgole che il server espone ai client. Il valore predefinito è vuoto.

### <a name="accesscontrolmaxage"></a>AccessControlMaxAge
(Solo Server di report di Power BI, Reporting Services 2017 e versioni successive) Specifica il numero di secondi durante i quali i risultati della richiesta preliminare possono essere memorizzati nella cache. Il valore predefinito è 600 (10 minuti).

### <a name="allowedresourceextensionsforupload"></a>AllowedResourceExtensionsForUpload
(Solo Server di report di Power BI, Reporting Services 2017 e versioni successive) Set di estensioni delle risorse che possono essere caricate nel server di report. Non è necessario includere le estensioni per i tipi di file predefiniti, ad esempio &ast;.rdl e &ast;.pbix. Il valore predefinito è "&ast;, &ast;.xml, &ast;.xsd, &ast;.xsl, &ast;.png, &ast;.gif, &ast;.jpg, &ast;.tif, &ast;.jpeg, &ast;.tiff, &ast;.bmp, &ast;.pdf, &ast;.svg, &ast;.rtf, &ast;.txt, &ast;.doc, &ast;.docx, &ast;.pps, &ast;.ppt, &ast;.pptx".

### <a name="customheaders"></a>CustomHeaders 

(Solo Server di report di Power BI gennaio 2020, Reporting Services 2019 e versioni successive)

Imposta i valori di intestazione per tutti gli URL che corrispondono ai criteri regex specificati. Gli utenti possono aggiornare il valore CustomHeaders con un XML valido per impostare i valori di intestazione per gli URL di richiesta selezionati. Gli amministratori possono aggiungere un numero qualsiasi di intestazioni in XML. Per impostazione predefinita, in Reporting Services 2019 non sono presenti intestazioni personalizzate e il valore è vuoto. Per impostazione predefinita, in Server di report di Power BI (gennaio 2020) e versioni successive il valore è questo:

```xml
<CustomHeaders>
    <Header>
        <Name>X-Frame-Options</Name>
        <Pattern>(?(?=.*api.*|.*rs:embed=true.*|.*rc:toolbar=false.*)(^((?!(.+)((\/api)|(\/(.+)(rs:embed=true|rc:toolbar=false)))).*$))|(^(?!(http|https):\/\/([^\/]+)\/powerbi.*$)))</Pattern>
        <Value>SAMEORIGIN</Value>
    </Header>
</CustomHeaders>
```

> [!NOTE]
> La presenza di un numero troppo elevato di intestazioni può compromettere le prestazioni. 

È consigliabile convalidare la configurazione della topologia per assicurarsi che il set di intestazioni sia compatibile con la distribuzione di Reporting Services. È possibile che le impostazioni scelte generino errori nei browser se questi ultimi non dispongono delle impostazioni appropriate. Ad esempio, non è consigliabile aggiungere una configurazione HSTS se il server non è configurato per HTTPS. Le intestazioni incompatibili possono causare errori di rendering del browser.

#### <a name="customheaders-xml-format"></a>Formato XML CustomHeaders

```xml
<CustomHeaders>
    <Header>
        <Name>{Name of the header}</Name>
        <Pattern>{Regex pattern to match URLs}</Pattern>
        <Value>{Value of the header}</Value>
    </Header>
</CustomHeaders>
```

#### <a name="setting-the-customheaders-property"></a>Impostazione della proprietà CustomHeaders

- È possibile impostare la proprietà con l'endpoint SOAP [SetSystemProperties](/dotnet/api/reportservice2010.reportingservice2010.setsystemproperties) passando la proprietà CustomHeaders come parametro.
- È possibile usare l'endpoint REST [UpdateSystemProperties](https://app.swaggerhub.com/apis/microsoft-rs/PBIRS/2.0#/System/UpdateSystemProperties):  `/System/Properties` passando la proprietà CustomHeaders

#### <a name="example"></a>Esempio

L'esempio seguente illustra come impostare HSTS e altre intestazioni personalizzate per gli URL usando criteri regex corrispondenti.

```xml
<CustomHeaders>
    <Header>
        <Name>Strict-Transport-Security</Name>
        <Pattern>(.+)\/Reports\/mobilereport(.+)</Pattern>
        <Value>max-age=86400; includeSubDomains=true</Value>
    </Header>
    <Header>
        <Name>Embed</Name>
        <Pattern>(.+)(/reports/)(.+)(rs:embed=true)</Pattern>
        <Value>True</Value>
    </Header>
</CustomHeaders>
```

La prima intestazione nel codice XML precedente aggiunge l'intestazione `Strict-Transport-Security: max-age=86400; includeSubDomains=true` alle richieste corrispondenti.
- http://adventureworks/Reports/mobilereport/New%20Mobile%20Report: il criterio regex corrisponde e imposterà l'intestazione HSTS
- http://adventureworks/ReportServer/mobilereport/New%20Mobile%20Report: il criterio non corrisponde

La seconda intestazione nel codice XML precedente aggiunge l'intestazione `Embed: True` per l'URL che contiene `/reports/` e il parametro di query `rs:embed=true`.
- https://adventureworks/reports/mobilereport/New%20Mobile%20Report?rs:embed=true: corrisponde
- https://adventureworks/reports/mobilereport/New%20Mobile%20Report?rs:embed=false: non corrisponde

### <a name="editsessioncachelimit"></a>EditSessionCacheLimit
Consente di specificare il numero di voci della cache di dati che possono essere attive in una sessione di modifica del report. Il numero predefinito è 5.  

### <a name="editsessiontimeout"></a>EditSessionTimeout
Consente di specificare il numero di secondi prima del timeout di una sessione di modifica del report. Il valore predefinito è 7200 secondi (due ore). 

### <a name="enablecdnvisuals"></a>EnableCDNVisuals 
(Solo Server di report di Power BI) Se l'opzione è abilitata, i report di Power BI caricano gli oggetti visivi personalizzati certificati più recenti da una rete per la distribuzione di contenuti (rete CDN), ospitata da Microsoft. Se il server non ha accesso alle risorse Internet, è possibile disattivare questa opzione. In tal caso, gli oggetti visivi personalizzati vengono caricati dal report pubblicato nel server. L'impostazione predefinita è **True**.  

###  <a name="enableclientprinting"></a>EnableClientPrinting  
Determina se il controllo ActiveX RSClientPrint è disponibile per il download dal server di report. I valori validi sono **true** e **false**. Il valore predefinito è **true**. Per altre informazioni sulle impostazioni aggiuntive necessarie per questo controllo, vedere [Abilitare e disabilitare la stampa sul lato client per Reporting Services](../../reporting-services/report-server/enable-and-disable-client-side-printing-for-reporting-services.md).  

### <a name="enablecustomvisuals"></a>EnableCustomVisuals 
(Solo Server di report di Power BI) Abilita la visualizzazione degli oggetti visivi personalizzati di Power BI. I valori consentiti sono True o False. *Il valore predefinito è True.*  

###  <a name="enableexecutionlogging"></a>EnableExecutionLogging  
Indica se la registrazione per l'esecuzione di report è attivata. Il valore predefinito è **true**. Per altre informazioni sul log di esecuzione del server di report, vedere [Vista ExecutionLog ed ExecutionLog3 del server di report](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md).  

### <a name="enableintegratedsecurity"></a>EnableIntegratedSecurity
Determina se la sicurezza integrata è supportata per le connessioni all'origine dati del report. Il valore predefinito è **True**. I valori validi sono i seguenti:

|Valori|Descrizione|
|---------|---------|
|**True**|La sicurezza integrata di Windows è abilitata.|
|**False**|La sicurezza integrata di Windows non è abilitata. Le origini dati dei report configurate per l'uso della sicurezza integrata di Windows non verranno eseguite.|

### <a name="enableloadreportdefinition"></a>EnableLoadReportDefinition
Selezionare questa opzione per specificare se gli utenti possono eseguire un report non pianificato da un report di Generatore report. Selezionando questa opzione si imposta la proprietà **EnableLoadReportDefinition** sul server di report.  

Se si deseleziona questa opzione, la proprietà viene impostata su False. Il server di report non genererà report click-through per i report che usano un modello di report come origine dati. Qualsiasi chiamata al metodo LoadReportDefinition verrà bloccata.  

La disattivazione di questa opzione consente di attenuare i rischi di attacchi Denial of Service condotti da utenti malintenzionati tramite overload del server di report con richieste LoadReportDefinition.  

### <a name="enablemyreports"></a>EnableMyReports  
Indica se la caratteristica Report personali è abilitata. Un valore **true** indica che la caratteristica è abilitata.  

### <a name="enablepowerbireportexportdata"></a>EnablePowerBIReportExportData 
(Solo Server di report di Power BI) Abilita l'esportazione di dati del Server di report di Power BI da oggetti visivi di Power BI. I valori sono True e False.  Il valore predefinito è true. 

### <a name="enablepowerbireportexportunderlyingdata"></a>EnablePowerBIReportExportUnderlyingData 
(Solo Server di report di Power BI) Indica se un cliente può o meno esportare i dati sottostanti dagli oggetti visivi di Power BI in Server di report di Power BI. Il valore True indica che la funzionalità è abilitata.

### <a name="enableremoteerrors"></a>EnableRemoteErrors
Include informazioni esterne sugli errori, ad esempio, informazioni sull'errore relative alle origini dati del report, nei messaggi di errore restituiti agli utenti che richiedono i report dai computer remoti. I valori validi sono **true** e **false**. Il valore predefinito è **false**. Per altre informazioni, vedere [Abilita errori remoti &#40;Reporting Services&#41;](../../reporting-services/report-server/enable-remote-errors-reporting-services.md).  

### <a name="enabletestconnectiondetailederrors"></a>EnableTestConnectionDetailedErrors
Indica se inviare messaggi di errore dettagliati al computer client quando gli utenti verificano le connessioni all'origine dati mediante il server di report. Il valore predefinito è **true**. Se l'opzione viene impostata su **false**, vengono inviati solo messaggi di errore generici.

###  <a name="executionlogdayskept"></a>ExecutionLogDaysKept  
Numero di giorni durante i quali le informazioni sulle esecuzioni dei report vengono conservate nel log di esecuzione. I valori validi per questa proprietà sono compresi tra **-1** e **2**,**147**,**483**,**647**. Se il valore è **-1** le voci non vengono eliminate dalla tabella del log di esecuzione. Il valore predefinito è **60**.  

> [!NOTE]
> Se si imposta un valore pari a **0, vengono** *eliminate* tutte le voci dal log di esecuzione. Il valore **-1** mantiene le voci del log di esecuzione e non le elimina.

### <a name="executionloglevel"></a>ExecutionLogLevel
Imposta il livello del log di esecuzione. *L'impostazione predefinita è Normal.*

### <a name="externalimagestimeout"></a>ExternalImagesTimeout
Determina l'intervallo di tempo consentito per il recupero di un file di immagine esterno prima del timeout della connessione. Il valore predefinito è **600** secondi.  

### <a name="interprocesstimeoutminutes"></a>InterProcessTimeoutMinutes
(Solo Server di report di Power BI, Reporting Services 2019 e versioni successive) Imposta il timeout del processo in minuti. *L'impostazione predefinita è 30.*

### <a name="maxfilesizemb"></a>MaxFileSizeMb
Imposta le dimensioni massime del file in MB. *L'impostazione predefinita è 1000.  Il valore massimo è 2000.*

### <a name="modelcleanupcycleminutes"></a>ModelCleanupCycleMinutes 
(Solo Server di report di Power BI) Imposta la frequenza per verificare la presenza di modelli inutilizzati nella memoria in minuti. *L'impostazione predefinita è 15.*

### <a name="modelexpirationminutes"></a>ModelExpirationMinutes 
(Solo Server di report di Power BI) Imposta la frequenza per rimuovere dalla memoria i modelli inutilizzati in minuti. *Il valore predefinito è 60.*

###  <a name="myreportsrole"></a>MyReportsRole  
Nome del ruolo utilizzato durante la creazione dei criteri di sicurezza nelle cartelle Report personali dell'utente. Il valore predefinito è **My Reports Role**.  

### <a name="officeaccesstokenexpirationseconds"></a>OfficeAccessTokenExpirationSeconds 
(Solo Server di report di Power BI, Reporting Services 2019 e versioni successive) Imposta la durata prima della scadenza del token di accesso di Office in secondi. *Il valore predefinito è 60.*

### <a name="officeonlinediscoveryurl"></a>OfficeOnlineDiscoveryURL 
(Solo Server di report di Power BI) Imposta l'indirizzo dell'istanza di Office Online Server per la visualizzazione di cartelle di lavoro di Excel.

### <a name="rdlxreporttimetout"></a>RDLXReportTimetout
Valore di timeout per l'elaborazione del report RDLX *(report di Power View in un'istanza di SharePoint Server)* in secondi per tutti i report gestiti nello spazio dei nomi del server di report. È possibile eseguire l'override del valore a livello di report. Se questa proprietà è impostata, il server di report tenta di arrestare l'elaborazione di un report quando scade il tempo specificato. I valori validi sono compresi tra **-1** e **2**,**147**,**483**,**647**. Se il valore è **-1** durante l'elaborazione non si verifica alcun timeout dei report nello spazio dei nomi. Il valore predefinito è **1800**.

### <a name="requireintune"></a>RequireIntune
(Solo Server di report di Power BI, Reporting Services 2017 e versioni successive) Richiede Intune per accedere ai report dell'organizzazione tramite l'app Power BI per dispositivi mobili. *Il valore predefinito è False.*

### <a name="restrictedresourcemimetypeforupload"></a>RestrictedResourceMimeTypeForUpload
(Solo Server di report di Power BI gennaio 2019, Reporting Services 2017 e versioni successive) Set di tipi MIME con cui gli utenti non sono autorizzati a caricare contenuto. Tutte le risorse già archiviate con un tipo MIME con restrizioni possono essere scaricate solo come application/octet-stream anziché essere aperte/eseguite dal browser.  Per impostazione predefinita, nell'elenco non sono presenti elementi con restrizioni. È tuttavia consigliabile che le organizzazioni completino tale elenco per assicurare un'esperienza più sicura.

### <a name="schedulerefreshtimeoutminutes"></a>ScheduleRefreshTimeoutMinutes 
(Solo Server di report di Power BI) Timeout in minuti per l'aggiornamento dei dati nell'aggiornamento pianificato dei report di Power BI con modelli AS incorporati. Il valore predefinito è 120 minuti.

### <a name="sessiontimeout"></a>SessionTimeout
Intervallo, in secondi, durante il quale una sessione rimane attiva. Il valore predefinito è **600**.  

### <a name="sharepointintegratedmode"></a>SharePointIntegratedMode
Proprietà di sola lettura che indica la modalità del server. Se il valore è False, il server di report è in esecuzione in modalità nativa.  

### <a name="showdownloadmenu"></a>ShowDownloadMenu
(Solo Server di report di Power BI, Reporting Services 2017 e versioni successive) Abilita il menu di download degli strumenti client. *Il valore predefinito è True.*

### <a name="sitename"></a>SiteName
Nome del sito del server di report visualizzato nel titolo della pagina del portale Web. Il valore predefinito è [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Questa proprietà può essere una stringa vuota. La lunghezza massima è di 8.000 caratteri.  

### <a name="snapshotcompression"></a>SnapshotCompression
Definisce come vengono compressi gli snapshot. Il valore predefinito è **SQL**. I valori validi sono i seguenti:

|Valori|Descrizione|
|---------|---------|
|**SQL**|Gli snapshot vengono compressi quando vengono archiviati nel database del server di report. Tale compressione è il comportamento corrente.|
|**Nessuno**|Gli snapshot non vengono compressi.|
|**Tutto**|Gli snapshot vengono compressi per tutte le opzioni di archiviazione, incluso il database del server di report o il file system.|

### <a name="storedparameterslifetime"></a>StoredParametersLifetime
Specifica il numero massimo di giorni per cui è possibile conservare un parametro archiviato. I valori validi sono compresi tra **-1**, **+1** e **2,147,483,647**. Il valore predefinito è **180** giorni.  

### <a name="storedparametersthreshold"></a>StoredParametersThreshold
Specifica il numero massimo di valori dei parametri che possono essere archiviati nel server di report. I valori validi sono compresi tra **-1**, **+1** e **2,147,483,647**. Il valore predefinito è **1500**.  

### <a name="supportedhyperlinkschemes"></a>SupportedHyperlinkSchemes 
(Solo Server di report di Power BI gennaio 2019, Reporting Services 2019 e versioni successive) Imposta un elenco di schemi URI separati da virgola di cui è consentita la definizione nelle azioni dei collegamenti ipertestuali di cui è consentito il rendering, o "&ast;" per abilitare tutti gli schemi di collegamento ipertestuale. Se ad esempio si imposta "http,https", sono consentiti collegamenti ipertestuali a "https://www. contoso.com", ma vengono rimossi i collegamenti ipertestuali a "mailto:bill@contoso.com" o "javascript:window.open('www.contoso.com', '_blank')". L'impostazione predefinita è "&ast;".

### <a name="systemreporttimeout"></a>SystemReportTimeout
Valore di timeout  predefinito per l'elaborazione dei report, espresso in secondi, per tutti i report gestiti nello spazio dei nomi del server di report. È possibile eseguire l'override del valore a livello di report. Se questa proprietà è impostata, il server di report tenta di arrestare l'elaborazione di un report quando scade il tempo specificato. I valori validi sono compresi tra **-1** e **2**,**147**,**483**,**647**. Se il valore è **-1** durante l'elaborazione non si verifica alcun timeout dei report nello spazio dei nomi. Il valore predefinito è **1800**.  

### <a name="systemsnapshotlimit"></a>SystemSnapshotLimit
Numero massimo di snapshot archiviati per un report. I valori validi sono compresi tra **-1** e **2**,**147**,**483**,**647**. Se il valore è **-1**, non vi sono limiti per gli snapshot.  

### <a name="timerinitialdelayseconds"></a>TimerInitialDelaySeconds
(Solo Server di report di Power BI, Reporting Services 2017 e versioni successive) Imposta la durata del ritardo del tempo iniziale in secondi. *Il valore predefinito è 60.*

### <a name="trustedfileformat"></a>TrustedFileFormat
(Solo Server di report di Power BI, Reporting Services 2017 e versioni successive) Imposta tutti i formati di file esterni che vengono aperti all'interno del browser nel sito del portale di Reporting Services. Per i formati di file esterni non inclusi nell'elenco viene proposto il download dell'opzione nel browser. I valori predefiniti sono jpg, jpeg, jpe, wav, bmp, pdf, img, gif, json, mp4, web, png.

### <a name="usesessioncookies"></a>UseSessionCookies
Indica se il server di report deve utilizzare cookie di sessione per le comunicazioni con i browser dei client. Il valore predefinito è **true**.  

## <a name="see-also"></a>Vedere anche

[Impostare le proprietà di un server di report &#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md)   
[Eseguire la connessione a un server di report in Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
[Proprietà di Reporting Services](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties.md)   
[Guida sensibile al contesto del server di report in Management Studio](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
[Proprietà di sistema del server di report](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md)   
[Utilizzare script per l'esecuzione di attività di distribuzione e di amministrazione](../../reporting-services/tools/script-deployment-and-administrative-tasks.md)   
[Abilitare e disabilitare la funzionalità Report personali](../../reporting-services/report-server/enable-and-disable-my-reports.md)  

Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
