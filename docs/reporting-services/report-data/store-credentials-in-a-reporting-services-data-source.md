---
title: Archiviare le credenziali in un'origine dati di Reporting Services | Microsoft Docs
description: Informazioni su come configurare le credenziali archiviate per i server di report sia in modalità nativa che in modalità SharePoint.
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
ms.custom: ''
ms.date: 05/24/2018
ms.openlocfilehash: c0fd3f93cd38c562d5374ecfa65d52b082eef07b
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/17/2020
ms.locfileid: "86458200"
---
# <a name="store-credentials-in-a-reporting-services-data-source"></a>Store Credentials in a Reporting Services Data Source

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)]

::: moniker-end

È possibile configurare le credenziali archiviate usate da un server di report di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per accedere ai dati esterni di un report. Le credenziali archiviate vengono usate se il report viene eseguito in modo automatico, ad esempio una sottoscrizione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] che pubblica un report come messaggio di posta elettronica. Il server di report recupera e usa le credenziali quando viene pianificata o attivata l'elaborazione del report. Questo argomento illustra la configurazione delle credenziali archiviate per i server di report sia in modalità nativa che in modalità SharePoint.  
  
##  <a name="security-policy-requirements-for-stored-credentials"></a><a name="bkmk_top"></a> Requisiti dei criteri di sicurezza per le credenziali archiviate  
 ![as_powerpivot_refresh_sss_set_key](https://docs.microsoft.com/analysis-services/analysis-services/power-pivot-sharepoint/media/as-powerpivot-refresh-sss-set-key.gif "as_powerpivot_refresh_sss_set_key") È necessario che l'account usato per le credenziali archiviate sia configurato per uno dei criteri di sicurezza seguenti nel server di report. È consigliabile selezionare i criteri con il livello minimo di autorizzazioni per l'ambiente.  
  
1.  **Consenti accesso locale**. Per altre informazioni, vedere [Consenti accesso locale](https://technet.microsoft.com/library/cc756809\(v=WS.10\).aspx).  
  
2.  **Accesso come processo batch**. Per altre informazioni, vedere [Accesso come processo batch](https://technet.microsoft.com/library/cc755659\(v=ws.10\).aspx).  
  
3.  Per informazioni generali sui criteri, vedere [Modificare un'impostazione di sicurezza in un oggetto Criteri di gruppo](https://technet.microsoft.com/library/cc736516\(v=ws.10\).aspx).  
  
##  <a name="configure-stored-credentials-for-a-report-specific-data-source-native-mode"></a><a name="bkmk_stored_credentials_data_source_native"></a> Configurare le credenziali archiviate per un'origine dati specifica del report (modalità nativa)  
  
1.  Nel portale Web passare alla cartella che contiene il report. Fare clic sui puntini di sospensione (...) nell'angolo superiore destro del riquadro di report.  
  
2.  Fare clic su **Gestisci** , quindi su **Origini dati**.  
  
3.  Fare clic su **Origine dei dati personalizzata**.  
  
4.  Nell'elenco **Tipo di origine dati** selezionare l'estensione per l'elaborazione dati usata per elaborare i dati dell'origine dati.  
  
5.  Per **Stringa di connessione**specificare la stringa utilizzata dal server di report per la connessione all'origine dei dati. L'esempio seguente illustra una stringa di connessione usata per la connessione al database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]:  
  
    ```  
    data source=<servername>;initial catalog=AdventureWorks2012  
    ```  
  
6.  Per **Connetti tramite**selezionare **Credenziali archiviate in modo protetto nel server di report**.  
  
7.  Digitare un nome utente e una password.  
  
    -   Se l'account è un account utente di dominio Windows, specificarlo nel formato \<domain>\\<account\> e quindi selezionare **Usa come credenziali di Windows per la connessione all'origine dei dati**.  
  
    -   Se il nome utente e la password sono credenziali del database, non selezionare **Usa come credenziali di Windows per la connessione all'origine dei dati**. Se il server di database supporta la rappresentazione o la delega, selezionare **Rappresenta l'utente autenticato dopo che è stata stabilita una connessione all'origine dei dati**.  
  
8.  Fare clic su **Applica**.  
  
     ![Icona freccia usata con il collegamento Torna all'inizio](https://docs.microsoft.com/analysis-services/analysis-services/instances/media/uparrow16x16.gif "Icona freccia usata con il collegamento Torna all'inizio") [Requisiti dei criteri di sicurezza per le credenziali archiviate](#bkmk_top)  
  
##  <a name="configure-stored-credentials-for-a-report-specific-data-source-sharepoint-mode"></a><a name="bkmk_stored_credentials_data_source_sharepoint"></a> Configurare le credenziali archiviate per un'origine dati specifica del report (modalità SharePoint)  
  
1.  Passare alla raccolta documenti che contiene il report, quindi fare clic sul menu Apri ![menu di scelta rapida della raccolta documenti per gli elementi ssrs](../../reporting-services/report-data/media/ssrs-sharepoint-item-context-menu.png "menu di scelta rapida della raccolta documenti per gli elementi ssrs").  
  
2.  Fare clic sul secondo menu Apri ![menu di scelta rapida della raccolta documenti per gli elementi ssrs](../../reporting-services/report-data/media/ssrs-sharepoint-item-context-menu.png "menu di scelta rapida della raccolta documenti per gli elementi ssrs") e quindi su **Gestisci origini dati**.  
  
3.  Fare clic sul nome dell'origine dati **personalizzata** da configurare con le credenziali archiviate.  
  
4.  Nell'elenco **Tipo di origine dati** selezionare l'estensione per l'elaborazione dati usata per elaborare i dati dell'origine dati.  
  
5.  Per **Stringa di connessione**specificare la stringa utilizzata dal server di report per la connessione all'origine dei dati. L'esempio seguente illustra una stringa di connessione usata per la connessione al database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]:  
  
    ```  
    data source=<servername>;initial catalog=AdventureWorks2012  
    ```  
  
6.  Per **Credenziali**selezionare **Credenziali archiviate**.  
  
7.  Digitare un **nome utente** e una **password**.  
  
    -   Se l'account è un account utente di dominio Windows, specificarlo nel formato \<domain>\\<account\> e quindi selezionare **Usa come credenziali di Windows per la connessione all'origine dei dati**.  
  
    -   Se il nome utente e la password sono credenziali del database, non selezionare **Usa come credenziali di Windows**. Se il server di database supporta la rappresentazione o la delega, è possibile selezionare **Imposta contesto di esecuzione sull'account seguente**.  
  
8.  Fare clic su **OK**.  
  
     ![Icona freccia usata con il collegamento Torna all'inizio](https://docs.microsoft.com/analysis-services/analysis-services/instances/media/uparrow16x16.gif "Icona freccia usata con il collegamento Torna all'inizio") [Requisiti dei criteri di sicurezza per le credenziali archiviate](#bkmk_top)  
  
##  <a name="configure-stored-credentials-for-a-shared-data-source-native-mode"></a><a name="bkmk_stored_credentials_shared_data_source_native"></a> Configurare le credenziali archiviate per un'origine dati condivisa (modalità nativa)  
  
1.  Nel portale Web passare all'origine dati condivisa. 
  
2.  Fare clic sui puntini di sospensione (...) nell'angolo superiore destro del riquadro di report > **Gestisci**. 
  
3.  Nell'elenco **Tipo** specificare l'estensione per l'elaborazione dati usata per elaborare i dati dell'origine dati.  
  
4.  Per **Stringa di connessione**specificare la stringa utilizzata dal server di report per la connessione all'origine dei dati. [!INCLUDE[msCoName](../../includes/msconame-md.md)] consiglia di evitare di specificare credenziali nella stringa di connessione.  
  
     Nell'esempio riportato di seguito viene illustrata una stringa di connessione usata per connettersi al database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] locale:  
  
    ```  
    data source=<localservername>; initial catalog=AdventureWorks2012  
    ```  
  
5.  Digitare un nome utente e una password.  
  
    -   Se l'account è un account utente di dominio Windows, specificarlo nel formato \<domain>\\<account\> e quindi selezionare **Usa come credenziali di Windows per la connessione all'origine dei dati**.  
  
    -   Se il nome utente e la password sono credenziali del database, non selezionare **Usa come credenziali di Windows per la connessione all'origine dei dati**. Se il server di database supporta la rappresentazione o la delega, selezionare **Rappresenta l'utente autenticato dopo che è stata stabilita una connessione all'origine dei dati**.  
  
6.  Fare clic su **Applica**.  
  
     ![Icona freccia usata con il collegamento Torna all'inizio](https://docs.microsoft.com/analysis-services/analysis-services/instances/media/uparrow16x16.gif "Icona freccia usata con il collegamento Torna all'inizio") [Requisiti dei criteri di sicurezza per le credenziali archiviate](#bkmk_top)  
  
##  <a name="configure-stored-credentials-for-a-shared-data-source-sharepoint-mode"></a><a name="bkmk_stored_credentials_shared_data_source_sharepoint"></a> Configurare le credenziali archiviate per un'origine dati condivisa (modalità SharePoint)  
  
1.  Nella raccolta documenti passare all'origine dei dati condivisa.![Icona dell'origine dei dati condivisa](../../reporting-services/report-data/media/hlp-16datasource.png "Icona dell'origine dati condivisa")  
  
2.  Fare clic sul menu di scelta rapida ![menu di scelta rapida della raccolta documenti per gli elementi ssrs](../../reporting-services/report-data/media/ssrs-sharepoint-item-context-menu.png "menu di scelta rapida della raccolta documenti per gli elementi ssrs") e quindi sul secondo menu di scelta rapida ![menu di scelta rapida della raccolta documenti per gli elementi ssrs](../../reporting-services/report-data/media/ssrs-sharepoint-item-context-menu.png "menu di scelta rapida della raccolta documenti per gli elementi ssrs").  
  
3.  Fare clic su **Modifica definizione origine dati**.  
  
4.  Nell'elenco **Tipo di origine dati** specificare l'estensione per l'elaborazione dati usata per elaborare i dati dell'origine dati.  
  
5.  Per **Stringa di connessione**specificare la stringa utilizzata dal server di report per la connessione all'origine dei dati. [!INCLUDE[msCoName](../../includes/msconame-md.md)] consiglia di evitare di specificare credenziali nella stringa di connessione.  
  
     Nell'esempio riportato di seguito viene illustrata una stringa di connessione usata per connettersi al database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] locale:  
  
    ```  
    data source=<localservername>; initial catalog=AdventureWorks2012  
    ```  
  
6.  Digitare un nome utente e una password.  
  
    -   Se l'account è un account utente di dominio Windows, specificarlo nel formato \<domain>\\<account\> e quindi selezionare **Usa come credenziali di Windows**.  
  
    -   Se il nome utente e la password sono credenziali del database, non selezionare **Usa come credenziali di Windows**. Se il server di database supporta la rappresentazione o la delega, è possibile selezionare **Imposta contesto di esecuzione sull'account seguente**.  
  
7.  Fare clic su **OK**.  
  
     ![Icona freccia usata con il collegamento Torna all'inizio](https://docs.microsoft.com/analysis-services/analysis-services/instances/media/uparrow16x16.gif "Icona freccia usata con il collegamento Torna all'inizio") [Requisiti dei criteri di sicurezza per le credenziali archiviate](#bkmk_top)  
  
## <a name="see-also"></a>Vedere anche  
 [Specificare le credenziali e le informazioni sulla connessione per le origini dati del report](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
  
