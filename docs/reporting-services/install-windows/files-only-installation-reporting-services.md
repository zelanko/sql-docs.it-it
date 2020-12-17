---
description: Installazione di tipo "solo file" (Reporting Services)
title: Installazione di tipo "solo file" (Reporting Services) | Microsoft Docs
ms.date: 05/24/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- files-only installation [Reporting Services]
- installation options [Reporting Services]
ms.assetid: bdc74a8f-046c-4aa0-bfbd-4f1711dfb9ce
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 891293ec27ca78578ea0aa8fff7a27dd3706d059
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97484283"
---
# <a name="files-only-installation-reporting-services"></a>Installazione di tipo "solo file" (Reporting Services)
  Con *installazione di tipo "solo file"* si intende un'installazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in cui il programma di installazione crea la struttura di cartelle per i file di programma di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , copia i file su disco, registra il servizio del server di report nel computer locale, configura l'account del servizio, concede autorizzazioni file all'account del servizio e registra il provider WMI per [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Un'installazione di tipo "solo file" include le caratteristiche di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] seguenti: il servizio del server di report (che ospita il servizio Web ReportServer e l'applicazione di elaborazione in background), Generatore report, lo strumento di configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e le utilità della riga di comando [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (rsconfig.exe, rskeymgmt.exe e rs.exe). Non è invece applicabile alle funzionalità condivise, ad esempio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], che devono essere specificate come elementi distinti, se installate.  
  
 Diversamente da altre modalità di installazione, un server di report installato in modalità "solo file" non è operativo al termine dell'installazione. Per portare il server di report online è necessario eseguire altre operazioni di configurazione usando [Gestione configurazione del server di report &#40;modalità nativa&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md).  
  
## <a name="when-to-select-files-only-installation-mode"></a>Casi in cui selezionare la modalità di installazione "solo file"  
 Eseguire un'installazione di tipo "solo file" nei casi seguenti:  
  
-   Si desidera connettere il server di report a un database del server di report remoto.  
  
-   Si desidera installare il server di report come istanza denominata.  
  
-   Si applicano requisiti di distribuzione che includono l'utilizzo di impostazioni o funzionalità personalizzate e si desidera disporre di controllo completo sui tempi e le modalità di configurazione del server.  
  
-   Si installa un cluster di failover di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che include [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
## <a name="how-to-perform-a-files-only-installation"></a>Come eseguire un'installazione di tipo "solo file"  
 L'installazione di tipo "solo file" rappresenta l'impostazione predefinita per [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 È possibile specificare un'installazione di tipo "solo file" tramite la riga di comando o nell'Installazione guidata. Negli argomenti seguenti vengono fornite istruzioni dettagliate:  
  
-   [Installare SQL Server dall'Installazione guidata &#40;Installazione&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md).  
  
-   [Installare SQL Server dal prompt dei comandi](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md).  
  
#### <a name="example-command-line-script"></a>Esempio di script da riga di comando  
 Per maggiore chiarezza, l'esempio include /RSINSTALLMODE="FilesOnlyMode". Poiché la modalità "solo file" rappresenta l'impostazione predefinita, è tuttavia possibile omettere questa parte di codice e ottenere comunque un'installazione in modalità "solo file".  
  
```  
setup /q /ACTION=install /FEATURES=RS /InstanceName=MSSQLSERVER /RSSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE" /RSINSTALLMODE="FilesOnlyMode"  
```  
  
#### <a name="installation-wizard"></a>Installazione guidata  
 Quando si seleziona [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nella pagina Selezione caratteristiche, viene visualizzata la pagina Configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , che consente di specificare la modalità di installazione. Per specificare un'installazione di tipo "solo file", selezionare **Installa senza configurare il server di report** nella pagina Configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
## <a name="see-also"></a>Vedere anche  
 [Verificare un'installazione di Reporting Services](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)   
 [Configurare l'account del servizio del server di report &#40;Gestione configurazione del server di report&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [Configurare gli URL del server di report &#40;Gestione configurazione del server di report&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
 [Configurare una connessione del database del server di report &#40;Gestione configurazione del server di report&#41;](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   

::: moniker range="=sql-server-2016"

 [Installare la modalità SharePoint di Reporting Services](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)   

::: moniker-end

 [Installare un server di report in modalità nativa di Reporting Services](~/reporting-services/install-windows/install-reporting-services-native-mode-report-server.md)   
 [Strumenti di Reporting Services](../../reporting-services/tools/reporting-services-tools.md)  
  
  

