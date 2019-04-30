---
title: URL Gestione report (modalità nativa SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- sql12.rsconfigtool.reportmanagervirtualdirectory.f1
ms.assetid: 45768952-23a6-45a5-b541-e7bf192b4a78
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: f5e472f0cb8cb1a2fc8ed9d85b73622617a3a70a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63282046"
---
# <a name="report-manager-url-ssrs-native-mode"></a>URL di Gestione report (modalità nativa SSRS)
  Utilizzare la pagina URL Gestione report per configurare o modificare l'URL utilizzato per accedere a Gestione report. Per impostazione predefinita, l'URL di Gestione report eredita il prefisso, l'indirizzo IP e la porta dell'URL del servizio Web ReportServer. Ciò è dovuto al fatto che Gestione report fornisce accesso front-end al servizio Web in cui è in esecuzione lo stesso servizio del server di report. Se si isolano le applicazioni del servizio e si utilizza Gestione report per accedere a un servizio Web ReportServer in un computer diverso, è necessario modificare il file RSReportServer.config perché Gestione report punti a un'istanza diversa. Per altre informazioni sulla configurazione di una connessione di gestione Report a un server di report remoto, vedere [Gestione configurazione Reporting Services &#40;in modalità nativa&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Se il server di report viene configurato per l'esecuzione in modalità integrata SharePoint, non creare un URL di Gestione report. Gestione report non è supportato nei server di report eseguiti in modalità integrata SharePoint. Se è già presente un URL per Gestione report, l'URL non sarà più disponibile in seguito alla configurazione del server di report per l'esecuzione in modalità integrata SharePoint.  
  
 Per aprire questa pagina, avviare Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e fare clic su **URL Gestione report** nel riquadro di navigazione. Per altre informazioni su come avviare Gestione configurazione, vedere [Gestione configurazione Reporting Services &#40;in modalità nativa&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
> [!NOTE]  
>  Se Gestione report non è abilitato, non è possibile impostare le opzioni in questa pagina. Per altre informazioni su come abilitare gestione Report, vedere [Gestione configurazione Reporting Services &#40;in modalità nativa&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
## <a name="options"></a>Opzioni  
 **Virtual Directory**  
 Consente di specificare il nome della directory virtuale per Gestione report. È possibile specificare un solo nome di directory virtuale per ogni istanza di Gestione report nello stesso computer.  
  
 **URL**  
 Consente di visualizzare l'URL definito per l'istanza corrente di Gestione report.  
  
 **Advanced**  
 Consente di aggiungere un altro URL per l'istanza corrente di Gestione report.  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare un URL &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)   
 [URL nei file di configurazione &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/urls-in-configuration-files-ssrs-configuration-manager.md)   
 [Configurare gli URL del server di report &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)  
  
  
