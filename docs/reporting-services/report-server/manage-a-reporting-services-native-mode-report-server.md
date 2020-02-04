---
title: Gestire un server di report in modalità nativa di Reporting Services | Microsoft Docs
ms.date: 05/14/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services Configuration tool
- configuration options [Reporting Services]
- report servers [Reporting Services], configuring
ms.assetid: 6ca03a09-d6a8-4c93-ba12-1c99dcbfb618
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 26b5bdacbdcf799ffc6c22113ebaec4fce2293b4
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "66499589"
---
# <a name="manage-a-reporting-services-native-mode-report-server"></a>Gestione di un server di report in modalità nativa
  In questa sezione sono disponibili le procedure per la configurazione di un'istanza del server di report in modalità nativa utilizzando Gestione configurazione Reporting Services.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 Gli argomenti di questa sezione sono organizzati in categorie per consentire un'individuazione ancora più semplice delle indicazioni desiderate. Nella prima sezione sono inclusi gli argomenti per le attività di configurazione di base per un server di report in modalità nativa. Nella seconda sezione sono inclusi gli argomenti relativi alla configurazione avanzata. Nella terza sezione sono inclusi gli argomenti per la configurazione di un server di report eseguito in modalità integrata SharePoint.  
  
### <a name="basic-configuration"></a>Configurazione di base  
 [Gestione configurazione Reporting Services &#40;modalità nativa&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)  
 Viene indicata la procedura per avviare lo strumento di configurazione di Reporting Services.  
  
 [Configurare l'account del servizio del server di report &#40;Gestione configurazione SSRS&#41;](../install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)  
 Viene illustrato come specificare le informazioni relative ad account e password per il servizio del server di report.  
  
 [Registrare un nome dell'entità servizio &#40;SPN&#41; per un server di report](../../reporting-services/report-server/register-a-service-principal-name-spn-for-a-report-server.md)  
 Viene illustrato come registrare manualmente un SPN per un server di report eseguito tramite un account utente di dominio in una rete che utilizza l'autenticazione Kerberos.  
  
 [Configurare un URL &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)  
 Viene illustrato come configurare uno o più URL usati per accedere al servizio Web ReportServer e al portale Web.  
  
 [Creare un database del server di report in modalità nativa &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)  
 Illustra le procedure per creare un database del server di report. Questa procedura è obbligatoria per la distribuzione di un'installazione di Reporting Services.  
  
### <a name="advanced-or-optional-configuration"></a>Configurazione avanzata o facoltativa  
 [Configurare una distribuzione con scalabilità orizzontale di un server di report in modalità nativa &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)  
 Viene indicata la procedura per la configurazione di più server di report in modo che condividano un database del server di report.  
  
 [Recapito tramite posta elettronica in Reporting Services](../install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md)   
 Illustra le procedure per configurare un server di report per la distribuzione tramite posta elettronica.  
  
 [Configurare un firewall per l'accesso al server di report](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)  
 Viene illustrato come aprire le porte utilizzate per le richieste in ingresso e le risposte in uscita da un server di report.  
  
 [Configurare un server di report in modalità nativa per gli amministratori locali &#40;SSRS&#41;](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)  
 Vengono descritti i passaggi aggiuntivi richiesti per connettersi al portale Web o a un server di report usando `https://localhost`.  
  
 [Configurare un server di report per l'amministrazione remota](../../reporting-services/report-server/configure-a-report-server-for-remote-administration.md)  
 Viene illustrato come configurare un'istanza remota del server di report a cui connettersi e da configurare per un computer diverso.  
  
 [Abilitare o disabilitare le funzionalità di Reporting Services](../../reporting-services/report-server/turn-reporting-services-features-on-or-off.md)  
 Viene illustrato come rimuovere le caratteristiche non utilizzate da un'installazione di Reporting Services.  
  
 [Abilita errori remoti &#40;Reporting Services&#41;](../../reporting-services/report-server/enable-remote-errors-reporting-services.md)  
 Viene illustrato come impostare le proprietà di un server di report in modo da restituire ulteriori informazioni sulle condizioni di errore che si verificano nei server remoti.  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare e amministrare un server di report &#40;modalità nativa SSRS&#41;](../../reporting-services/report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)   
 [Configurazione e amministrazione di un server di report &#40;modalità SharePoint di Reporting Services&#41;](../../reporting-services/report-server-sharepoint/configuration-and-administration-of-a-report-server.md)  
  
  
