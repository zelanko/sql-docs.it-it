---
title: Configurare un server di report per il recapito tramite posta elettronica (SSRS Configuration Manager) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], distributing
- report servers [Reporting Services], e-mail delivery
- remote SMTP service [Reporting Services]
- distributing reports [Reporting Services], e-mail
- CDO
- Collaboration Data Objects
- SMTP settings [Reporting Services]
- e-mail [Reporting Services]
- sending reports
- mail [Reporting Services]
- local SMTP service [Reporting Services]
ms.assetid: b838f970-d11a-4239-b164-8d11f4581d83
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: c2e34258f10033c61f9966e62fa7c14025423613
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "71952328"
---
# <a name="configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager"></a>Configurare un server di report per il recapito tramite posta elettronica (Gestione configurazione SSRS)


  In [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] è disponibile un'estensione per il recapito tramite posta elettronica che consente di distribuire report tramite posta elettronica. A seconda di come viene definita la sottoscrizione tramite posta elettronica, un recapito può essere costituito da una notifica, un collegamento, un allegato o un report incorporato. L'estensione per il recapito tramite posta elettronica può essere utilizzata con la tecnologia del server di posta elettronica esistente. Il server di posta elettronica deve essere un server SMTP o un server di inoltro. Il server di report si connette a un server SMTP tramite librerie Collaboration Data Objects, o CDO, (cdosys.dll) fornite dal sistema operativo.  
  
 Per impostazione predefinita, l'estensione per il recapito tramite posta elettronica del server di report non è configurata. Per configurare al minimo l'estensione, è necessario utilizzare Gestione configurazione Reporting Services. Per impostare le proprietà avanzate, è necessario modificare il file `RSReportServer.config` . Se non è possibile configurare il server di report per utilizzare questa estensione, è possibile invece recapitare i report in una cartella condivisa. Per ulteriori informazioni, vedere [File Share Delivery in Reporting Services](../../reporting-services/subscriptions/file-share-delivery-in-reporting-services.md).  
  
