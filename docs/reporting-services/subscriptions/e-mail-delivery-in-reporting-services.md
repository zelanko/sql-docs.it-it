---
title: Recapito tramite posta elettronica in Reporting Services | Microsoft Docs
description: In questo articolo viene illustrato come usare l'estensione per il recapito tramite posta elettronica, che consente di inviare un report a utenti o gruppi tramite posta elettronica.
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: subscriptions
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], e-mail
- e-mail [Reporting Services]
- mail [Reporting Services]
ms.assetid: fda2f130-97b9-4258-9dbb-e93a70f4d08a
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: c25fa11961ec082a6c8b912eca471d578a29a057
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/17/2020
ms.locfileid: "81632532"
---
# <a name="e-mail-delivery-in-reporting-services"></a>Recapito tramite posta elettronica in Reporting Services
  In SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] è disponibile un'estensione per il recapito tramite posta elettronica che consente di inviare un report a utenti o gruppi tramite posta elettronica. Per distribuire un report usando la posta elettronica, 1) configurare il server di report per il recapito della posta elettronica e 2) definire una sottoscrizione standard oppure una sottoscrizione guidata dai dati. Una singola sottoscrizione non può recapitare più report nello stesso messaggio di posta elettronica. È possibile, tuttavia, creare più sottoscrizioni.  
  
 Il server di report si connette a un server di posta elettronica tramite una connessione standard. Non usa la comunicazione crittografata tramite TLS (Transport Layer Security), protocollo precedentemente noto come SSL (Secure Sockets Layer). Il server di posta elettronica deve essere un server SMTP (Simple Mail Transfer Protocol) locale o remoto disponibile nella stessa rete del server di report.  
  
 Per informazioni dettagliate sulla creazione di una sottoscrizione, vedere quanto segue:  
  
-   [Creare e gestire sottoscrizioni per server di report in modalità nativa](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md)  
  
-   [Creare e gestire sottoscrizioni per server di report in modalità SharePoint](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md)  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  Modalità SharePoint di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] &#124; Modalità nativa di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
  
## <a name="e-mail-delivery-options"></a>Opzioni di recapito tramite posta elettronica  
 La funzionalità di recapito della posta elettronica del server di report consente di recapitare report in base alle modalità seguenti  
  
-   Invio di una notifica e di un collegamento ipertestuale al report generato.  
  
-   Invio di una notifica nel campo Oggetto di un messaggio di posta elettronica. Per impostazione predefinita, nel campo Oggetto nella definizione della sottoscrizione sono incluse le variabili seguenti che vengono sostituite da informazioni specifiche del report al momento dell'elaborazione della sottoscrizione:  
  
     **\@ReportName** specifica il nome del report.  
  
     **\@ExecutionTime** specifica l'ora in cui il report è stato eseguito.  
  
     È possibile utilizzare queste variabili in combinazione con testo statico o modificare il testo nel campo Oggetto per ogni sottoscrizione.  
  
-   Invio di un report incorporato o allegato. Il formato di rendering e il browser determinano se il report verrà incorporato o allegato.  
  
     Se il browser supporta HTML 4.0 e MHTML e si sceglie Archivio Web come formato di rendering, il report verrà incorporato nel messaggio. Con tutti gli altri formati di rendering (CSV, PDF e così via), il report verrà recapitato come allegato. Per i server di report in modalità nativa è possibile disabilitare questa funzionalità nel file di configurazione RSReportServer.config.  
  
     [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] non esegue la verifica delle dimensioni dell'allegato né di quelle del messaggio prima dell'invio del report. Se l'allegato o il messaggio supera il limite massimo consentito dal server di posta elettronica, il report non viene recapitato. Se il report è di grandi dimensioni, è consigliabile selezionare una delle altre opzioni di recapito, ad esempio la notifica o l'invio dell'URL.  
  
 Per determinare il modo in cui un report viene recapitato alla creazione della sottoscrizione, è possibile impostare le opzioni di recapito. Ad esempio, se nella sottoscrizione si seleziona **Includi collegamento** , nel messaggio di posta elettronica viene incluso un collegamento ipertestuale al report.  
  
## <a name="native-mode-role-based-e-mail-settings"></a>Impostazioni per la posta elettronica basate sui ruoli in modalità nativa  
 In un ambiente di server di report in modalità nativa le impostazioni per il recapito della posta elettronica disponibili variano in base al fatto che il ruolo includa l'attività "Gestione di sottoscrizioni individuali" o "Gestione di tutte le sottoscrizioni".  
  
