---
title: Abilitare o disabilitare le funzionalità di Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, configuration
- security [Reporting Services], strategies
ms.assetid: b69db02a-43a7-4fdc-ad9b-438d817a7f83
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: cf44b6af30d5db32c006c5a7d9b59d1810840d18
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66103184"
---
# <a name="turn-reporting-services-features-on-or-off"></a>Abilitare o disabilitare le funzionalità di Reporting Services
  È possibile disabilitare le funzionalità del server di report non utilizzate come parte di una strategia di blocco per ridurre la superficie di attacco di un server di report di produzione. Nella maggior parte dei casi, è consigliabile eseguire le funzionalità di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] simultaneamente in modo da poter utilizzare tutte le funzionalità disponibili in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Tuttavia, a seconda del modello di distribuzione, è possibile disabilitare le funzionalità che non sono necessarie. Ad esempio, è possibile abilitare solo l'elaborazione in background se tutte le operazioni di elaborazione dei report vengono configurate come operazioni pianificate. Analogamente, se si desidera che la generazione di report venga eseguita solo in modo interattivo e su richiesta, è possibile eseguire solo il servizio Web ReportServer.  
  
 Nelle procedure presenti in questo argomento viene illustrato come disabilitare le funzionalità di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità nativa. Le funzionalità possono essere configurate in modi diversi, ad esempio modificando direttamente il file `RsReportServer.config` o usando il facet **Configurazione superficie di attacco per Reporting Services** della gestione basata su criteri in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Utilizzare i collegamenti per trovare la procedura o le procedure che illustrano come abilitare o disabilitare una funzionalità:  
  
