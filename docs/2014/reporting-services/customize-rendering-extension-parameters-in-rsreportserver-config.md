---
title: Personalizzare i parametri di estensione per il rendering in RSReportServer.config. | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- configuration options [Reporting Services]
- DeviceInfo settings
- rendering extensions [Reporting Services], overriding behaviors
- parameters [Reporting Services], report rendering
- overriding report rendering behavior
- extensions [Reporting Services], rendering
ms.assetid: 3bf7ab2b-70bb-41c8-acda-227994d15aed
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: efdea595034f91497befdc7f7b12adacef8d73ff
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66109550"
---
# <a name="customize-rendering-extension-parameters-in-rsreportserverconfig"></a>Personalizzare i parametri di estensione per il rendering in RSReportServer.config.
  È possibile specificare i parametri di estensione per il rendering nel file di configurazione RSReportServer per sostituire il comportamento di rendering predefinito per i report in esecuzione in un server di report di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . È possibile modificare i parametri di estensione per il rendering per ottenere gli obiettivi seguenti:  
  
-   Modificare il nome dell'estensione per il rendering nell'elenco Esporta sulla barra degli strumenti del report, cambiando, ad esempio, "Archivio Web" in "MHTML" oppure localizzare il nome in una lingua diversa.  
  
-   Creare più istanze della stessa estensione per il rendering, per supportare diverse opzioni di presentazione del report, ad esempio versioni con orientamento orizzontale e verticale dell'estensione per il rendering delle immagini.  
  
-   Modificare i parametri di estensione per il rendering predefiniti per utilizzare valori diversi. Il formato di output predefinito dell'estensione per il rendering delle immagini è, ad esempio, TIFF, ma è possibile modificare i parametri di estensione affinché venga utilizzato il formato EMF.  
  
 La modifica dei parametri di estensione per il rendering influisce solo sulle operazioni di rendering nel server di report. Non è possibile sostituire le impostazioni dell'estensione per il rendering in un'anteprima del report in Progettazione report.  
  
 La definizione dei parametri di estensione per il rendering nei file di configurazione influisce globalmente sulle estensioni per il rendering. Le impostazioni nei file di configurazione sono utilizzate al posto dei valori predefiniti ogni volta che viene utilizzata un'estensione per il rendering specifica. Se si vuole impostare i parametri di estensione per il rendering per un'operazione di rendering o per un report specifico, è necessario specificare le informazioni sul dispositivo a livello di programmazione tramite il metodo <xref:ReportExecution2005.ReportExecutionService.Render%2A> o nell'URL di un report. Per altre informazioni sulla definizione delle impostazioni relative alle informazioni sul dispositivo per un'operazione di rendering e per visualizzare l'elenco completo di tali impostazioni, vedere [Passaggio delle impostazioni relative alle informazioni sul dispositivo alle estensioni per il rendering](report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md).  
  
## <a name="finding-and-modifying-rsreportserverconfig"></a>Individuazione e modifica del file RSReportServer.config  
 Le impostazioni di configurazione per i formati di output del report vengono specificate come parametri di estensione per il rendering nel file RSReportServer.config. Per specificare i parametri di estensione per il rendering nei file di configurazione, è necessario saper definire le strutture XML per l'impostazione dei parametri di rendering. È possibile modificare due strutture XML:  
  
-   L'elemento `OverrideNames` definisce il nome visualizzato e la lingua dell'estensione per il rendering.  
  
