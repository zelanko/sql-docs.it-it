---
title: Funzionalità (modalità SharePoint) e impostazioni del sito di Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: e0040fec-e2b7-4099-ae01-3b9bb9128bbd
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: b2e6997afd52c8b999d981c5c15b782ad9a56407
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56031072"
---
# <a name="reporting-services-site-settings-and-site-featuressharepoint-mode"></a>Funzionalità e impostazioni del sito di Reporting Services (modalità SharePoint)
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] La modalità SharePoint include diverse funzionalità personalizzate a livello di sito e la funzionalità del sito che può essere gestita dalla pagina Impostazioni sito SharePoint. Le impostazioni sono a livello di sito e riguardano tutte le applicazioni di servizio [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . Per visualizzare questa pagina, è necessario disporre delle autorizzazioni Gestione contenuto e Amministratore sistema.  
  
|Impostazione del sito|Descrizione|  
|------------------|-----------------|  
|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] Impostazioni sito|Le impostazioni a livello di sito descritte in questo argomento.|  
|Gestisci avvisi dati|Funzionalità di gestione dei dati di avviso.|  
|Sincronizzazione file server di report|Funzionalità a livello di sito che è disattivata per impostazione predefinita.<br /><br /> Sincronizza i file del server di report (estensioni .rdl, .rsds, .smdl, .rsd, .rsc, .rdlx) da una raccolta documenti di SharePoint al server di report quando i file vengono aggiunti o aggiornati direttamente nella raccolta documenti.<br /><br /> Per altre informazioni, vedere [Attivare la funzionalità Sincronizzazione file server di report in Amministrazione centrale SharePoint](../../2014/reporting-services/activate-report-server-file-sync-feature-sharepoint-central-administration.md)|  
  
## <a name="to-open-the-reporting-services-site-settings-page"></a>Per aprire la pagina Impostazioni sito di Reporting Services  
  
1.  Del sito di SharePoint **Azioni sito** dal menu **Impostazioni sito**.  
  
2.  Nella sezione **Reporting Services** fare clic su **Impostazioni del sito per Reporting Services**.  
  
## <a name="options-for-reporting-services-site-settings"></a>Opzioni per Impostazioni del sito per Reporting Services  
  
|Opzione|Descrizione|  
|------------|-----------------|  
|**Consenti download del controllo ActiveX RSClientPrint**|Il controllo visualizza una finestra di dialogo di stampa personalizzata che supporta funzionalità comuni ad altre finestre di dialogo di stampa, inclusi l'anteprima di stampa, la selezione delle pagine per specificare pagine e intervalli, i margini delle pagine e l'orientamento. Per altre informazioni sul controllo, vedere [Utilizzo del controllo RSClientPrint in applicazioni personalizzate](report-server-web-service/net-framework/using-the-rsclientprint-control-in-custom-applications.md)|  
|**Abilita i messaggi di errore in modalità locale**|Mostra o nasconde i messaggi di errore dettagliati nei computer remoti quando in esecuzione in modalità locale. Se viene visualizzato un messaggio di errore simile al seguente è possibile che l'abilitazione di errori remoti sia utile:<br /><br /> `For more information about this error navigate to the report server on the local server machine or enable remote errors`|  
|**Abilita i metadati di accessibilità per i report**|Abilita i metadati di accessibilità nell'output HTML per i report|  
|**Abilita ridimensionamento visualizzazioni di dati esatto per i report**|Configurare il comportamento di adattamento per la visualizzazione dei dati in una tablix, in modo che si adattino esattamente. Sono inclusi grafici, misuratori e mappe. Se l'opzione è disabilitata, il comportamento per la visualizzazione dei dati consiste nell'adattamento approssimativo che potrebbe lasciare spazi vuoti. Questa impostazione si applica solo al rendering nella Web part del visualizzatore di report. Per gestire questo comportamento per il rendering lato server è necessario modificare il file **rsreportserver.config** . Per ulteriori informazioni, vedere quanto segue:<br /><br /> [File di configurazione RSReportServer](report-server/rsreportserver-config-configuration-file.md).<br /><br /> [Personalizzare i parametri di estensione per il rendering in RSReportServer.config](customize-rendering-extension-parameters-in-rsreportserver-config.md).<br /><br /> [Impostazioni relative alle informazioni sul dispositivo HTML](html-device-information-settings.md).<br /><br /> L'abilitazione del ridimensionamento esatto può avere impatto sulle prestazioni perché l'elaborazione per determinare la dimensione esatta potrebbe impiegare più molto tempo di un adattamento approssimativo.|  
  
## <a name="see-also"></a>Vedere anche  
 [Gestire un'applicazione di servizio SharePoint di Reporting Services](../../2014/reporting-services/manage-a-reporting-services-sharepoint-service-application.md)  
  
  
