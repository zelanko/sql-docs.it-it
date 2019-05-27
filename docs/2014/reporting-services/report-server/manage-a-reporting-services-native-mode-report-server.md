---
title: Gestire un server di report in modalità nativa di Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services Configuration tool
- configuration options [Reporting Services]
- report servers [Reporting Services], configuring
ms.assetid: 6ca03a09-d6a8-4c93-ba12-1c99dcbfb618
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: da2eb97e5ce57a2e6a82dda3e264b33e1e3a3b11
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66103785"
---
# <a name="manage-a-reporting-services-native-mode-report-server"></a>Gestione di un server di report in modalità nativa
  In questa sezione sono disponibili le procedure per la configurazione di un'istanza del server di report in modalità nativa utilizzando Gestione configurazione Reporting Services.  
  
## <a name="in-this-section"></a>In questa sezione  
 Gli argomenti di questa sezione sono organizzati in categorie per consentire un'individuazione ancora più semplice delle indicazioni desiderate. Nella prima sezione sono inclusi gli argomenti per le attività di configurazione di base per un server di report in modalità nativa. Nella seconda sezione sono inclusi gli argomenti relativi alla configurazione avanzata. Nella terza sezione sono inclusi gli argomenti per la configurazione di un server di report eseguito in modalità integrata SharePoint.  
  
### <a name="basic-configuration"></a>Configurazione di base  
 [Gestione configurazione Reporting Services &#40;modalità nativa&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)  
 Viene indicata la procedura per avviare lo strumento di configurazione di Reporting Services.  
  
 [Configurare l'account del servizio del server di report &#40;Gestione configurazione SSRS&#41;](../../sql-server/install/configure-a-service-account-ssrs-configuration-manager.md)  
 Viene illustrato come specificare le informazioni relative ad account e password per il servizio del server di report.  
  
 [Registrare un nome dell'entità servizio &#40;SPN&#41; per un server di report](register-a-service-principal-name-spn-for-a-report-server.md)  
 Viene illustrato come registrare manualmente un SPN per un server di report eseguito tramite un account utente di dominio in una rete che utilizza l'autenticazione Kerberos.  
  
 [Configurare un URL &#40;Gestione configurazione SSRS&#41;](../install-windows/configure-a-url-ssrs-configuration-manager.md)  
 Viene illustrato come configurare uno o più URL utilizzati per accedere al servizio Web ReportServer e a Gestione report.  
  
 [Creare un database del server di report in modalità nativa &#40;Gestione configurazione SSRS&#41;](../install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)  
 Illustra le procedure per creare un database del server di report. Questa procedura è obbligatoria per la distribuzione di un'installazione di Reporting Services.  
  
### <a name="advanced-or-optional-configuration"></a>Configurazione avanzata o facoltativa  
 [Configurare una distribuzione con scalabilità orizzontale di un server di report in modalità nativa &#40;Gestione configurazione SSRS&#41;](../install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)  
 Viene indicata la procedura per la configurazione di più server di report in modo che condividano un database del server di report.  
  
 [Configurare un Server di Report per il recapito tramite posta elettronica &#40;Gestione configurazione SSRS&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)  
 Illustra le procedure per configurare un server di report per la distribuzione tramite posta elettronica.  
  
 [Configurare un firewall per l'accesso al server di report](configure-a-firewall-for-report-server-access.md)  
 Viene illustrato come aprire le porte utilizzate per le richieste in ingresso e le risposte in uscita da un server di report.  
  
 [Configurare un server di report in modalità nativa per gli amministratori locali &#40;SSRS&#41;](configure-a-native-mode-report-server-for-local-administration-ssrs.md)  
 Vengono descritti i passaggi aggiuntivi richiesti per connettersi a Gestione report o a un server di report usando http://localhost.  
  
 [Configurare un server di report per l'amministrazione remota](configure-a-report-server-for-remote-administration.md)  
 Viene illustrato come configurare un'istanza remota del server di report a cui connettersi e da configurare per un computer diverso.  
  
 [Abilitare o disabilitare le funzionalità di Reporting Services](turn-reporting-services-features-on-or-off.md)  
 Viene illustrato come rimuovere le caratteristiche non utilizzate da un'installazione di Reporting Services.  
  
 [Abilita errori remoti &#40;Reporting Services&#41;](enable-remote-errors-reporting-services.md)  
 Viene illustrato come impostare le proprietà di un server di report in modo da restituire ulteriori informazioni sulle condizioni di errore che si verificano nei server remoti.  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare e amministrare un server di report &#40;modalità nativa SSRS&#41;](configure-and-administer-a-report-server-ssrs-native-mode.md)   
 [Configurazione e amministrazione di un server di report &#40;modalità SharePoint di Reporting Services&#41;](../configure-administer-report-server-reporting-services-sharepoint-mode.md)  
  
  