-   La struttura XML `DeviceInfo` definisce le impostazioni relative alle informazioni sul dispositivo utilizzate da un'estensione per il rendering. La maggior parte dei parametri di estensione per il rendering viene specificata come impostazioni relative alle informazioni sul dispositivo.  
  
 Per modificare il file, è possibile utilizzare un editor di testo. Il file RSReportServer.config si trova nella cartella \Reporting Services\Report Server\Bin. Per altre informazioni su come modificare il file di configurazione, vedere [Modificare un file di configurazione di Reporting Services &#40;RSreportserver.config&#41;](report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md).  
  
## <a name="changing-the-display-name"></a>Modifica del nome visualizzato  
 Il nome di un'estensione per il rendering viene visualizzato nell'elenco Esporta sulla barra degli strumenti del report. Tra i nomi visualizzati predefiniti vi sono Archivio Web, File TIFF e File Acrobat (PDF). È possibile sostituire il nome visualizzato predefinito con un valore personalizzato specificando l'elemento `OverrideNames` nei file di configurazione. Se si stanno definendo due istanze di un'unica estensione per il rendering, è inoltre possibile utilizzare l'elemento `OverrideNames` per distinguere ogni istanza nell'elenco Esporta.  
  
 Poiché i nomi visualizzati sono localizzati, se si sta sostituendo il nome visualizzato predefinito con un valore personalizzato, è necessario impostare l'attributo `Language`. In caso contrario, eventuali nomi specificati verranno ignorati. La lingua impostata deve essere valida per il computer del server di report. Se, ad esempio, il server di report è in esecuzione in un sistema operativo francese, è necessario specificare "fr-FR" come valore dell'attributo.  
  
 Nell'esempio seguente viene illustrato come definire un nome personalizzato in un server di report inglese:  
  
```  
<Extension Name="XML" Type="Microsoft.ReportingServices.Rendering.DataRenderer.XmlDataReport,Microsoft.ReportingServices.DataRendering">  
   <OverrideNames>  
     <Name Language="en-US">My Custom Display Name for XML Rendering</Name>  
   </OverrideNames>  
</Extension>  
```  
  
## <a name="changing-device-information-settings"></a>Modifica delle impostazioni relative alle informazioni sul dispositivo  
 Per modificare le impostazioni predefinite relative alle informazioni sul dispositivo utilizzate da un'estensione per il rendering già distribuita nel server di report, digitare la struttura XML `DeviceInfo` nei file di configurazione. Ogni estensione per il rendering supporta impostazioni relative alle informazioni sui dispositivi specifici per quella estensione. Per l'elenco completo delle impostazioni relative alle informazioni sul dispositivo, vedere [Passaggio delle impostazioni relative alle informazioni sul dispositivo alle estensioni per il rendering](report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md).  
  
 Nell'esempio seguente vengono illustrate la struttura XML e la sintassi per la modifica delle impostazioni predefinite dell'estensione per il rendering delle immagini:  
  
```  
<Render>  
    <Extension Name="IMAGE (EMF)" Type="Microsoft.ReportingServices.Rendering.ImageRenderer.ImageRenderer,Microsoft.ReportingServices.ImageRendering">  
        <OverrideNames>  
            <Name Language="en-US">Image (EMF)</Name>  
        </OverrideNames>  
        <Configuration>  
            <DeviceInfo>  
                <ColorDepth>32</ColorDepth>  
                <DpiX>300</DpiX>  
                <DpiY>300</DpiY>  
                <OutputFormat>EMF</OutputFormat>  
            </DeviceInfo>  
        </Configuration>  
    </Extension>  
</Render>  
```  
  
## <a name="configuring-multiple-entries-for-a-rendering-extension"></a>Configurazione di più voci per un'estensione per il rendering  
 È possibile creare più istanze della stessa estensione per il rendering, per supportare diverse opzioni di presentazione del report. Per ogni istanza definita è possibile specificare una diversa combinazione di valori dei parametri. Quando si definiscono nuove istanze di un'estensione per il rendering esistente, accertarsi di eseguire le operazioni seguenti:  
  
-   Specificare un nome univoco per l'estensione.  
  
     L'attributo `Name` di ogni istanza deve avere un valore univoco. Nell'esempio seguente vengono utilizzati i nomi "IMAGE (EMF Landscape)" e "IMAGE (EMF Portrait)" per distinguere tra le due istanze.  
  
     Fare attenzione quando si modifica il nome di un'estensione per il rendering già distribuita. Gli sviluppatori che specificano estensioni per il rendering a livello di programmazione utilizzano i nomi delle estensioni per identificare l'istanza da utilizzare per un'operazione di rendering specifica. Se nel server di report sono in esecuzione applicazioni di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] personalizzate, verificare che lo sviluppatore sia informato se si modifica il nome di un'estensione esistente o se ne aggiunge uno nuovo.  
  
-   Specificare un nome visualizzato univoco per consentire agli utenti di comprendere le differenze per ogni formato di output.  
  
     Se si configurano più versioni della stessa estensione, è possibile assegnare a ogni versione un nome univoco specificando un valore per `OverrideNames`. In caso contrario, nell'elenco relativo alle opzioni di esportazione sulla barra degli strumenti del report tutte le versioni dell'estensione avranno lo stesso nome.  
  
 Nell'esempio seguente viene illustrato come utilizzare l'estensione per il rendering delle immagini predefinita, che prevede la creazione di output in formato TIFF, per generare un output in formato EMF con orientamento verticale insieme a una seconda istanza per l'output di report in formato EMF con orientamento orizzontale. Si noti che ogni estensione ha un nome univoco. Quando si testa questo esempio, ricordarsi di scegliere report che non contengano funzionalità interattive, ad esempio opzioni per mostrare o nascondere gli elementi, matrici o collegamenti drill-through, in quanto le funzionalità di questo tipo non funzionano con l'estensione per il rendering delle immagini.  
  
```  
<Render>  
    <Extension Name="IMAGE (EMF Landscape)" Type="Microsoft.ReportingServices.Rendering.ImageRenderer.ImageRenderer,Microsoft.ReportingServices.ImageRendering">  
        <OverrideNames>  
            <Name Language="en-US">EMF in Landscape Mode</Name>  
        </OverrideNames>  
        <Configuration>  
            <DeviceInfo>  
                <OutputFormat>EMF</OutputFormat>  
                <PageHeight>8.5in</PageHeight>  
                <PageWidth>11in</PageWidth>  
            </DeviceInfo>  
        </Configuration>  
    </Extension>  
    <Extension Name="IMAGE (EMF Portrait)" Type="Microsoft.ReportingServices.Rendering.ImageRenderer.ImageRenderer,Microsoft.ReportingServices.ImageRendering">  
        <OverrideNames>  
            <Name Language="en-US">EMF in Portait Mode</Name>  
        </OverrideNames>  
        <Configuration>  
            <DeviceInfo>  
                <OutputFormat>EMF</OutputFormat>  
                <PageHeight>11in</PageHeight>  
                <PageWidth>8.5in</PageWidth>  
            </DeviceInfo>  
        </Configuration>  
    </Extension>  
</Render>  
```  
  
## <a name="see-also"></a>Vedere anche  
 [File di configurazione RSReportServer](report-server/rsreportserver-config-configuration-file.md)   
 [RSReportDesigner - file di configurazione](report-server/rsreportdesigner-configuration-file.md)   
 [Impostazioni relative alle informazioni sul dispositivo CSV](csv-device-information-settings.md)   
 [Impostazioni relative alle informazioni sul dispositivo Excel](excel-device-information-settings.md)   
 [Impostazioni relative alle informazioni sul dispositivo HTML](html-device-information-settings.md)   
 [Impostazioni relative alle informazioni sul dispositivo immagine](image-device-information-settings.md)   
 [Impostazioni relative alle informazioni sul dispositivo MHTML](mhtml-device-information-settings.md)   
 [Impostazioni relative alle informazioni sul dispositivo PDF](pdf-device-information-settings.md)   
 [Impostazioni relative alle informazioni sul dispositivo XML](xml-device-information-settings.md)  
  
  
