---
title: Recapito tramite posta elettronica in Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], e-mail
- e-mail [Reporting Services]
- mail [Reporting Services]
ms.assetid: fda2f130-97b9-4258-9dbb-e93a70f4d08a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 68024e36dd5f8188097ebcc673056c1b6d11e59b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66100893"
---
# <a name="e-mail-delivery-in-reporting-services"></a>Recapito tramite posta elettronica in Reporting Services
  In SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] è disponibile un'estensione per il recapito tramite posta elettronica che consente di inviare un report a utenti o gruppi tramite posta elettronica. L'estensione per il recapito tramite posta elettronica viene configurata mediante Gestione configurazione Reporting Services e la modifica dei file di configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 Per distribuire o ricevere un report tramite posta elettronica, è necessario definire una sottoscrizione standard oppure una sottoscrizione guidata dai dati. È possibile sottoscrivere o distribuire un solo report per volta. Non è possibile creare una sottoscrizione che recapiti più report nello stesso messaggio di posta elettronica. Per ulteriori informazioni sulle sottoscrizioni, vedere [creare, modificare ed eliminare sottoscrizioni Standard &#40;Reporting Services in modalità nativa&#41;](create-and-manage-subscriptions-for-native-mode-report-servers.md).  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Modalità SharePoint &#124; SharePoint 2010 e SharePoint 2013<br /><br /> **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Modalità nativa|  
  
## <a name="e-mail-delivery-options"></a>Opzioni di recapito tramite posta elettronica  
 La funzionalità di recapito tramite posta elettronica del server di report consente di recapitare report in base alle modalità seguenti:  
  
-   Invio di una notifica e di un collegamento ipertestuale al report generato.  
  
-   Invio di una notifica nel campo Oggetto di un messaggio di posta elettronica. Per impostazione predefinita, nel campo Oggetto nella definizione della sottoscrizione sono incluse le variabili seguenti che vengono sostituite da informazioni specifiche del report al momento dell'elaborazione della sottoscrizione:  
  
     **@ReportName**Specifica il nome del report.  
  
     **@ExecutionTime**Specifica quando il report è stato eseguito.  
  
     È possibile utilizzare queste variabili in combinazione con testo statico o modificare il testo nel campo Oggetto per ogni sottoscrizione.  
  
-   Invio di un report incorporato o allegato. Il formato di rendering e il browser determinano se il report verrà incorporato o allegato.  
  
     Se il browser supporta HTML 4.0 e MHTML e si sceglie Archivio Web come formato di rendering, il report verrà incorporato nel messaggio. Con tutti gli altri formati di rendering (CSV, PDF e così via), il report verrà recapitato come allegato. È possibile disabilitare questa funzionalità nel file di configurazione RSReportServer.  
  
     
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] non esegue la verifica delle dimensioni dell'allegato né di quelle del messaggio prima dell'invio del report. Se l'allegato o il messaggio supera il limite massimo consentito dal server di posta elettronica, il report non viene recapitato. Se il report è di grandi dimensioni, è consigliabile selezionare una delle altre opzioni di recapito, ad esempio la notifica o l'invio dell'URL.  
  
 Per determinare il modo in cui un report viene recapitato alla creazione della sottoscrizione, è possibile impostare le opzioni di recapito. Ad esempio, se nella sottoscrizione si seleziona **Includi collegamento** , nel messaggio di posta elettronica viene incluso un collegamento ipertestuale al report.  
  
## <a name="role-based-e-mail-settings"></a>Impostazioni per la posta elettronica basate sui ruoli  
 Per la sottoscrizione di un report, le impostazioni per il recapito tramite posta elettronica disponibili variano in base al fatto che il ruolo includa l'attività "Gestione di sottoscrizioni individuali" o "Gestione di tutte le sottoscrizioni".  
  
|Attività|Impostazioni disponibili|  
|----------|------------------------|  
|Gestione di sottoscrizioni individuali|Visualizza i campi che consentono a un utente di impostare la creazione e il recapito automatici di un report a se stesso. In questa modalità non sono disponibili i campi per l'inserimento di alias di posta elettronica.|  
|Gestione di tutte le sottoscrizioni|Visualizza i campi che consentono una distribuzione più ampia, ovvero A, Cc, Ccn e Risposta, in modo che sia possibile inviare il report a più sottoscrittori con modalità diverse. La disponibilità dei campi per gli alias di posta elettronica viene definita tramite le impostazioni del file di configurazione RSReportServer.|  
  
## <a name="specifying-e-mail-addresses-in-a-subscription"></a>Impostazione di indirizzi di posta elettronica in una sottoscrizione  
 Se si distribuiscono report all'interno di una rete Intranet ed è in uso un gateway SMTP a un server di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Exchange, digitare l'alias di posta elettronica (come se si stesse inviando un messaggio di posta elettronica a un collega). Se invece i report vengono recapitati a un account di posta elettronica esterno, digitare l'indirizzo di posta elettronica completo. Se si specificano altri indirizzi di posta elettronica per inserire altri utenti nella sottoscrizione, i sottoscrittori riceveranno una copia del report generato da tale sottoscrizione.  
  
 Il server di report non convalida gli indirizzi di posta elettronica né recupera indirizzi dal server di posta elettronica. È pertanto necessario conoscere gli indirizzi esatti da utilizzare. Per impostazione predefinita, è possibile inviare report tramite posta elettronica a qualsiasi account di posta elettronica valido all'interno o all'esterno dell'organizzazione. È tuttavia possibile intervenire sulle impostazioni di configurazione per limitare il recapito tramite posta elettronica a determinati host specificandone il nome. È inoltre possibile specificare ulteriori host per consentire il recapito tramite posta elettronica a utenti che non fanno parte della propria organizzazione.  
  
 Il messaggio di posta elettronica utilizzato per recapitare il report deve essere inviato da un account di posta elettronica definito nel server di posta elettronica. L'account di posta elettronica viene specificato tramite un'impostazione di configurazione specifica. L'account di posta elettronica viene utilizzato per tutti i report recapitati dall'estensione per il recapito tramite posta elettronica. Non è possibile specificare più account o utilizzare un altro account per report specifici.  
  
## <a name="e-mail-server-configuration"></a>Configurazione del server di posta elettronica  
 Il server di report si connette a un server di posta elettronica tramite una connessione standard. non mediante comunicazioni crittografate attraverso SSL (Secure Sockets Layer). Il server di posta elettronica deve essere un server SMTP (Simple Mail Transfer Protocol) locale o remoto disponibile nella stessa rete del server di report.  
  
 Per informazioni su come configurare un server di report in modalità nativa, vedere quanto segue:  
  
-   [Configurare un server di report per il recapito tramite posta elettronica &#40;Configuration Manager SSRS&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)  
  
-   [Impostazioni posta elettronica-Configuration Manager &#40;modalità nativa SSRS&#41;](../install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md)  
  
 Per informazioni su come configurare un server di report in modalità SharePoint, vedere quanto segue:  
  
-   [Configurare la posta elettronica per un'applicazione di servizio Reporting Services &#40;SharePoint 2010 e SharePoint 2013&#41;](../install-windows/configure-e-mail-for-a-reporting-services-service-application.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Attività e autorizzazioni](../security/tasks-and-permissions.md)   
 [Sottoscrizioni e recapito &#40;Reporting Services&#41;](subscriptions-and-delivery-reporting-services.md)   
 [Data-Driven Subscriptions](data-driven-subscriptions.md)   
 [Assegnazioni di ruolo](../security/role-assignments.md)  
  
  
