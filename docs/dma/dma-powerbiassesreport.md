---
title: Analizzare i report di valutazione consolidati con Power BI
titleSuffix: Data Migration Assistant
description: Informazioni su come usare Power BI per analizzare i report di valutazione della migrazione dei dati importati e consolidati in SQL Server
ms.custom: seo-lt-2019
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
ms.openlocfilehash: f2385914fc97fa8e118d871ddac6e0cdc9d49247
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056501"
---
# <a name="analyze-consolidated-assessment-reports-created-by-data-migration-assistant-with-power-bi"></a>Analizzare i report di valutazione consolidati creati da Data Migration Assistant con Power BI

Questo articolo descrive come creare un report Power BI per analizzare le valutazioni della migrazione consolidate.

Per informazioni sul consolidamento delle valutazioni della migrazione create dal Data Migration Assistant, vedere [consolidate Assessment Reports](../dma/dma-consolidatereports.md).

## <a name="sample-power-bi-reports"></a>Report Power BI di esempio

È possibile scaricare esempi di report di Power BI per le valutazioni della migrazione consolidate da questo [repository GitHub](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/data-migration-assistant).

Sono inclusi i report seguenti: 

- [Dashboard](#dashboard-report)

  Include le statistiche snapshot e un report drill-down.

- [Preparazione dell'aggiornamento locale](#on-premises-upgrade-readiness-report)

  L'origine dati è la vista UpgradeSuccessRanking nel database DMAReporting.  Questo report Mostra la percentuale di esito positivo dell'aggiornamento per i database valutati.

- [Parità di funzionalità locale](#on-premises-feature-parity-report)

  Mostra i suggerimenti sulle funzionalità per la versione SQL Server di destinazione.

- [Preparazione aggiornamenti del database SQL di Azure](#azure-sql-db-upgrade-readiness-report)

  L'origine dati è la vista UpgradeSuccessRanking nel database DMAReporting.  Questo report Mostra la percentuale di esito positivo dell'aggiornamento per i database valutati per le migrazioni del database SQL di Azure.

- [Funzionalità non supportate del database SQL di Azure](#azure-sql-db-unsupported-features-report)

  Mostra le funzionalità nei database esistenti che non sono supportate nel database SQL di Azure (V12).

È possibile modificare questi report in modo che funzionino con l'ambiente modificando l'origine dati in Power BI. 

1. Selezionare la freccia rivolta verso il basso accanto a **modifica query**e selezionare **Impostazioni origine dati**.

   ![Menu Modifica query, impostazioni origine dati](../dma/media/DataSourceSettings.png)

1. Selezionare **Modifica origine...** , quindi immettere i valori del server e del database.

   ![Modifica origine, server e database](../dma/media/ChangeSource.png)

1. Selezionare **OK**, quindi fare clic su **Chiudi**.

1. Aggiornare i report.

   ![Aggiorna Power BI report](../dma/media/RefreshReport.png)

### <a name="dashboard-report"></a>Report Dashboard

![Report Dashboard](../dma/media/DashboardReport.png)

Il dashboard Mostra i dettagli relativi a tutte le valutazioni. È possibile utilizzare i filtri dei dati sul lato sinistro per filtrare in base all'istanza o al database. È possibile utilizzare il grafico a barre per eseguire il drill-down in categorie specifiche per vedere dove si verificano i problemi.

Per eseguire il drill-down, selezionare il cerchio con la freccia in giù nell'angolo superiore destro del grafico a barre.

![Drill-down categoria](../dma/media/CategoryDrillDown.png)

La sequenza di drill-down è impostata come illustrato nell'immagine seguente (in **asse**). Per modificare la sequenza, trascinare le colonne nell'ordine desiderato.

![Visualizzazioni, asse del grafico a barre](../dma/media/VisualizationsAxis.png)

Questa visualizzazione diventa ancora più potente quando si filtra per la prima volta in base a un database specifico e quindi si esegue il drill-down per individuare i problemi di categoria specifici. Nell'esempio seguente, il database HR è selezionato per l'istanza **SQL01** per visualizzare tutti gli oggetti che impediscono le migrazioni (modifiche di rilievo).

![Modifiche di rilievo per il database HR](../dma/media/BreakingChanges.png)

### <a name="on-premises-upgrade-readiness-report"></a>Report sulla conformità dell'aggiornamento locale

![Report sulla conformità dell'aggiornamento locale](../dma/media/OnPremisesUpgradeReadinessReport.png)

Questo report Mostra uno snapshot del modo in cui è possibile eseguire la migrazione dei database a una versione successiva di SQL Server. I dati in questo report provengono da dbo. UpgradeSuccessFactor\_vista locale nel database di DMAReporting.

Filtrando in base all'istanza e al nome del database e usando la scheda Score nella parte superiore, è possibile visualizzare la versione di cui è possibile eseguire la migrazione del database. Se, ad esempio, si filtra in base al database AdventureWorks 2012, è possibile osservare che il database è pronto per lo spostamento in tutte le versioni SQL Server elencate nel report. Questa operazione viene determinata verificando che non siano presenti modifiche di rilievo per il database e il livello di compatibilità.

![Aggiornamento del fattore di riuscita per il database AdventureWorks](../dma/media/UpgradeSuccessFactor.png)

### <a name="on-premises-feature-parity-report"></a>Report di parità delle funzionalità locali

![Report di parità delle funzionalità locali](../dma/media/OnPremisesFeatureParityReport.png)

Utilizzare questo report per evidenziare nuove funzionalità che possono essere utilizzate per il database nella versione di SQL Server di destinazione.

Quando si seleziona una funzionalità nel grafico a imbuto, i dati nella parte inferiore evidenziano gli oggetti interessati dalla funzionalità. Nell'esempio seguente viene selezionata la funzionalità **Stretch database per l'archiviazione di risparmio** e viene elencata una tabella che può trarre vantaggio da questa funzionalità.

![Raccomandazione per le funzionalità per Stretch Database](../dma/media/FeatureRecommend_StretchDatabase.png)

### <a name="azure-sql-db-upgrade-readiness-report"></a>Report conformità aggiornamenti database SQL di Azure

![Report conformità aggiornamenti database SQL di Azure](../dma/media/AzureSQLDBUpgradeReadinessReport.png)

Questo report Mostra la preparazione del database per eseguire la migrazione alla versione 12 del database SQL di Azure. I dati di questo report provengono da dbo. Visualizzazione UpgradeSuccessRanking nel database DMAReporting.

### <a name="azure-features-parity-report"></a>Report di parità delle funzionalità di Azure

![Report di parità delle funzionalità di Azure](../dma/media/AzureFeaturesParityReport.png)

Usare questo report per evidenziare le *funzionalità a livello di istanza* che non sono supportate dal database SQL V12 di Azure.

Quando si seleziona una funzionalità nel grafico a imbuto, i dati nella parte inferiore elencano le istanze e le funzionalità del database che non sono supportate. Nell'esempio seguente questa funzionalità è selezionata: la **configurazione del gruppo di disponibilità always on non è supportata nel database SQL di Azure**.  

![Funzionalità del gruppo di disponibilità always on](../dma/media/Feature_AlwaysOnAvailability.png)

 
### <a name="azure-sql-db-unsupported-features-report"></a>Report funzionalità non supportate del database SQL di Azure

![Report funzionalità non supportate del database SQL di Azure](../dma/media/AzureSQLDBUnsupportedFeaturesReport.png)

Questo report evidenzia le funzionalità non supportate per un determinato **database** quando la destinazione è il database SQL di Azure (V12).

Filtrando in base al nome del database e al valore della funzionalità nel grafico a imbuto, è possibile visualizzare i dettagli sulla funzionalità non supportata. I dettagli includono l'oggetto interessato e i consigli per risolvere il problema.

Ad esempio, il filtro in base al database DTC e ai **database di sola lettura non può essere aggiornato**, è possibile visualizzare un elenco di oggetti interessati.

![Non è possibile aggiornare i database di sola lettura](../dma/media/ReadOnlyDatabases.png)

## <a name="see-also"></a>Vedere anche

[Panoramica di Data Migration Assistant](../dma/dma-overview.md)

[Download Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595)

[Download Power BI](https://powerbi.microsoft.com/)
