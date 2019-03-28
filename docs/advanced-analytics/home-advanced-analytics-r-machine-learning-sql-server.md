---
title: Documentazione delle estensioni di Machine Learning e programmazione di R e Python - Machine Learning SQL Server
description: R e Python in SQL Server, con algoritmi incorporati di modellazione Data science e machine learning per l'analisi dati su larga scala di livello enterprise.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/10/2019
ms.topic: overview
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 20acdf2789158bf067319930a5be65770eae67f3
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58512228"
---
# <a name="sql-server-machine-learning"></a>SQL Server Machine Learning

::: moniker range="=sql-server-ver15||=sqlallproducts-allversions"

## <a name="sql-server-machine-learning-and-programming-extensions-documentation"></a>Documentazione delle estensioni di Machine Learning e programmazione di SQL Server

Informazioni su come usare le librerie esterne e i linguaggi R e Python su dati relazionali residenti: guide introduttive, esercitazioni e procedure dettagliate. Le librerie R e Python in [SQL Server Machine Learning](what-is-sql-server-machine-learning.md) includono distribuzioni di base, modelli di analisi scientifica dei dati, algoritmi di Machine Learning e funzioni per l'esecuzione di analisi ad alte prestazioni su larga scala, senza richiedere il trasferimento di dati in rete.

In SQL Server 2019 l'esecuzione di codice Java usa lo stesso framework di estendibilità di R e Python, ma non include le librerie di funzioni di Machine Learning e analisi scientifica dei dati. Per altre informazioni sulle nuove funzionalità, vedere [Novità di SQL Server Machine Learning Services](what-s-new-in-sql-server-machine-learning-services.md).

|   |   |
|---|:--|
| ![Logo di R](media/index/logo_r.png) | R open source con [RevoScaleR](/machine-learning-server/r-reference/revoscaler/revoscaler) e gli algoritmi di Microsoft AI in [MicrosoftML](/machine-learning-server/r-reference/microsoftml/microsoftml-package). Queste librerie offrono modelli di previsioni e stime, analisi statistiche, visualizzazione e gestione dei dati su larga scala.<br/>L'integrazione di R inizia in [SQL Server 2016](install/sql-r-services-windows-install.md) ed è anche disponibile in [SQL Server 2017](install/sql-machine-learning-services-windows-install.md). |
| ![Logo di Python](media/index/logo_python.png) | Gli sviluppatori Python possono usare le librerie Microsoft [revoscalepy](/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) e [microsoftml](/machine-learning-server/python-reference/microsoftml/microsoftml-package) per l'analisi predittiva e il machine learning su larga scala. La distribuzione di base è costituita da librerie compatibili con Anaconda e Python 3.5.<br/>L'integrazione con Python inizia in [SQL Server 2017](install/sql-machine-learning-services-windows-install.md). |
| ![Logo di Java](media/index/logo_java.png) | Gli sviluppatori Java possono usare l'[estensione del linguaggio Java](java/extension-java.md) per racchiudere codice in stored procedure o in un formato binario accessibile tramite Transact-SQL.<br/>L'integrazione di Java inizia in [SQL Server 2019 - Anteprima](install/sql-machine-learning-services-ver15.md). |
| &nbsp; | &nbsp; |
::: moniker-end

::: moniker range="=sql-server-2016||=sql-server-2017"

## <a name="sql-server-machine-learning-r-and-python-documentation"></a>Documentazione di Python e R per SQL Server Machine Learning

Informazioni su come usare le librerie esterne e i linguaggi R e Python su dati relazionali residenti: guide introduttive, esercitazioni e procedure dettagliate. Le librerie R e Python in [SQL Server Machine Learning](what-is-sql-server-machine-learning.md) includono distribuzioni di base, modelli di analisi scientifica dei dati, algoritmi di Machine Learning e funzioni per l'esecuzione di analisi ad alte prestazioni su larga scala, senza richiedere il trasferimento di dati in rete.

|   |   |
|---|:--|
| ![Logo di R](media/index/logo_r.png) | R open source con [RevoScaleR](/machine-learning-server/r-reference/revoscaler/revoscaler) e gli algoritmi di Microsoft AI in [MicrosoftML](/machine-learning-server/r-reference/microsoftml/microsoftml-package). Queste librerie offrono modelli di previsioni e stime, analisi statistiche, visualizzazione e gestione dei dati su larga scala.<br/>L'integrazione di R inizia in [SQL Server 2016](install/sql-r-services-windows-install.md) ed è anche disponibile in [SQL Server 2017](install/sql-machine-learning-services-windows-install.md). |
| ![Logo di Python](media/index/logo_python.png) | Gli sviluppatori Python possono usare le librerie Microsoft [revoscalepy](/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) e [microsoftml](/machine-learning-server/python-reference/microsoftml/microsoftml-package) per l'analisi predittiva e il machine learning su larga scala. La distribuzione di base è costituita da librerie compatibili con Anaconda e Python 3.5.<br/>L'integrazione con Python inizia in [SQL Server 2017](install/sql-machine-learning-services-windows-install.md). |
| &nbsp; | &nbsp; |
::: moniker-end

## <a name="5-minute-quickstarts"></a>Guide introduttive di 5 minuti

- [Creare un modello predittivo in R](tutorials/rtsql-create-a-predictive-model-r.md)

- [Eseguire la stima e il tracciato da un modello con R](tutorials/rtsql-predict-and-plot-from-model.md)

## <a name="step-by-step-tutorials"></a>Esercitazioni dettagliate

- [Come aggiungere Machine Learning e il framework di estendibilità a SQL Server](install/sql-machine-learning-services-windows-install.md)

- [Come eseguire R da T-SQL e stored procedure](tutorials/sqldev-in-database-r-for-sql-developers.md)

- [Come usare l'analisi incorporata in Python](tutorials/sqldev-in-database-python-for-sql-developers.md)

## <a name="video-introduction"></a>Introduzione video

> [!VIDEO https://www.youtube.com/embed/ACejZ9optCQ]

## <a name="reference"></a>Riferimenti

| Pacchetto | Linguaggio | Descrizione |
|:--------|:---------|:------------|
| [RevoScaleR](/machine-learning-server/r-reference/revoscaler/revoscaler) | R | Elaborazione distribuita e parallela per le attività R: trasformazione dei dati, esplorazione, visualizzazione e analisi statistiche e predittive. |
| [MicrosoftML](/machine-learning-server/r-reference/microsoftml/microsoftml-package) | R | Funzioni basate su algoritmi di Microsoft AI, adattate per R. |
| [olapR](/machine-learning-server/r-reference/olapr/olapr) | R | Importa dati dai cubi OLAP |
| [sqlRUtils](/machine-learning-server/r-reference/sqlrutils/sqlrutils) | R | Funzioni di supporto per l'incapsulamento di R e T-SQL. |
[revoscalepy](/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | Python | Elaborazione distribuita e parallela per le attività Python: trasformazione dei dati, esplorazione, visualizzazione e analisi statistiche e predittive. |
| [microsoftml](/machine-learning-server/python-reference/microsoftml/microsoftml-package) | Python | Funzioni basate su algoritmi Microsoft AI, adattate per Python. |
| &nbsp; | &nbsp; | &nbsp; |
