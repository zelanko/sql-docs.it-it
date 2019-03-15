---
title: Analizzare consolidati i report di valutazione Data Migration Assistant con Power BI (SQL Server) | Microsoft Docs
description: Informazioni su come usare Power BI per analizzare i report di valutazione della migrazione dei dati che è stato importato e consolidati in SQL Server
ms.custom: ''
ms.date: 03/12/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: HJToland3
ms.author: rajpo
manager: craigg
ms.openlocfilehash: 786e86fb6f0326e2f8ea568f4c069828ff1ff4c6
ms.sourcegitcommit: e9fcd10c7eb87a4f09ac2d8f7647018e83a5f5c5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/14/2019
ms.locfileid: "57974120"
---
# <a name="analyze-consolidated-assessment-reports-created-by-data-migration-assistant-with-power-bi"></a>Analizzare i report consolidati di valutazione creati dai Data Migration Assistant con Power BI

Questo articolo descrive come creare un report di Power BI per analizzare le valutazioni di migrazione consolidati.

Per informazioni su consolidare le valutazioni di migrazione create da Data Migration Assistant, vedere [consolidare i report di valutazione](../dma/dma-consolidatereports.md).

## <a name="sample-power-bi-reports"></a>Report di Power BI di esempio

È possibile scaricare esempi di report di Power BI per valutazioni consolidate migrazione da questa [repository Github](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/data-migration-assistant).

I report seguenti sono inclusi: 