|Attività|Impostazioni disponibili|  
|----------|------------------------|  
|Gestione di sottoscrizioni individuali|Visualizza i campi che consentono a un utente di impostare la creazione e il recapito automatici di un report a se stesso. In questa modalità non sono disponibili i campi per l'inserimento di alias di posta elettronica.|  
|Gestione di tutte le sottoscrizioni|Visualizza i campi che consentono una distribuzione più ampia, ovvero A, Cc, Ccn e Risposta, in modo che sia possibile inviare il report a più sottoscrittori con modalità diverse. La disponibilità dei campi per gli alias di posta elettronica viene definita tramite le impostazioni del file di configurazione RSReportServer.|  
  
## <a name="specifying-e-mail-addresses-in-a-subscription"></a>Impostazione di indirizzi di posta elettronica in una sottoscrizione  
 Se si distribuiscono report all'interno di una rete Intranet ed è in uso un gateway SMTP a un server di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Exchange, digitare l'alias di posta elettronica (come se si stesse inviando un messaggio di posta elettronica a un collega). Se invece i report vengono recapitati a un account di posta elettronica esterno, digitare l'indirizzo di posta elettronica completo. Se si specificano altri indirizzi di posta elettronica per inserire altri utenti nella sottoscrizione, i sottoscrittori riceveranno una copia del report generato da tale sottoscrizione.  
  
 Il server di report non convalida gli indirizzi di posta elettronica né recupera indirizzi dal server di posta elettronica. È pertanto necessario conoscere gli indirizzi esatti da utilizzare. Per impostazione predefinita, è possibile inviare report tramite posta elettronica a qualsiasi account di posta elettronica valido all'interno o all'esterno dell'organizzazione. È tuttavia possibile intervenire sulle impostazioni di configurazione per limitare il recapito tramite posta elettronica a determinati host specificandone il nome. È inoltre possibile specificare ulteriori host per consentire il recapito tramite posta elettronica a utenti che non fanno parte della propria organizzazione.  
  
 Il messaggio di posta elettronica utilizzato per recapitare il report deve essere inviato da un account di posta elettronica definito nel server di posta elettronica. L'account di posta elettronica viene specificato tramite un'impostazione di configurazione specifica. L'account di posta elettronica viene utilizzato per tutti i report recapitati dall'estensione per il recapito tramite posta elettronica. Non è possibile specificare più account o utilizzare un altro account per report specifici.  
  
## <a name="controlling-e-mail-delivery"></a>Controllo del recapito tramite posta elettronica  
 È possibile configurare un server di report in modo che la distribuzione tramite posta elettronica sia circoscritta a domini host specifici. È possibile, ad esempio, fare in modo che un server di report nativo recapiti un report solo ai domini indicati nel file di configurazione **RSReportServer.config** .  
  
 È inoltre possibile definire le impostazioni di configurazione in modo che il campo **A** di una sottoscrizione venga nascosto. In questo caso, i report verranno recapitati solo all'utente che definisce la sottoscrizione. Non è tuttavia possibile impedire a un utente che ha ricevuto un report di inoltrarlo.  
  
 Il modo più efficace per controllare la distribuzione dei report consiste nel configurare un server di report in modo che invii unicamente un URL del server di report. Il server di report utilizza l'autenticazione di Windows e un modello di autorizzazione basata sui ruoli per controllare l'accesso a un report. Se un utente riceve per errore tramite posta elettronica un report che non è autorizzato a visualizzare, il server di report non visualizzerà il report. Per altre informazioni sulle sottoscrizioni, vedere quanto segue.  
  
## <a name="e-mail-server-configuration"></a>Configurazione del server di posta elettronica  
 Per un server di report in modalità nativa l'estensione per il recapito della posta elettronica viene configurata con Gestione configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità nativa e la modifica dei file di configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Per un server di report in modalità SharePoint, l'estensione per il recapito della posta elettronica è configurata nella pagine di gestione di SharePoint e negli script di PowerShell.  
  
 
 Per altre informazioni su come configurare un server di report in modalità nativa, vedere [Impostazioni posta elettronica - Modalità nativa di Reporting Services (Gestione configurazione)](../install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md).
 
 
 Per informazioni su come configurare un server di report in modalità SharePoint, vedere quanto segue:  
  
  
## <a name="see-also"></a>Vedere anche  
 [Attività e autorizzazioni](../../reporting-services/security/tasks-and-permissions.md)   
 [Sottoscrizioni e recapito &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [Data-Driven Subscriptions](../../reporting-services/subscriptions/data-driven-subscriptions.md)   
 [Assegnazioni di ruolo](../../reporting-services/security/role-assignments.md)  
  
  
