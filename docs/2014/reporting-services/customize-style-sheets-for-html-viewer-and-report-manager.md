---
title: Personalizzare i fogli di stile per il visualizzatore HTML e gestione di Report | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- style sheets [Reporting Services]
ms.assetid: df805cff-b1de-4062-b2ac-423f37390fbd
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d9c4a57413db37c8f93b1a311542398417bfeff0
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "59969527"
---
# <a name="customize-style-sheets-for-html-viewer-and-report-manager"></a>Personalizzare i fogli di stile per il visualizzatore HTML e Gestione report
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] fornisce stile CSS predefiniti file sheets (CSS) che definiscono stili per il **report** sulla barra degli strumenti Visualizzatore HTML e per gestione Report. Gli sviluppatori Web o gli utenti con esperienza nella creazione di fogli di stile CSS possono modificare gli stili predefiniti a loro rischio per modificare i colori, i tipi di carattere e il layout della barra degli strumenti di Gestione report. Né i fogli di stile predefiniti né le istruzioni relative alla loro modifica sono documentati in questa versione.  
  
 L'errata modifica dei fogli di stile può causare errori all'apertura dei report. Se non si conoscono con esattezza le procedure per modificare i fogli di stile, utilizzare quelli predefiniti. Se si decide di personalizzare i fogli di stile, creare un backup di tutti i file con estensione css predefiniti prima di apportare qualsiasi modifica.  
  
 La modifica dei fogli di stile non comporta alcuna conseguenza sull'aspetto di report pubblicati eseguiti in un server di report. In [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]i report non fanno riferimento a fogli di stile. I report ad hoc generati automaticamente dal server di report utilizzano le informazioni di stile archiviate come risorsa incorporata nei file di programma del server di report. I report creati in Progettazione report utilizzano i tipi di carattere, i colori e il layout specificati nelle relative definizioni. Gli stili vengono creati inline con il resto del layout.  
  
> [!NOTE]  
>  Se si desidera utilizzare stili di report predefiniti, utilizzare la Creazione guidata report per creare un report. Nella Creazione guidata report sono disponibili numerosi temi che è possibile utilizzare per creare report con stili che utilizzano tipi di carattere e combinazioni di colori diversi. È possibile modificare i modelli di stile che definiscono i temi per un report.  
  
## <a name="reporting-services-style-sheets"></a>Fogli di stile di Reporting Services  
 Nella tabella seguente vengono descritti i fogli di stile CSS utilizzati in un'installazione di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
|Foglio di stile|Descrizione|  
|-----------------|-----------------|  
|Htmlviewer.css|Foglio di stile di esempio che è possibile utilizzare come modello per creare stili personalizzati per la barra degli strumenti **report** del Visualizzatore HTML.<br /><br /> Gli stili predefiniti utilizzati dal Visualizzatore HTML vengono compilati nel server di report. Nel file Htmlviewer.css è contenuto un esempio degli stili utilizzati dal visualizzatore.|  
|ReportingServices.css|Definisce gli stili per Gestione report.|  
  
> [!NOTE]  
>  I fogli di stile vengono usati per la documentazione online di gestione Report e non devono mai essere modificati: CSS e mailto. Altri fogli di stile definiscono stili per i report e per Gestione report aperti in web part di SharePoint. Tali fogli di stile includono Rswebparts.css, Sp_full.css e Sp_small.css. Non è consigliabile modificare i fogli di stile di SharePoint. Per altre informazioni sull'uso di Web part, vedere [esplorare nativo modalità report con Web part di SharePoint e visualizzazione &#40;SSRS&#41;](reports/view-and-explore-native-mode-reports-using-sharepoint-web-parts-ssrs.md).  
  
## <a name="configuring-reporting-services-to-use-a-custom-style-sheet"></a>Configurazione di Reporting Services per l'utilizzo di un foglio di stile personalizzato  
 Il foglio di stile deve essere un file con estensione css valido e deve essere contenuto nella cartella Styles. Per impostazione predefinita, si trova nella cartella Styles \< *unità*>: \Programmi\Microsoft SQL Server\MSSQL. *n*services\reportserver\styles.  
  
 Per utilizzare un foglio di stile personalizzato per il Visualizzatore HTML in fase di esecuzione, è possibile procedere in uno dei modi seguenti:  
  
-   Aggiungere il <`HTMLViewerStyleSheet`> impostando sul [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] file di configurazione.  
  
-   Specificare il foglio di stile nell'URL del report.  
  
### <a name="modifying-the-rsreportserverconfig-file"></a>Modifica del file RSReportServer.config  
 È possibile modificare il file RSReportServer.config per specificare un foglio di stile personalizzato per il Visualizzatore HTML. Il <`HTMLViewerStyleSheet`> impostazione non è incluso nel file per impostazione predefinita. È necessario digitarla nella <`Configuration`> selezione di RSReportServer. config di file e quindi specificare il foglio di stile da usare. Non includere l'estensione del file css quando si specifica il foglio di stile.  
  
 Nell'esempio seguente viene illustrato come specificare il foglio di stile:  
  
```  
<Configuration>  
...  
          <HTMLViewerStyleSheet>MyStyleSheet</HTMLViewerStyleSheet>  
...  
</Configuration>  
```  
  
### <a name="specifying-a-style-sheet-on-a-report-url"></a>Impostazione di un foglio di stile nell'URL del report  
 È possibile utilizzare il parametro di accesso dell'URL `rc:StyleSheet` per specificare un foglio di stile personalizzato nell'URL del report. Per altre informazioni su come specificare i parametri di accesso tramite URL, vedere [riferimento ai parametri di accesso URL](url-access-parameter-reference.md).  
  
 Nell'esempio seguente viene illustrato come aggiungere stili personalizzati:  
  
```  
http://localhost/reportserver?/AdventureWorksSampleReports/Product+Line+Sales&rs:Command=Render&rc:Stylesheet=MyStyleSheet  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione report &#40;modalità nativa SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Visualizzatore HTML e barra degli strumenti Report](html-viewer-and-the-report-toolbar.md)   
 [File di configurazione RSReportServer](report-server/rsreportserver-config-configuration-file.md)  
  
  
