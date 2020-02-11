---
title: Impostazioni posta elettronica-Configuration Manager (modalità nativa SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.rsconfigtool.emailsettings.f1
helpviewer_keywords:
- SQL11.rsconfigtool.emailsettings.F1
ms.assetid: cdad1529-bfa6-41fb-9863-d9ff1b802577
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 808ad67429ee49d6b04533863112b4cbb3af2514
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66108883"
---
# <a name="e-mail-settings---configuration-manager-ssrs-native-mode"></a>Impostazioni di posta elettronica - Gestione configurazione (modalità nativa SSRS)
  Utilizzare questa pagina per specificare le impostazioni SMTP (Simple Mail Transport Protocol) che consentono il recapito tramite posta elettronica dal server di report. È possibile utilizzare l'estensione per il recapito tramite posta elettronica del server di report per distribuire report o notifiche di elaborazione dei report utilizzando sottoscrizioni tramite posta elettronica. L'estensione per il recapito tramite posta elettronica del server di report richiede un server SMTP e un indirizzo di posta elettronica da utilizzare nel campo Da.  
  
 Le impostazioni di configurazione aggiuntive, incluse quelle che limitano la disponibilità di estensioni per il rendering e gli host del server, possono essere utilizzate per personalizzare ulteriormente le sottoscrizioni alla posta elettronica. Non è possibile specificare queste impostazioni in Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Per configurare le impostazioni aggiuntive, è necessario modificare manualmente il file RSReportServer.config. Per ulteriori informazioni, vedere [configurare un server di report per il recapito tramite posta elettronica &#40;SSRS Configuration Manager&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md) e [Reporting Services i file di configurazione](../report-server/reporting-services-configuration-files.md) nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Per aprire questa pagina, avviare il Reporting Services Configuration Manager e fare clic su **Impostazioni posta elettronica** nel riquadro di spostamento. Per altre informazioni, vedere [Gestione configurazione Reporting Services &#40;modalità nativa&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
 [!INCLUDE[applies](../../includes/applies-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modalità nativa.  
  
## <a name="options"></a>Opzioni  
 **Indirizzo mittente**  
 Consente di specificare l'indirizzo di posta elettronica da utilizzare nel campo Da di un messaggio di posta elettronica generato. È necessario specificare un account utente che abbia l'autorizzazione per l'invio di posta elettronica dal server SMTP.  
  
 **Metodo di recapito SMTP corrente**  
 Consente di specificare che il reindirizzamento della posta elettronica del server di report viene eseguito tramite un server SMTP. Si tratta dell'unico metodo di recapito che è possibile specificare in Gestione configurazione Reporting Services.  
  
 In alternativa a questo metodo, è possibile utilizzare una directory di prelievo del servizio SMTP locale, se non è disponibile un servizio SMTP di rete. Per specificare una directory di prelievo del servizio SMTP locale, è necessario modificare il file RSReportServer.config. Se si modifica il file di configurazione per utilizzare una directory di prelievo del servizio SMTP locale, il Reporting Services Configuration Manager imposta l'opzione del **metodo di recapito** su *Custom* per indicare che il metodo di recapito è specificato nel file di configurazione.  
  
 Nel file di configurazione il metodo di recapito viene specificato tramite l'impostazione di configurazione `SendUsing`. Per ulteriori informazioni su come specificare `SendUsing` l'impostazione, vedere [configurare un server di report per il recapito tramite posta elettronica &#40;SSRS Configuration Manager&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md).  
  
 **Server SMTP**  
 Consente di specificare il server o il gateway SMTP da utilizzare. È possibile utilizzare un server locale o un server SMTP nella rete.  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare un server di report per il recapito tramite posta elettronica &#40;Configuration Manager SSRS&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)   
 [Reporting Services Configuration Manager argomenti della Guida F1 &#40;modalità nativa di SSRS&#41;](../../sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)  
  
  
