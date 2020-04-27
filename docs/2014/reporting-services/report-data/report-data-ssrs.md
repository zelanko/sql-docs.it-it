---
title: Dati del report
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.prod: sql-server-2014
ms.technology: reporting-services
ms.prod_service: reporting-services-native, reporting-services-sharepoint
ms.topic: conceptual
ms.custom: seodec18
ms.date: 12/14/2018
ms.openlocfilehash: be36e61a44a416283e77638f01005f1b3e16883b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "67413050"
---
# <a name="report-data-in-sql-server-reporting-services-ssrs"></a>Dati del report in SQL Server Reporting Services (SSRS)

  I dati del report possono provenire da più origini dei dati dell'organizzazione. Il primo passaggio nella progettazione di un report consiste nel creare le origini dati e i set di dati che rappresentano i dati del report sottostanti. Ogni origine dati include le informazioni sulle connessione dati. Ogni set di dati include un comando di query che consente di definire il set di campi da utilizzare come dati di un'origine dati. Per visualizzare i dati di ogni set di dati, aggiungere un'area dati, ad esempio una tabella, una matrice, un grafico o una mappa. Durante l'elaborazione del report, le query vengono eseguite sull'origine dati e ogni area dati viene espansa in base alle esigenze per visualizzare i risultati della query per il set di dati.  
  
