---
title: Installazione di tipo "solo file" (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- files-only installation [Reporting Services]
- installation options [Reporting Services]
ms.assetid: bdc74a8f-046c-4aa0-bfbd-4f1711dfb9ce
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c76e3e4f1f2e427d8f56c0b832475a22aee6648d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63262278"
---
# <a name="files-only-installation-reporting-services"></a>Installazione di tipo "solo file" (Reporting Services)
  Con*installazione di tipo "solo file"* si intende un'installazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in cui il programma di installazione crea la struttura di cartelle per i file di programma di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , copia i file su disco, registra il servizio del server di report nel computer locale, configura l'account del servizio, concede autorizzazioni file all'account del servizio e registra il provider WMI per [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Un'installazione "solo file" include quanto segue [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] funzionalità: Servizio ReportServer (che ospita il servizio Web ReportServer, elaborazione in background dell'applicazione e gestione Report), Generatore Report, il [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] strumento di configurazione e la [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] utilità della riga di comando (rsconfig.exe, rskeymgmt.exe e RS.exe). Non è invece applicabile alle caratteristiche condivise, ad esempio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], che devono essere specificate come elementi distinti, se installate.  
  
 Diversamente da altre modalità di installazione, un server di report installato in modalità "solo file" non è operativo al termine dell'installazione. Per portare il server di report online è necessario eseguire ulteriori operazioni di configurazione usando [Gestione configurazione Reporting Services &#40;modalità nativa&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
## <a name="when-to-select-files-only-installation-mode"></a>Casi in cui selezionare la modalità di installazione "solo file"  
 Eseguire un'installazione di tipo "solo file" nei casi seguenti:  
  
-   Si desidera connettere il server di report a un database del server di report remoto.  
  
-   Si desidera installare il server di report come istanza denominata.  
  
-   Si applicano requisiti di distribuzione che includono l'utilizzo di impostazioni o funzionalità personalizzate e si desidera disporre di controllo completo sui tempi e le modalità di configurazione del server.  
  
-   Si installa un cluster di failover di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che include [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
## <a name="how-to-perform-a-files-only-installation"></a>Come eseguire un'installazione di tipo "solo file"  
 L'installazione di tipo "solo file" rappresenta l'impostazione predefinita per [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 È possibile specificare un'installazione di tipo "solo file" tramite la riga di comando o nell'Installazione guidata. Negli argomenti seguenti vengono fornite istruzioni dettagliate:  
  
-   [Installare SQL Server 2014 dall'installazione guidata di &#40;installazione&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md).  
  
-   [Installare SQL Server 2014 dal Prompt dei comandi](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md).  
  
#### <a name="example-command-line-script"></a>Esempio di script da riga di comando  
 Per maggiore chiarezza, l'esempio include /RSINSTALLMODE="FilesOnlyMode". Poiché la modalità "solo file" rappresenta l'impostazione predefinita, è tuttavia possibile omettere questa parte di codice e ottenere comunque un'installazione in modalità "solo file".  
  
```  
setup /q /ACTION=install /FEATURES=RS /InstanceName=MSSQLSERVER /RSSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE" /RSINSTALLMODE="FilesOnlyMode"  
```  
  
#### <a name="installation-wizard"></a>Installazione guidata  
 Quando si seleziona [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nella pagina Selezione caratteristiche, viene visualizzata la pagina Configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , che consente di specificare la modalità di installazione. Per specificare un'installazione di tipo "solo file", selezionare **Installa senza configurare il server di report** nella pagina Configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
## <a name="see-also"></a>Vedere anche  
 [Verificare un'installazione di Reporting Services](verify-a-reporting-services-installation.md)   
 [Configurare l'account del servizio del server di report &#40;Gestione configurazione SSRS&#41;](configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [Configurare gli URL del server di report &#40;Gestione configurazione SSRS&#41;](configure-report-server-urls-ssrs-configuration-manager.md)   
 [Configurare una connessione del database del server di report &#40;Gestione configurazione SSRS&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [Installazione in modalità SharePoint di Reporting Services &#40;SharePoint 2010 e SharePoint 2013&#41;](install-reporting-services-sharepoint-mode.md)   
 [Installare un server di report in modalità nativa di Reporting Services](install-reporting-services-native-mode-report-server.md)   
 [Strumenti di Reporting Services](../tools/reporting-services-tools.md)  
  
  
