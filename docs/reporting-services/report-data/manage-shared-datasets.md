---
title: Gestire set di dati condivisi | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.assetid: 2cbb1fa3-959e-4df6-9887-ebc93cc1b686
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 4da49802b5f1d6aa6dbaa082c3d9a10e6273f3b8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65572063"
---
# <a name="manage-shared-datasets"></a>Gestire set di dati condivisi
  In [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]i set di dati condivisi consentono il recupero di dati da origini dati condivise tramite cui si esegue la connessione alle origini dati esterne. Un set di dati condiviso consente di condividere una query per fornire un set di dati coerente a più report. Nella query del set di dati possono essere inclusi i parametri di quest'ultimo. È possibile configurare un set di dati condiviso per memorizzare nella cache i risultati della query per specifiche combinazioni di parametri al primo utilizzo o specificando una pianificazione. È possibile inoltre utilizzare la memorizzazione nella cache del set di dati condiviso in combinazione con la memorizzazione nella cache dei report e con i feed di dati del report per consentire di gestire l'accesso a un'origine dati.  
  
 I set di dati condivisi utilizzano solo origini dati condivise, non origini dati incorporate, e possono essere basati su qualsiasi origine dati per un'estensione per i dati [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] supportata o su un modello di report.  
  
## <a name="creating-and-using-shared-datasets"></a>Creazione e utilizzo di set di dati condivisi  
 Per creare un set di dati condiviso, è necessario utilizzare un'applicazione che crea un file di definizione del set di dati condiviso (con estensione rsd). Per creare un set di dati condiviso, è possibile utilizzare una delle applicazioni seguenti:  
  
-   Generatore report   Usare la modalità progettazione del set di dati condiviso e salvare quest'ultimo in un server di report oppure in un sito di SharePoint.  
  
-   Progettazione report in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] Creare i set di dati condivisi nella cartella Set di dati condiviso in Esplora soluzioni. Per pubblicare un set di dati condiviso, distribuirlo in un server di report oppure in un sito di SharePoint.  
  
