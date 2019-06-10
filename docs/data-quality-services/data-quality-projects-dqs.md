---
title: Progetti Data Quality (DQS) | Microsoft Docs
ms.custom: ''
ms.date: 10/01/2012
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: a43fc9c0-19b6-414a-8661-4c7c55e0c03e
author: lrtoyou1223
ms.author: lle
manager: jroth
ms.openlocfilehash: eeaef98e2bd5ae195cb8a15b9c82a2946807d90d
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66797691"
---
# <a name="data-quality-projects-dqs"></a>Progetti Data Quality (DQS)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Un progetto di qualità dei dati in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) consiste nell'utilizzo di una Knowledge Base per migliorare la qualità dei dati di origine eseguendo attività di *pulizia dei dati* e di *individuazione di corrispondenze tra dati* ed esportando quindi i dati risultanti in un database SQL Server o in un file csv. È possibile creare un progetto di qualità dei dati come progetto di pulizia o come progetto di corrispondenza per eseguire le rispettive attività. È possibile eseguire progetti di pulizia e di individuazione delle corrispondenze utilizzando la stessa Knowledge Base, poiché le informazioni per la pulizia e per l'individuazione di corrispondenze possono essere inserite all'interno della stessa Knowledge Base.  
  
 Un progetto di qualità dei dati offre i vantaggi seguenti:  
  
-   Consente di eseguire la pulizia dei dati sui dati di origine utilizzando le informazioni in una Knowledge Base DQS.  
  
-   Consente di eseguire l'individuazione delle corrispondenze sui dati di origine utilizzando i criteri di corrispondenza in una Knowledge Base.  
  
-   Fornisce una procedura guidata per supportare le attività di pulizia e individuazione delle corrispondenze e consente di esportare i dati selezionati in un database SQL Server o in un file csv. L'amministratore dei dati può utilizzare il progetto di qualità dei dati per eseguire e controllare i passaggi di pulizia e di individuazione delle corrispondenze sia computerizzati che interattivi.  
  
##  <a name="Cleansing"></a> Progetto Data Quality: attività di pulizia dei dati  
 I progetti Data Quality di pulizia consentono di pulire i dati di origine in base a una Knowledge Base. L'attività di pulizia dei dati in DQS è un processo in due passaggi:  
  
1.  Un processo *computerizzato* di pulizia dei dati tramite cui vengono analizzati i dati di origine in base alle informazioni incluse nella Knowledge Base e vengono proposte modifiche. I dati elaborati vengono suddivisi da DQS in categorie (suggerito, nuovo, non valido, con correzione e corretto), quindi vengono presentati all'utente per ulteriore elaborazione.  
  
2.  Quando il processo di pulizia è *interattivo* , l'amministratore dei dati può approvare, rifiutare o modificare i dati proposti dal processo di pulizia computerizzato.  
  
 Per informazioni dettagliate sull'attività di pulizia in un progetto di qualità dei dati, vedere [Data Cleansing](../data-quality-services/data-cleansing.md).  
  
##  <a name="Matching"></a> Progetto Data Quality: attività di individuazione delle corrispondenze  
 Un progetto Data Quality di corrispondenza tra dati consente di eseguire l'attività di individuazione di corrispondenze in base ai criteri di corrispondenza in una Knowledge Base per impedire la duplicazione dei dati mediante l'identificazione di corrispondenze esatte e approssimative e permettendo quindi la rimozione dei dati duplicati. Si consiglia di pulire i dati prima di eseguire su questi l'individuazione di corrispondenze. A tale scopo:  
  
1.  Creare un progetto Data Quality, selezionare l'attività **Pulizia** , completare l'attività di pulizia sui dati di origine, quindi esportarli in una tabella di un database di SQL Server.  
  
2.  Creare un altro progetto Data Quality utilizzando una Knowledge Base che contiene criteri di corrispondenza, selezionare l'attività **Corrispondenza** , quindi nella pagina **Mappa** , selezionare il database e la tabella dove sono stati esportati i dati puliti nel passaggio 1.  
  
3.  Completare l'attività di individuazione delle corrispondenze sui dati puliti.  
  
 Per informazioni dettagliate sull'attività di individuazione delle corrispondenze in un progetto Data Quality, vedere [Data Matching](../data-quality-services/data-matching.md).  
  
##  <a name="ProfilingNotification"></a> Profiling di dati e notifiche  
 Durante l'esecuzione delle attività di pulizia e corrispondenza in un progetto Data Quality, è possibile ottenere statistiche e informazioni in tempo reale sui dati elaborati da DQS. Il profiling dati consente di valutare l'efficacia dei processi di pulizia e di corrispondenza nonché l'entità del miglioramento dei dati grazie alla pulizia o all'individuazione delle corrispondenze. Il profiling DQS fornisce due dimensioni della qualità dei dati: *completezza* (l'entità della presenza dei dati) e *accuratezza* (la misura entro cui i dati possono essere utilizzati per gli scopi previsti). Inoltre, in base alle informazioni sul profiling dei dati, vengono presentate notifiche riguardanti azioni che possono essere intraprese per migliorare la pulizia dei dati e le operazioni di individuazione delle corrispondenze. Per informazioni dettagliate sul profiling dei dati e sulle notifiche, vedere [Data Profiling and Notifications in DQS](../data-quality-services/data-profiling-and-notifications-in-dqs.md).  
  
## <a name="related-tasks"></a>Attività correlate  
  
|Descrizione dell'attività|Argomento|  
|----------------------|-----------|  
|Viene descritto come creare un progetto Data Quality.|[Creare un progetto Data Quality](../data-quality-services/create-a-data-quality-project.md)|  
|Viene descritto come aprire, sbloccare, rinominare ed eliminare un progetto Data Quality.|[Aprire, sbloccare, rinominare ed eliminare un progetto Data Quality](open-unlock-rename-and-delete-a-data-quality-project.md)|  
|Viene descritto come aprire un progetto di Integration Services in [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)].|[Aprire progetti di Integration Services in Data Quality Client](../data-quality-services/open-integration-services-projects-in-data-quality-client.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Knowledge Base e domini DQS](../data-quality-services/dqs-knowledge-bases-and-domains.md)  
  
  
