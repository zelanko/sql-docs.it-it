---
title: Creare e gestire una partizione locale (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- local partitions [Analysis Services]
- partitions [Analysis Services], local
- partitions [Analysis Services], creating
ms.assetid: eaa95278-9ce9-47d5-a6b6-1046e7076599
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c06e40e452fa0db682e2f79b523ddcd90d0450c2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "78175790"
---
# <a name="create-and-manage-a-local-partition-analysis-services"></a>Creare e gestire una partizione locale (Analysis Services)
  Per migliorare le prestazioni di elaborazione è possibile creare partizioni aggiuntive per un gruppo di misure. Con più partizioni è possibile allocare le tabelle dei fatti in un numero corrispondente di file di dati fisici sia su server locali che su server remoti. In Analysis Services le partizioni possono essere elaborate in modo indipendente e in parallelo, offrendo maggiore controllo sull'elaborazione dei carichi di lavoro sul server.

 È possibile creare le partizioni in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] durante la progettazione dei modelli o dopo la distribuzione della soluzione usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o XMLA. Si consiglia di scegliere un unico approccio. Se si alterna tra gli strumenti, è possibile che le modifiche apportate a un database distribuito in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] vengono sovrascritte quando si ridistribuisce successivamente la soluzione da [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].

## <a name="before-you-start"></a>Prima di iniziare
 Verificare di disporre della Business Intelligence Edition o della Enterprise Edition. La Standard Edition non supporta più partizioni. Per controllare l'edizione, fare clic con il pulsante destro del [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] mouse sul nodo del server in e scegliere **report** | **generale**. Per ulteriori informazioni sulla disponibilità delle funzionalità, vedere [funzionalità supportate dalle edizioni di SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).

 È importante tenere presente che, per poter unire le partizioni in secondo momento, è necessario che queste condividano la stessa progettazione delle aggregazioni. Le partizioni possono essere unite solo se dispongono della stessa modalità di archiviazione e della medesima progettazione delle aggregazioni.

> [!TIP]
>  Esplorare i dati nella vista origine dati per determinare l'intervallo e la profondità dei dati da partizionare. Ad esempio, se si esegue il partizionamento in base alla data, è possibile effettuare l'ordinamento in base a una colonna di date per determinare i limiti superiore e inferiore di ogni partizione.

## <a name="choose-an-approach"></a>Scegliere un approccio
 L'aspetto più importante per la creazione di partizioni è segmentare i dati in modo che non siano presenti righe duplicate. I dati devono essere archiviati in un'unica partizione per evitare il doppio conteggio delle righe. Per questo è abbastanza frequente utilizzare il partizionamento per data, in modo da definire limiti chiari tra ogni partizione.

 È possibile utilizzare qualsiasi tecnica per distribuire le tabelle dei fatti tra più partizioni. Per segmentare i dati è possibile utilizzare le tecniche riportate di seguito.

|Tecnica|Consigli|
|---------------|---------------------|
|Utilizzare query SQL per segmentare le tabelle dei fatti|Le partizioni possono essere originate da query SQL. Durante l'elaborazione, la query SQL recupera i dati. Con la clausola WHERE della query viene specificato il filtro che segmenta i dati per ogni partizione. In Analysis Services la query viene generata automaticamente, ma è necessario compilare la clausola WHERE per segmentare i dati in modo corretto.<br /><br /> Il vantaggio principale di questo approccio consiste nella semplicità con cui è possibile partizionare i dati da una singola tabella di origine. Se tutti i dati di origine provengono da una tabella dei fatti di grandi dimensioni, è possibile query per filtrare i dati in partizioni distinte, senza dover creare strutture dei dati aggiuntive nella vista origine dati.<br /><br /> Lo svantaggio è che l'utilizzo delle query interrompe l'associazione tra la partizione e la vista origine dati. Se in un secondo momento si effettua l'aggiornamento della vista origine dati nel progetto di Analysis Services, ad esempio aggiungendo colonne alla tabella dei fatti, è necessario modificare manualmente le query per ogni partizione in modo da includere la nuova colonna. Il secondo approccio, descritto di seguito, non presenta questo svantaggio.|
|Utilizzare le tabelle nella vista origine dati per segmentare le tabelle dei fatti|È possibile associare una partizione a una tabella, una query denominata o una vista nella vista origine dati. Come base di una partizione, tutte e tre sono equivalenti dal punto di vista funzionale. L'intera tabella, query denominata o vista fornisce tutti i dati per una singola partizione.<br /><br /> L'utilizzo di una tabella, una vista o una query denominata comporta l'inclusione dell'intera logica di selezione di dati nella vista origine dati, facilitando la gestione e il mantenimento nel tempo. Un importante vantaggio offerto da questo approccio è che le associazioni di tabella vengono mantenute. Se si aggiorna tabella di origine in un secondo momento, non è necessario modificare le partizioni che la utilizzano. In secondo luogo tutte le tabelle, le query denominate e le viste si trovano in un'area di lavoro comune, rendendo gli aggiornamenti più pratici rispetto all'apertura e alla modifica delle singole query per le partizioni.|