-   [servizio Web ReportServer](#RSWebSvc)  
  
-   [Elaborazione ed eventi pianificati](#Sched)  
  
-   [Gestione report](#ReportManager)  
  
-   [Generatore report](#ReportBuilder)  
  
-   [Sicurezza integrata di Windows per le origini dei dati dei report](#WinIntSec)  
  
##  <a name="RSWebSvc"></a> Report Server Web Service  
  
#### <a name="to-turn-on-or-off-the-report-server-web-service-by-editing-configuration"></a>Per abilitare o disabilitare il servizio Web ReportServer mediante la modifica della configurazione  
  
1.  Aprire il file `RsReportServer.config` in un editor di testo. Per altre informazioni, vedere [Modificare un file di configurazione di Reporting Services &#40;RSreportserver.config&#41;](modify-a-reporting-services-configuration-file-rsreportserver-config.md) nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  Per abilitare il servizio Web ReportServer, impostare `IsWebServiceEnabled` su `true`:  
  
    ```  
    <IsWebServiceEnabled>true</IsWebServiceEnabled>  
    ```  
  
3.  Per disabilitare il servizio Web ReportServer, impostare `IsWebServiceEnabled` su `false`:  
  
    ```  
    <IsWebServiceEnabled>false</IsWebServiceEnabled>  
    ```  
  
4.  Salvare le modifiche, quindi chiudere il file.  
  
#### <a name="to-turn-on-or-off-the-report-server-web-service-by-using-sql-server-management-studio"></a>Per abilitare o disabilitare il servizio Web ReportServer mediante l'utilizzo di SQL Server Management Studio  
  
1.  Aprire [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e connettersi all'istanza di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] che si desidera configurare.  
  
2.  In Esplora oggetti fare clic con il pulsante destro del mouse sul nodo di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , scegliere **Criteri**, quindi fare clic su **Facet**.  
  
3.  Nell'elenco **Facet** selezionare **Configurazione superficie di attacco per Reporting Services**.  
  
4.  In **Proprietà facet**:  
  
    -   Per abilitare il servizio Web ReportServer, impostare **WebServiceAndHTTPAccessEnabled** a `True`.  
  
    -   Per disattivare il servizio Web ReportServer, impostare **WebServiceAndHTTPAccessEnabled** a `False`.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="Sched"></a> Recapito ed eventi pianificati  
  
#### <a name="to-turn-on-or-off-scheduled-events-and-delivery-by-editing-configuration"></a>Per abilitare o disabilitare il recapito e gli eventi pianificati mediante la modifica della configurazione  
  
1.  Aprire il file RsReportServer.config in un editor di testo. Per altre informazioni, vedere [Modificare un file di configurazione di Reporting Services &#40;RSreportserver.config&#41;](modify-a-reporting-services-configuration-file-rsreportserver-config.md) nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  Per abilitare l'elaborazione e il recapito pianificati dei report, impostare `IsSchedulingService`, `IsNotificationService` e `IsEventService` su `true`:  
  
    ```  
    <IsSchedulingService>true</IsSchedulingService>  
    <IsNotificationService>true</IsNotificationService>  
    <IsEventService>true</IsEventService>  
    ```  
  
3.  Per disabilitare l'elaborazione e il recapito pianificati dei report, impostare `IsSchedulingService`, `IsNotificationService` e `IsEventService` su `false`:  
  
    ```  
    <IsSchedulingService>false</IsSchedulingService>  
    <IsNotificationService>false</IsNotificationService>  
    <IsEventService>false</IsEventService>  
    ```  
  
4.  Salvare le modifiche, quindi chiudere il file.  
  
> [!NOTE]  
>  Non è possibile disabilitare completamente l'elaborazione in background, in quanto fornisce funzionalità di manutenzione dei database necessarie per le operazioni del server.  
  
#### <a name="to-turn-on-or-off-scheduled-events-and-delivery-by-using-sql-server-management-studio"></a>Per abilitare o disabilitare il recapito e gli eventi pianificati mediante l'utilizzo di SQL Server Management Studio  
  
1.  Aprire [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e connettersi all'istanza di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] che si desidera configurare.  
  
2.  In Esplora oggetti fare clic con il pulsante destro del mouse sul nodo di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , scegliere **Criteri**, quindi fare clic su **Facet**.  
  
3.  Nell'elenco **Facet** selezionare **Configurazione superficie di attacco per Reporting Services**.  
  
4.  In **Proprietà facet**:  
  
    -   Per abilitare il recapito e gli eventi pianificati, impostare **ScheduleEventsAndReportDeliveryEnabled** a `True`.  
  
    -   Per disabilitare il recapito e gli eventi pianificati, impostare **ScheduleEventsAndReportDeliveryEnabled** a `False`.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
> [!NOTE]  
>  Non è possibile disabilitare completamente l'elaborazione in background, in quanto fornisce funzionalità di manutenzione dei database necessarie per le operazioni del server.  
  
##  <a name="ReportManager"></a> Gestione report  
  
#### <a name="to-turn-on-or-off-report-manager-by-editing-configuration"></a>Per abilitare o disabilitare Gestione report mediante la modifica della configurazione  
  
1.  Aprire il file RsReportServer.config in un editor di testo. Per le istruzioni vedere [Modificare un file di configurazione di Reporting Services &#40;RSreportserver.config&#41;](modify-a-reporting-services-configuration-file-rsreportserver-config.md) nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  Per abilitare Gestione report, impostare `IsReportManagerEnabled` su `true`:  
  
    ```  
    <IsReportManagerEnabled>true</IsReportManagerEnabled>  
    ```  
  
3.  Per disabilitare Gestione report, impostare `IsReportManagerEnabled` su `false`:  
  
    ```  
    <IsReportManagerEnabled>false</IsReportManagerEnabled>  
    ```  
  
4.  Salvare le modifiche, quindi chiudere il file.  
  
#### <a name="to-turn-on-or-off-report-manager-by-using-sql-server-management-studio"></a>Per abilitare o disabilitare Gestione report mediante l'utilizzo di SQL Server Management Studio  
  
1.  Aprire [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e connettersi all'istanza di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] che si desidera configurare.  
  
2.  In **Esplora oggetti**fare clic con il pulsante destro del mouse sul nodo di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , scegliere **Criteri**, quindi fare clic su **Facet**.  
  
3.  Nell'elenco **Facet** selezionare **Configurazione superficie di attacco per Reporting Services**.  
  
4.  In **Proprietà facet**:  
  
    -   Per abilitare gestione Report, impostare **ReportManagerEnabled** a `True`.  
  
    -   Per disabilitare Gestione Report, impostare **ReportManagerEnabled** a `False`.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="ReportBuilder"></a> Generatore report  
  
#### <a name="to-turn-on-or-off-report-builder-by-using-sql-server-management-studio"></a>Per abilitare o disabilitare Generatore report mediante l'utilizzo di SQL Server Management Studio  
  
1.  Aprire [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e connettersi all'istanza di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] che si desidera configurare.  
  
2.  In Esplora oggetti fare clic con il pulsante destro del mouse sul nodo di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e scegliere **Proprietà**.  
  
3.  In **Selezione pagina** nella finestra di dialogo **Proprietà server**fare clic su **Sicurezza**.  
  
    -   Per abilitare Generatore report, selezionare l'opzione **Consenti esecuzione report ad hoc** .  
  
    -   Per disabilitare Generatore report, deselezionare l'opzione **Consenti esecuzione report ad hoc** .  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="WinIntSec"></a> Sicurezza integrata di Windows  
  
#### <a name="to-turn-on-or-off-windows-integrated-security-by-using-sql-server-management-studio"></a>Per abilitare o disabilitare la sicurezza integrata di Windows mediante l'utilizzo di SQL Server Management Studio  
  
1.  Aprire [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e connettersi all'istanza di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] che si desidera configurare.  
  
2.  In Esplora oggetti fare clic con il pulsante destro del mouse sul nodo di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e scegliere **Proprietà**.  
  
3.  In **Selezione pagina** nella finestra di dialogo **Proprietà server**fare clic su **Sicurezza**.  
  
    -   Per abilitare la sicurezza integrata di Windows, selezionare l'opzione **Abilita la sicurezza integrata di Windows per le origini dati dei report** .  
  
    -   Per disabilitare la sicurezza integrata di Windows, deselezionare l'opzione **Abilita la sicurezza integrata di Windows per le origini dati dei report** .  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione configurazione Reporting Services &#40;modalità nativa&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)  
  
  