##  <a name="terms"></a><a name="BkMk_ReportDataTerms"></a>Termini

 Se non si ha familiarità [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] con i concetti, esaminare i termini seguenti in [Reporting Services concetti &#40;SSRS&#41;](../reporting-services-concepts-ssrs.md): *connessione dati*, *origini dati incorporate*, *origini dati condivise*, set di dati *incorporati*, *set*di dati condivisi, *query del set*di dati, parti del *report*e *avvisi dati*.  
  
##  <a name="tips-for-specifying-report-data"></a><a name="BkMk_ReportDataTips"></a>Suggerimenti per specificare i dati del report

 Per progettare una strategia per i dati del report, utilizzare le seguenti informazioni.  
  
- **Origini dati** Le origini dati possono essere pubblicate e gestite in un server di report o in un sito di SharePoint indipendentemente dai report. Per ogni origine dati l'utente o il proprietario del database possono gestire le informazioni sulla connessione in un'unica posizione. Le credenziali dell'origine dati vengono archiviate in modo protetto nel server di report; non è necessario includere password nella stringa di connessione. È possibile reindirizzare un'origine dati da un server di prova a un server di produzione. È possibile disabilitare un'origine dati per sospendere tutti i report dai quali viene utilizzata. Per un elenco delle origini dati supportate, vedere [connessioni dati, origini dati e stringhe di connessione in Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md).  
  
- **Set di dati** I set di dati possono essere pubblicati e gestiti indipendentemente dai report o dalle origini dati condivise dai quali dipendono. L'utente o il proprietario del database può fornire query ottimizzate per l'utilizzo da parte degli autori dei report. Quando si modifica la query, tutti i report che utilizzano il set di dati condiviso utilizzano la query aggiornata. È possibile abilitare la memorizzazione nella cache del set di dati per migliorare le prestazioni. È possibile pianificare la memorizzazione nella cache delle query per un'ora specifica oppure utilizzare una pianificazione condivisa.  
  
- **Dati utilizzati dalle parti del report** Le parti del report possono includere i dati dai quali dipendono. Per altre informazioni sulle parti del report, vedere [Parti del report in Progettazione Report &#40;SSRS&#41;](../report-design/report-parts-in-report-designer-ssrs.md).  
  
- **Filtro di dati** I dati del report possono essere filtrati nella query o nel report. È possibile utilizzare i set di dati e le variabili di query per creare parametri di propagazione e consentire all'utente di ridurre migliaia di scelte possibili a un numero più gestibile. È possibile filtrare i dati in una tabella o in un grafico in base ai valori dei parametri o ad altri valori specificati.  
  
- **Parametri** I comandi di query dei set di dati che includono variabili di query consentono di creare automaticamente i parametri del report corrispondenti. È inoltre possibile creare i parametri manualmente. Quando si visualizza un report, i parametri vengono visualizzati nella relativa barra degli strumenti. Gli utenti possono selezionare i valori per controllare i dati o l'aspetto del report. Per personalizzare i dati del report per gruppi di destinatari specifici, è possibile creare set di parametri del report con valori predefiniti diversi collegati alla stessa definizione di report oppure utilizzare il campo `UserID` predefinito. Per altre informazioni, vedere [Parametri report &#40;Generatore report e Progettazione report&#41;](../report-design/report-parameters-report-builder-and-report-designer.md) e [Raccolte predefinite nelle espressioni &#40;Generatore report e SSRS&#41;](../report-design/built-in-collections-in-expressions-report-builder.md).  
  
- **Avvisi dati** Dopo la pubblicazione di un report è possibile creare avvisi basati sui dati del report e ricevere messaggi di posta elettronica quando tale report soddisfa le regole specificate.  
  
- **Raggruppamento e aggregazione di dati** I dati del report possono essere raggruppati o aggregati nella query o nel report. Se si aggregano i valori nella query, è possibile continuare a combinare i valori nel report sulla base di ciò che è significativo.  Per altre informazioni, vedere [Filtro, raggruppamento e ordinamento di dati &#40;Generatore report e SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md) e [Funzione Aggregate &#40;Generatore report e SSRS&#41;](../report-design/report-builder-functions-aggregate-function.md).  
  
- **Ordinamento di dati** I dati del report possono essere ordinati nella query o nel report. Nelle tabelle è inoltre possibile aggiungere un pulsante di ordinamento interattivo per consentire all'utente di controllare l'ordinamento.  
  
- **Dati basati su espressioni** La maggior parte delle proprietà di un report può essere basata su espressioni e le espressioni possono includere riferimenti a campi del set di dati e a parametri del report. Ciò consente di scrivere espressioni efficaci che permettono di controllare i dati e l'aspetto del report. È possibile consentire a un utente di controllare i dati visualizzati tramite una definizione dei parametri.  
  
- **Visualizzazione di dati da un set di dati** I dati di un set di dati vengono in genere visualizzati in una o più aree dati, ad esempio, una tabella e un grafico.  
  
- **Visualizzazione di dati da più set di dati**  In un'area dati basata su un unico set di dati è possibile scrivere espressioni che consentono di cercare valori o aggregazioni in altri set di dati. È possibile includere sottoreport in una tabella basata su un unico set di dati per visualizzare i dati di un'origine dati diversa.  
  
## <a name="data-connections-data-sources-and-datasets"></a>Connessioni dati, origini dati e set di dati

 Utilizzare l'elenco seguente per definire le origini dei dati per un report.  
  
- Valutare se utilizzare origini dati e set di dati incorporati o condivisi. Collaborare con i proprietari delle origini dei dati per implementare e utilizzare la tecnologia di autenticazione e autorizzazione adatta per l'organizzazione.  
  
- Comprendere l'architettura del livello dati del software per la propria organizzazione e i potenziali problemi derivanti dai tipi di dati. Comprendere in che modo le estensioni per i dati e le estensioni per l'elaborazione dati possono influire sui risultati delle query. I tipi di dati dell'origine dei dati, dei provider di dati e i tipi di dati archiviati nel file di definizione del report (con estensione rdl) sono diversi.  
  
- Comprendere le architetture e gli strumenti client/server di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Ad esempio, in Progettazione report è possibile creare report in un computer client in cui vengono utilizzati tipi di origini dati predefiniti. Quando si pubblica un report, è necessario che i tipi di origini dati siano supportati nel server di report o nel sito di SharePoint.  Per altre informazioni, vedere [Origini dati supportate da Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md).  
  
- Le origini dati e i set di dati vengono creati in un report e pubblicati in un server di report o in un sito di SharePoint da uno strumento client di creazione. Le origini dati possono essere create direttamente nel server di report. Una volta pubblicate, le credenziali e altre proprietà possono essere configurate nel server di report. Per altre informazioni, vedere [connessioni dati, origini dati e stringhe di connessione in Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md) e [Reporting Services Tools](../tools/reporting-services-tools.md).  
  
- Le origini dati che è possibile utilizzare dipendono dalle estensioni per i dati di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] installate. Il supporto per le origini dati può variare in base allo strumento client di creazione, alla versione del server di report e alla piattaforma di quest'ultimo. Per altre informazioni, vedere [Origini dati supportate da Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md).  
  
- Le credenziali delle origini dati variano in base al tipo di origine dati e a seconda se i report vengono visualizzati nel client, nel server di report o nel sito di SharePoint. Per altre informazioni, vedere [Impostare autorizzazioni per gli elementi del server di report in un sito di SharePoint &#40;Reporting Services in modalità integrata SharePoint&#41;](../security/set-permissions-for-report-server-items-on-a-sharepoint-site.md), [Specificare le credenziali e le informazioni sulla connessione per le origini dati del report](../../integration-services/connection-manager/data-sources.md) e le informazioni sulle credenziali specifiche di ogni strumento in [Strumenti di Reporting Services](../tools/reporting-services-tools.md).  
  
## <a name="related-tasks"></a>Attività correlate

 Attività correlate alla creazione di connessioni dati, all'aggiunta di dati da origini, set di dati e query esterne.  
  
|||  
|-|-|  
|**Attività comuni**|**Collegamenti**|  
|Creare connessioni dati|[Connessioni dati, origini dati e stringhe di connessione in Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)|  
|Creare set di dati e query|[Set di dati condivisi e incorporati del report &#40;Generatore report e SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)|  
|Gestire origini dati dopo che sono state pubblicate|[Gestire origini dati dei report](manage-report-data-sources.md)|  
|Gestire origini dati condivise dopo che sono state pubblicate|[Gestire set di dati condivisi](manage-shared-datasets.md)|  
|Creare e gestire avvisi dati|[Reporting Services Data Alerts](../tutorial-creating-a-basic-table-report-report-builder.md)|  
|Memorizzare nella cache un set di dati condiviso|[Memorizzare nella cache set di dati condivisi &#40;SSRS&#41;](../report-server/cache-shared-datasets-ssrs.md)|  
|Pianificare un set di dati condiviso da precaricare nella cache|[Pianificazioni](../subscriptions/schedules.md)|  
|Aggiungere un'estensioni per i dati|[Implementazione di un'estensione per l'elaborazione dati](../extensions/data-processing/implementing-a-data-processing-extension.md)|