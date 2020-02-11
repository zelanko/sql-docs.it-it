---
title: Creare e gestire sottoscrizioni per server di report in modalità nativa | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], managing
ms.assetid: 7f46cbdb-5102-4941-bca2-5e0ff9012c6b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d6f18ff05cf6283e4358e8f8afd76a5858b0b41a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66109603"
---
# <a name="create-and-manage-subscriptions-for-native-mode-report-servers"></a>Creare e gestire sottoscrizioni per server di report in modalità nativa
  In questa sezione sono disponibili argomenti sull'elaborazione, l'amministrazione e il controllo delle sottoscrizioni. La modalità di gestione delle sottoscrizioni varia in base al tipo di sottoscrizione da gestire che può essere standard o guidata dai dati. Le sottoscrizioni standard sono in genere di proprietà degli utenti e gestite da questi, mentre le sottoscrizioni guidate dai dati sono in genere create e gestite da un amministratore del server di report.  
  
 Le funzionalità di sottoscrizione e recapito sono abilitate per impostazione predefinita, mentre il recapito tramite posta elettronica può essere utilizzato solo dopo averlo configurato. Le estensioni per il recapito predefinite includono il recapito tramite posta elettronica e il recapito tramite condivisione file del server di report. A meno di creare o installare estensioni per il recapito personalizzate, questi sono gli unici metodi di distribuzione disponibili per le sottoscrizioni in un server di report in modalità nativa.  
  
## <a name="permissions-for-subscribing-to-reports-on-a-native-mode-report-server"></a>Autorizzazioni per sottoscrivere report in un server di report in modalità nativa  
 In base al modo con cui si utilizzano i ruoli, è possibile concedere a determinati gruppi di utenti la possibilità di gestire le sottoscrizioni abilitando o disabilitando le attività di sottoscrizione per ruoli diversi. Le funzionalità di sottoscrizione sono disponibili per gli utenti mediante due attività:  
  
-   L'attività "Gestione di sottoscrizioni individuali" consente di creare, modificare ed eliminare sottoscrizioni per un report specifico. Nei ruoli predefiniti questa attività appartiene ai ruoli Visualizzazione e Generatore report. Le assegnazioni di ruolo che includono questa attività consentono a un utente di gestire solo le proprie sottoscrizioni.  
  
-   L'attività "Gestione di tutte le sottoscrizioni" consente di accedere a tutte le sottoscrizioni e di modificarle. Questa attività è necessaria per creare sottoscrizioni guidate dai dati. Nei ruoli predefiniti solo il ruolo Gestione contenuto include questa attività.  
  
## <a name="disabling-subscriptions"></a>Disabilitazione di sottoscrizioni  
 Per impedire agli utenti di creare sottoscrizioni, deselezionare l'attività "Gestione di sottoscrizioni individuali" per il ruolo desiderato. Se si rimuove questa attività, le pagine per le sottoscrizioni non saranno disponibili. In Gestione report la pagina Sottoscrizioni personali risulta vuota e non può essere eliminata, anche se in precedenza conteneva sottoscrizioni. La rimozione di attività relative alle sottoscrizioni impedisce agli utenti di creare e modificare sottoscrizioni, ma non comporta l'eliminazione delle sottoscrizioni esistenti che continueranno a essere eseguite finché non vengono eliminate. Per ulteriori informazioni sull'eliminazione di sottoscrizioni, vedere [creare, modificare ed eliminare sottoscrizioni Standard &#40;Reporting Services in modalità nativa&#41;](subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md).  
  
 Per disabilitare l'elaborazione di sottoscrizioni in un server di report, `ScheduleEventsAndReportDeliveryEnabled` è possibile `False` impostare la proprietà su nella **configurazione superficie** di attacco [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per Reporting Services facet della gestione basata su criteri. In questo modo sarà possibile impedire l'esecuzione di tutte le operazioni pianificate. Nel server di report non è possibile disabilitare solo l'elaborazione di sottoscrizioni.  
  
 Per istruzioni su come annullare una sottoscrizione di elaborazione nel server di report, vedere [gestire un processo in esecuzione](subscriptions/manage-a-running-process.md).  
  
## <a name="disabling-delivery-extensions"></a>Disabilitazione di estensioni per il recapito  
 Tutte le estensioni per il recapito installate in un server di report sono disponibili per qualsiasi utente autorizzato a creare una sottoscrizione per un determinato report. Sono disponibili le seguenti estensioni per il recapito configurate automaticamente:  
  
-   Condivisione file di Windows  
  
-   Raccolta di SharePoint (disponibile solo da un sito di SharePoint con un server di report in modalità integrata SharePoint)  
  
 Prima che sia possibile utilizzare l'estensione per il recapito tramite posta elettronica, è necessario configurarla. In caso contrario, l'estensione non sarà disponibile. Per ulteriori informazioni, vedere [configurare un server di report per il recapito tramite posta elettronica &#40;SSRS Configuration Manager&#41;](../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md).  
  
 Se si desidera disabilitare estensioni specifiche, è possibile rimuovere voci dell'estensione nel file RSReportServer.config. Per ulteriori informazioni, vedere [file di configurazione RSReportServer](report-server/rsreportserver-config-configuration-file.md) e [configurare un server di report per il recapito tramite posta elettronica &#40;SSRS Configuration Manager&#41;](../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md).  
  
 Dopo avere rimosso un'estensione per il recapito, questa non sarà più disponibile in Gestione report o in un sito di Share Point. Se si rimuove un'estensione per il recapito, alcune sottoscrizioni potrebbero diventare inattive. Assicurarsi di eliminare le sottoscrizioni o di configurarle per l'utilizzo di un'estensione per il recapito diversa prima di rimuovere un'estensione.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [Utilizzare Sottoscrizioni personali](subscriptions/use-my-subscriptions-native-mode-report-server.md)  
 Illustra come utilizzare la pagina Sottoscrizioni personali per gestire le proprie sottoscrizioni.  
  
 [Sospendere l'elaborazione del report e della sottoscrizione](subscriptions/disable-or-pause-report-and-subscription-processing.md)  
 Descrive le varie modalità per mettere in pausa l'elaborazione del report, ad esempio tramite le assegnazioni di ruolo o la disabilitazione delle risorse del server di report.  
  
 [Controllare la distribuzione dei report](../../2014/reporting-services/control-report-distribution.md)  
 Descrive le impostazioni di configurazione e le opzioni di recapito che è possibile utilizzare per controllare la distribuzione dei report.  
  
 [Monitorare le sottoscrizioni di Reporting Services](subscriptions/monitor-reporting-services-subscriptions.md)  
 Descrive come determinare se una sottoscrizione ha avuto esito positivo o negativo nonché gli effetti sulle sottoscrizioni esistenti delle modifiche apportate ai report.  
  
## <a name="see-also"></a>Vedere anche  
 [Creare, modificare ed eliminare sottoscrizioni standard &#40;Reporting Services in modalità nativa&#41;](subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md)  
  
  