-   Caricamento di un file di definizione del set di dati condiviso (con estensione rsd)   È possibile caricare un file in un server di report oppure in un sito di SharePoint. In un sito di SharePoint un file caricato non è convalidato rispetto allo schema fino a quando il set di dati condiviso non viene memorizzato nella cache o utilizzato in un report.  
  
 Nella definizione del set di dati condiviso sono inclusi una query, parametri del set di dati con i relativi valori predefiniti, opzioni dei dati, ad esempio la distinzione tra maiuscole e minuscole, e filtri del set di dati. I valori impostati nella definizione vengono utilizzati tutte le volte che il set di dati condiviso è incluso in un report.  
  
 Per utilizzare un set di dati condiviso in un report, aprire un'applicazione, ad esempio Generatore report, spostarsi nel server di report oppure in un sito di SharePoint, quindi selezionare il set di dati condiviso. In questo modo un'istanza del set di dati condiviso viene aggiunta al report. Nel report non è possibile visualizzare o modificare la query o l'origine dati condivisa per il set di dati condiviso, ma è possibile specificare un set aggiuntivo di valori della proprietà del set di dati da applicare all'istanza nel report. È possibile ad esempio aggiungere un filtro o modificare le opzioni dei dati, quale la distinzione tra maiuscole e minuscole. Per altre informazioni, vedere [Set di dati condivisi e incorporati del report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md) nella [documentazione di Generatore report](https://go.microsoft.com/fwlink/?LinkId=154494) sul sito msdn.microsoft.com.  
  
## <a name="managing-shared-datasets"></a>Gestione di set di dati condivisi  
 Per gestire le proprietà di un set di dati condiviso pubblicato, è possibile utilizzare Gestione report per un server di report in modalità nativa o le pagine dell'applicazione in un sito di SharePoint se il server di report è stato distribuito in modalità integrata SharePoint. Le attività che è possibile eseguire su un set di dati condiviso dipendono dalle assegnazioni di ruolo e dalle autorizzazioni a livello di sito e di elemento, incluse le autorizzazioni sulla cartella se è attiva l'ereditarietà delle autorizzazioni. Il modello di sicurezza a livello di elemento per i set di dati condivisi è lo stesso di quello utilizzato per i report. Per altre informazioni, vedere [Proteggere gli elementi del set di dati condiviso](../../reporting-services/security/secure-shared-dataset-items.md).  
  
 È possibile gestire le proprietà dell'elemento del set di dati condiviso, ad esempio l'origine dati condivisa da utilizzare, indipendentemente dal report che utilizza il set di dati condiviso o l'origine dati condivisa dalla quale dipende. Per modificare la query o altre proprietà del set di dati che appartengono alla definizione del set di dati condiviso, è necessario modificare la definizione.  
  
### <a name="manage-shared-dataset-item-properties"></a>Gestire le proprietà dell'elemento del set di dati condiviso  
 Nella tabella seguente vengono elencate le proprietà che è possibile modificare per un elemento del set di dati condiviso.  
  
|||  
|-|-|  
|Modifica nome|Consente di modificare il nome del set di dati condiviso. Tutti i riferimenti dagli elementi dipendenti continueranno a funzionare.|  
|Modifica descrizione|Consente di modificare la descrizione del set di dati condiviso.|  
|Modifica timeout esecuzione query|Consente di impostare il timeout di esecuzione delle query in secondi. Il valore zero (0) indica l'assenza di timeout. La proprietà determina il numero di secondi prima del timeout della query del set di dati. Per non utilizzare alcun timeout, specificare il valore 0. Per altre informazioni, vedere [Impostazione dei valori di timeout per l'elaborazione di report e di set di dati condivisi &#40;SSRS&#41;](../../reporting-services/report-server/setting-time-out-values-for-report-and-shared-dataset-processing-ssrs.md).|  
|Visualizza elementi dipendenti|Consente di visualizzare gli elementi che utilizzano questo set di dati condiviso, ovvero parti di report pubblicate, origini dati condivise e report.|  
  
 Le proprietà aggiuntive del set di dati condiviso seguenti vengono configurate automaticamente:  
  
|Proprietà|Descrizione|  
|--------------|-----------------|  
|HasDataSourceCredentials|Indica se per l'origine dati condivisa associata sono presenti credenziali salvate nel server di report.|  
|HasUserProfileDependencies|Indica se il report dispone di un riferimento alla raccolta globale dell'utente nella query o nelle espressioni di filtro relative.|  
  
## <a name="viewing-or-changing-the-shared-dataset-definition"></a>Visualizzazione o modifica della definizione del set di dati condiviso  
 Le proprietà dei set di dati condivisi, che includono query, parametri del set di dati, valori predefiniti, filtri del set di dati e opzioni dei dati, ad esempio regole di confronto e distinzione tra maiuscole e minuscole, vengono salvate nella definizione del set di dati. Se si dispone di autorizzazioni sufficienti, è possibile visualizzare e modificare la definizione.  
  
 Per visualizzare o modificare la definizione del set di dati condiviso, modificare quest'ultimo in un'applicazione, ad esempio Generatore report, in modalità progettazione del set di dati condiviso. Dopo aver apportato le modifiche, salvare nuovamente la definizione del set di dati condiviso nel server o nel sito.  
  
 Per visualizzare la definizione del set di dati condiviso in XML, è inoltre possibile utilizzare la sintassi di accesso all'URL in Gestione report. Per visualizzare i valori predefiniti per ogni parametro del set di dati, è possibile ad esempio utilizzare il comando di accesso all'URL seguente per visualizzare una definizione del set di dati condiviso denominata DataSet1 dal server di report:  
  
```  
https://localhost/reportserver/?/DataSet1&rs:command=GetShareddatasetDefinition  
```  
  
## <a name="controlling-access-to-the-shared-dataset-definition"></a>Controllo dell'accesso alla definizione del set di dati condiviso  
 Per impostazione predefinita, le attività seguenti si applicano alle operazioni sui set di dati condivisi.  
  
-   **Visualizzazione di report** Visualizza gli elementi del set di dati condiviso e le relative proprietà.  
  
-   **Utilizzo di report** Legge le definizioni del set di dati condiviso.  
  
-   **Gestione di report** Crea ed elimina set di dati condivisi e ne modifica le proprietà.  
  
-   **Impostazione della sicurezza per singoli elementi** Visualizza e modifica le impostazioni di sicurezza per i set di dati condivisi.  
  
 Per altre informazioni sulle attività e sulle autorizzazioni per il controllo dell'accesso alle proprietà di un'origine dati in un server di report in modalità nativa, vedere [Proteggere gli elementi del set di dati condiviso](../../reporting-services/security/secure-shared-dataset-items.md).  
  
 Le autorizzazioni per la visualizzazione e la modifica delle proprietà per gli elementi di una raccolta di SharePoint sono determinate dall'amministratore del sito. Per altre informazioni, vedere [Informazioni di riferimento sulle autorizzazioni relative a elenchi e siti di SharePoint per gli elementi del server di report](../../reporting-services/security/sharepoint-site-and-list-permission-reference-for-report-server-items.md).  
  
## <a name="how-to-work-with-shared-dataset-properties-on-a-report-server"></a>Utilizzo delle proprietà dei set di dati condivisi in un server di report  
 Con i set di dati condivisi è possibile utilizzare numerosi strumenti. Nella tabella seguente sono riepilogati gli approcci e gli strumenti disponibili e viene fornito un collegamento a ulteriori istruzioni.  
  
|Attività|Strumento|Collegamento|  
|----------|----------|----------|  
|Aggiunta di un set di dati condiviso o modifica delle proprietà della definizione del set di dati condiviso.|Salvataggio in Generatore report<br /><br /> Distribuzione in Progettazione report<br /><br /> Caricamento di un file con estensione rsd in Gestione report|[Set di dati condivisi e incorporati del report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md) nella [documentazione di Generatore report](https://go.microsoft.com/fwlink/?LinkId=154494) sul sito msdn.microsoft.com<br /><br /> [Pagina Carica file &#40;Gestione report&#41;](https://msdn.microsoft.com/library/7bb3166f-9374-4449-b66a-ffb77298507d)<br /><br /> Se si carica un set di dati condiviso prima che venga pubblicata l'origine dati condivisa da cui dipende, è necessario associare manualmente il set di dati condiviso all'origine dati condivisa. Per altre informazioni, vedere [Pagina delle proprietà Generale, Set di dati condivisi &#40;Gestione report&#41;](https://msdn.microsoft.com/library/10798e41-24c3-4e69-893b-7ee6af7fc958).|  
|Modifica delle proprietà dell'elemento del set di dati condiviso.|Gestione report|[Pagina delle proprietà Generale, Set di dati condivisi &#40;Gestione report&#41;](https://msdn.microsoft.com/library/10798e41-24c3-4e69-893b-7ee6af7fc958)|  
|Specifica di proprietà aggiuntive del set di dati condiviso per un'istanza del set di dati condiviso in un report.|Progettazione report di Generatore report|[Finestra di dialogo Proprietà set di dati, Query](https://msdn.microsoft.com/library/1fa34a4b-7de0-4e92-99fa-bc28a206773f)|  
|Associazione di un set di dati condiviso a un'origine dati condivisa diversa.|Gestione report|[Pagina di selezione dell'origine dei dati &#40;Gestione report&#41;](https://msdn.microsoft.com/library/7f7e8b19-0c0b-4b1f-9cc1-057099aa07eb)|  
|Verifica di valori predefiniti per i parametri del set di dati.|Apertura in Generatore report o sintassi di accesso all'URL.|Esempio:<br /><br /> `https://localhost/reportserver/?/DataSet1&rs:command=GetShareddatasetDefinition`|  
|Abilitazione della memorizzazione nella cache.|Gestione report|[Memorizzare nella cache set di dati condivisi &#40;SSRS&#41;](../../reporting-services/report-server/cache-shared-datasets-ssrs.md)<br /><br /> [Pagina Memorizzazione nella cache, set di dati condivisi &#40;Gestione report&#41;](https://msdn.microsoft.com/library/eac372e9-d2a1-48a8-bbe5-09d101df16ea)|  
|Creazione o modifica di un piano di aggiornamento della cache.|Gestione report|[Opzioni di aggiornamento cache &#40;Gestione report&#41;](https://msdn.microsoft.com/library/227da40c-6bd2-48ec-aa9c-50ce6c1ca3a6)|  
|Visualizzazione dello schema della definizione del set di dati condiviso.|Gestione report|`https://<reportserver>/shareddatasetdefinition.xsd`|  
|In modalità integrata SharePoint, sincronizzazione della definizione del set di dati condiviso tra il server di report e il sito di SharePoint.|Pagine dell'applicazione SharePoint|Modifica delle proprietà dell'elemento del set di dati condiviso<br /><br /> Modifica delle opzioni della cache<br /><br /> Modifica dell'origine dati condivisa|  
  
## <a name="comparing-shared-datasets-with-other-report-server-items"></a>Confronto di set di dati condivisi con altri elementi del server di report  
 Quando si gestiscono più tipi di elementi in un server di report, è utile comprendere le similitudini e le differenze tra gli elementi e altri elementi del server di report.  
  
 Di seguito vengono indicate le similitudini tra i set di dati condivisi e le origini dati condivise e i report.  
  
-   In modo analogo alle origini dati condivise, i set di dati condivisi vengono gestiti indipendentemente dai report nei quali vengono utilizzati. Parte della gestione di un set di dati condiviso in un server di report viene realizzata dalla possibilità di modificare l'origine dati condivisa da cui il set di dati condiviso dipende senza modificare la definizione del set stesso.  
  
-   In modo analogo ai report, i set di dati condivisi possono essere memorizzati nella cache. È necessario che le credenziali richieste dall'origine dati soddisfino le restrizioni relative alla memorizzazione nella cache e che siano specificati valori predefiniti per ogni parametro. Per altre informazioni, vedere [Memorizzare nella cache set di dati condivisi &#40;SSRS&#41;](../../reporting-services/report-server/cache-shared-datasets-ssrs.md).  
  
-   In modo analogo ai report, a ogni elaborazione viene utilizzata la definizione corrente dell'elemento nel server di report. Se si apportano modifiche a un set di dati condiviso, ogni report che lo include utilizzerà la definizione corrente nel server di report quando viene elaborato. Se per il set di dati condiviso è abilitata la memorizzazione nella cache e alla definizione del set si apportano modifiche, quest'ultime non vengono utilizzate fino a quando i dati presenti nella cache non scadono. È possibile utilizzare piani di aggiornamento della cache per specificare un set di dati coerente per più report.  
  
 Di seguito viene indicata la differenza tra i set di dati condivisi e le parti di report pubblicate.  
  
-   A differenza delle parti di report pubblicate, le modifiche alla definizione del set di dati condiviso in un server di report non attivano notifiche di aggiornamento quando il report viene aperto in un client di creazione di report. Quando si esegue il report, vengono utilizzati i dati della definizione del set di dati condiviso corrente sul server di report.  
  
 Di seguito vengono indicate le similitudini tra i set di dati condivisi e le sottoscrizioni.  
  
-   I set di dati condivisi possono utilizzare pianificazioni condivise e specifiche dell'elemento per la memorizzazione nella cache.  
  
-   In modo analogo alle sottoscrizioni, i set di dati condivisi seguono le stesse regole per la specifica dei valori dei parametri.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione contenuto del server di report &#40;modalità nativa SSRS&#41;](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)   
 [Concessione di autorizzazioni in un server di report in modalità nativa](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
  
  
