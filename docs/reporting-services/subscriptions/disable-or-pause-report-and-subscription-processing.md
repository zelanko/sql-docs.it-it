---
title: Disabilitare o sospendere l'elaborazione di report e sottoscrizioni | Microsoft Docs
ms.date: 06/19/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: subscriptions
ms.topic: conceptual
helpviewer_keywords:
- pausing schedules
- subscriptions [Reporting Services], pausing
- report processing [Reporting Services], pausing
- shared data sources [Reporting Services]
- pausing subscription processing
- pausing report processing
- temporarily stopping report processing
- disabling shared data sources
- roles [Reporting Services], modifying
- shared schedules [Reporting Services], pausing
ms.assetid: 3cf9a240-24cc-46d4-bec6-976f82d8f830
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: bfebb45330ef9775a3e707ad244122654a1f582e
ms.sourcegitcommit: 3f2936e727cf8e63f38e5f77b33442993ee99890
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/21/2019
ms.locfileid: "67314000"
---
# <a name="disable-or-pause-report-and-subscription-processing"></a>Disabilitare o sospendere l'elaborazione di report e sottoscrizioni  
Esistono diversi approcci per disabilitare o sospendere l'elaborazione di report e sottoscrizioni di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Gli approcci descritti in questo articolo vanno dalla disabilitazione di una sottoscrizione all'interruzione della connessione all'origine dati. Non tutti gli approcci sono possibili con entrambi [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] le modalità del server. I seguenti riepilogano i metodi di tabelle e supportato [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] le modalità server:  
  
##  <a name="bkmk_top"></a> Contenuto dell'articolo  
  
