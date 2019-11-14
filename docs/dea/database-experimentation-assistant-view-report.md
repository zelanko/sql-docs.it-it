---
title: Visualizzare i report di analisi per gli aggiornamenti di SQL Server
description: Visualizzare i report di analisi in Database Experimentation Assistant
ms.custom: seo-lt-2019
ms.date: 10/22/2018
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: ajaykar
ms.reviewer: mathoma
ms.openlocfilehash: fddc71bf7cdf7686154b4f9b5612cf671ca64fce
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056659"
---
# <a name="view-analysis-reports-in-database-experimentation-assistant"></a>Visualizzare i report di analisi in Database Experimentation Assistant

Dopo aver [creato il report di analisi](database-experimentation-assistant-create-report.md) in database EXPERIMENTATION Assistant (DEA), completare la procedura descritta in questo articolo per visualizzare il report e ottenere informazioni dettagliate sulle prestazioni fornite dal test a/B.

## <a name="select-a-server"></a>Selezionare un server

In DEA selezionare l'icona di menu. Nel menu espanso selezionare report di **analisi** accanto all'icona dell'elenco di controllo per aprire la finestra report di analisi.

In **report di analisi**immettere il nome di un computer che esegue SQL Server con un database di analisi. Selezionare **Connetti**. 

![Connettersi a un report esistente](./media/database-experimentation-assistant-view-report/dea-view-report-connect.png)

Se non sono presenti dipendenze, nella pagina dei **prerequisiti vengono richiesti** i collegamenti per installarli. Installare i prerequisiti, quindi selezionare **Riprova**.

![Pagina dei prerequisiti](./media/database-experimentation-assistant-view-report/dea-view-report-prereq.png)

## <a name="select-an-analysis-report-to-view"></a>Selezionare un report di analisi da visualizzare

Nell'elenco dei report di analisi, fare doppio clic su un report per aprirlo.

![Visualizza report esistente](./media/database-experimentation-assistant-view-report/dea-view-report-view-existing.png)

È possibile ottenere informazioni dettagliate sull'ottima rappresentazione del carico di lavoro, come illustrato in questo grafico di esempio:

![Grafici Rep del carico di lavoro](./media/database-experimentation-assistant-view-report/dea-view-report-workload-compare.png)

## <a name="view-and-understand-the-analysis-report"></a>Visualizzare e comprendere il report di analisi

In questa sezione viene illustrato il report di analisi.

### <a name="query-categories"></a>Categorie di query

Selezionare sezioni diverse del grafico a torta a sinistra per visualizzare solo le query che rientrano in tale categoria.

![Sezioni della torta del report](./media/database-experimentation-assistant-view-report/dea-view-report-pie-slices.png)

- **Query**ridotte: query con prestazioni migliori in a rispetto a B.  
- **Errori**: query che mostrano errori nell'istanza B ma non nell'istanza a.  
- **Query migliorate**: query con prestazioni migliori nell'istanza B rispetto all'istanza a.  
- **Query indeterminate**: query con una modifica indeterminata delle prestazioni.  
- **Stesso**: query in cui le prestazioni sono rimaste invariate tra le istanze a e B.

### <a name="individual-query-drill-down"></a>Drill-down per query singole

È possibile selezionare i collegamenti al modello di query per visualizzare informazioni più dettagliate su query specifiche.

![Drill-down query](./media/database-experimentation-assistant-view-report/dea-view-report-drilldown.png)

Selezionare una query specifica per aprire un riepilogo di confronto per la query.

![Riepilogo confronto](./media/database-experimentation-assistant-view-report/dea-view-report-comparison-summary.png)

È possibile visualizzare le istanze A e B su cui è stata eseguita la query. È anche possibile visualizzare un modello di come potrebbe apparire la query. Una tabella Visualizza informazioni sulle query specifiche per le istanze A e B.

### <a name="error-queries"></a>Query di errore

Il report di riepilogo confronto include le sezioni informazioni **sugli errori** espandibili e **informazioni sul piano di query** . Nelle sezioni vengono illustrati gli errori e le informazioni sul piano per entrambe le istanze.

Selezionare la torta di errore (rosso) per visualizzare questi tipi di errori:
- **Errori esistenti**: errori che si sono verificati in un oggetto.
- **Nuovi errori**: errori che si sono verificati in B.
- **Errori risolti**: errori che si sono verificati in, ma non in B.

![Grafici degli errori](./media/database-experimentation-assistant-view-report/dea-view-report-error-charts.png)

## <a name="next-steps"></a>Passaggi successivi

- Per informazioni su come generare un report di analisi da un prompt dei comandi, vedere [Run al prompt dei comandi](database-experimentation-assistant-run-command-prompt.md).

- Per un'introduzione di 19 minuti a DEA e dimostrazione, Guarda il video seguente:

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
