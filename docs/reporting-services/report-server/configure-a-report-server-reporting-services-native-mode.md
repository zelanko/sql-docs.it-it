---
title: Configurare un server di report (modalità nativa di Reporting Services) | Microsoft Docs
description: Altre informazioni sulla configurazione aggiuntiva di un server di report di SQL Server, che dipende dalle opzioni selezionate durante l'installazione.
ms.date: 06/18/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- report server configuration
- report servers [Reporting Services], configuring
ms.assetid: ef84ce9d-9156-48e9-8073-7e0535476932
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: f3c23ea4581998fe462175cad1b0e12107d39b0e
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84545561"
---
# <a name="configure-a-report-server-reporting-services-native-mode"></a>Configurare un server di report (modalità nativa di Reporting Services)
  A seconda delle opzioni selezionate durante l'installazione, il server di report potrebbe richiedere passaggi di configurazione aggiuntivi prima che sia possibile utilizzarlo. La configurazione di un server di report è costituita almeno dai componenti seguenti:  
  
-   Un account del servizio del server di report configurato durante l'installazione.  
  
-   Un URL di servizio Web che fornisce l'accesso al server di report.  
  
-   Un database del server di report che archivia i dati dell'applicazione, i report e altri elementi.  
  
 Durante l'installazione vengono configurate le impostazioni minime se si seleziona una delle modalità di installazione seguenti: configurazione predefinita in modalità nativa o configurazione predefinita in modalità di integrazione con SharePoint. Se il server di report è stato installato in modalità "solo file", ovvero è stata selezionata l'opzione **Installa senza configurare il server di report** nell'Installazione guidata, viene configurato solo l'account del servizio. L'URL del servizio Web e il database del server di report devono essere configurati al termine dell'installazione.  
  
È consigliabile configurare il portale Web in modo che sia possibile concedere l'accesso utente al server di report e gestire il contenuto del server di report. Se il server di report è distribuito in modalità integrata SharePoint, usare il front-end Web di un server di SharePoint per concedere l'accesso.  
  
 Se necessario, è possibile configurare caratteristiche aggiuntive come ad esempio la posta elettronica e l'account di esecuzione automatica del server di report. Per altre informazioni, vedere [Gestione di un server di report in modalità nativa](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md).  
  
 Per configurare un server di report, utilizzare lo strumento di configurazione di Reporting Services.  
  
## <a name="to-minimally-configure-a-report-server-installation"></a>Per eseguire la configurazione minima di un'installazione del server di report  
  
1.  Avviare lo strumento di configurazione di Reporting Services e connettersi all'istanza del server di report. Per le istruzioni, vedere [Gestione configurazione Reporting Services &#40;modalità nativa&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md).  
  
2.  Fare clic su **URL servizio Web** per aprire la pagina per la configurazione di un URL per il server di report. Per istruzioni su come definire l'URL, vedere [Configurare un URL &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md).  
  
3.  Fare clic su **Database** per creare il database del server di report. Per istruzioni, vedere [Creare un database del server di report in modalità nativa &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md).  
  
4.  Tornare nella pagina **URL servizio Web** e fare clic sull'URL per verificarne il funzionamento.  
  
5.  Seguire le istruzioni riportate nella sezione "Passaggi successivi" per completare la distribuzione.  
  
## <a name="next-steps"></a>Passaggi successivi  
 Per completare la distribuzione, configurare il portale Web o l'integrazione con SharePoint. Per altre informazioni, vedere [Configurare il portale Web](../../reporting-services/report-server/configure-web-portal.md).  
  
 Se Windows Firewall è abilitato, la porta configurata per l'utilizzo da parte del server di report è probabilmente chiusa. La visualizzazione di una pagina vuota quando si tenta di aprire il portale Web da un computer client remoto indica che una porta potrebbe essere chiusa. Per informazioni sulla configurazione del firewall, vedere [Configure a Firewall for Report Server Access](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md).  
  
 Se si usa Windows Vista o Windows Server 2008, è necessario completare altri passaggi prima che sia possibile aprire il portale Web in locale. Per altre informazioni, vedere [Configurare un server di report in modalità nativa per gli amministratori locali &#40;SSRS&#41;](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).  
  
 Per verificare l'installazione, creare cartelle, caricare elementi ed eseguire report. Seguire le istruzioni in [Verificare un'installazione di Reporting Services](../../reporting-services/install-windows/verify-a-reporting-services-installation.md) per verificare l'installazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione di un server di report in modalità nativa](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)   
 [Configurare un firewall per l'accesso al server di report](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)   
 [Configurare un server di report in modalità nativa per gli amministratori locali &#40;SSRS&#41;](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)   
 [Configurare un server di report per l'amministrazione remota](../../reporting-services/report-server/configure-a-report-server-for-remote-administration.md)   
 [Gestione configurazione Reporting Services &#40;modalità nativa&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)  
  
