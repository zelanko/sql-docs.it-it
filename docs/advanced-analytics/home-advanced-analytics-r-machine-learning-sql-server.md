---
title: R e Python documentazione di machine learning - SQL Server Machine Learning Services
description: R e Python in SQL Server, con algoritmi incorporati di modellazione Data science e machine learning per l'analisi dati su larga scala di livello enterprise.
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/22/2019
ms.topic: overview
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: e93d9ad5fd6415b6d8c1b6208857e81d60de2bd0
ms.sourcegitcommit: be09f0f3708f2e8eb9f6f44e632162709b4daff6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/21/2019
ms.locfileid: "65994123"
---
# <a name="sql-server-machine-learning-services"></a>SQL Server Machine Learning Services

## <a name="sql-server-machine-learning-services-r-and-python-documentation"></a>SQL Server documentazione di Machine Learning Services (R e Python)

Informazioni su come usare le librerie esterne e i linguaggi R e Python su dati relazionali residenti: guide introduttive, esercitazioni e procedure dettagliate. Le librerie R e Python in [SQL Server Machine Learning](what-is-sql-server-machine-learning.md) includono distribuzioni di base, modelli di analisi scientifica dei dati, algoritmi di Machine Learning e funzioni per l'esecuzione di analisi ad alte prestazioni su larga scala, senza richiedere il trasferimento di dati in rete.

::: moniker range="=sql-server-ver15||=sqlallproducts-allversions"
> [!NOTE]
> Per la documentazione di Java, vedere la [documentazione di SQL Server le estensioni del linguaggio](https://docs.microsoft.com/sql/language-extensions/language-extensions-overview).
::: moniker-end

|   |   |
|---|:--|
| ![Logo di R](media/index/logo_r.png) | R open source con [RevoScaleR](/machine-learning-server/r-reference/revoscaler/revoscaler) e gli algoritmi di Microsoft AI in [MicrosoftML](/machine-learning-server/r-reference/microsoftml/microsoftml-package). Queste librerie offrono modelli di previsioni e stime, analisi statistiche, visualizzazione e gestione dei dati su larga scala.<br/>L'integrazione di R inizia in [SQL Server 2016](install/sql-r-services-windows-install.md) ed è anche disponibile in [SQL Server 2017](install/sql-machine-learning-services-windows-install.md). |
| ![Logo di Python](media/index/logo_python.png) | Gli sviluppatori Python possono usare le librerie Microsoft [revoscalepy](/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) e [microsoftml](/machine-learning-server/python-reference/microsoftml/microsoftml-package) per l'analisi predittiva e il machine learning su larga scala. La distribuzione di base è costituita da librerie compatibili con Anaconda e Python 3.5.<br/>L'integrazione con Python inizia in [SQL Server 2017](install/sql-machine-learning-services-windows-install.md). |
| &nbsp; | &nbsp; |

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
