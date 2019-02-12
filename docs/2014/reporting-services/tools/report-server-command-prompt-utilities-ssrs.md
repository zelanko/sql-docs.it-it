---
title: Utilità della riga di comando del server di report (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- rsconfig utility
- components [Reporting Services], command line utilities
- rs utility
- command prompt utilities [Reporting Services]
- rskeymgmt utility
ms.assetid: 68f2f9f4-f894-40ff-a71c-f9756bf4b68c
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 108eea6b0633f0dc17c29ad9d8fb8e5603e1facd
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56020253"
---
# <a name="report-server-command-prompt-utilities-ssrs"></a>Utilità della riga di comando del server di report (SSRS)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] include diverse utilità della riga di comando che è possibile usare per gestire un server di report. Tali utilità vengono installate automaticamente al momento dell'installazione di un server di report.  
  
|nome|File di comando|Modalità di distribuzione supportata|Descrizione|  
|----------|------------------|-------------------------------|-----------------|  
|Utilità RSS|rs.exe|Modalità nativa e modalità SharePoint. Nella versione [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] è stato introdotto il supporto per la modalità SharePoint.|L' [utilità rs](rs-exe-utility-ssrs.md) è un host di script che è possibile usare per l'esecuzione di operazioni inserite nello script. Questo strumento consente di eseguire script di [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] per la copia di dati tra database del server di report, la pubblicazione di report, la creazione di elementi in un database del server di report e altro ancora. Per sapere di più sull'uso di script per gestire un server, vedere [Utilizzare script per l'esecuzione di attività di distribuzione e di amministrazione](script-deployment-and-administrative-tasks.md).|  
|Cmdlet di PowerShell||Solo SharePoint|Per un elenco dei cmdlet di PowerShell, vedere [PowerShell cmdlets for Reporting Services SharePoint Mode](../powershell-cmdlets-for-reporting-services-sharepoint-mode.md)(Cmdlet di PowerShell per la modalità SharePoint di Reporting Services).|  
|rsconfig - utilità|rsconfig.exe|Solo nativa|L' [utilità rsconfig](rsconfig-utility-ssrs.md) consente di configurare e gestire una connessione del server di report al database del server di report. È inoltre possibile utilizzarla per specificare un account utente per l'elaborazione automatica dei report. Per altre informazioni, vedere [Reporting Services Report Server &#40;Native Mode&#41;](../report-server/reporting-services-report-server-native-mode.md). Per altre informazioni sulla configurazione della connessione, vedere [Configurare una connessione del database del server di report &#40;Gestione configurazione SSRS&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md).|  
|Utilità rskeymgmt|rskeymgmt.exe|Solo nativa|L' [utilità rskeymgmt](rskeymgmt-utility-ssrs.md) è uno strumento di gestione delle chiavi di crittografia. È possibile utilizzarla per eseguire il backup, applicare, ricreare ed eliminare chiavi simmetriche. Questo strumento può inoltre essere utilizzato per associare un'istanza del server di report a un database del server di report condiviso e in operazioni di recupero del database. È possibile riutilizzare un database esistente in una nuova installazione applicando una copia di backup della chiave simmetrica. Nel caso non sia possibile recuperare le chiavi, questo strumento consente di eliminare il contenuto crittografato non più utilizzabile. Per altre informazioni sulla gestione delle chiavi e sull'archiviazione dei dati sensibili, vedere [Archiviare i dati crittografati del server di report &#40;Gestione configurazione SSRS&#41;](../install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md) e [Configurare e gestire chiavi di crittografia &#40;Gestione configurazione SSRS&#41;](../install-windows/ssrs-encryption-keys-manage-encryption-keys.md).|  
  
> [!NOTE]  
>  Se si preferisce uno strumento con interfaccia utente grafica, è possibile utilizzare Gestione configurazione Reporting Services anziché `rsconfig` e `rskeymgmt`.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione configurazione Reporting Services &#40;modalità nativa&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [Strumenti di Reporting Services](reporting-services-tools.md)   
 [Server di report di Reporting Services &#40;modalità nativa&#41;](../report-server/reporting-services-report-server-native-mode.md)  
  
  
