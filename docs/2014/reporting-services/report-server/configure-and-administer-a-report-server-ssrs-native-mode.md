---
title: Configurare e amministrare un server di report (modalità nativa SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, components
- deploying [Reporting Services], component options
- report servers [Reporting Services], component options
- configuration options [Reporting Services]
- administering Reporting Services
- components [Reporting Services], configuring
- configuring servers [Reporting Services]
ms.assetid: cfec012b-56f1-4346-9814-247acf22351c
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 2507a3d07ffacc14a8335766a472375822e7d591
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56024162"
---
# <a name="configure-and-administer-a-report-server-ssrs-native-mode"></a>Configurare e amministrare un server di report (modalità nativa SSRS)
  In questo argomento vengono riepilogati gli approcci disponibili per la configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. È inoltre incluso un elenco di argomenti che illustrano come configurare componenti, caratteristiche specifiche o del server. Per configurare [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], è possibile:  
  
-   Utilizzare Gestione configurazione Reporting Services. Molti degli argomenti di questa sezione contengono informazioni su come configurare caratteristiche specifiche tramite questo strumento.  
  
-   Usare [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] per personalizzare le proprietà del server, attivare la funzionalità Report personali, attivare i log di traccia e impostare valori predefiniti a livello di sito. Per altre informazioni sulle impostazioni del sito, vedere [Server di report di Reporting Services &#40;modalità nativa&#41;](reporting-services-report-server-native-mode.md) . Si noti che è possibile creare ed eseguire uno script che consente di impostare le proprietà del server a livello di programmazione. Per altre informazioni, vedere [Utilizzare script per l'esecuzione di attività di distribuzione e di amministrazione](../tools/script-deployment-and-administrative-tasks.md) e [Proprietà di sistema del server di report](../report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md).  
  
-   Utilizzare Gestione report per concedere autorizzazioni per accedere al server di report. Le autorizzazioni vengono assegnate tramite assegnazioni di ruolo definite per ogni account utente o di gruppo. Per altre informazioni, vedere [Ruoli e autorizzazioni &#40;Reporting Services&#41;](../security/roles-and-permissions-reporting-services.md).  
  
-   Modificare i file di configurazione per cambiare le impostazioni delle applicazioni (facoltativo). Per altre informazioni su ogni file e le linee guida per modificarli, vedere [File di configurazione di Reporting Services](reporting-services-configuration-files.md).  
  
## <a name="in-this-section"></a>In questa sezione  
 [Configurare gli URL del server di report &#40;Gestione configurazione SSRS&#41;](../install-windows/configure-report-server-urls-ssrs-configuration-manager.md)  
 Descrive come definire gli URL utilizzati per accedere al servizio del server di report e a Gestione report.  
  
 [Configurare l'account del servizio del server di report &#40;Gestione configurazione SSRS&#41;](../install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)  
 Include indicazioni e procedure per la modifica dell'account e delle password dei servizi.  
  
 [Creare un database del server di report &#40;Gestione configurazione SSRS&#41;](../../sql-server/install/create-a-report-server-database-ssrs-configuration-manager.md)  
 Descrive come creare un database del server di report necessario per l'archiviazione di oggetti e metadati del server.  
  
 [Configurare una connessione del database del server di report &#40;Gestione configurazione SSRS&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)  
 Descrive come modificare la stringa di connessione usata dal server di report per la connessione al database.  
  
 [Configurare un Server di Report per il recapito tramite posta elettronica &#40;Gestione configurazione SSRS&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)  
 Descrive come configurare un server di report in modo da supportare la distribuzione dei report tramite posta elettronica.  
  
 [Configurare l'account di esecuzione automatica &#40;Gestione configurazione SSRS&#41;](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)  
 Descrive come configurare un account utente per l'esecuzione automatica dei report.  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare l'accesso a Generatore report](configure-report-builder-access.md)   
 [File di configurazione di Reporting Services](reporting-services-configuration-files.md)   
 [Gestione configurazione Reporting Services &#40;modalità nativa&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [Sicurezza e protezione di Reporting Services](../security/reporting-services-security-and-protection.md)   
 [Server di report di Reporting Services &#40;modalità nativa&#41;](reporting-services-report-server-native-mode.md)  
  
  
