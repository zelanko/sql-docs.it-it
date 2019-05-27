---
title: Sicurezza (Generatore report) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: ed38291a-6afe-449f-9f32-3ae04502bd6f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8a68a050627d431570327822cccc60dd0aaf860b
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66107610"
---
# <a name="security-report-builder"></a>Sicurezza (Generatore report)
  Generatore report è un'applicazione client di creazione di report progettata per utilizzare un server di report di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Il server di report può essere configurato per lavorare in modalità nativa come server autonomo o in modalità integrata SharePoint per supportare i report in un sito di SharePoint.  
  
 In Generatore report è possibile creare report, set di dati condivisi e parti del report riutilizzabili. Da un server di report o un sito di SharePoint, è possibile modificare report e aggiungere origini dati condivise, set di dati condivisi e parti del report condivise.  
  
 Per creare, pubblicare e utilizzare report ed elementi correlati a un report, è necessario capire la correlazione tra le caratteristiche di sicurezza e le aree seguenti:  
  
-   **Il server di report o il sito di SharePoint dove si pubblicano report** Queste caratteristiche sono gestite dall'amministratore del server di report o dall'amministratore del sito di SharePoint.  
  
-   **Report pubblicati ed elementi correlati al report** Tra gli elementi correlati al report ci sono le origini dati condivise e incorporate, le credenziali, i set di dati condivisi, i parametri, le parti del report e i modelli di report. Le caratteristiche di sicurezza relative a questi elementi sono gestite dall'autore del report. Per pubblicare e condividere gli elementi, all'autore del report devono essere concesse le autorizzazioni sufficienti da parte dell'amministratore del server di report o dell'amministratore del sito di SharePoint.  
  
-   **Origini dati esterne utilizzate da un report** Queste caratteristiche sono gestite dal proprietario dell'origine dati esterna.  
  
-   **Modelli di report basati su origini dati esterne** Queste caratteristiche sono gestite dal progettista di modelli.  
  
-   **Caratteristiche del report interattive quali i parametri** Queste caratteristiche sono gestite dall'autore del report.  
  
 Rivedere le informazioni in questo argomento per capire meglio come utilizzare le caratteristiche di sicurezza per gestire e proteggere i report e gli elementi correlati al report.  
  
##  <a name="ReportServers"></a> Informazioni sulla sicurezza per i server di report  
 La pubblicazione e la visualizzazione di report sono operazioni privilegiate. Un amministratore di server di report concede autorizzazioni per garantire che solo gli utenti autorizzati possano pubblicare e visualizzare report in uno dei tipi seguenti di server di report:  
  
-   Server di report configurato in modalità nativa  
  
     Per connettersi o passare a un server di report, è necessario disporre di un URL valido e di autorizzazioni di accesso al server sufficienti.  
  
     Per visualizzare o pubblicare elementi in un server di report, i set di autorizzazioni che si applicano a elementi correlati al report e le operazioni sono organizzati in ruoli. L'amministratore di un server di report assegna un utente a uno o più ruoli. Ad esempio, il ruolo predefinito Visitatore consente di visualizzare report, cartelle, modelli e risorse.  
  
     Se non è possibile connettersi o passare a un server di report, contattare l'amministratore del server di report. Per altre informazioni, vedere [Sicurezza e protezione di Reporting Services](../security/reporting-services-security-and-protection.md) nella documentazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [Books Online](https://go.microsoft.com/fwlink/?linkid=121312).  
  
-   Server di report configurato in modalità integrata SharePoint  
  
     Per connettersi a un sito di SharePoint integrato con un server di report, è necessario disporre di un URL valido al sito di SharePoint o al sito secondario e disporre delle autorizzazioni di accesso sufficienti.  
  
     L'autorizzazione per l'accesso a elementi correlati al report e a operazioni viene concessa tramite criteri di sicurezza di SharePoint che consentono di eseguire il mapping di un account utente o di gruppo a un determinato livello di autorizzazione, relativamente a un elemento specifico.  
  
     Se non è possibile connettersi o passare a un sito di SharePoint o a un sito secondario, contattare l'amministratore del sito di SharePoint.  
  
