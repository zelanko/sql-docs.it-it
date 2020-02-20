---
title: Tipo di connessione PowerPivot (SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.assetid: a104c3c7-f118-4d02-9a0f-6859f1469d11
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 8d6c9273abda883b175a46d9695d4d231cc5bc73
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "74190758"
---
# <a name="power-pivot-connection-type-ssrs"></a>Tipo di connessione PowerPivot (SSRS)
  È possibile usare l'estensione per l'elaborazione dati di SQL Server Analysis Services per recuperare dati da una cartella di lavoro di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] pubblicata in una raccolta [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] di SharePoint.  
  
 Usare le informazioni presenti in questo argomento per compilare un'origine dati. Per istruzioni dettagliate, vedere [Aggiungere e verificare una connessione dati &#40;Generatore report e SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
## <a name="prerequisites"></a>Prerequisites  
 L'origine dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] deve essere pubblicata in una raccolta [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] in un sito di SharePoint.  
  
 Per supportare connessioni da Generatore report in una cartella di lavoro di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , è necessario che nel computer workstation sia disponibile SQL Server 2008 R2 ADOMD.NET. La libreria client viene installata con [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per Excel, ma se si usa un computer che non include questa applicazione, è necessario scaricare e installare ADOMD.NET dalla pagina relativa a [SQL Server 2008 R2 Feature Pack](https://www.microsoft.com/download/details.aspx?id=16978).  
  
## <a name="data-source-type"></a>Tipo di origine dati  
 Utilizzare il tipo di origine dati del report **Microsoft SQL Server Analysis Services**.  
  
## <a name="connection-string"></a>Connection String  
 La stringa di connessione è l'URL alla cartella di lavoro [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] pubblicata in SharePoint nella raccolta [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] o in un'altra libreria, ad esempio `https://contoso-srv/subsite/PowerPivotLibrary/ContosoSales.xlsx`.  
  
## <a name="credentials"></a>Credenziali  
 Specificare le credenziali necessarie per accedere alla cartella di lavoro di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] e al sito di SharePoint, ad esempio Autenticazione di Windows (sicurezza integrata). Per altre informazioni, vedere [Creare stringhe di connessione dati - Generatore report e SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md) o [Specificare le credenziali e le informazioni sulla connessione per le origini dati del report](specify-credential-and-connection-information-for-report-data-sources.md).  
  
## <a name="queries"></a>Query  
 Dopo essersi connessi all'origine dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , usare la query in formato grafico MDX per compilare una query individuando e selezionando una delle strutture di dati sottostanti. Dopo aver compilato una query, eseguirla per visualizzare dati di esempio nel riquadro dei risultati.  
  
 La query viene analizzata tramite Progettazione query per determinare i campi del set di dati. È inoltre possibile modificare manualmente la raccolta dei campi del set di dati nel riquadro dei **dati del report** . Per altre informazioni, vedere [Aggiunta, modifica e aggiornamento di campi nel riquadro dei dati del report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-data/add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md).  
  
## <a name="filters"></a>Filtri  
 Nel riquadro Filtri specificare le dimensioni e i membri da filtrare o includere nei risultati delle query.  
  
## <a name="parameters"></a>Parametri  
 Nel riquadro Filtri selezionare l'opzione **Parametri** affinché un filtro crei automaticamente un parametro di report con valori disponibili che corrispondono alle selezioni del filtro.  
  
## <a name="remarks"></a>Osservazioni  
 Se viene aperto Generatore report dalla cartella di lavoro di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] in una raccolta [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , le tabelle pivot, i grafici pivot, i filtri dei dati e altre caratteristiche di layout e analitiche della cartella di lavoro di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] non vengono ricreati nel report. Al contrario, nel report vuoto è inclusa un'origine dati preconfigurata che punta ai dati della cartella di lavoro di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . La progettazione di report basati su una cartella di lavoro di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] può richiedere molto tempo a seconda del numero di filtri dei dati, di filtri, di tabelle o di grafici che si vuole ricreare nel report. Un approccio migliore consiste nel prevedere la presentazione dei dati desiderati in un report indipendentemente dalla progettazione di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
 I dati di una cartella di lavoro di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] sono molto compressi, mentre i dati recuperati dalla cartella di lavoro di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per un report non sono compressi. Utilizzare Progettazione query per specificare i filtri e i parametri utili per limitare i dati a quelli necessari per il report.  
  
 A differenza della connessione a un cubo di Analysis Services, un modello [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] non ha gerarchie. Per fornire una funzionalità simile ai filtri dei dati correlati nella cartella di lavoro, è necessario creare parametri di propagazione nel report. Per altre informazioni, vedere [Aggiungere parametri di propagazione a un report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/add-cascading-parameters-to-a-report-report-builder-and-ssrs.md).  
  
 In alcuni casi, potrebbe essere necessario regolare le espressioni per contenere i valori dei dati sottostanti dal modello [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , nonché modificare le espressioni per convertire i dati nel tipo di dati corretto oppure aggiungere o rimuovere una funzione di aggregazione. Ad esempio, per convertire il tipo di dati da String a Integer, utilizzare `=CInt`. Verificare sempre che nel report vengano visualizzati i valori previsti dai dati del modello [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] prima di pubblicare il report.  
  
 Le immagini di anteprima di un report in una raccolta [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] vengono generate solo se vengono soddisfatte le condizioni seguenti:  
  
-   Il report e la cartella di lavoro [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] che fornisce i dati devono venire archiviati insieme nella stessa Raccolta [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
-   Il report contiene solo dati di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] da un'origine dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
## <a name="see-also"></a>Vedere anche  
 [Interfaccia utente di Progettazione query MDX di Analysis Services &#40;Generatore report&#41;](https://msdn.microsoft.com/library/7e288eee-2d37-485e-a6a0-dbba5e041e26)   
 [Espressioni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  
