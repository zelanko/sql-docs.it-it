---
title: Impostazioni relative alle informazioni sul dispositivo HTML | Microsoft Docs
description: Informazioni sulle impostazioni relative alle informazioni sul dispositivo disponibili per il rendering in formato HTML.
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- HTML [Reporting Services], rendering
- device information settings [Reporting Services], HTML rendering
ms.assetid: f505f478-dd6d-444a-957c-34f7cfb98911
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 6d86394f22eabb73c055329b2ad583f589b45ea8
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/28/2020
ms.locfileid: "87247190"
---
# <a name="html-device-information-settings"></a>Impostazioni relative alle informazioni sul dispositivo HTML
Nella tabella seguente si elencano le impostazioni relative alle informazioni sul dispositivo per il rendering nel formato HTML.  
  
> [!IMPORTANT]  
>  Le impostazioni relative alle informazioni sui dispositivi elencate nella tabella di seguito con un **(\*)** sono deprecate, pertanto è consigliabile non usarle nelle nuove applicazioni. Per altre informazioni, vedere [Funzionalità deprecate di SQL Server Reporting Services in SQL Server 2016](../reporting-services/deprecated-features-in-sql-server-reporting-services-ssrs.md)   
  
|Impostazione|Valore|  
|-------------|-----------|  
|**AccessibleTablix**|Indica se eseguire il rendering con i metadati di accessibilità aggiuntivi per l'utilizzo con le utilità per la lettura dello schermo. I metadati di accessibilità aggiuntivi fanno in modo che il report visualizzabile sia conforme agli standard tecnici riportati di seguito definiti nella sezione 1194.22 relativa alle informazioni e alle applicazioni Intranet e Internet basate sul web nel documento Electronic and Information Technology Accessibility Standards (Sezione 508):<br /><br /> (g) Le intestazioni di riga e colonna devono essere identificate per le tabelle di dati.<br /><br /> (h) Il markup deve essere usato per associare celle di dati e celle di intestazione per le tabelle di dati che dispongono di due o più livelli logici di intestazioni di riga o colonna.|  
|**ActionScript(\*)**|Specifica il nome della funzione JavaScript da usare quando si verifica un evento relativo alla funzione, ad esempio la scelta di un segnalibro o un drill-through. Se viene specificato questo parametro, un evento relativo all'azione genererà la funzione JavaScript anziché un postback al server.|  
|**BookmarkID**|ID del segnalibro a cui passare nel report.|  
|**DocMap**|Indica se mostrare o nascondere la mappa documento del report. Il valore predefinito di questo parametro è **true**.|  
|**ExpandContent**|Indica se il report deve essere incluso in una struttura di tabella per limitarne la dimensione orizzontale.|  
|**FindString**|Testo da cercare nel report. Il valore predefinito di questo parametro è una stringa vuota.|  
|**GetImage (\*)**|Ottiene una determinata icona per l'interfaccia utente del visualizzatore HTML.|  
|**HTMLFragment**|Indica se viene creato un frammento HTML al posto di un documento HTML completo. In un frammento HTML il contenuto del report viene inserito in un elemento TABLE e gli elementi HTML e BODY vengono omessi. Il valore predefinito è **false**. Se si esegue il rendering in formato HTML usando il metodo **M:ReportExecution2005.ReportExecutionService.Render(System.String,System.String,System.String@,System.String@,System.String@, ReportExecution2005.Warning[]@,System.String[]@)** del SOAP API, è necessario impostare queste informazioni sul dispositivo su **true** se si esegue il rendering di un report con immagini. Se si esegue il rendering tramite SOAP con la proprietà **HTMLFragment** impostata su **true** , vengono creati URL contenenti informazioni sulla sessione che è possibile usare per richiedere correttamente le immagini. Le immagini devono essere risorse caricate nel database del server di report.|  
|**ImageConsolidation**|Indica se consolidare il grafico, la mappa, il misuratore e le immagini dell'indicatore di cui è stato eseguito il rendering in un'unica grande immagine. Il consolidamento di immagini consente di migliorare le prestazioni del report nel browser del client quando il report contiene molti elementi di visualizzazione dei dati. Il valore predefinito per i browser più recenti è **true** .|  
|**JavaScript**|Indica se JavaScript è supportato nel report visualizzabile. Il valore predefinito è **true**.|  
|**LinkTarget**|Destinazione dei collegamenti ipertestuali nel report. È possibile impostare come destinazione una finestra o un frame fornendo il nome della finestra, ad esempio **LinkTarget**=*window_name*oppure impostare come destinazione una finestra nuova usando **LinkTarget**=_blank. Altri nomi di destinazione validi includono _self, _parent e _top.|  
|**OnlyVisibleStyles(\*)**|Indica che vengono generati solo gli stili condivisi per la pagina di cui è stato attualmente eseguito il rendering.|  
|**OutlookCompat**|Indica se eseguire il rendering con metadati aggiuntivi che comportano una visualizzazione migliore del report in Outlook, mentre per altri il valore predefinito è **false**.|  
|**Parameters**|Indica se mostrare o nascondere l'area dei parametri della barra degli strumenti. Se si imposta questo parametro su **true**, l'area dei parametri della barra degli strumenti viene visualizzata. Il valore predefinito di questo parametro è **true**.|  
|**PrefixId**|Se usato con **HTMLFragment**, aggiunge il prefisso specificato a tutti gli attributi **ID** nel frammento HTML creato.|  
|**ReplacementRoot(\*)**|Stringa da anteporre a tutti i collegamenti di drill-through, attivazione/disattivazione e segnalibro nel report quando viene eseguito il rendering al di fuori del controllo ReportViewer. Ad esempio, viene usata per il reindirizzamento di un clic utente a una pagina personalizzata.|  
|**ResourceStreamRoot(\*)**|Stringa da anteporre all'URL per tutte le risorse dell'immagine, ad esempio le immagini per l'attivazione o la disattivazione oppure l'ordinamento.|  
|**Sezione**|Numero di pagina del report di cui eseguire il rendering. Un valore **0** indica che viene eseguito il rendering di tutte le sezioni del report. Il valore predefinito è **1**.|  
|**StreamRoot (\*)**|Percorso usato per anteporre un prefisso al valore dell'attributo **src** dell'elemento IMG nel report HTML restituito dal server di report. Per impostazione predefinita, il percorso viene fornito dal server di report. È possibile usare questa impostazione per specificare un percorso radice per le immagini in un report, ad esempio **https://\<servername>/risorse/immaginiazienda**.|  
|**StyleStream**|Indica se stili e script vengono creati come flusso separato anziché nel documento. Il valore predefinito è **false**.|  
|**Barra degli strumenti**|Indica se mostrare o nascondere la barra degli strumenti. Il valore predefinito di questo parametro è **true**. Se il valore di questo parametro è **false**, tutte le opzioni rimanenti (ad eccezione della mappa documento) vengono ignorate. Se si omette questo parametro, la barra degli strumenti viene visualizzata automaticamente nei formati di rendering che la supportano.<br /><br /> Il rendering della barra degli strumenti del Visualizzatore report viene eseguito quando si usano l'accesso con URL per il rendering di un report, ma non quando si usano l'API SOAP. L'impostazione relativa alle informazioni sul dispositivo **Toolbar** influisce tuttavia sulla modalità di visualizzazione del report in caso di utilizzo del metodo **Render** SOAP. Se il valore di questo parametro è **true** quando si usano SOAP per eseguire il rendering in formato HTML, viene eseguito il rendering solo della prima sezione del report. Se il valore è **false**, viene eseguito il rendering dell'intero report HTML come singola pagina HTML.|  
|**UserAgent**|La stringa **user-agent** del browser che effettua la richiesta, situata nella richiesta HTTP.|  
|**Zoom (\*)**|Valore di zoom del report come percentuale di un valore intero o come costante stringa. I valori stringa standard comprendono **Page Width** e **Whole Page**. Questo parametro viene ignorato dalle versioni di [!INCLUDE[msCoName](../includes/msconame-md.md)] Internet Explorer precedenti a Internet Explorer 5.0 e da tutti i browser non[!INCLUDE[msCoName](../includes/msconame-md.md)] . Il valore predefinito di questo parametro è **100**.|  
|**DataVisualizationFitSizing**|Indica il comportamento di adattamento della visualizzazione dei dati all'interno di una tablix. Sono inclusi grafici, misuratori e mappe.<br /><br /> I valori possibili sono **Approssimato** ed **Esatto**.<br /><br /> Il valore predefinito è **Approssimato**. Se l'impostazione viene rimossa dal file **rsreportserver.config** il comportamento predefinito è **Esatto**.<br /><br /> L'abilitazione del ridimensionamento **Esatto** può avere impatto sulle prestazioni perché l'elaborazione per determinare la dimensione esatta potrebbe impiegare più molto tempo di un adattamento approssimativo.|  
  
## <a name="see-also"></a>Vedere anche  
 [Passaggio delle impostazioni relative alle informazioni sul dispositivo alle estensioni per il rendering](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [Personalizzare i parametri di estensione per il rendering in RSReportServer.Config](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [Riferimento tecnico &#40;SSRS&#41;](../reporting-services/technical-reference-ssrs.md)  
  
  
