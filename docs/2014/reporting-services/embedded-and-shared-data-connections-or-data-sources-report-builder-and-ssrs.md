---
title: Incorporate e condivise le connessioni dati o origini dati (Generatore Report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- embedded data sources
- shared data sources
- data sources
ms.assetid: f417782c-b85a-4c4d-8a40-839176daba56
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: bf9b9bfd500c5ddb9e10fb1e2320bf0287114808
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63164813"
---
# <a name="embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs"></a>Connessioni dati o origini dati incorporate e condivise (Generatore report e SSRS)
  Nei report vengono usate le connessioni dati per il recupero di dati per un report quando viene eseguita una query o viene elaborato il report. È possibile scegliere da un elenco di tipi di connessione dati incorporati per la connessione a un database relazionale, un database multidimensionale, un servizio Web o ad altre origini di dati. Per la descrizione delle connessioni dati vengono usati i termini riportati di seguito.  
  
-   **Connessione dati.** Nota anche come *origine dati*. In una connessione dati sono inclusi un nome e le proprietà di connessione che dipendono dal tipo di connessione. In base alle caratteristiche di progettazione, in una connessione dati non sono incluse le credenziali. Una connessione dati non consente di specificare i dati da recuperare dall'origine dati esterna. A tale scopo, è necessario specificare una query durante la creazione di un set di dati.  
  
-   **Definizione dell'origine dati.** File che contiene la rappresentazione XML di un'origine dati del report. Quando viene pubblicato un report, le relative origini dati vengono salvate nel server di report o in un sito di SharePoint come definizioni dell'origine dati, indipendentemente dalla definizione del report. Ad esempio, un amministratore del server di report potrebbe aggiornare la stringa di connessione o le credenziali. In un server di report nativo, il tipo di file è con estensione rds. In un sito di SharePoint, il tipo di file è con estensione rsds.  
  
-   **Stringa di connessione.** Una stringa di connessione è una versione della stringa delle proprietà di connessione che sono necessarie per la connessione a un'origine dati. Le proprietà di connessione variano in base al tipo di connessione dati. Per esempi, vedere [connessioni dati, origini dati e stringhe di connessione in Generatore Report](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-report-builder.md).  
  
-   **Origine dati condivisa.** Un'origine dati condivisa è disponibile in un server di report o in un sito di SharePoint per essere usata da più report.  
  
-   **Origine dati incorporata.** Nota anche come *origine dati specifica del report*. Un'origine dati viene definita in un report e utilizzata solo dal report specifico.  
  
-   **Credenziali.** Si tratta delle informazioni di autenticazione necessarie per consentire l'accesso ai dati esterni.  
  
 La differenza tra le origini dati incorporate e quelle condivise dipende dalle diverse modalità di creazione, archiviazione e gestione.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  
## <a name="shared-data-sources"></a>Origini dati condivise  
 Le origini dati condivise sono utili quando si usano spesso le stesse origini dati. Si consiglia di usare le origini dati condivise il più possibile. Rendono i report e l'accesso ai report più facile da gestire, offrono una maggiore protezione dei report e delle origini dati usate. Se è necessaria un'origine dati condivisa, chiedere all'amministratore di sistema di creare una.  
  
 In Generatore report non è possibile creare un'origine dati condivisa. È possibile individuare e selezionare un'origine dati condivisa dal server di report. Per altre informazioni, vedere [Data Connections, Data Sources, and Connection Strings in Report Builder](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-report-builder.md).  
  
 In Progettazione report non è possibile individuare un'origine dati condivisa nel server di report. È possibile creare origini dati condivisi come parte di un progetto in Esplora soluzioni e scegliere se distribuirle in un server di report. È possibile scegliere di usarle solo in locale a causa delle differenze nelle credenziali richieste dal computer in uso o dal server di report. Per altre informazioni, vedere [Connessioni dati, origini dati e stringhe di connessione in Reporting Services](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md).  
  
 L'icona seguente indica un elemento dell'origine dati condivisa nella gerarchia di cartelle del server di report: ![Icona di origine dati condivisa](media/hlp-16datasource.png "Icona di origine dati condivisa")  
  
## <a name="embedded-data-sources"></a>Origini dati incorporate  
 Una connessione a un'origine dati incorporata è una connessione dati salvata nella definizione del report. Le informazioni di connessione a un'origine dati incorporata possono essere usate solo dal report che la contiene. Per definire e gestire le origini dati incorporate, usare la finestra di dialogo **Proprietà origine dati** .  
  
##  <a name="Comparing"></a> Confronto tra incorporate e origini dati condivise  
 Nella tabella seguente vengono riepilogate le differenze fra le origini dati incorporate e quelle condivise:  
  
|Descrizione|Origine dati<br /><br /> origine dati|Condivisa<br /><br /> origine dati|  
|-----------------|------------------------------|----------------------------|  
|La connessione dati è incorporata nella definizione del report.|![Disponibile](media/greencheck.gif "Disponibile")||  
|Il puntatore alla connessione dati nel server di report è incorporato nella definizione del report.||![Disponibile](media/greencheck.gif "Disponibile")|  
|Gestita nel server di report|![Disponibile](media/greencheck.gif "Disponibile")|![Disponibile](media/greencheck.gif "Disponibile")|  
|Richiesta per i set di dati condivisi||![Disponibile](media/greencheck.gif "Disponibile")|  
|Richiesta per i componenti||![Disponibile](media/greencheck.gif "Disponibile")|  
  
## <a name="data-source-credentials"></a>Credenziali origine dati  
 Le credenziali vengono usate per creare un'origine dati incorporata, per eseguire una query o per recuperare dati durante l'elaborazione di report. Il proprietario dell'origine dati determina il tipo di credenziali che è necessario usare per accedere ai dati. Le credenziali sono gestite indipendentemente dalla connessione dati in un server di report, un sito di SharePoint o in un computer locale in un ambiente di creazione di report. A seconda del tipo di origine dati, è possibile salvare le credenziali per evitare la richiesta o di impostare di chiedere conferma a ciascun utente. Le credenziali necessarie potrebbero variare a seconda se la connessione all'origine dati viene eseguita dal computer in uso o dal server di report. Per altre informazioni, vedere [specificare le credenziali in Generatore Report](../../2014/reporting-services/specify-credentials-in-report-builder.md) e [connessioni dati, origini dati e stringhe di connessione in Reporting Services](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiungere dati a un Report &#40;Report e SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [Concetti relativi alla creazione di report &#40;Generatore report e SSRS&#41;](report-design/report-authoring-concepts-report-builder-and-ssrs.md)   
 [Origini dei dati supportate da Reporting Services &#40;SSRS&#41;](create-deploy-and-manage-mobile-and-paginated-reports.md)   
 [Aggiungere e verificare una connessione dati o un'origine dati &#40;Report e SSRS&#41;](report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)   
 [Set di dati condivisi e incorporati &#40;Generatore report e SSRS&#41;](report-data/embedded-and-shared-datasets-report-builder-and-ssrs.md)  
  
  
