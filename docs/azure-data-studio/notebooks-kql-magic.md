---
title: Notebook con KQL (Kusto Query Language) magic in Azure Data Studio
description: Questa esercitazione illustra come è possibile creare ed eseguire Kqlmagic in Azure Data Studio.
author: markingmyname
ms.author: maghan
ms.reviewer: jukoesma
ms.topic: conceptual
ms.prod: sql
ms.technology: azure-data-studio
ms.custom: ''
ms.date: 04/27/2020
ms.openlocfilehash: a3c4af3166d7c227af1846114321228af9ce7753
ms.sourcegitcommit: 69f93dd1afc0df76c3b4d9203adae0ad7dbd7bb2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/30/2020
ms.locfileid: "82598727"
---
# <a name="kqlmagic-extension-in-azure-data-studio"></a>Estensione Kqlmagic in Azure Data Studio

**Kqlmagic** è un comando che estende le funzionalità del kernel Python in **[notebook di Azure Data Studio](notebooks-guidance.md)** . È possibile combinare Python e il **[linguaggio di query Kusto (KQL)](https://docs.microsoft.com/azure/data-explorer/kusto/query)** per eseguire query e visualizzare i dati tramite la libreria avanzata Plot.ly integrata con i comandi `render`. Kqlmagic riunisce i vantaggi di notebook, analisi dei dati e funzionalità avanzate di Python nella stessa posizione. Le origini dati supportate con Kqlmagic includono **[Esplora dati di Azure](https://docs.microsoft.com/azure/data-explorer/data-explorer-overview)** , **[Application Insights](https://docs.microsoft.com/azure/azure-monitor/app/app-insights-overview)** e i **[log di Monitoraggio di Azure](https://docs.microsoft.com/azure/azure-monitor/platform/data-platform-logs)** .

Questo articolo illustra come creare ed eseguire un notebook in Azure Data Studio usando l'estensione Kqlmagic per un cluster di Esplora dati di Azure, un log di Application Insights e i log di Monitoraggio di Azure.

## <a name="prerequisites"></a>Prerequisiti

- [Azure Data Studio](download-azure-data-studio.md)
- [Python](https://www.python.org/downloads/)

## <a name="install-and-set-up-kqlmagic-in-a-notebook"></a>Installare e configurare Kqlmagic in un notebook

I passaggi descritti in questa sezione vengono tutti eseguiti in un notebook di Azure Data Studio.

1. Creare un nuovo notebook e impostare **Kernel** su *Python 3*.

   ![Nuovo notebook](media/notebooks-kql-magic/install-new-notebook.png)

2. Quando viene richiesto, selezionare **Sì** per aggiornare i pacchetti Python.

   ![Sì](media/notebooks-kql-magic/install-python-yes.png)

3. Installare Kqlmagic:

   ```python
   !pip install Kqlmagic --no-cache-dir --upgrade
   ```

   Verificare che sia installato:

   ```python
   !pip list
   ```

   ![Elenco](media/notebooks-kql-magic/install-list.png)

4. Caricare Kqlmagic:

   ```python
   %reload_ext Kqlmagic
   ```

   > [!Note]
   > Se questo passaggio ha esito negativo, chiudere il file e riaprirlo.

   ![Caricare l'estensione Kqlmagic](media/notebooks-kql-magic/install-load-kql-magic-ext.png)

5. È possibile verificare se Kqlmagic è stato caricato correttamente visualizzando la documentazione della Guida o controllando la versione.

   ```python
   %kql --help "help"
   ```

   > [!Note]
   > Se `Samples@help` richiede una password, è possibile lasciarla vuota e premere **INVIO**.

   ![Guida](media/notebooks-kql-magic/install-help.png)

   Per individuare la versione di Kqlmagic installata, eseguire il comando seguente.

   ```python
   %kql --version
   ```

## <a name="kqlmagic-with-an-azure-data-explorer-cluster"></a>Kqlmagic con un cluster di Esplora dati di Azure

Questa sezione illustra come eseguire un'analisi dei dati usando Kqlmagic con un cluster di Esplora dati di Azure.

### <a name="load-and-authenticate-kqlmagic-for-azure-data-explorer"></a><a name="ade-load-auth"></a> Caricare e autenticare Kqlmagic per Esplora dati di Azure

   > [!Note]
   > Ogni volta che si crea un nuovo notebook in Azure Data Studio è necessario caricare l'estensione Kqlmagic.

1. Verificare che **Kernel** sia impostato su *Python3*.

   ![Nuovo notebook](media/notebooks-kql-magic/change-kernel.png)

2. Caricare Kqlmagic:

   ```python
   %reload_ext Kqlmagic
   ```

   ![Caricare l'estensione Kqlmagic](media/notebooks-kql-magic/install-load-kql-magic-ext.png)

3. Connettersi al cluster ed eseguire l'autenticazione:

   ```python
   %kql azureDataExplorer://code;cluster='help';database='Samples'
   ```

   Usare l'account di accesso del dispositivo per l'autenticazione. Copiare il codice dall'output e selezionare **authenticate** per aprire un browser in cui è necessario incollare il codice. Una volta eseguita l'autenticazione, è possibile tornare ad Azure Data Studio per continuare con il resto dello script.

   ![Autenticazione in Esplora dati di Azure](media/notebooks-kql-magic/ade-auth.png)

### <a name="query-and-visualize-for-azure-data-explorer"></a>Eseguire query e visualizzare dati per Esplora dati di Azure

Eseguire la query dei dati usando l'[operatore di rendering](https://docs.microsoft.com/azure/data-explorer/kusto/query/renderoperator) e visualizzare i dati tramite la libreria ploy.ly. La query e la visualizzazione forniscono un'esperienza integrata che fa uso di KQL (linguaggio di query Kusto) nativo.

1. Analizzare i primi 10 eventi tempesta (StormEvents) per stato e frequenza:

   ```python
   %kql StormEvents | summarize count() by State | sort by count_ | limit 10
   ```

   Se si ha familiarità con il linguaggio di query Kusto (KQL), è possibile digitare la query dopo `%kql`.

   ![Analizzare gli eventi tempesta](media/notebooks-kql-magic/ade-analyze-storm-events.png)

2. Visualizzare un grafico della sequenza temporale:

   ```python
   %kql StormEvents \
   | summarize event_count=count() by bin(StartTime, 1d) \
   | render timechart title= 'Daily Storm Events'
   ```

   ![Visualizzare un diagramma temporale](media/notebooks-kql-magic/ade-visualize-timechart.png)

3. Esempio di query su più righe con `%%kql`.

   ```python
   %%kql
   StormEvents
   | summarize count() by State
   | sort by count_
   | limit 10
   | render columnchart title='Top 10 States by Storm Event count'
   ```

   ![Esempio di query su più righe](media/notebooks-kql-magic/ade-multiline-query-sample.png)

## <a name="kqlmagic-with-application-insights"></a>Kqlmagic con Application Insights

### <a name="load-and-authenticate-kqlmagic-for-application-insights"></a><a name="appin-load-auth"></a> Caricare e autenticare Kqlmagic per Application Insights

1. Verificare che **Kernel** sia impostato su *Python3*.

   ![Nuovo notebook](media/notebooks-kql-magic/change-kernel.png)

2. Caricare Kqlmagic:

   ```python
   %reload_ext Kqlmagic
   ```

   ![Caricare l'estensione Kqlmagic](media/notebooks-kql-magic/install-load-kql-magic-ext.png)

   > [!Note]
   > Ogni volta che si crea un nuovo notebook in Azure Data Studio è necessario caricare l'estensione Kqlmagic.

3. Connettersi ed eseguire l'autenticazione

   ```python
   %kql appinsights://appid='DEMO_APP';appkey='DEMO_KEY'
   ```

### <a name="query-and-visualize-for-application-insights"></a>Eseguire query e visualizzare dati per Application Insights

Eseguire la query dei dati usando l'[operatore di rendering](https://docs.microsoft.com/azure/data-explorer/kusto/query/renderoperator) e visualizzare i dati tramite la libreria ploy.ly. La query e la visualizzazione forniscono un'esperienza integrata che fa uso di KQL (linguaggio di query Kusto) nativo.

1. Mostrare le visualizzazioni pagina:

   ```python
   %%kql
   pageViews
   | limit 10
   ```

   ![Visualizzazioni pagina](media/notebooks-kql-magic/appin-page-views.png)

   > [!Note]
   > Usare il mouse per trascinare su un'area del grafico per eseguire lo zoom avanti fino alla data o alle date specifiche.

2. Mostrare le visualizzazioni pagina in un grafico con sequenza temporale:

   ```python
   %%kql
   pageViews
   | summarize event_count=count() by name, bin(timestamp, 1d)
   | render timechart title= 'Daily Page Views'
   ```

   ![Grafico con sequenza temporale](media/notebooks-kql-magic/appin-timechart.png)

## <a name="kqlmagic-with-azure-monitor-logs"></a>Kqlmagic con i log di Monitoraggio di Azure

### <a name="load-and-authenticate-kqlmagic-for-azure-monitor-logs"></a><a name="aml-load-auth"></a> Caricare e autenticare Kqlmagic per i log di Monitoraggio di Azure

1. Verificare che **Kernel** sia impostato su *Python3*.

   ![Nuovo notebook](media/notebooks-kql-magic/change-kernel.png)

2. Caricare Kqlmagic:

   ```python
   %reload_ext Kqlmagic
   ```

   ![Caricare l'estensione Kqlmagic](media/notebooks-kql-magic/install-load-kql-magic-ext.png)

   > [!Note]
   > Ogni volta che si crea un nuovo notebook in Azure Data Studio è necessario caricare l'estensione Kqlmagic.

3. Connettersi ed eseguire l'autenticazione:

   ```python
   %kql loganalytics://workspace='DEMO_WORKSPACE';appkey='DEMO_KEY';alias='myworkspace'
   ```

   ![Autenticazione di Log Analytics](media/notebooks-kql-magic/aml-auth.png)

### <a name="query-and-visualize-for-azure-monitor-logs"></a>Eseguire query e visualizzare dati per i log di Monitoraggio di Azure

Eseguire la query dei dati usando l'[operatore di rendering](https://docs.microsoft.com/azure/data-explorer/kusto/query/renderoperator) e visualizzare i dati tramite la libreria ploy.ly. La query e la visualizzazione forniscono un'esperienza integrata che fa uso di KQL (linguaggio di query Kusto) nativo.

1. Visualizzare un grafico con sequenza temporale:

   ```python
   %%kql
   KubeNodeInventory
   | summarize event_count=count() by Status, bin(TimeGenerated, 1d)
   | render timechart title= 'Daily Kubernetes Nodes'
   ```

   ![Diagramma temporale dei nodi Kubernetes giornalieri di Log Analytics](media/notebooks-kql-magic/aml-timechart-daily-kubernetes-nodes.png)

## <a name="next-steps"></a>Passaggi successivi

Altre informazioni sui notebook e Kqlmagic:

- [Usare Jupyter Notebook e l'estensione Kqlmagic per analizzare i dati in Esplora dati di Azure](https://docs.microsoft.com/azure/data-explorer/Kqlmagic)
- [Extension (Magic) to Jupyter notebook and Jupyter lab, that enable notebook experience working with Kusto, Application Insights, and LogAnalytics data](https://github.com/Microsoft/jupyter-Kqlmagic) (Estensione Magic per notebook di Jupyter e lab Jupyter che abilitano l'esperienza dei notebook usando dati Kusto, Application Insights e Log Analytics)
- [Kqlmagic](https://pypi.org/project/Kqlmagic/)
- [KustoMagicSamples](https://notebooks.azure.com/RknDzgn/projects/KustoMagicSamples/html/Getting%20Started%20with%20Kqlmagic%20on%20Azure%20Data%20Explorer-Copy.ipynb)
- [Come usare i notebook](notebooks-guidance.md)
- [Come gestire i notebook in Azure Data Studio](notebooks-manage-sql-server.md)
