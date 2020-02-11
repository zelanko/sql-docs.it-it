---
title: Creare, modificare ed eliminare origini dati condivise (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- modifying data source properties
- shared data sources [Reporting Services]
- removing shared data sources
- roles [Reporting Services], shared data sources
- data sources [Reporting Services], shared
- data sources [Reporting Services], modifying properties
- deleting shared data sources
ms.assetid: 1e58c1c2-5ecf-4ce6-9d04-0a8acfba17be
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 4a2239e07cc24842c5cbdf44c8743ea2d79ea7cb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66107395"
---
# <a name="create-modify-and-delete-shared-data-sources-ssrs"></a>Creare, modificare ed eliminare origini dati condivise (SSRS)
  Un'origine dati condivisa è un set di proprietà di connessione dell'origine dati a cui è possibile fare riferimento in più report, modelli e sottoscrizioni guidate dai dati in esecuzione su un server di report [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Le origini dei dati condivise rappresentano una soluzione semplice per gestire proprietà dell'origine dati soggette a frequenti modifiche. Se un account utente o una password viene modificata o se si sposta il database in un server diverso, è possibile aggiornare le informazioni di connessione da una posizione centralizzata.  
  
 Le origini dei dati condivise sono facoltative per i report e le sottoscrizioni guidate dai dati, ma obbligatorie per i modelli di report. Se si intende utilizzare modelli di report per il reporting ad hoc, è necessario creare e gestire un'origine dei dati condivisa per fornire al modello le informazioni di connessione.  
  
 Un'origine dei dati condivisa è costituita dalle seguenti parti:  
  
|Parte|Descrizione|  
|----------|-----------------|  
|Nome|Un nome che identifica l'elemento all'interno della gerarchia di cartelle del server di report.|  
|Descrizione|Una descrizione che viene visualizzata con l'elemento in Gestione report quando si visualizza il contenuto della cartella.|  
|Tipo di connessione|L'estensione per l'elaborazione dati utilizzata con l'origine dati. È possibile utilizzare solo estensioni per l'elaborazione dati distribuite sul server di report. Per altre informazioni sulle estensioni per l'elaborazione dati incluse in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], vedere [Origini dati supportate da Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md).|  
|Stringa di connessione|La stringa di connessione per il database. Per ulteriori informazioni e per visualizzare esempi di stringhe di connessione alle origini dati utilizzate di frequente, vedere [connessioni dati, origini dati e stringhe di connessione in Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md).|  
|Tipo di credenziali|Specifica in che modo vengono ottenute le credenziali per la connessione e se devono essere utilizzate quando viene stabilita la connessione. Per ulteriori informazioni, vedere [specificare le credenziali e le informazioni di connessione per le origini dati del report](../../integration-services/connection-manager/data-sources.md).|  
  
 Le origini dei dati condivise non contengono informazioni sulla query utilizzata per recuperare i dati. La query viene sempre mantenuta all'interno della definizione del report.  
  
## <a name="creating-and-modifying-a-shared-data-source"></a>Creazione e modifica di un'origine dei dati condivisa  
 Per creare un'origine dati condivisa o modificarne le proprietà, è necessario avere le autorizzazioni **Gestione di origini dei dati** sul server di report. Se il server di report viene eseguito in modalità nativa, è possibile utilizzare Gestione report per creare e configurare l'origine dei dati condivisa. Se il server di report viene eseguito in modalità integrata SharePoint, è possibile utilizzare le pagine dell'applicazione su un sito di SharePoint. Per qualsiasi server di report, indipendentemente dalla modalità, è possibile creare un'origine dei dati condivisa in Progettazione report e pubblicarla su un server di destinazione.  
  
 Per ulteriori informazioni sulla creazione di un'origine dei dati condivisa, vedere:  
  
-   [Creare un'origine dati incorporata o condivisa &#40;SSRS&#41;](../create-an-embedded-or-shared-data-source-ssrs.md)  
  
-   [Creare e gestire origini dati condivise &#40;Reporting Services in modalità integrata SharePoint&#41;](../create-manage-shared-data-sources-reporting-services-sharepoint-integrated-mode.md)  
  
 Dopo avere creato un'origine dei dati condivisa sul server di report, è possibile creare assegnazioni di ruolo per controllarne l'accesso, spostarla in un percorso diverso, rinominarla o disconnetterla per impedire l'elaborazione dei report durante l'esecuzione di operazioni di manutenzione sull'origine dati esterna. Se si rinomina un'origine dei dati condivisa o la si sposta in una posizione diversa nella gerarchia di cartelle del server di report, vengono di conseguenza aggiornate le informazioni sul percorso in tutti i report e sottoscrizioni che fanno riferimento all'origine dei dati condivisa. Se l'origine dei dati condivisa è offline, tutti i report, i modelli e le sottoscrizioni non verranno eseguite finché l'origine dati non viene nuovamente abilitata.  
  
 Per altre informazioni sul controllo dell'accesso alle origini dati condivise nella gerarchia delle cartelle del server di report, vedere [Proteggere le origini dei dati condivise](../security/secure-shared-data-source-items.md).  
  
## <a name="deleting-a-shared-data-source"></a>Eliminazione di un'origine dei dati condivisa  
 È possibile eliminare un'origine dei dati condivisa in modo analogo a quando si elimina un elemento qualsiasi dal server di report. In Gestione report aprire la cartella in visualizzazione dettagli, selezionare l'elemento e fare clic su **Elimina**. In una pagina dell'applicazione in un sito di SharePoint aprire la raccolta di SharePoint, selezionare l'elemento e fare clic su **Elimina**.  
  
 Quando si elimina un'origine dei dati condivisa, verranno disattivati tutti i report, i modelli o le sottoscrizioni guidate dai dati in cui viene utilizzata. In assenza delle informazioni sulla connessione all'origine dati, gli elementi non verranno più eseguiti. Per attivare tali elementi, è necessario aprirli singolarmente ed eseguire le seguenti operazioni:  
  
-   Per i report e le sottoscrizioni guidate dai dati che fanno riferimento all'origine dei dati condivisa, è possibile specificare le informazioni sulla connessione all'origine dati nelle proprietà del report o nella sottoscrizione. In alternativa, è possibile selezionare una nuova origine dei dati condivisa che include i valori che si desidera utilizzare.  
  
-   Per i modelli e i report di Generatore report che utilizzano tale modello, è necessario specificare una nuova origine dei dati condivisa. I modelli ottengono le informazioni sulla connessione all'origine dati solo tramite origini dei dati condivise.  
  
 Per visualizzare un elenco di report e modelli che utilizzano l'origine dati, aprire la pagina Elementi dipendenti relativa all'origine dei dati condivisa. È possibile accedere a questa pagina quando si apre l'origine dati in Gestione report o in una pagina dell'applicazione di SharePoint. Si noti che nella pagina Elementi dipendenti non vengono visualizzate le sottoscrizioni guidate dai dati. Se un'origine dei dati condivisa viene utilizzata da una sottoscrizione, questa non sarà inclusa nell'elenco degli elementi dipendenti.  
  
 Non è prevista alcuna operazione di annullamento per l'eliminazione di un'origine dei dati condivisa. Se tuttavia si elimina accidentalmente un'origine dei dati condivisa, è possibile crearne una nuova utilizzando gli stessi valori di proprietà di quella eliminata. Sarà necessario aprire i singoli report, modelli e sottoscrizioni guidate dai dati per riassociare l'origine dei dati condivisa all'elemento in cui viene utilizzata, ma i report, i modelli e le sottoscrizioni continueranno a funzionare come in precedenza purché le proprietà dell'origine dati siano identiche a quelle precedenti.  
  
## <a name="see-also"></a>Vedere anche  
 [Creare e gestire origini dati condivise &#40;Reporting Services in modalità integrata SharePoint&#41;](../create-manage-shared-data-sources-reporting-services-sharepoint-integrated-mode.md)   
 [Connessioni dati, origini dati e stringhe di connessione in Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [Gestire origini dati dei report](manage-report-data-sources.md)   
 [Gestione report &#40;modalità nativa SSRS&#41;](../report-manager-ssrs-native-mode.md)   
 [Connessioni dati o origini dati incorporate e condivise &#40;Generatore report e SSRS&#41;](../embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md)   
 [Pagina delle proprietà origini dati &#40;Gestione report&#41;](../data-sources-properties-page-report-manager.md)   
 [Creare, eliminare o modificare un'origine dati condivisa &#40;Gestione report&#41;](../create-delete-or-modify-a-shared-data-source-report-manager.md)   
 [Configurare le proprietà delle origini dati per un report &#40;Gestione report&#41;](configure-data-source-properties-for-a-report-report-manager.md)  
  
  
