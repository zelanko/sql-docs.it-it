---
title: Tipo di connessione PowerPivot (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: a104c3c7-f118-4d02-9a0f-6859f1469d11
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 50ce060d270cf06a771136c581bf96fe1ec21eee
ms.sourcegitcommit: 59c09dbe29882cbed539229a9bc1de381a5a4471
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/11/2020
ms.locfileid: "79112140"
---
# <a name="powerpivot-connection-type-ssrs"></a>Tipo di connessione PowerPivot (SSRS)
  È possibile utilizzare l'estensione di elaborazione dei dati di SQL Server Analysis Services per recuperare dati da una cartella di lavoro di PowerPivot pubblicata in una raccolta PowerPivot di SharePoint.  
  
 Usare le informazioni presenti in questo argomento per compilare un'origine dati. Per istruzioni dettagliate, vedere [aggiungere e verificare una connessione dati o un'origine dati &#40;Generatore report e SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
## <a name="prerequisites"></a>Prerequisites  
 L'origine dati PowerPivot deve essere pubblicata in una raccolta PowerPivot in un sito di SharePoint.  
  
 Per supportare connessioni da Generatore report in una cartella di lavoro di PowerPivot, è necessario che nel computer workstation sia disponibile SQL Server 2008 R2 ADOMD.NET. La libreria client viene installata con PowerPivot per Excel, ma se si utilizza un computer che non dispone di questa applicazione, è necessario scaricare e installare ADOMD.NET dalla pagina relativa a [SQL Server 2008 R2 Feature Pack](https://www.microsoft.com/download/details.aspx?id=44272).  
  
## <a name="data-source-type"></a>Tipo di origine dati  
 Utilizzare il tipo di origine dati del report **Microsoft SQL Server Analysis Services**.  
  
## <a name="connection-string"></a>Connection String  
 La stringa di connessione è l'URL della cartella di lavoro di PowerPivot pubblicata in SharePoint nella raccolta PowerPivot o in un'altra http://contoso-srv/subsite/PowerPivotLibrary/ContosoSales.xlsxlibreria, ad esempio.  
  
## <a name="credentials"></a>Credenziali  
 Specificare le credenziali necessarie per accedere alla cartella di lavoro di PowerPivot e al sito di SharePoint, ad esempio Autenticazione di Windows (sicurezza integrata). Per ulteriori informazioni, vedere [connessioni dati, origini dati e stringhe di connessione in Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md) o [specificare le credenziali in Generatore report](../specify-credentials-in-report-builder.md).  
  
## <a name="queries"></a>Query  
 Dopo essersi connessi all'origine dati PowerPivot, utilizzare la query in formato grafico MDX per compilare una query visualizzando e selezionando dalle strutture di dati sottostanti. Dopo aver compilato una query, eseguirla per visualizzare dati di esempio nel riquadro dei risultati.  
  
 La query viene analizzata tramite Progettazione query per determinare i campi del set di dati. È inoltre possibile modificare manualmente la raccolta dei campi del set di dati nel riquadro dei **dati del report** . Per altre informazioni, vedere [Aggiunta, modifica e aggiornamento di campi nel riquadro dei dati del report &#40;Generatore report e SSRS&#41;](add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md).  
  
## <a name="filters"></a>Filtri  
 Nel riquadro Filtri specificare le dimensioni e i membri da filtrare o includere nei risultati delle query.  
  
## <a name="parameters"></a>Parametri  
 Nel riquadro Filtri selezionare l'opzione **Parametri** affinché un filtro crei automaticamente un parametro di report con valori disponibili che corrispondono alle selezioni del filtro.  
  
## <a name="remarks"></a>Osservazioni  
 Se viene aperto Generatore report dalla cartella di lavoro di PowerPivot in una raccolta PowerPivot, le tabelle pivot, i grafici pivot, i filtri dei dati e altre caratteristiche di layout e analitiche della cartella di lavoro di PowerPivot non vengono ricreati nel report. Al contrario, nel report vuoto è inclusa un'origine dati preconfigurata che punta ai dati della cartella di lavoro di PowerPivot. La progettazione di report basati su una cartella di lavoro di PowerPivot può richiedere molto tempo a seconda del numero di filtri dei dati, di filtri, di tabelle o di grafici che si desidera ricreare nel report. Un approccio migliore consiste nel prevedere la presentazione dei dati desiderati in un report indipendentemente dalla progettazione di PowerPivot.  
  
 I dati di una cartella di lavoro di PowerPivot sono molto compressi, mentre i dati recuperati dalla cartella di lavoro di PowerPivot per un report non sono compressi. Utilizzare Progettazione query per specificare i filtri e i parametri utili per limitare i dati a quelli necessari per il report.  
  
 A differenza della connessione a un cubo di Analysis Services, un modello PowerPivot non dispone di gerarchie. Per fornire una funzionalità simile ai filtri dei dati correlati nella cartella di lavoro, è necessario creare parametri di propagazione nel report. Per altre informazioni, vedere [Aggiungere parametri di propagazione a un report &#40;Generatore report e SSRS&#41;](../report-design/add-cascading-parameters-to-a-report-report-builder-and-ssrs.md).  
  
 In alcuni casi, potrebbe essere necessario regolare le espressioni per contenere i valori dei dati sottostanti dal modello PowerPivot, nonché modificare le espressioni per convertire i dati nel tipo di dati corretto oppure aggiungere o rimuovere una funzione di aggregazione. Ad esempio, per convertire il tipo di dati da String a Integer, utilizzare `=CInt`. Verificare sempre che nel report vengano visualizzati i valori previsti dai dati del modello PowerPivot prima di pubblicare il report.  
  
 Le immagini di anteprima di un report in una raccolta PowerPivot vengono generate solo se vengono soddisfatte le condizioni seguenti:  
  
-   Il report e la cartella di lavoro di PowerPivot che fornisce i dati devono essere archiviati insieme nella stessa raccolta PowerPivot.  
  
-   Nel report sono contenuti solo dati PowerPivot di un'origine dati PowerPivot.  
  
## <a name="see-also"></a>Vedere anche  
 [Interfaccia utente di Progettazione query MDX di Analysis Services &#40;Generatore report&#41;](../analysis-services-mdx-query-designer-user-interface-report-builder.md)   
 [Espressioni &#40;Generatore report e SSRS&#41;](../report-design/expressions-report-builder-and-ssrs.md)  
  
  
