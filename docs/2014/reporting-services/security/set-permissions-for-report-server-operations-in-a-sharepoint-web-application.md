---
title: Impostare le autorizzazioni per le operazioni del server di report in un'applicazione Web di SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- permissions [Reporting Services], SharePoint integrated mode
- SharePoint integration [Reporting Services], permissions
- SharePoint integration [Report Builder]
- security [Reporting Services], SharePoint integrated mode
- Report Builder 1.0, SharePoint integration
- model item security [Reporting Services]
ms.assetid: 9ea71f1a-ee9e-4337-95ff-d7cef79946e7
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: cb19f95d2dc5de8f461285d84776b80e3f9fb778
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66101545"
---
# <a name="set-permissions-for-report-server-operations-in-a-sharepoint-web-application"></a>Impostare le autorizzazioni per le operazioni del server di report in un'applicazione Web di SharePoint
  Per un server di report eseguito in modalità integrata SharePoint, le impostazioni di sicurezza definite nel sito di SharePoint determinano le modalità di visualizzazione e gestione di report, modelli di report e origini dei dati condivise. Se si usano le assegnazioni di autorizzazioni, i livelli di autorizzazione e i gruppi di SharePoint predefiniti, sarà possibile usare i report e gli altri documenti tramite le impostazioni di sicurezza correnti.  
  
 Se le impostazioni di sicurezza predefinite non garantiscono il livello di accesso desiderato, sarà possibile usare le informazioni fornite nelle sezioni seguenti per identificare le autorizzazioni necessarie per operazioni specifiche.  
  
