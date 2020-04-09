---
title: Use an External Data Source for Subscriber Data (Data-Driven Subscription) (Usare un'origine dei dati esterna per i dati del Sottoscrittore (sottoscrizione guidata dai dati)) | Microsoft Docs
description: Informazioni su come usare un'origine dati esterna per una sottoscrizione dinamica guidata dai dati. Informazioni sull'elaborazione dei dati, l'esecuzione di query, le opzioni di recapito e il passaggio di parametri.
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: subscriptions
ms.topic: conceptual
helpviewer_keywords:
- subscriber data sources [Reporting Services]
- subscriptions [Reporting Services], external data sources
- query-based subscriptions [Reporting Services]
- external data sources [Reporting Services]
- data-driven subscriptions
- data sources [Reporting Services], subscriptions
ms.assetid: 1cade8ec-729c-4df8-a428-e75c9ad86369
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 8d071905e9efe6c084cafaeeb8304a37b03fbbb5
ms.sourcegitcommit: c6a2efe551e37883c1749bdd9e3c06eb54ccedc9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/06/2020
ms.locfileid: "80742223"
---
# <a name="use-an-external-data-source-for-subscriber-data-data-driven-subscription"></a>Utilizzare un'origine dei dati esterna per i dati del Sottoscrittore (sottoscrizione guidata dai dati)
  In una sottoscrizione guidata dai dati i dati di sottoscrizione dinamici vengono ottenuti tramite una query o un comando che consente di recuperare i dati da un'origine dei dati esterna. I dati di sottoscrizione possono essere recuperati da qualsiasi origine dei dati supportata che soddisfi i requisiti per l'elaborazione della sottoscrizione guidata dai dati. La sintassi della query o del comando deve essere valida per un'estensione per l'elaborazione dati installata con il server di report.  
  
## <a name="data-processing-requirements"></a>Requisiti per l'elaborazione dati  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usa le estensioni per l'elaborazione dei dati per recuperare i dati di sottoscrizione. I tipi di origine dei dati consigliati sono i seguenti:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database relazionali  
  
-   database Oracle  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] origini dati di data mining e multidimensionali  
  
-   Origini dei dati XML  
  
     Quando si utilizza l'estensione per l'elaborazione dati XML per i dati del Sottoscrittore, aumentare le impostazioni di timeout per le query nella sottoscrizione. Per i valori di timeout per le query, nell'estensione per l'elaborazione dati XML vengono utilizzati i millisecondi anziché i secondi. Se non si aumenta il valore di timeout, la sottoscrizione potrebbe non riuscire a causa di tempi di elaborazione non sufficienti.  
  
     Quando si configura la connessione all'origine dei dati del Sottoscrittore, evitare di usare l'opzione **Credenziali non richieste** . Quando si utilizza l'estensione per l'elaborazione dati XML per recuperare i dati di sottoscrizione in fase di esecuzione è consigliabile utilizzare le credenziali archiviate.  
  
 Potrebbe essere possibile utilizzare altri tipi di origine dei dati supportati, ma il loro funzionamento non è garantito. I tipi di origine dei dati seguenti, ad esempio, non possono essere utilizzati per i dati del Sottoscrittore:  
  
-   Database SAP Netweaver BI  
  
-   Modelli di report  
  
 Se si ha un'estensione per l'elaborazione dati personalizzata che si vuole usare nelle sottoscrizioni guidate dai dati, è necessario che siano implementate le interfacce <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand> e <xref:Microsoft.ReportingServices.DataProcessing.IDataReader> . L'estensione per l'elaborazione dati deve supportare l'esecuzione di query sul solo schema. Questo tipo di query è utilizzato per recuperare i metadati delle colonne in fase di progettazione, per consentire agli utenti di eseguire il mapping tra le colonne e le opzioni di recapito e i parametri del report nella definizione della sottoscrizione. L'esecuzione di query sul solo schema avviene in una fase iniziale, durante la definizione della sottoscrizione.  
  
## <a name="query-requirements"></a>Requisiti per le query  
 Quando si crea una query per recuperare i dati di sottoscrizione, tenere presente quanto segue:  
  
-   È possibile creare una sola query per la sottoscrizione.  
  
-   La query deve restituire tutti i valori che si desidera utilizzare per le opzioni di recapito e per specificare i parametri del report.  
  
-   Tramite il server di report viene creato un recapito di report per ogni riga del set di risultati. Se il set di risultati è costituito da trecento righe, tramite il server di report verrà eseguito un tentativo di recapitare trecento report.  
  
## <a name="setting-delivery-options-using-variable-data-from-a-subscriber-database"></a>Impostazione di opzioni di recapito tramite dati di un database del Sottoscrittore  
 È possibile utilizzare i dati del database del Sottoscrittore per personalizzare le opzioni di recapito per ogni destinatario. Le opzioni disponibili sono determinate dal tipo di estensione per il recapito in uso. Se si utilizza l'estensione per il recapito tramite posta elettronica del server di report, la query dovrebbe contenere un alias di posta elettronica per ogni sottoscrittore. Se si utilizza un recapito alla condivisione file, i dati del Sottoscrittore devono includere valori che possano essere utilizzati per creare file di report specifici del Sottoscrittore o per offrire una destinazione per il recapito. Per altre informazioni, vedere [Recapito tramite posta elettronica in Reporting Services](../../reporting-services/subscriptions/e-mail-delivery-in-reporting-services.md).  
  
## <a name="passing-parameter-values-from-the-subscriber-database-to-the-report"></a>Passaggio di valori dei parametri dal database del Sottoscrittore al report  
 Se si sta creando una sottoscrizione guidata dai dati per un report con parametri, è possibile fornire valori dei parametri variabili per personalizzare l'output di ogni report. Ad esempio, un database del Sottoscrittore potrebbe contenere numeri di identificazione, date di assunzione, titoli professionali e ubicazioni degli uffici dei dipendenti, tutte informazioni utilizzabili per filtrare i dati dei report. Se il report accetta parametri basati su queste o altre colonne di dati disponibili, è possibile eseguire il mapping di ogni parametro alla colonna appropriata.  
  
 Quando si esegue il mapping dei campi del Sottoscrittore ai parametri del report, verificare che i tipi di dati e la lunghezza delle colonne siano compatibili. Nel caso siano presenti tipi di dati non corrispondenti si verificherà un errore durante l'elaborazione della sottoscrizione. Per altre informazioni sull'uso di dati del sottoscrittore in un report con parametri, vedere [Creare una sottoscrizione guidata dai dati &#40;esercitazione su SSRS&#41;](../../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md).  
  
## <a name="modifying-the-subscriber-data-source"></a>Modifica dell'origine dei dati del sottoscrittore  
 Le modifiche all'origine dei dati del sottoscrittore descritte di seguito possono impedire l'esecuzione della sottoscrizione:  
  
-   Rimozione di colonne cui si fa riferimento nella sottoscrizione.  
  
-   Modifica della struttura della tabella dell'origine dei dati.  
  
-   Modifica del tipo di dati e altre proprietà della colonna.  
  
 Se si apporta una qualsiasi di queste modifiche, sarà necessario aggiornare la sottoscrizione.  
  
## <a name="see-also"></a>Vedere anche  
 [Come creare, modificare ed eliminare le sottoscrizioni guidate dai dati](../../reporting-services/subscriptions/create-modify-and-delete-data-driven-subscriptions.md)   
 [Data-Driven Subscriptions](../../reporting-services/subscriptions/data-driven-subscriptions.md)   
 [Sottoscrizioni e recapito &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)  
  
  
