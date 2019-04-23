---
title: Gestire origini dati dei report | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], data
- published reports [Reporting Services], data source connections
- shared data sources [Reporting Services]
- data sources [Reporting Services], managing
ms.assetid: 0475aded-c8fe-4337-a2b5-4df0ec4c46af
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 13454c9f73b54da7977dd52bbbdc7c1d2cddb28c
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "59947987"
---
# <a name="manage-report-data-sources"></a>Gestire origini dati dei report
  In [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]i report, i modelli di report e le sottoscrizioni guidate dai dati recuperano i dati da origini dati esterne. Per connettersi a un'origine dati esterna, un server di report utilizza le informazioni di connessione all'origine dei dati definite in o a cui si fa riferimento dal report, dal modello o dalla sottoscrizione. Le proprietà di connessione alle origini dati vengono sempre definite al momento della creazione del report o del modello, ma possono essere gestite in modo indipendente dopo la pubblicazione del report o del modello in un server di report.  
  
 Per gestire le origini dati del report, è possibile utilizzare Gestione report per un server di report in modalità nativa o le pagine dell'applicazione in un sito di SharePoint se il server di report è stato distribuito in modalità integrata SharePoint.  
  
 La gestione delle connessioni alle origini dati è caratterizzata dalle attività seguenti, descritte in questo argomento:  
  
-   Modifica delle stringhe di connessione.  
  
-   Modifica delle credenziali.  
  
-   Creazione e utilizzo di origini dati condivise in un server di report, con il passaggio a un'origine dati incorporata per un'origine dati condivisa.  
  
-   Controllo dell'accesso alle proprietà dell'origine dati impostando le autorizzazioni sul report, sul modello o sulle origini dati condivise in uso.  
  
 Si noti che la modifica delle query non fa parte della gestione delle connessioni a origini dati. Per modificare una query per un report o un modello, è necessario utilizzare uno strumento di creazione e apportare le modifiche nella definizione del report o del modello.  
  
## <a name="managed-properties-data-source-type-connection-strings-and-credentials"></a>Proprietà gestite: Tipo di origine dati, le stringhe di connessione e credenziali  
 Le proprietà dell'origine dati che è possibile gestire in un server di report sono le seguenti:  
  
|Proprietà|Descrizione|Modalità di gestione|  
|--------------|-----------------|----------------------|  
|Tipo di origine dati|Determina quale estensione per l'elaborazione dati del server di report utilizzare nei dati esterni. Alcuni esempi di componenti per l'elaborazione dati sono SQL Server, Analysis Services e Oracle.|Il tipo di origine dati è una proprietà gestita perché è configurabile. Tuttavia, è necessario configurare un tipo di origine dati solo se si crea una nuova origine dati condivisa.<br /><br /> Non modificare il tipo di origine dati nelle pagine delle proprietà di un report o di un modello pubblicato; in caso contrario, la connessione verrà quasi certamente invalidata. È improbabile che le strutture dati richieste da un report o da un modello siano identiche in una piattaforma dati diversa.|  
|Stringa di connessione|Stabilisce la connessione iniziale a un'origine dati esterna. Un report può utilizzare stringhe di connessione statiche o dinamiche.<br /><br /> Una *stringa di connessione statica* è un set di valori che il report usa sempre per stabilire la connessione alla stessa origine dati ogni volta che viene eseguito.<br /><br /> Una *stringa di connessione dinamica* è un'espressione compilata nel report, che consente all'utente di selezionare l'origine dati da usare in fase di esecuzione. È necessario compilare l'elenco di selezione di espressioni e origini dati nel report quando lo si crea in Progettazione report.|La modifica di una stringa di connessione risulta utile se si sposta un'origine dati in un altro computer oppure se i report sono stati creati utilizzando dati di test ma si desidera distribuirli con un database di produzione.<br /><br /> È possibile gestire una stringa di connessione statica sostituendo la stringa originale con una diversa.<br /><br /> Per gestire una stringa di connessione dinamica in Gestione report o su un sito di SharePoint, è possibile solo sostituirla con una stringa di connessione statica. Non è possibile modificare l'espressione stessa, né modificare l'elenco di selezione di origini dati. Per modificare l'elenco di espressioni o di valori validi, è necessario modificare la definizione del report e ripubblicarla nel server di report. Per altre informazioni, vedere [Connessioni dati, origini dati e stringhe di connessione in Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md).|  
|Credenziali|Fornisce il nome e password di un utente che dispone dell'autorizzazione per la lettura di dati dall'origine dati.<br /><br /> Se un'origine dati non supporta l'autenticazione, ad esempio se si tratta di un file XML nel file system, è possibile configurare l'account di esecuzione automatica per consentire al server di report di connettersi all'origine dati esterna senza passare credenziali.|È possibile gestire le credenziali aggiornando l'account utente o una password, se è scaduta.<br /><br /> È anche possibile modificare la modalità con cui si ottengono le credenziali, ad esempio richiedendo agli utenti di immetterle in fase di esecuzione.<br /><br /> Se si desidera che gli utenti siano in grado di sottoscrivere un report, è necessario configurare il report per l'utilizzo di credenziali archiviate.|  
  
## <a name="creating-and-using-shared-data-sources"></a>Creazione e utilizzo di origini dati condivise  
 Se si pubblica un report con le proprietà dell'origine dati incorporate, passare alle proprietà di un'origine dati condivisa. Le origini dati condivise possono essere gestite più facilmente, perché è possibile aggiornare le credenziali e le stringhe di connessione in un'unica pagina. Le modifiche vengono immediatamente applicate in tutti i report, i modelli e le sottoscrizioni guidate dai dati che utilizzano tale origine dati. È anche possibile portare un'origine dati condivisa offline, mettendo in pausa il report o la sottoscrizione per impedirne l'esecuzione durante la risoluzione o l'analisi di eventuali problemi che si verificano.  
  