## <a name="option-1-filter-a-fact-table-for-multiple-partitions"></a>Opzione 1: filtrare una tabella dei fatti per più partizioni
 Per creare più partizioni, iniziare modificando la proprietà **Origine** della partizione predefinita. Per impostazione predefinita, un gruppo di misure viene creato utilizzando una sola partizione associata a una singola tabella della vista origine dati. Prima di poter aggiungere ulteriori partizioni è necessario modificare la partizione originale in modo che contenga solo una parte delle tabelle dei fatti. È quindi possibile continuare a creare partizioni aggiuntive per archiviare il resto dei dati.

 Costruire i filtri in modo che i dati non vengano duplicati tra le partizioni. Un filtro di una partizione indica i dati della tabella dei fatti utilizzati nella partizione. È importante che i filtri di tutte le partizioni di un cubo estraggano dalla tabella dei fatti set di dati che si escludono reciprocamente. La stessa tabella dei fatti potrebbe essere conteggiata due volte se si trova in più partizioni.

1.  In [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], in Esplora soluzioni fare doppio clic sul cubo per aprirlo in Progettazione cubi, quindi scegliere la scheda **Partizioni** .

2.  Espandere il gruppo di misure per il quale vengono aggiunte le partizioni. Per impostazione predefinita, ogni gruppo di misure dispone di una partizione, associata a una tabella dei fatti nella vista origine dati.

3.  Nella colonna di origine fare clic sul pulsante Sfoglia (. .) per aprire la finestra di dialogo Origine partizione.

     ![Colonna di origine nel riquadro Partizione](../media/ssas-partitionsource.png "Colonna di origine nel riquadro Partizione")

4.  In Tipo di associazione selezionare **Associazione di query**. La query SQL per la selezione dei dati viene automaticamente visualizzata.