- [Dashboard](#dashboard--details)

  Include un report drill-down e statistiche di snapshot.

- [Preparazione aggiornamenti in locale](#on-premises-upgrade-readiness--details)

  L'origine dati è la visualizzazione UpgradeSuccessRanking nel database DMAReporting.  Questo report mostra il corretto aggiornamento percentuale per i database valutati.

- [Parità delle funzionalità in locale](#on-premise-feature-parity--details)

  Illustra le funzionalità consigliate per la versione di SQL Server di destinazione.

- [Azure SQL DB preparazione aggiornamenti](#azure-sql-db-upgrade-readiness--details)

  L'origine dati è la visualizzazione UpgradeSuccessRanking nel database DMAReporting.  Questo report mostra il corretto aggiornamento percentuale per i database valutato per le migrazioni di database SQL di Azure.

- [Funzionalità di Azure SQL DB non supportati](#azure-sql-db-unsupported-features--details)

  Mostra le funzionalità dei database esistenti che non sono supportate in database SQL di Azure (V12).

È possibile modificare tali report da usare con l'ambiente, la modifica dell'origine dati in Power BI. 

1. Selezionare la freccia giù accanto a **modifica query**e selezionare **impostazioni origine dati**.

   ![Le query menu Modifica, impostazioni dell'origine dati](../dma/media/DataSourceSettings.png)

1. Selezionare **modificare l'origine...** e immettere i valori di server e database.

   ![Modificare l'origine, server e database](../dma/media/ChangeSource.png)

1. Selezionare **OK**, quindi selezionare **Chiudi**.

1. Aggiornare i report.

   ![Aggiornare i report di Power BI](../dma/media/RefreshReport.png)

### <a name="dashboard-report"></a>Report del dashboard

![Report del dashboard](../dma/media/DashboardReport.png)

Il dashboard Visualizza informazioni dettagliate su tutte le valutazioni. È possibile utilizzare i filtri dei dati sul lato sinistro per filtrare in base al database o istanza. È possibile utilizzare il grafico a barre per eseguire il drill-in categorie specifiche per vedere dove si trovano i problemi.

Per eseguire il drill-, selezionare il cerchio con freccia in giù nell'angolo superiore destro del grafico a barre.

![Drill-down categoria](../dma/media/CategoryDrillDown.png)

La sequenza di drill-down viene impostata come illustrato nell'immagine seguente (sotto **asse**). Per modificare la sequenza, trascinare le colonne nell'ordine desiderato.

![Visualizzazioni, asse del grafico a barre](../dma/media/VisualizationsAxis.png)

In questa vista diventa ancora più potente quando si filtra prima di tutto per un database specifico e quindi eseguire il drill down i problemi di categoria specifica. Nell'esempio seguente è selezionato, ad esempio il database delle risorse Umane **SQL01** per visualizzare tutti gli oggetti che impediscono le migrazioni (modifiche di rilievo).

![Modifiche di rilievo per database delle risorse Umane](../dma/media/BreakingChanges.png)

### <a name="on-premises-upgrade-readiness-report"></a>Report di conformità di aggiornamento in locale

![Report di conformità di aggiornamento in locale](../dma/media/OnPremisesUpgradeReadinessReport.png)

Questo report visualizza un'istantanea del livello di preparazione dei database devono eseguire la migrazione a una versione successiva di SQL Server. I dati in questo report provengono da dbo. UpgradeSuccessFactor\_OnPrem vista nel database DMAReporting.

Filtro di istanza e nome del database e usando le schede di punteggio nella parte superiore, è possibile vedere quale versione di database è stato possibile eseguire la migrazione troppo. Ad esempio, se Filtra per il database AdventureWorks 2012, si noterà che il database è pronto a passare a tutte le versioni di SQL Server elencate nel report. Ciò è determinato dal assicurando che non sono presenti modifiche di rilievo per quel database e livello di compatibilità.

![Fattore di successo aggiornamento per il database AdventureWorks](../dma/media/UpgradeSuccessFactor.png)

### <a name="on-premises-feature-parity-report"></a>Report di parità delle funzionalità in locale

![Report di parità delle funzionalità in locale](../dma/media/OnPremisesFeatureParityReport.png)

Usare questo report per evidenziare le nuove funzionalità che può essere utilizzata per il database nella versione di SQL Server di destinazione.

Quando si seleziona una funzionalità nel grafico a imbuto, i dati nella parte inferiore che evidenzia gli oggetti che sono interessati dalla funzionalità. Nell'esempio seguente, il **Stretch database per risparmiare spazio di archiviazione** funzionalità sia selezionata e una tabella viene indicata che possono trarre vantaggio da questa funzionalità.

![Consiglio di funzionalità per Stretch Database](../dma/media/FeatureRecommend_StretchDatabase.png)

### <a name="azure-sql-db-upgrade-readiness-report"></a>Report di preparazione aggiornamenti di Azure SQL DB

![Report di preparazione aggiornamenti di Azure SQL DB](../dma/media/AzureSQLDBUpgradeReadinessReport.png)

Questo report mostra la conformità del database per eseguire la migrazione al Database SQL di Azure V12. I dati da questo report provengono da dbo. UpgradeSuccessRanking vista nel database DMAReporting.

### <a name="azure-features-parity-report"></a>Report di parità di funzionalità di Azure

![Report di parità di funzionalità di Azure](../dma/media/AzureFeaturesParityReport.png)

Usare questo report per evidenziare le *le funzionalità a livello di istanza* che non sono supportate da Azure SQL Database V12.

Quando si seleziona una funzionalità nel grafico a imbuto, i dati nella parte inferiore sono elencate le istanze e funzionalità del database che non sono supportate. Nell'esempio seguente, viene selezionata questa funzionalità: **Sempre sulla disponibilità del gruppo configurazione non è supportata nel Database SQL di Azure**.  

![Sempre nella funzionalità gruppo di disponibilità](../dma/media/Feature_AlwaysOnAvailability.png)

 
### <a name="azure-sql-db-unsupported-features-report"></a>Report delle funzionalità non supportate di database SQL di Azure

![Report delle funzionalità non supportate di database SQL di Azure](../dma/media/AzureSQLDBUnsupportedFeaturesReport.png)

Questo report evidenzia le funzionalità che non sono supportate per un determinato **database** quando la destinazione è il Database SQL di Azure (V12).

Filtrando in base al valore di nome e la funzionalità di database nel grafico a imbuto, è possibile visualizzare i dettagli su funzionalità non supportata. I dettagli includono l'oggetto è interessato e consigli per risolvere il problema.

Ad esempio, il filtro per il database DTC e **non è possibile aggiornare i database di sola lettura**, è possibile visualizzare un elenco di oggetti che sono interessati.

![Database di sola lettura non possono essere aggiornati problema](../dma/media/ReadOnlyDatabases.png)

## <a name="see-also"></a>Vedere anche

[Panoramica di Data Migration Assistant](../dma/dma-overview.md)

[Data Migration Assistant di download](https://www.microsoft.com/download/details.aspx?id=53595)

[Download di Power BI](https://powerbi.microsoft.com/)