||  
|-|  
|[!INCLUDE[applies](../../includes/applies-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modalità nativa|  
  
 
  
##  <a name="bkmk_configuration_requirements"></a>Requisiti di configurazione  
  
-   La funzionalità di recapito tramite posta elettronica del server di report viene implementata in oggetti CDO (Collaboration Data Objects) e per essa è richiesto un server SMTP (Simple Mail Transfer Protocol) locale o remoto o un server d'inoltro SMTP. SMTP non è supportato in tutti i sistemi operativi Windows. Se si utilizza l'edizione basata su Itanium di Windows Server 2008, SMTP non è supportato. Per ulteriori informazioni sulle opzioni di configurazione disponibili tramite CDO, vedere la pagina relativa alla [coclasse Configuration](https://go.microsoft.com/fwlink/?LinkId=98237) nel sito Web MSDN.  
  
-   L'account del servizio del server di report deve disporre dell'autorizzazione necessaria per inviare messaggi di posta elettronica nel server SMTP.  
  
-   L'estensione per il recapito tramite posta elettronica utilizza la codifica UTF-8 negli allegati di posta elettronica. Non è possibile modificare la codifica. L'estensione per il rendering HTML supporta solo la codifica UTF-8.  
  
> [!NOTE]  
>  L'estensione predefinita per il recapito tramite posta elettronica non supporta la firma digitale e la crittografia dei messaggi in uscita.  
  
 
  
##  <a name="bkmk_configure_for_local_or_remote_SMTP"></a>Configurazione di un server di report per il servizio SMTP locale o remoto  
 È possibile utilizzare un servizio SMTP locale o un server SMTP remoto o un server d'inoltro per supportare il recapito tramite posta elettronica. Se si ha accesso a un server SMTP remoto esistente, è consigliabile utilizzarlo. Se non esiste alcun server SMTP disponibile o se in seguito vengono generati errori di recapito dei report che possono essere attribuiti a errori di connessione del computer, utilizzare un servizio SMTP locale. Più avanti in questo argomento vengono forniti dettagli sulla configurazione di un server di report per un servizio locale o remoto.  
  
  
  
##  <a name="bkmk_setting_email_delivery"></a>Impostazione delle opzioni di configurazione per il recapito tramite posta elettronica  
 Prima di poter utilizzare il recapito tramite posta elettronica di Server report, è necessario impostare valori di configurazione che offrano informazioni sul server SMTP da utilizzare.  
  
 Per configurare un server di report per il recapito tramite posta elettronica, eseguire le operazioni seguenti:  
  
-   Utilizzare Gestione configurazione Reporting Services se si specifica soltanto un server SMTP e un account utente con autorizzazione a inviare posta elettronica. Si tratta delle impostazioni minime necessarie per la configurazione dell'estensione per il recapito tramite posta elettronica di Server report. Per ulteriori informazioni, vedere [Impostazioni posta elettronica-Configuration Manager &#40;modalità nativa SSRS&#41;](../../reporting-services/install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md) e [recapito tramite posta elettronica in Reporting Services](../../reporting-services/subscriptions/e-mail-delivery-in-reporting-services.md).  
  
-   Utilizzare un editor di testo per specificare impostazioni aggiuntive nel file RSreportserver.config (facoltativo). Questo file contiene tutte le impostazioni di configurazione per il recapito tramite posta elettronica del server di report. È necessario specificare impostazioni aggiuntive in questi file se si utilizza un server SMTP locale o se il recapito tramite posta elettronica è limitato a host specifici. Per ulteriori informazioni sull'individuazione e la modifica dei file di configurazione, vedere [modificare un file di configurazione di Reporting Services &#40;&#41;RSReportServer. config](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md) documentazione online di SQL Server.  
  
> [!NOTE]  
>  Le impostazioni della posta elettronica del server di report sono basate su CDO. Per ulteriori informazioni su impostazioni specifiche, fare riferimento alla documentazione di CDO.  
  

  
##  <a name="bkmk_example_config_file"></a>Esempio di configurazione della posta elettronica del server di report  
 Nell'esempio seguente vengono illustrate le impostazioni nel file RSreportserver.config per un server SMTP remoto. Per ulteriori nella documentazione online diformazioni sulle descrizioni e sui valori validi dell'impostazione, vedere [RSReportServer Configuration File](../../reporting-services/report-server/rsreportserver-config-configuration-file.md) nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Books Onlnella documentazione online die or the CDO product documentation.  
  
```  
<RSEmailDPConfiguration>  
     <SMTPServer>mySMTPServer.Adventure-Works.com</SMTPServer>  
     <SMTPServerPort></SMTPServerPort>  
     <SMTPAccountName></SMTPAccountName>  
     <SMTPConnectionTimeout></SMTPConnectionTimeout>  
     <SMTPServerPickupDirectory></SMTPServerPickupDirectory>  
     <SMTPUseSSL></SMTPUseSSL>  
     <SendUsing>2</SendUsing>  
     <SMTPAuthenticate></SMTPAuthenticate>  
     <From>my-rs-email-account@Adventure-Works.com</From>  
     <EmbeddedRenderFormats>  
          <RenderingExtension>MHTML</RenderingExtension>  
     </EmbeddedRenderFormats>  
     <PrivilegedUserRenderFormats></PrivilegedUserRenderFormats>  
     <ExcludedRenderFormats>  
          <RenderingExtension>HTMLOWC</RenderingExtension>  
          <RenderingExtension>NULL</RenderingExtension>  
     </ExcludedRenderFormats>  
     <SendEmailToUserAlias>True</SendEmailToUserAlias>  
     <DefaultHostName></DefaultHostName>  
     <PermittedHosts>  
          <HostName>Adventure-Works.com</HostName>  
          <HostName>hotmail.com</HostName>  
     </PermittedHosts>  
</RSEmailDPConfiguration>  
```  
  

  
##  <a name="bkmk_setting_TO_field"></a>Opzioni di configurazione per l'impostazione del campo a: in un messaggio  
 Le sottoscrizioni definite dall'utente create in base alle autorizzazioni concesse dall'attività **Gestisci sottoscrizioni individuali** contengono un nome utente preimpostato che si basa sull'account utente di dominio. Quando l'utente crea la sottoscrizione, l'indirizzo del nome del destinatario incluso nel campo **A:** viene immesso automaticamente in base all'account utente di dominio della persona che crea la sottoscrizione.  
  
 Se si utilizza un server SMTP o un server d'inoltro che utilizza account di posta elettronica diversi dall'account utente di dominio, il recapito del report non riuscirà quando il server SMTP tenterà di recapitare il report a tale utente.  
  
 Per ovviare a questo problema, è possibile modificare le impostazioni di configurazione che consentono agli utenti di immettere un nome nel campo **A:**  
  
1.  Aprire RSReportServer.config con un editor di testo.  
  
2.  Impostare `SendEmailToUserAlias` su `False`.  
  
3.  Impostare `DefaultHostName` sul nome DNS (Domain Name System) o sull'indirizzo IP del server SMTP o del server d'inoltro.  
  
4.  Salvare il file.  
  
  
  
##  <a name="bkmk_options_remote_SMTP"></a>Opzioni di configurazione per il servizio SMTP remoto  
 La connessione tra il server di report e un server SMTP o un server d'inoltro viene determinata tramite le impostazioni di configurazione seguenti:  
  
-   
  `SendUsing` specifica un metodo per l'invio di messaggi. È possibile scegliere tra un servizio SMTP di rete o una directory di prelievo del servizio SMTP locale. Per utilizzare un servizio SMTP remoto, questo valore deve essere impostato su **2** nel file RSReportServer.config.  
  
-   
  `SMTPServer` specifica il server SMTP remoto o il server d'inoltro. Questo valore è obbligatorio se si utilizza un server SMTP remoto o un server d'inoltro.  
  
-   `From`imposta il valore che viene visualizzato nella riga **da:** di un messaggio di posta elettronica. Questo valore è obbligatorio se si utilizza un server SMTP remoto o un server d'inoltro.  
  
 Tra gli altri valori utilizzati per il servizio SMTP remoto sono inclusi quelli indicati di seguito. Si noti che non è necessario specificare tali valori, a meno che non si desideri ignorare i valori predefiniti.  
  
-   **SMTPServerPort** è configurato per la porta 25.  
  
-   **SMTPAuthenticate** specifica il modo in cui il server di report si connette al server SMTP remoto. Il valore predefinito è 0, ovvero nessuna autenticazione. In questo caso, la connessione viene stabilita tramite l'accesso anonimo. In base alla configurazione del dominio, potrebbe essere necessario che il server di report e il server SMTP siano membri dello stesso dominio.  
  
     Per inviare messaggi di posta elettronica a liste di distribuzione limitate, ad esempio liste di distribuzione in cui si accettano i messaggi in arrivo solo da account autenticati, impostare **SMTPAuthenticate** su **2**.  
  

  
##  <a name="bkmk_options_local_SMTP"></a>Opzioni di configurazione per il servizio SMTP locale  
 La configurazione di un servizio SMTP locale è utile se si desidera testare o risolvere i problemi di recapito tramite posta elettronica del server di report. Il servizio SMTP locale non è attivato per impostazione predefinita. Per istruzioni su come abilitarlo, vedere [configurare un server di report per il recapito tramite posta elettronica (ssrs Configuration Manager)](../../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md) e [le impostazioni di posta elettronica-Configuration Manager &#40;modalità nativa di SSRS&#41;](../../reporting-services/install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md).  
  
 La connessione tra il server di report e un server SMTP locale o un server d'inoltro viene determinata tramite le impostazioni di configurazione seguenti:  
  
-   `SendUsing`è impostato su **1**.  
  
-   **SMTPServerPickupDirectory** è impostato su una cartella nell'unità locale.  
  
    > [!NOTE]  
    >  Assicurarsi di non impostare `SMTPServer` se si utilizza un server SMTP locale.  
  
-   `From`imposta il valore che viene visualizzato nella riga **da:** di un messaggio di posta elettronica. Questo valore è obbligatorio.  
  
 
  
##  <a name="bkmk_use_configuration_manager"></a>Per configurare la posta elettronica del server di report utilizzando il Reporting Services Configuration Manager  
  
1.  Verificare che il servizio Windows ReportServer disponga delle autorizzazioni `Send As` sul server SMTP.  
  
2.  Avviare Gestione configurazione Reporting Services e connettersi all'istanza del server di report.  
  
3.  Nella pagina Impostazioni posta elettronica immettere il nome del server SMTP. Questo valore può corrispondere a un indirizzo IP, un nome UNC di un computer dell'Intranet aziendale o un nome di dominio completo.  
  
4.  In **Indirizzo mittente**immettere il nome di un account autorizzato a inviare messaggi di posta elettronica dal server SMTP.  
  
5.  Fare clic su **Apply**.  
  

  
##  <a name="bkmk_confiugre_remote_SMTP"></a>Per configurare un servizio SMTP remoto per il server di report  
  
1.  Verificare che il servizio Windows ReportServer disponga delle autorizzazioni `Send As` sul server SMTP.  
  
2.  Aprire il file RSReportServer.config in un editor di testo.  
  
3.  Verificare che <`UrlRoot`> sia impostato sull'indirizzo URL del server di report. Questo valore viene impostato quando si configura il server di report e quindi dovrebbe essere già inserito. In caso contrario, digitare l'indirizzo URL del server di report.  
  
4.  Nella sezione relativa al recapito trovare `ReportServerEmail` <>.  
  
5.  In <`SMTPServer`> digitare il nome del server SMTP. Questo valore può corrispondere a un indirizzo IP, un nome UNC di un computer dell'Intranet aziendale o un nome di dominio completo.  
  
6.  Verificare che <`SendUsing`> sia impostato su 2. Se è impostato un valore diverso, il server di report non è configurato per l'utilizzo di un servizio SMTP remoto.  
  
7.  In <`From`>, digitare il nome di un account che disponga dell'autorizzazione per l'invio di messaggi di posta elettronica dal server SMTP.  
  
8.  Salvare il file.  
  
     Il server di report utilizzerà automaticamente le nuove impostazioni e non sarà necessario riavviare il servizio. È possibile specificare impostazioni SMTP aggiuntive per configurare ulteriormente la modalità di utilizzo del server SMTP per il recapito tramite posta elettronica del server di report. Per altre nella documentazione online diformazioni, vedere [Configurnella documentazione online dig a Report Server for E-Mail Delivery](../../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md) e [RSReportServer Configuration File](../../reporting-services/report-server/rsreportserver-config-configuration-file.md) nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Books Onlnella documentazione online die.  
  

  
##  <a name="bkmk_confiugre_local_SMTP"></a>Per configurare un servizio SMTP locale per il server di report  
  
1.  Nel Pannello di controllo fare clic su **Installazione applicazioni**.  
  
2.  Fare clic su **Installazione componenti di Windows** per avviare l'Aggiunta guidata componenti di Windows.  
  
3.  Selezionare **Server applicazioni** e fare clic su **Dettagli**.  
  
4.  Selezionare **IIS (Internet Information Services)** e fare clic su **Dettagli**.  
  
5.  Selezionare la casella di controllo **Servizio SMTP** e fare clic su **OK**.  
  
6.  In Aggiunta guidata componenti di Windows fare clic su **Avanti**. Fare clic su **Fine**.  
  
7.  Nella console **Servizi** verificare che il servizio sia in esecuzione.  
  
8.  Aprire il file **RSReportServer. config** in un editor di testo.  
  
9. Verificare che `<UrlRoot>` sia impostato sull'indirizzo URL del server di report. Questo valore viene impostato quando si configura il server di report e quindi dovrebbe essere già inserito. In caso contrario, digitare l'indirizzo URL del server di report.  
  
10. Nella sezione relativa al recapito individuare `<ReportServerEmail>.`  
  
11. In `<SMTPServer>`cancellare tutti i valori eventualmente presenti per questa impostazione ma non eliminare i tag.  
  
12. Impostare `<SendUsing>` su 1. Se è impostato un valore diverso, il server di report non è configurato per l'utilizzo di un servizio SMTP locale.  
  
13. Impostare `<SMTPServerPickupDirectory>` su una cartella nell'unità locale.  
  
14. Impostare `<From>` su un account autorizzato a inviare messaggi di posta elettronica dal server SMTP.  
  
15. Salvare il file.  
  
 
  
## <a name="see-also"></a>Vedere anche  
 [Gestione configurazione Reporting Services &#40;modalità nativa&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)  
  
  