||Modalità server supportata|  
|-|---------------------------|  
|[Abilitare e disabilitare le sottoscrizioni](#bkmk_disable_subscription)|Modalità nativa|  
|[Sospendere una pianificazione condivisa](#bkmk_pause_schedule)|Modalità nativa e modalità SharePoint|  
|[Disabilitare un'origine dati condivisa](#bkmk_disable_shared_datasource)|Modalità nativa e modalità SharePoint|  
|[Modificare le assegnazioni di ruolo per impedire l'accesso a un report (modalità nativa)](#bkmk_modify_role_assignment)|Modalità nativa|  
|[Rimuovere le autorizzazioni per la gestione della sottoscrizione dal ruolo (modalità nativa)](#bkmk_remove_manage_subscriptions_permission)|Modalità nativa|  
|[Disabilitare le estensioni per il recapito](#bkmk_disable_extensions)|Modalità nativa e modalità SharePoint|  
  
##  <a name="bkmk_disable_subscription"></a>Abilitare e disabilitare le sottoscrizioni  
  
>[!TIP]  
>Novità di SQL 2016 Reporting Services *abilitare e disabilitare le sottoscrizioni*. Sono disponibili nuove opzioni dell'interfaccia utente che consentono di abilitare e disabilitare rapidamente le sottoscrizioni. Le sottoscrizioni disabilitate mantengono le rispettive proprietà di configurazione, ad esempio la pianificazione, e possono essere riabilitate con facilità. È possibile abilitare e disabilitare le sottoscrizioni o controllare le sottoscrizioni disabilitate anche a livello di codice.  
  
  ![I pulsanti di abilitazione e disabilitazione della pagina sottoscrizioni ](../../reporting-services/subscriptions/media/disable-or-pause-report-and-subscription-processing/subscription-enable-and-disable-buttons.png)  
  
Nel portale web, passare alla sottoscrizione dal **sottoscrizioni personali** pagina o nella **sottoscrizioni** pagina di una singola sottoscrizione. Selezionare una o più sottoscrizioni e quindi fare clic sul pulsante Disabilita o sul pulsante Abilita sulla barra multifunzione (vedere l'immagine precedente). La colonna stato passerà a "Disabilitato" o "Abilitata" rispettivamente.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Scrive una riga nel [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] accedere quando una sottoscrizione viene abilitata o disabilitata. Ad esempio, nel file di log del server di report:  
  
 `C:\Program Files\Microsoft SQL Server Reporting Services\SSRS\LogFiles\RSPortal_2019_06_20_00_49_22.log`  
  
 saranno visualizzate righe simili alle seguenti:  
  
 `RSPortal!subscription!RSPortal.exe!93!06/20/2019-01:16:47:: i INFO: Subscription 2b409d66-d4ea-408a-918c-0f9e41ce49ca disabled at 06/20/2019 01:16:47`  
  
 `RSPortal!subscription!RSPortal.exe!93!06/20/2019-01:16:51:: i INFO: Subscription 2b409d66-d4ea-408a-918c-0f9e41ce49ca enabled at 06/20/2019 01:16:51`  
  
![Contenuto correlato di PowerShell](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "Contenuto correlato di PowerShell") **Usare Windows PowerShell per disabilitare una singola sottoscrizione:** usare lo script di PowerShell seguente per disabilitare una sottoscrizione specifica. Aggiornare il nome del server e l'ID della sottoscrizione nello script.  
  
```PS  
#disable specific subscription  
$rs2010 = New-WebServiceProxy -Uri "https://SERVERNAME/ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptionID = "subscription guid";  
$rs2010.DisableSubscription($subscriptionID);  
  
```  
  
 È possibile usare lo script seguente per elencare tutte le sottoscrizioni con i relativi ID. Aggiornare il nome del server.  
  
```  
#list all subscriptions  
$rs2010 = New-WebServiceProxy -Uri "https://SERVERNAME /ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptions = $rs2010.ListSubscriptions("/");  
$subscriptions | select subscriptionid, report, status, path  
  
```  
  
 ![Contenuto correlato di PowerShell](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "Contenuto correlato di PowerShell") **Usare Windows PowerShell per elencare tutte le sottoscrizioni disabilitate:** usare lo script di PowerShell seguente per elencare tutte le sottoscrizioni disabilitate nel server di report in modalità nativa corrente. Aggiornare il nome del server.  
  
```  
#list all disabled subscriptions  
$rs2010 = New-WebServiceProxy -Uri "https://uetestb03/ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptions = $rs2010.ListSubscriptions("/");  
Write-Host "--- Disabled Subscriptions ---";  
Write-Host "----------------------------------- ";  
$subscriptions | Where-Object {$_.Active.DisabledByUserSpecified -and $_.Active.DisabledByUser } | select subscriptionid, report, status, lastexecuted,path | format-table -auto  
```  
  
 ![Contenuto correlato di PowerShell](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "Contenuto correlato di PowerShell") **Usare Windows PowerShell per abilitare tutte le sottoscrizioni disabilitate:** usare lo script di PowerShell seguente per abilitare tutte le sottoscrizioni attualmente disabilitate. Aggiornare il nome del server.  
  
```  
#enable all subscriptions  
$rs2010 = New-WebServiceProxy -Uri "https://SERVERNAME/ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptions = $rs2010.ListSubscriptions("/") | Where-Object {$_.status -eq "disabled" } ;  
ForEach ($subscription in $subscriptions)  
{  
    $rs2010.EnableSubscription($subscription.SubscriptionID);  
    $subscription | select subscriptionid, report, path  
}  
  
```  
  
 ![Contenuto correlato di PowerShell](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "Contenuto correlato di PowerShell") **Usare Windows PowerShell per DISABILITARE tutte le sottoscrizioni:** usare lo script di PowerShell seguente per disabilitare **TUTTE** le sottoscrizioni.  
  
```  
#DISABLE all subscriptions  
$rs2010 = New-WebServiceProxy -Uri "https://SERVERNAME/ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptions = $rs2010.ListSubscriptions("/") ;  
ForEach ($subscription in $subscriptions)  
{  
    $rs2010.DisableSubscription($subscription.SubscriptionID);  
    $subscription | select subscriptionid, report, path  
}  
```  
  
##  <a name="bkmk_pause_schedule"></a> Sospendere una pianificazione condivisa  
 Se una sottoscrizione o un report viene eseguito in base a una pianificazione condivisa, è possibile sospendere la pianificazione per impedire l'elaborazione del report o della sottoscrizione. Tutte le operazioni di elaborazione del report o della sottoscrizione eseguite in base alla pianificazione verranno posticipate fino a quando verrà ripresa la pianificazione.  
  
-   **Modalità SharePoint:** ![Impostazioni SharePoint](../../analysis-services/media/as-sharepoint2013-settings-gear.gif "Impostazioni SharePoint") in **Impostazioni sito** selezionare **Gestisci pianificazioni condivise**. Selezionare la pianificazione e fare clic su **Sospendi pianificazioni selezionate**.  
  
-   **Modalità nativa:** nel portale web, selezionare il **delle impostazioni** pulsante ![pulsante Impostazioni](media/ssrs-portal-settings-gear.png) dalla barra dei menu nella parte superiore della schermata del portale web e selezionare **Impostazioni sito**dal menu di riepilogo a discesa. Selezionare il **pianificazioni** pressione di tab per visualizzare la pagina pianificazioni. Selezionare le caselle di controllo accanto alle pianificazioni si desidera abilitare o disabilitare e quindi selezionare il **abilitare** oppure **disabilitare** pulsante rispettivamente per eseguire l'azione desiderata. La colonna stato verrà aggiornato di conseguenza in "Disabilitato" o "Abilitato".  
  
##  <a name="bkmk_disable_shared_datasource"></a> Disabilitare un'origine dati condivisa  
 Uno dei vantaggi dell'utilizzo di origini dei dati condivise è rappresentato dalla possibilità di disabilitarle per impedire l'esecuzione di un report o di una sottoscrizione guidata dai dati. Quando si disabilita un'origine dei dati condivisa, il report viene disconnesso dalla relativa origine dei dati esterna. Dopo la disabilitazione l'origine dei dati non sarà più disponibile per tutti i report e le sottoscrizioni che la utilizzano.  
  
 Si noti che il report viene caricato anche se la relativa origine dati non è disponibile. Il report non conterrà dati, ma gli utenti con le autorizzazioni appropriate potranno accedere alle pagine delle proprietà, alle impostazioni di sicurezza, alla cronologia e alle informazioni di sottoscrizione associate al report.  
  
-   **Modalità SharePoint** : per disabilitare un'origine dati condivisa in un server di report in modalità SharePoint, passare alla raccolta documenti che contiene l'origine dati. ![Icona di origine dati condivisa](../../reporting-services/report-data/media/hlp-16datasource.png "Icona di origine dati condivisa") Fare clic sull'origine dati e quindi deselezionare la casella di controllo **Abilita questa origine dati**.  
  
-   **Modalità nativa:** per disabilitare un'origine dati condivisa in un server di report in modalità nativa, aprire l'origine dati nel portale Web e deselezionare la casella di controllo **Abilita questa origine dati**.  
  
##  <a name="bkmk_modify_role_assignment"></a> Modificare le assegnazioni di ruolo per impedire l'accesso a un report (modalità nativa)  
Un modo per rendere non disponibile un report consiste nel rimuovere temporaneamente l'assegnazione di ruolo che consente l'accesso al report. Questa strategia può essere utilizzata con tutti i report, indipendentemente dalla modalità di connessione all'origine dei dati. L'operazione ha effetto solo sul report in questione, non su altri report o elementi.  
  
 Per rimuovere l'assegnazione di ruolo, aprire il **sicurezza** pagina del report nel portale web. Se il report eredita la sicurezza da un elemento padre, è possibile selezionare **Personalizza sicurezza** e quindi selezionare **Conferma** nella finestra di dialogo **Modifica sicurezza elemento** per creare criteri di sicurezza restrittivi privi di assegnazioni di ruolo che consentono l'accesso a numerosi utenti. È possibile, ad esempio, rimuovere un'assegnazione di ruolo che consente l'accesso al gruppo Everyone e mantenere l'assegnazione di ruolo che consente l'accesso a un gruppo ristretto di utenti, ad esempio Administrators.  
  
##  <a name="bkmk_remove_manage_subscriptions_permission"></a> Rimuovere le autorizzazioni per la gestione della sottoscrizione dal ruolo (modalità nativa)  
 Per impedire agli utenti di creare sottoscrizioni, deselezionare l'attività **Gestione di sottoscrizioni individuali** per il ruolo. Se si rimuove questa attività, le pagine per le sottoscrizioni non saranno disponibili. Nel portale Web la pagina Sottoscrizioni personali risulta vuota e non può essere eliminata, anche se in precedenza conteneva sottoscrizioni. La rimozione di attività relative alle sottoscrizioni impedisce agli utenti di creare e modificare sottoscrizioni, ma non comporta l'eliminazione delle sottoscrizioni esistenti che continuano a essere eseguite finché non vengono eliminate. Per rimuovere l'autorizzazione:  
  
1.  Aprire [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. 
  
2.  Connettersi al server di report [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
3.  Espandere il nodo **Sicurezza** .  
  
4.  Espandere la **ruoli** nodo e selezionare il ruolo desiderato.  
  
5.  Fare clic con il pulsante destro del mouse sul ruolo, quindi scegliere **Proprietà**.  
  
6.  Cancella il **gestione di sottoscrizioni individuali** e il **gestire tutte le sottoscrizioni** attività.  
  
7.  Selezionare **OK** per applicare le modifiche.

  
##  <a name="bkmk_disable_extensions"></a> Disabilitare le estensioni per il recapito  
 Tutte le estensioni per il recapito installate in un server di report sono disponibili per qualsiasi utente autorizzato a creare una sottoscrizione per un determinato report. Sono disponibili le seguenti estensioni per il recapito configurate automaticamente:  
  
-   Condivisione file di Windows  
  
-   Raccolta di SharePoint (disponibile solo da un sito di SharePoint con un server di report in modalità integrata SharePoint)  
  
 Prima che sia possibile utilizzare l'estensione per il recapito tramite posta elettronica, è necessario configurarla. In caso contrario, l'estensione non sarà disponibile. Per altre informazioni, vedere [impostazioni di posta elettronica - modalità nativa di Reporting Services (Gestione configurazione)](../install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md).  
  
 Per disattivare estensioni specifiche, è possibile rimuovere voci dell'estensione nel file **RSReportServer.config** . Per altre informazioni, vedere [del file di configurazione di Reporting Services](../../reporting-services/report-server/reporting-services-configuration-files.md) e [impostazioni di posta elettronica - modalità nativa di Reporting Services (Gestione configurazione)](../install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md).  
  
 Dopo avere rimosso un'estensione per il recapito, questa non sarà più disponibile nel portale Web o in un sito di Share Point. Se si rimuove un'estensione per il recapito, alcune sottoscrizioni potrebbero diventare inattive. Assicurarsi di eliminare le sottoscrizioni o di configurarle per l'utilizzo di un'estensione per il recapito diversa prima di rimuovere un'estensione.  
  
## <a name="see-also"></a>Vedere anche  
 [Sottoscrizioni e recapito &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [File di configurazione di Reporting Services](../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [Configurare il portale Web](../../reporting-services/report-server/configure-web-portal.md)   
 [Server di report di Reporting Services &#40;modalità nativa&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [Portale Web di un server di report (modalità nativa SSRS)](../../reporting-services/web-portal-ssrs-native-mode.md)   
 [Elementi a protezione diretta](../../reporting-services/security/securable-items.md) 
  
