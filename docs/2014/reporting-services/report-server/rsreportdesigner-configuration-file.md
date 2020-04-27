---
title: File di configurazione RSReportDesigner | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Report Designer [Reporting Services], configuration file
- RSReportDesigner configuration file
ms.assetid: fdcc9c58-3bad-45b3-ba8e-c7816d64f14c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f5ba4168f5417260b0857accdb9cf8fb3fa0f3c0
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66103340"
---
# <a name="rsreportdesigner-configuration-file"></a>RSReportDesigner - file di configurazione
  Nel file RSReportDesigner.config sono archiviate le impostazioni delle estensioni per il rendering e l'elaborazione dati disponibili per Progettazione report. Le informazioni sulle estensioni per l'elaborazione dati sono contenute nell'elemento `Data`. Le informazioni sulle estensioni per il rendering sono incluse nell'elemento `Render`. L'elemento `Designer` enumera i generatori di query utilizzati in Progettazione report.  
  
 Per la visualizzazione in anteprima dei report, Progettazione report sfrutta la funzionalità incorporata nel server di report. È possibile specificare impostazioni relative al server per il supporto dell'elaborazione sul lato server locale per la visualizzazione in anteprima. Per ulteriori informazioni sulle impostazioni di configurazione del server di report, vedere [file di configurazione RSReportServer](rsreportserver-config-configuration-file.md).  
  
## <a name="file-location"></a>Percorso file  
 Il percorso del file è \Programmi\Microsoft Visual Studio 8\Common7\IDE\PrivateAssemblies.  
  
## <a name="editing-guidelines"></a>Linee guida per la modifica  
 Evitare di modificare le impostazioni di questo file, a meno che non sia stia distribuendo o rimuovendo un'estensione personalizzata, disabilitando la memorizzazione nella cache durante la visualizzazione in anteprima oppure registrando una nuova estensione per l'elaborazione dati dopo un aggiornamento tramite Service Pack.  
  
 Sono disponibili istruzioni specifiche per la modifica di file di configurazione se si personalizzano impostazioni di estensione per il rendering. Per altre informazioni, vedere [personalizzare i parametri di estensione per il rendering in RSReportServer.Config](../customize-rendering-extension-parameters-in-rsreportserver-config.md).  
  
 Per istruzioni generali su come modificare i file di configurazione, vedere [Modificare un file di configurazione di Reporting Services &#40;RSreportserver.config&#41;](modify-a-reporting-services-configuration-file-rsreportserver-config.md).  
  
## <a name="example-configuration-file"></a>File di configurazione di esempio  
 Nell'esempio seguente viene illustrato il formato del file RSReportDesigner.config.  
  
```  
<Configuration>  
  <Add Key="SecureConnectionLevel" Value="0" />  
  <Add Key="InstanceName" Value="Microsoft.ReportingServices.PreviewServer" />  
  <Add Key="SessionCookies" Value="true" />  
  <Add Key="SessionTimeoutMinutes" Value="3" />  
  <Add Key="PolicyLevel" Value="rspreviewpolicy.config" />  
  <Add Key="CacheDataForPreview" Value="true" />  
  <Extensions>  
    <Render> . . . </Render>  
    <Data> . . . </Data>  
    <Designer> . . . </Designer>  
```  
  
## <a name="configuration-settings"></a>Impostazioni di configurazione  
  
|Impostazione|Descrizione|  
|-------------|-----------------|  
|`SecureConnectionLevel`|Indica il livello di sicurezza della connessione del servizio Web. I valori validi sono compresi nell'intervallo da 0 a 3, dove 0 indica il livello meno protetto. Per altre informazioni, vedere [utilizzo di metodi del servizio Web protetti](../report-server-web-service/net-framework/using-secure-web-service-methods.md).|  
|`InstanceName`|Identificatore del server in cui viene visualizzata l'anteprima. Non modificare questo valore.|  
|`SessionCookies`|Indica se il server di report utilizza i cookie del browser per mantenere le informazioni sulla sessione. I valori validi includono `true` e `false`. Il valore predefinito è `true`. Se si imposta questo valore su False, i dati della sessione vengono archiviati nel database **reportservertempdb** .|  
|`SessionTimeoutMinutes`|Indica il periodo di validità del cookie di una sessione. Il valore predefinito è 3 minuti.|  
|`PolicyLevel`|Indica il file di configurazione dei criteri di sicurezza. Il valore valido è rspreviewpolicy. config. Per ulteriori informazioni, vedere [utilizzo di Reporting Services file dei criteri di sicurezza](../extensions/secure-development/using-reporting-services-security-policy-files.md).|  
|`CacheDataForPreview`|Se viene impostata su `True`, Progettazione report archivia i dati in un file di cache nel computer locale. I valori validi sono `True` (valore predefinito) e `False`. Per altre informazioni, vedere [anteprima dei report](../reports/previewing-reports.md).|  
|`Render`|Enumera le estensioni per il rendering che Progettazione report può utilizzare per la visualizzazione in anteprima dei report. Il set di estensioni per il rendering disponibili per la visualizzazione in anteprima deve essere uguale al set di estensioni installate con il server di report.<br /><br /> `Name` indica il nome dell'estensione per il rendering. Se si decide di chiamare un'estensione per il rendering tramite il codice, utilizzare questo valore.<br /><br /> `Type` indica il nome completo della classe dell'estensione e il nome della libreria, separati da virgola.<br /><br /> `Visible` indica se il nome viene visualizzato o meno nelle interfacce utente. Il valore può essere `True` (valore predefinito) o `False`. Se si imposta `True`, il nome viene visualizzato nelle interfacce utente.|  
|`Data`|Enumera le estensioni per l'elaborazione dati che Progettazione report può utilizzare per le connessioni alle origini dei dati dei report. Il set di estensioni per l'elaborazione dati utilizzate in Progettazione report può essere uguale al set di estensioni installate con il server di report. Se si aggiungono o rimuovono estensioni personalizzate, vedere [distribuzione di un'estensione per l'elaborazione dati](../extensions/data-processing/deploying-a-data-processing-extension.md).<br /><br /> `Name` indica il nome dell'estensione per l'elaborazione dati.<br /><br /> `Type` indica il nome completo della classe dell'estensione e il nome della libreria, separati da virgola.|  
|`Designer`|Enumera i generatori di query disponibili per Progettazione report. I generatori di query presentano un'interfaccia utente che semplifica la creazione di query per il recupero dei dati da utilizzare nei report. I generatori di query possono variare a seconda dell'estensione per l'elaborazione dati. Per impostazione predefinita, in Reporting Services è disponibile un'interfaccia utente uguale per tutte le estensioni per l'elaborazione dati incluse nel prodotto. Se, tuttavia, si utilizzano estensioni per l'elaborazione dati personalizzate o di terze parti, le interfacce utente dei generatori di query potrebbero essere diverse.|  
|`PreviewProcessingServiceStartupTimeoutSeconds`|Specifica il periodo di attesa dell'avvio del servizio di elaborazione dell'anteprima prima che venga visualizzato un messaggio di errore. Il valore predefinito è 15 secondi.|  
  
## <a name="see-also"></a>Vedere anche  
 [File di configurazione di Reporting Services](reporting-services-configuration-files.md)   
 [Strumenti di progettazione query in Progettazione report SQL Server Data Tools &#40;SSRS&#41;](../report-data/query-design-tools-ssrs.md)  
  
  