=
  
##  <a name="Reports"></a> Informazioni sulla sicurezza per i report pubblicati e gli elementi correlati al report  
 La sicurezza per i report e gli elementi correlati al report è gestita dall'amministratore del server di report. Gli elementi correlati al report includono le origini dati condivise e incorporate che includono credenziali, set di dati condivisi, parametri, parti del report e modelli.  
  
 In un server di report o sito di SharePoint, i report, gli elementi correlati al report e le operazioni sono entità a protezione diretta. L'autorizzazione per l'accesso a elementi e operazioni viene concessa tramite criteri di sicurezza che consentono di eseguire il mapping di un account utente o di gruppo a un determinato livello di autorizzazione, relativamente a un elemento specifico. Per ridurre la complessità e l'overhead della gestione di un numero elevato di criteri, le autorizzazioni su un contenitore, quale una cartella, sono ereditate dagli elementi nel contenitore. Ad esempio, se un utente dispone dell'autorizzazione di visualizzazione dei report specifica su una cartella, dispone dell'autorizzazione di visualizzazione dei report sugli elementi nella cartella.  
  
 L'override delle autorizzazioni può essere eseguito su elementi o cartelle utilizzando la sicurezza a livello di elemento. Quando viene applicata la sicurezza a livello di elemento, non viene più applicata l'ereditarietà dell'autorizzazione dal contenitore padre all'elemento. Se la sicurezza a livello di elemento viene applicata a una cartella, le cartelle nidificate ereditano le stesse autorizzazioni.  
  
 Se non si è in grado di visualizzare e trovare elementi pubblicati da un altro utente, la causa potrebbe essere un problema di autorizzazioni sull'elemento o sulla cartella.  
  
 Per consentire ad altri utenti di visualizzare e trovare elementi pubblicati per essere condivisi, è necessario collaborare con l'amministratore del server di report per configurare un'organizzazione della cartella che fornisca l'accesso agli utenti. L'accesso deve essere disponibile per la creazione di report e per l'esecuzione di report pubblicati.  
  
 Per ulteriori informazioni, vedere gli argomenti seguenti nella documentazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] inclusa nella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [di](https://go.microsoft.com/fwlink/?linkid=121312):  
  
-   [Ruoli e autorizzazioni &#40;Reporting Services&#41;](../security/roles-and-permissions-reporting-services.md)  
  
-   [Gestire set di dati condivisi](../report-data/manage-shared-datasets.md)  
  
### <a name="update-notifications-for-report-parts"></a>Aggiornare notifiche per parti del report  
 Le parti del report vengono pubblicate a un server di report in modo che altri possano condividerle. Per motivi strutturali, si specifica la posizione nella quale pubblicare le parti del report.  
  
 Gli utenti che includono parti del report nei propri report possono abilitare la caratteristica di aggiornamento. Quando questa caratteristica è abilitata, agli utenti viene notificato quando le parti del report vengono modificate nel server di report.  
  
 Se le parti del report vengono spostate dalla posizione originale, l'avviso di aggiornamento include sia la posizione corrente che quella precedente. Si consiglia di accettare gli aggiornamenti solo se provenienti da posizioni attendibili.  
  
 Per altre informazioni, vedere [Parti del report &#40;Generatore report e SSRS&#41;](../report-parts-report-builder-and-ssrs.md).  
  
=  
  
##  <a name="Data"></a> Informazioni sulla sicurezza dei dati dei report e delle origini dati esterne  
 Per accedere a dati da ogni origine dati esterna in un report, occorre creare un'origine dati incorporata o aggiungere un riferimento a un'origine dati condivisa o un set di dati condiviso nel report.  
  
 Per ogni origine dati esterna, è necessario fornire delle credenziali che siano sufficienti per accedere all'origine e ai dati sottostanti. Il proprietario dell'origine dati specifica il tipo di credenziali di accesso.  
  
 Le credenziali non vengono salvate nella definizione del report. Vengono gestite indipendentemente dal report nel server di report o sul sito di SharePoint e nel client di creazione di report.  
  
 In fase di progettazione del report, le credenziali vengono utilizzare per eseguire query di set di dati e visualizzare in anteprima il report. In fase di esecuzione, le credenziali vengono utilizzare per eseguire il report e memorizzare nella cache i risultati delle query. È inoltre possibile memorizzare indipendentemente nella cache i risultati di query del set di dati condiviso. Le credenziali nella fase di progettazione e nella fase di esecuzione possono essere differenti. Per altre informazioni, vedere [Specifica di credenziali in Generatore report](../specify-credentials-in-report-builder.md).  
  
 Per altre informazioni sulla sicurezza dei dati, vedere l'argomento seguente nella documentazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] inclusa nella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [di](https://go.microsoft.com/fwlink/?linkid=121312):  
  
-   [Centro di sicurezza per il motore di database di SQL Server e il database SQL di Azure](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
 Per altre informazioni, vedere la pagina relativa alla [connessioni dati, alle origini dati e alle stringhe di connessione in Generatore report](../data-connections-data-sources-and-connection-strings-in-report-builder.md).  
  
=
  
##  <a name="Models"></a> Informazioni sui modelli e sui filtri di sicurezza  
 Quando i dati vengono recuperati da un modello di report basato su dati esterni, è possibile applicare dei filtri di sicurezza nel modello. Si tratta di una valida soluzione per proteggere i dati in modo che ogni utente che esegue un report possa vedere solo i dati per i quali dispone delle autorizzazioni necessarie.  
  
 I parametri del report non vengono utilizzati per la sicurezza a livello di riga poiché non impediscono a utenti o a gruppi di utenti di visualizzare righe specifiche di dati. Per applicare la sicurezza ai dati visualizzati in un report è necessario utilizzare i filtri di sicurezza oppure la sicurezza degli elementi dei modelli.  
  
=
  
##  <a name="Interactive"></a> Informazioni sulla sicurezza per la creazione di report per le caratteristiche interattive  
 Nei report vengono spesso utilizzati parametri che consentono a un utente di personalizzare in modo interattivo la visualizzazione di un report. Utilizzare i suggerimenti seguenti per progettare report che seguano procedure consigliate:  
  
-   Non utilizzare parametri basati su parametri di query e che sono di tipo **Text** a meno che si forniscano valori validi. Un elenco dei valori disponibili aiuta un utente a scegliere solo valori validi. Senza questo elenco non è possibile limitare i valori che possono essere immessi da un utente.  
  
-   Non usare il parametro globale [&UserID] per proteggere i dati privati. Come parametro del report, questo valore può essere specificato in un URL del report tramite la sintassi di accesso agli URL. L'utilizzo di questo valore in un'espressione in un set di dati condiviso evita la memorizzazione nella cache del set di dati. Per altre informazioni, vedere [Riferimento ai parametri di accesso con URL](../url-access-parameter-reference.md) nella documentazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [Books Online](https://go.microsoft.com/fwlink/?linkid=121312).  
  
 Una volta che gli elementi sono pubblicati in un server di report, l'amministratore del server di report può facilitarne la protezione assegnando la sicurezza basata sui ruoli o cartella e la sicurezza a livello di elemento. Per altre informazioni, vedere [Garantire la sicurezza di report e risorse](../security/secure-reports-and-resources.md) nella documentazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [Books Online](https://go.microsoft.com/fwlink/?linkid=121312).  
  
 
  
## <a name="see-also"></a>Vedere anche  
 [Installare, disinstallare e supporto di Generatore Report](../install-uninstall-and-report-builder-support.md)   
 [Parametri report &#40;Generatore report e Progettazione report&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)  
  
  