5.  Nella clausola WHERE in basso aggiungere un filtro che segmenti i dati per questa partizione.

     Esempi di sintassi della clausola WHERE includono `WHERE OrderDateKey >= '20060101'` o `WHERE OrderDateKey BETWEEN '20051001' AND '20051201'`. Per altri esempi, vedere [WHERE &#40;Transact-SQL&#41;](/sql/t-sql/queries/where-transact-sql).

     Notare che i filtri seguenti si escludono reciprocamente all'interno di ogni set:

    |||
    |-|-|
    |Set 1:|"SaleYear" = 2012<br /><br /> "SaleYear" = 2013|
    |Set 2:|"Continent" = 'NorthAmerica'<br /><br /> "Continent" = 'Europe'<br /><br /> "Continent" = 'SouthAmerica'|
    |Set 3:|"Country" = 'USA'<br /><br /> "Country" = 'Mexico'<br /><br /> ("Country" <> 'USA' AND "Country" <> 'Mexico')|

6.  Fare clic su **Controlla** per verificare la presenza di errori di sintassi, quindi fare clic su **OK**.

7.  Ripetere i passaggi precedenti per creare le partizioni rimanenti, modificando di volta in volta la clausola WHERE per selezionare la sezione di dati successiva.

8.  Distribuire la soluzione o elaborare la partizione per caricare i dati. Assicurarsi di elaborare tutte le partizioni.

9. Esplorare il cubo per verificare che vengano restituiti i dati corretti.

 Avendo a disposizione un gruppo di misure in cui vengono utilizzati più gruppi di misure, è possibile creare ulteriori partizioni in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. In un gruppo di misure, fare clic con il pulsante destro del mouse sulla cartella Partizioni e selezionare **Nuove partizioni** per avviare la procedura guidata.

> [!NOTE]
>  Anziché filtrare i dati di una partizione, è possibile utilizzare la stessa query per creare una query denominata nella vista origine dati e quindi basare la partizione sulla query denominata.

## <a name="option-2-use-tables-views-or-named-queries"></a>Opzione 2: utilizzare tabelle, viste o query denominate
 Se nella vista origine dati i fatti sono già organizzati in singole tabelle, ad esempio per anno o trimestre, è possibile creare partizioni basate su una singola tabella, in modo che ogni partizione disponga della propria tabella di origine dati. Questa è essenzialmente la modalità predefinita di partizionamento dei gruppi di misure, ma nel caso di più partizioni si suddivide la partizione originale in più partizioni e si esegue il mapping di ogni nuova partizione alla tabella di origine che fornisce dati specifici.

 Viste e query denominate sono funzionalmente equivalenti alle tabelle, in quanto tutti e tre gli oggetti vengono definiti nella vista origine dati e associati a una partizione utilizzando l'opzione Associazione tabella nella finestra di dialogo Origine partizione. È possibile creare una vista o una query denominata per generare il segmento di dati necessario per ogni partizione. Per altre informazioni, vedere [Definire query denominate in una vista origine dati &#40;Analysis Services&#41;](define-named-queries-in-a-data-source-view-analysis-services.md).

> [!IMPORTANT]
>  Quando si creano query denominate che si escludono a vicenda per le partizioni in una vista origine dati, assicurarsi che l'insieme dei dati per le partizioni includa tutti i dati di un gruppo di misure che si desidera inserire nel cubo. Assicurarsi inoltre che non sia presente una partizione predefinita basata sull'intera tabella per il gruppo di misure, altrimenti le partizioni basate su query risulteranno sovrapposte alla query basata sull'intera tabella.

1.  Creare una o più query denominate da utilizzare come origine delle partizioni. Per altre informazioni, vedere [Definire query denominate in una vista origine dati &#40;Analysis Services&#41;](define-named-queries-in-a-data-source-view-analysis-services.md).

     La query denominata deve essere basata sulla tabella dei fatti associata al gruppo di misure. Ad esempio, se si sta effettuando il partizionamento del gruppo di misure FactInternetSales, nelle query denominate nella vista origine dati deve essere specificata la tabella FactInternetSales nell'istruzione FROM.

2.  In [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], in Esplora soluzioni fare doppio clic sul cubo per aprirlo in Progettazione cubi, quindi scegliere la scheda **Partizioni** .

3.  Espandere il gruppo di misure per il quale vengono aggiunte le partizioni.

4.  Fare clic su **Nuova partizione** per avviare la Creazione guidata partizione. Se sono state create query denominate utilizzando la tabella dei fatti associata al gruppo di misure, dovrebbero apparire le query denominate create nel passaggio precedente.

5.  In Impostazione informazioni origine scegliere una delle query denominate create in un passaggio precedente. Se non viene visualizzata alcuna query denominata, tornare alla vista origine dati e controllare l'istruzione FROM.

6.  Fare clic su **Avanti** per accettare i valori predefiniti per ogni pagina successiva.

7.  Nell'ultima pagina, Completamento procedura guidata, assegnare alla partizione un nome descrittivo.

8.  Fare clic su **Fine**.

9. Ripetere i passaggi precedenti per creare le partizioni rimanenti, scegliendo di volta in volta una diversa query denominata per selezionare la sezione di dati successiva.

10. Distribuire la soluzione o elaborare la partizione per caricare i dati. Assicurarsi di elaborare tutte le partizioni.

11. Esplorare il cubo per verificare che vengano restituiti i dati corretti.

## <a name="next-step"></a>passaggio successivo
 Quando si creano query che si escludono reciprocamente per le partizioni, verificare che i dati combinati delle partizioni includano tutti i dati che si desidera inserire nel cubo.

 Come passaggio finale in genere si rimuove la partizione predefinita basata sulla tabella stessa (se ancora esistente) per evitare che le query basate sulle partizioni si sovrappongano alla query basata sulla tabella completa.

## <a name="see-also"></a>Vedere anche
 [Partizioni &#40;Analysis Services-Dati multidimensionali&#41;](../multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md) partizioni [Remote](../multidimensional-models-olap-logical-cube-objects/partitions-remote-partitions.md) [unire partizioni in Analysis Services &#40;SSAS-multidimensionale&#41;](merge-partitions-in-analysis-services-ssas-multidimensional.md)