## <a name="controlling-access-data-source-properties"></a>Controllo dell'accesso alle proprietà di un'origine dati condivisa  
 Per impostazione predefinita, chiunque disponga dell'autorizzazione per la gestione dei report può impostare qualsiasi proprietà sul report, incluse le proprietà che determinano il tipo di origine dati, la stringa di connessione, le credenziali e se il report ottiene le informazioni sulla connessione da un'origine dati incorporata o condivisa. Per altre informazioni sulle attività e sulle autorizzazioni per il controllo dell'accesso alle proprietà di un'origine dati in un server di report in modalità nativa, vedere [Proteggere le origini dei dati condivise](../security/secure-shared-data-source-items.md) e [Garantire la sicurezza di report e risorse](../security/secure-reports-and-resources.md).  
  
 Le autorizzazioni per la visualizzazione e la modifica delle proprietà per gli elementi di una raccolta di SharePoint sono determinate dall'amministratore del sito. Per altre informazioni sulle autorizzazioni che controllano l'accesso alle proprietà di connessione alle origini dati, vedere [Informazioni di riferimento sulle autorizzazioni relative a elenchi e siti di SharePoint per gli elementi del server di report](../security/sharepoint-site-and-list-permission-reference-for-report-server-items.md).  
  
## <a name="how-to-work-with-data-source-properties-on-a-report-server"></a>Gestione delle proprietà dell'origine dati in un server di report  
 È possibile utilizzare un'ampia varietà di strumenti per creare e modificare le proprietà dell'origine dati. Nella tabella seguente sono riepilogati gli approcci e gli strumenti disponibili e viene fornito un collegamento a ulteriori istruzioni.  
  
|Attività|Strumento|Collegamento|  
|----------|----------|----------|  
|Visualizzare esempi di stringhe di connessione.||[Connessioni dati, origini dati e stringhe di connessione in Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)|  
|Scegliere un approccio per ottenere le credenziali per la connessione a un'origine dati.||[Specificare le credenziali e le informazioni sulla connessione per le origini dati del report](specify-credential-and-connection-information-for-report-data-sources.md)|  
|Aggiungere proprietà di connessione alle origini dati in un file di definizione del report (con estensione rdl).|Progettazione report|[Creare un'origine dati incorporata o condivisa &#40;SSRS&#41;](../create-an-embedded-or-shared-data-source-ssrs.md)|  
|Aggiungere un collegamento al file di un'origine dati condivisa (con estensione rds) nel progetto di un report.|Progettazione report|[Creare, modificare ed eliminare origini dati condivise &#40;SSRS&#41;](create-modify-and-delete-shared-data-sources-ssrs.md)|  
|Creare un elenco predefinito di origini dati che gli utenti possono selezionare in fase di esecuzione. Quando un utente richiede un report, viene fornito un elenco di origini dati. L'utente deve selezionare l'origine dati da utilizzare prima di eseguire il report. Per aggiungere un elenco di selezione di origini dati a un report, si utilizza un'espressione<br /><br /> Tale espressione è nota come connessione all'origine dati dinamica.|Progettazione report|[Connessioni dati, origini dati e stringhe di connessione in Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)|  
|Creare un'origine dei dati condivisa in un server di report.|Gestione report|[Creare, eliminare o modificare un'origine dei dati condivisa &#40;Gestione report&#41;](../create-delete-or-modify-a-shared-data-source-report-manager.md)|  
|Archiviare credenziali come prerequisito per la creazione di sottoscrizioni o snapshot del report.|Gestione report|[Archiviare le credenziali in un'origine dati di Reporting Services](store-credentials-in-a-reporting-services-data-source.md)|  
|Modificare le proprietà di connessione alle origini dati in un report pubblicato.|Gestione report|[Configurare le proprietà delle origini dati per un report &#40;Gestione report&#41;](configure-data-source-properties-for-a-report-report-manager.md)|  
|Creare un'origine dei dati condivisa in un server di report.|Sito di SharePoint|[Creare e gestire origini dati condivise &#40;Reporting Services in modalità integrata SharePoint&#41;](../create-manage-shared-data-sources-reporting-services-sharepoint-integrated-mode.md)|  
|Utilizzare le informazioni di connessione odc esistenti con un report.|Sito di SharePoint|[Utilizzare una connessione Office Data Connection &#40;.odc&#41; ai report &#40;Reporting Services in modalità integrata SharePoint&#41;](use-an-office-data-connection-odc-with-reports.md)|  
  
> [!NOTE]  
>  Le connessioni alle origini dei dati dei report vengono gestite in modo diverso rispetto alla connessione del server di report al relativo database. Per altre informazioni sulla connessione di un server di report al relativo archivio dati interno, vedere [Configurare una connessione del database del server di report &#40;Gestione configurazione SSRS&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Associare un report o un modello a un'origine dati condivisa &#40;SSRS&#41;](bind-a-report-or-model-to-a-shared-data-source-ssrs.md)   
 [Creare, eliminare o modificare un'origine dei dati condivisa &#40;Gestione report&#41;](../create-delete-or-modify-a-shared-data-source-report-manager.md)   
 [Archiviare le credenziali in un'origine dati di Reporting Services](store-credentials-in-a-reporting-services-data-source.md)   
 [Connessioni dati, origini dati e stringhe di connessione in Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [Origini dei dati supportate da Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md)   
 [Gestione contenuto del server di report &#40;modalità nativa SSRS&#41;](../report-server/report-server-content-management-ssrs-native-mode.md)  
  
  
