---
title: Visualizzare i report di analisi nel Database sperimentazione Assistant per gli aggiornamenti di SQL Server
description: Visualizzare i report di analisi nel Database sperimentazione Assistant
ms.custom: ''
ms.date: 10/22/2018
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: ajaykar
ms.reviewer: douglasl
manager: craigg
ms.openlocfilehash: 49758d367f5ec22ffe3893896ab607917f28bf31
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63274087"
---
# <a name="view-analysis-reports-in-database-experimentation-assistant"></a>Visualizzare i report di analisi nel Database sperimentazione Assistant

Dopo aver [creare i report di analisi](database-experimentation-assistant-create-report.md) nel Database sperimentazione Assistant DEA (), completare i passaggi descritti in questo articolo per visualizzare il report e ottenere informazioni dettagliate sulle prestazioni fornite dall'oggetto test a / B.

## <a name="select-a-server"></a>Selezionare un server

In DEA, selezionare l'icona di menu. Nel menu espanso, selezionare **report di analisi** accanto all'icona di elenco di controllo per aprire la finestra di report di analisi.

Sotto **report di analisi**, immettere il nome di un computer che esegue SQL Server che dispone di un database di analisi. Selezionare **Connetti**. 

![Connettersi a un report esistente](./media/database-experimentation-assistant-view-report/dea-view-report-connect.png)

Se sono necessari elementi eventuali dipendenze, il **prerequisiti** pagina richiede con collegamenti di installarli. Installare i prerequisiti e quindi selezionare **riprovare**.

![Pagina dei prerequisiti](./media/database-experimentation-assistant-view-report/dea-view-report-prereq.png)

## <a name="select-an-analysis-report-to-view"></a>Selezionare un report di analisi per visualizzare

Nell'elenco dei report di analisi, fare doppio clic su un report per aprirlo.

![Visualizzazione di report esistente](./media/database-experimentation-assistant-view-report/dea-view-report-view-existing.png)

È possibile ottenere informazioni dettagliate sulle prestazioni del carico di lavoro è rappresentato, come illustrato in questo grafico di esempio:

![Rep del carico di lavoro grafici](./media/database-experimentation-assistant-view-report/dea-view-report-workload-compare.png)

## <a name="view-and-understand-the-analysis-report"></a>Visualizzare e comprendere il report di analisi

In questa sezione illustra il report di analisi.

### <a name="query-categories"></a>Categorie delle query

Selezionare diverse sezioni del grafico a torta a sinistra per mostrare solo le query che rientrano in tale categoria.

![Sezioni della torta report](./media/database-experimentation-assistant-view-report/dea-view-report-pie-slices.png)

- **Riduzione query**: Query eseguita meglio in una classe a in B.  
- **Errori**: Query che mostrano gli errori nell'istanza B, ma non nell'istanza di r.  
- **Migliorate le query**: Query eseguite per una migliore nell'istanza B rispetto a quella nell'istanza di r.  
- **Le query Indeterminate**: Query con una modifica prestazioni indeterminato.  
- **Stesso**: Query in cui le prestazioni rimanessero invariati tra più istanze di A e B.

### <a name="individual-query-drill-down"></a>Singola query drill-down

È possibile selezionare i collegamenti del modello di query per visualizzare informazioni più dettagliate sulle query specifiche.

![Eseguire una query drill-down](./media/database-experimentation-assistant-view-report/dea-view-report-drilldown.png)

Selezionare una query specifica per aprire un confronto riepilogativo per la query.

![Riepilogo di confronto](./media/database-experimentation-assistant-view-report/dea-view-report-comparison-summary.png)

È possibile visualizzare le istanze di A e B che ha eseguita la query in. È anche possibile visualizzare un modello di ciò che potrebbe essere simile alla query. Una tabella visualizza le informazioni di query specifico alle istanze di A e B.

### <a name="error-queries"></a>Query di errore

Il report di riepilogo di confronto è espandibile **informazioni sull'errore** e **Query prevede informazioni** sezioni. Le sezioni mostrano gli errori e le informazioni per entrambe le istanze del piano.

Selezionare il grafico a torta errore (rosso) per visualizzare questi tipi di errori:
- **Gli errori esistenti**: Errori che erano in r.
- **Nuovi errori**: Errori che erano in B.
- **Gli errori risolti**: Errori che erano in oggetto ma non in B.

![Grafici di errore](./media/database-experimentation-assistant-view-report/dea-view-report-error-charts.png)

## <a name="next-steps"></a>Passaggi successivi

- Per informazioni su come generare un report di analisi in un prompt dei comandi, vedere [prompt dei comandi eseguire](database-experimentation-assistant-run-command-prompt.md).

- Per un'introduzione di 19 minuti DEA e dimostrazione, guardare il video seguente:

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