-   [Autorizzazioni per la visualizzazione e la gestione dei report](#permissionReports)  
  
-   [Autorizzazioni per la creazione di report e utilizzo di Generatore report](#permissionReportBuilder)  
  
-   [Autorizzazioni per la creazione e la gestione di pianificazioni condivise](#permissionSharedSchedules)  
  
-   [Autorizzazioni per la creazione e la gestione di sottoscrizioni](#permissionSubscriptions)  
  
-   [Autorizzazioni per la creazione e la gestione di origini dei dati condivise e modelli di report](#permissionDataSources)  
  
 Per completare la maggior parte delle operazioni in un sito di SharePoint, sono necessarie alcune autorizzazioni principali. Queste autorizzazioni non sono elencate di seguito nelle tabelle delle attività e delle autorizzazioni, ma è necessario includerle se si creano livelli di autorizzazione personalizzati:  
  
-   Visualizzazione informazioni utenti  
  
-   Utilizzo interfacce remote  
  
-   Apertura  
  
-   Visualizzazione pagine applicazione  
  
 Se si usano i livelli di autorizzazione predefiniti, non è necessario alcun intervento perché le autorizzazioni indicate in precedenza sono già incluse nei ruoli Controllo completo, Progettazione, Collaborazione, Lettura e Accesso limitato. Tuttavia, queste autorizzazioni devono essere aggiunte manualmente se si usano livelli di autorizzazione personalizzati o si modificano le autorizzazioni assegnate a un particolare utente o gruppo.  
  
 L'autorizzazione "Visualizzazione informazioni utenti" consente al server di report di restituire informazioni sull'autore dell'elemento e sull'utente che ha eseguito l'ultima modifica dell'elemento. Senza questa autorizzazione, il server di report restituirà gli errori seguenti. Per le operazioni di ricerca, l'errore è: "Il Server di report ha rilevato un errore di SharePoint. ---> System.UnauthorizedAccessException: Accesso negato". Per le operazioni di pubblicazione, l'errore è: "Le autorizzazioni concesse all'utente '\<dominio >\\< utente\>' non sono sufficienti per eseguire questa operazione."  
  
##  <a name="permissionReports"></a> Autorizzazioni per la visualizzazione e la gestione dei report  
 Le autorizzazioni relative alle definizioni dei report sono specificate tramite le autorizzazioni Elenco per la raccolta che contiene il report ma, se si desidera limitare l'accesso, è possibile impostare autorizzazioni per i singoli report. Nella tabella seguente è riportato un elenco di attività, indicando per ognuna le autorizzazioni che la supportano.  
  
|Attività|Autorizzazione|  
|----------|----------------|  
|Visualizzazione di un report.|Autorizzazione**Visualizzazione elementi** per la raccolta che contiene i file o per il singolo report.|  
|Visualizzazione di un report click-through che usa un modello di report come origine dei dati.|Autorizzazione**Visualizzazione elementi** per la raccolta che contiene il report e il modello di report o per il report e il modello specifici. Se non si dispone di autorizzazioni di visualizzazione per il modello, sarà comunque possibile aprire il report ma non effettuare un'esplorazione ad hoc dei dati.<br /><br /> Se il modello di report usa la sicurezza degli elementi, l'utente deve inoltre disporre dell'autorizzazione **Enumerazione autorizzazioni** per il modello di report.|  
|Visualizzazione di snapshot nella cronologia di un report.|Autorizzazione**Modifica elementi** per la raccolta che contiene i file o per il singolo report. Per un report specifico, è possibile determinare se l'utente può visualizzare o meno tutta la cronologia del report, ma non è possibile impostare autorizzazioni per i singoli snapshot nella cronologia del report.|  
|Caricamento o pubblicazione di un report in una raccolta.|Autorizzazione**Aggiunta elementi** per la raccolta che contiene il report.|  
|Impostazione di proprietà per un report, incluse le informazioni per la connessione a un'origine dati, le opzioni di elaborazione e le proprietà dei parametri.|Autorizzazione**Modifica elementi** per la raccolta che contiene il report o per il singolo report. Per selezionare un'origine dei dati condivisa (file con estensione rsds) al fine di utilizzarla con il report, è necessario disporre di autorizzazioni di visualizzazione per tale origine dei dati.|  
|Pianificazione dell'elaborazione di un report.|Per selezionare una pianificazione condivisa, è necessario disporre dell'autorizzazione **Apertura** per il sito in cui si trova la raccolta che contiene il report. Per pianificare l'elaborazione dei dati o la scadenza della cache, è necessario disporre dell'autorizzazione **Modifica elementi** per la raccolta che contiene il report o per il singolo report.|  
|Eliminazione di un report.|Autorizzazione**Eliminazione elementi** per la raccolta che contiene il report o per il singolo report.|  
|Sostituzione di definizioni di report (senza modificarne proprietà, autorizzazioni, cronologia o sottoscrizioni) con una versione più aggiornata.|Autorizzazione**Modifica elementi** per la raccolta che contiene il report o per il singolo report.|  
|Creazione di snapshot nella cronologia di un report.|Autorizzazione**Aggiunta elementi** per la raccolta che contiene il report per cui si sta creando la cronologia.|  
|Creazione di snapshot nella cronologia di un report.|Autorizzazione**Aggiunta elementi** per la raccolta che contiene il report per cui si sta creando la cronologia.|  
|Eliminazione di snapshot nella cronologia di un report ed eliminazione di versioni specifiche delle definizioni di report estratte e modificate nel corso del tempo.|Autorizzazione**Eliminazione versioni** per la raccolta che contiene il report per cui si intende eliminare la cronologia.|  
|Visualizzazione di snapshot nella cronologia di un report e visualizzazione di versioni specifiche delle definizioni dei report estratte e modificate nel corso del tempo.|Autorizzazione**Visualizzazione versioni** per la raccolta che contiene il report.|  
  
##  <a name="permissionReportBuilder"></a> Autorizzazioni per la creazione di report e utilizzo di Generatore report  
 Generatore report è uno strumento per la creazione di report che può essere usato per creare report ad hoc. Questo strumento usa modelli di report come origine dati per supportare l'esplorazione ad hoc dei dati. È possibile caricare un modello in Generatore report per creare un report, eseguirlo, esplorare i dati nel modello e, facoltativamente, salvare il report in una raccolta. Gli utenti che dispongono di autorizzazioni sufficienti potranno quindi aprire lo stesso report ed eseguire attività di esplorazione ad hoc dei dati.  
  
> [!NOTE]  
>  L'accesso a Generatore report può essere determinato da fattori diversi dalle autorizzazioni. Un amministratore di sito può disabilitare il reporting ad hoc impostando le proprietà del server oppure limitare la disponibilità di Generatore report evitando di aggiungere il tipo di contenuto Report di Generatore report a una raccolta, per impedire agli utenti di creare nuovi report tramite il menu **Nuovo** di una raccolta. Un amministratore del server di report può inoltre rendere non disponibile Generatore report impostando alcune proprietà sul server di report. Se per il server in uso si verifica almeno una di queste condizioni, non sarà possibile usare Generatore report anche se si dispone di tutte le autorizzazioni necessarie.  
  
 Nella tabella seguente sono elencate alcune attività relative alla creazione dei report e all'utilizzo di Generatore report con l'indicazione per ognuna delle autorizzazioni che la supportano:  
  
|Attività|Autorizzazione|  
|----------|----------------|  
|Avvio di Generatore report.|Non esistono autorizzazioni che consentono di controllare esplicitamente l'accesso per l'utilizzo di Generatore report. Generatore report è disponibile se è configurata l'integrazione del server di report e si dispone delle autorizzazioni necessarie per aggiungere elementi a una raccolta. Per avviare Generatore report dal menu **Nuovo** della raccolta, è necessario registrare il tipo di contenuto di Generatore report. Per altre informazioni, vedere [aggiungere tipi di contenuto in una raccolta di &#40;Reporting Services in modalità integrata SharePoint&#41;](../add-reporting-services-content-types-to-a-sharepoint-library.md).|  
|Caricamento di un modello o di un'origine dati condivisa.|Autorizzazione**Aggiunta elementi** per la raccolta a cui si desidera aggiungere i file.|  
|Visualizzazione di un modello o di un'origine dati condivisa.|Autorizzazione**Visualizzazione elementi** per la raccolta che contiene i file.<br /><br /> Se il modello contiene impostazioni di sicurezza degli elementi del modello, l'utente deve inoltre disporre dell'autorizzazione **Enumerazione autorizzazioni** per il modello di report.|  
|Generazione di un modello da un'origine dati condivisa.|Autorizzazione**Aggiunta elementi** per la raccolta che contiene il file dell'origine dati condivisa (con estensione rsds) da cui si desidera generare il modello.|  
|Impostazione di autorizzazioni nell'ambito di un modello per specifici elementi del modello.|Autorizzazione**Gestione autorizzazioni** per il sito che contiene la raccolta e il file del modello di report (con estensione smdl).|  
|Caricamento di un modello in Generatore report.|Autorizzazione**Modifica elementi** per il file del modello di report (con estensione smdl).|  
|Creazione di una definizione di report in Generatore report e salvataggio di un report in una raccolta.|Autorizzazione**Aggiunta elementi** per il salvataggio del file in una raccolta.|  
|Modifica di un report in Generatore report.|Autorizzazione**Modifica elementi** per il file della definizione del report.|  
  
 Le autorizzazioni per la creazione e l'utilizzo delle sottoscrizioni e della cronologia dei report e per l'impostazione delle opzioni di elaborazione di report o dati per un report di Generatore report sono identiche a quelle usate per eseguire le stesse azioni sui file delle definizioni di report standard.  
  
##  <a name="permissionSharedSchedules"></a> Autorizzazioni per la creazione e la gestione di pianificazioni condivise  
 Le pianificazioni condivise non sono documenti archiviati in una raccolta. Per tale motivo, per la creazione e la gestione di questo tipo di pianificazioni sono necessarie autorizzazioni a livello di sito. Non è possibile limitare l'accesso a pianificazioni condivise specifiche. Tutte le pianificazioni condivise create sono disponibili a tutti gli utenti che dispongono dell'autorizzazione Apertura a livello di sito.  
  
 Nella tabella seguente sono elencate le attività per la creazione, la gestione e l'utilizzo delle pianificazioni condivise con l'indicazione per ognuna delle autorizzazioni necessarie:  
  
|Attività|Autorizzazione|  
|----------|----------------|  
|Creazione, modifica o eliminazione di una pianificazione condivisa.|Autorizzazione**Gestione sito web** per il sito.|  
|Selezione di una pianificazione condivisa per l'elaborazione delle sottoscrizioni o il recupero dei dati.|Autorizzazione**Apertura** per il sito che contiene la raccolta.|  
  
##  <a name="permissionSubscriptions"></a> Autorizzazioni per la creazione e la gestione di sottoscrizioni  
 In SharePoint viene stabilita una dipendenza tra le sottoscrizioni e le autorizzazioni di visualizzazione. Non è possibile sottoscrivere un report che non si è autorizzati a visualizzare. Se si concedono autorizzazioni per la sottoscrizione di un report, le autorizzazioni di visualizzazione corrispondenti verranno concesse automaticamente.  
  
 Nella tabella seguente sono elencate alcune attività e le autorizzazioni per la creazione, la gestione e l'utilizzo delle sottoscrizioni:  
  
|Attività|Autorizzazione|  
|----------|----------------|  
|Creazione, modifica o eliminazione di una sottoscrizione personale di un utente per un report specifico.|Autorizzazione**Modifica elementi** per la libreria che contiene il report o per il report stesso. Visualizzazione elementi è un'autorizzazione dipendente e verrà automaticamente inclusa nel livello di autorizzazione. Gli utenti autorizzati a creare una sottoscrizione possono creare anche pianificazioni personalizzate che eseguono tale sottoscrizione.|  
|Selezione di una pianificazione condivisa da usare con la sottoscrizione.|Autorizzazione**Apertura** per il sito che contiene la raccolta.|  
|Creazione, modifica o eliminazione di qualsiasi sottoscrizione nell'ambito di un sito.|Autorizzazione**Gestione avvisi** per il sito.|  
  
##  <a name="permissionDataSources"></a> Autorizzazioni per la creazione e la gestione di origini dei dati condivise e modelli di report  
 Il file di un'origine dati condivisa (con estensione rsds) contiene informazioni di connessione a un'origine dati che possono essere usate da più report e modelli. Per i report standard, l'utilizzo di un file rsds per specificare le informazioni per la connessione all'origine dei dati è facoltativo. Per i report basati su modelli, l'utilizzo di un file rsds è obbligatorio. I modelli di report usano sempre un file rsds per la connessione alle origini dati esterne.  
  
 Le origini dati condivise dispongono di proprietà che consentono di specificare i singoli utenti autorizzati a visualizzarle o a gestirle. Le autorizzazioni per la visualizzazione o la gestione delle origini dei dati condivise sono diverse dalle autorizzazioni di visualizzazione dei report. È possibile visualizzare un report che usa un file rsds anche se non si dispone dell'autorizzazione per la visualizzazione del file rsds stesso.  
  
|Attività|Autorizzazione|  
|-----------|----------------|  
|Creazione di un'origine dei dati condivisa.|Autorizzazione**Aggiunta elementi** per la raccolta che contiene l'origine dei dati condivisa. Per creare nuove origini dei dati condivise è possibile usare il menu Nuovo di una raccolta. A tale scopo, è necessario registrare il tipo di contenuto Origine dati report nella raccolta. Per altre informazioni, vedere [aggiungere tipi di contenuto in una raccolta di &#40;Reporting Services in modalità integrata SharePoint&#41;](../add-reporting-services-content-types-to-a-sharepoint-library.md).|  
|Modifica di un'origine dei dati condivisa.|Autorizzazione**Modifica elementi** per la raccolta che contiene l'origine dei dati condivisa o per l'origine dei dati condivisa stessa.|  
|Eliminazione di un'origine dati condivisa.|Autorizzazione**Eliminazione elementi** per la raccolta che contiene l'origine dei dati condivisa o per l'origine dei dati condivisa stessa.|  
|Utilizzo di un'origine dati condivisa (file con estensione rsds) con un report.|Autorizzazione**Modifica elementi** per il report o per la raccolta che contiene il report. La selezione di un'origine dati condivisa fa parte dell'impostazione delle proprietà di un'origine dati per un report.|  
|Generazione di un modello di report da un'origine dati condivisa.|Autorizzazione**Aggiunta elementi** per la raccolta che contiene il modello di report.|  
|Eliminazione di un modello di report.|Autorizzazione**Eliminazione elementi** per la raccolta che contiene il modello di report o per il modello di report stesso.|  
|Impostazione di autorizzazioni nell'ambito di un modello per specifici elementi del modello.|Autorizzazione**Gestione autorizzazioni** per il sito che contiene la raccolta e il file del modello di report (con estensione smdl).|  
  
> [!NOTE]  
>  Non sono disponibili autorizzazioni per la modifica dei modelli di report. Sebbene sia possibile generare o eliminare modelli di report, non è possibile modificarli da un sito di SharePoint. Per modificare modelli di report è necessario Progettazione modelli, uno strumento client di creazione indipendente dalle autorizzazioni impostate in SharePoint.  
  
## <a name="see-also"></a>Vedere anche  
 [Concessione di autorizzazioni per elementi del server di report in un sito di SharePoint](granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [Confrontare ruoli e attività di Reporting Services con autorizzazioni e gruppi di SharePoint](../reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)   
 [Concessione di autorizzazioni per elementi del server di report in un sito di SharePoint](granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [Utilizzare la sicurezza predefinita di Windows SharePoint Services per gli elementi del server di report](use-built-in-security-in-windows-sharepoint-services-for-report-server-items.md)  
  
  
