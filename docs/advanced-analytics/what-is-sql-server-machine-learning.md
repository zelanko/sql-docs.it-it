---
title: Che cos'è Machine Learning Services per SQL Server (Python e R)?
titleSuffix: ''
description: Machine Learning Services è una funzionalità di SQL Server che offre la possibilità di eseguire script Python e R con dati relazionali. È possibile usare pacchetti e framework open source, oltre ai pacchetti Python e R di Microsoft per l'analisi predittiva e le funzioni di Machine Learning. Gli script vengono eseguiti nel database senza trasferire i dati all'esterno di SQL Server o in rete. Questo articolo illustra le nozioni di base di Machine Learning Services per SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 02/06/2020
ms.topic: overview
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a94a3aea418a4c404b568fe6df7af701bc46de34
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79285905"
---
# <a name="what-is-sql-server-machine-learning-services-python-and-r"></a>Che cos'è Machine Learning Services per SQL Server (Python e R)?
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Machine Learning Services è una funzionalità di SQL Server che offre la possibilità di eseguire script Python e R con dati relazionali. È possibile usare pacchetti e framework open source, oltre ai [pacchetti Python e R di Microsoft](#packages) per l'analisi predittiva e le funzioni di Machine Learning. Gli script vengono eseguiti nel database senza trasferire i dati all'esterno di SQL Server o in rete. Questo articolo illustra le nozioni di base di Machine Learning Services per SQL Server.

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
> [!NOTE]
> Per l'esecuzione di Java in SQL Server, vedere la [documentazione sulle estensioni del linguaggio](../language-extensions/language-extensions-overview.md).
::: moniker-end

## <a name="what-is-machine-learning-services"></a>Che cos'è Machine Learning Services?

Machine Learning Services per SQL Server consente di eseguire script Python e R nel database. È possibile usare questa funzionalità per preparare e pulire i dati, eseguire la progettazione delle caratteristiche e il training, la valutazione e la distribuzione di modelli di Machine Learning all'interno di un database. La funzionalità esegue gli script nella posizione in cui i dati risiedono, eliminando la necessità di trasferire i dati in rete in un altro server.

Le distribuzioni di base di Python e R sono incluse in Machine Learning Services. È possibile installare e usare pacchetti e framework open source, come PyTorch, TensorFlow e scikit-learn, oltre ai pacchetti Microsoft [revoscalepy](python/ref-py-revoscalepy.md) e [microsoftml](python/ref-py-microsoftml.md) per Python e [RevoScaleR](r/ref-r-revoscaler.md), [MicrosoftML](r/ref-r-microsoftml.md), [olapR](r/ref-r-olapr.md) e [sqlrutils](r/ref-r-sqlrutils.md) per R.

Machine Learning Services usa un framework di estendibilità per eseguire gli script Python e R in SQL Server. Altre informazioni sono disponibili in:

+ [Framework di estendibilità](concepts/extensibility-framework.md)
+ [Estensione di Python](concepts/extension-python.md)
+ [Estensione di R](concepts/extension-r.md)

## <a name="what-can-i-do-with-machine-learning-services"></a>Che cosa è possibile fare con Machine Learning Services?

È possibile usare Machine Learning Services per creare ed eseguire il training di modelli di Machine Learning e Deep Learning all'interno di SQL Server. È inoltre possibile distribuire modelli esistenti in Machine Learning Services e usare dati relazionali per le stime.

Tra gli esempi del tipo di stime per cui è possibile usare Machine Learning Services per SQL Server rientrano:

|||
|-|-|
|Classificazione/categorizzazione|Suddivisione automatica dei commenti e dei suggerimenti degli utenti in categorie positive e negative|
|Regressione/stima di valori continui|Previsione del prezzo delle case in base alle dimensioni e alla posizione|
|Anomaly Detection|Rilevamento di transazioni bancarie fraudolente |
|Consigli|Suggerimento di prodotti che gli acquirenti online potrebbero voler acquistare, in base agli acquisti precedenti|

### <a name="how-to-execute-python-and-r-scripts"></a>Come eseguire gli script Python e R

Esistono due modi per eseguire gli script Python e R in Machine Learning Services:

+ Il modo più comune consiste nell'usare la stored procedure T-SQL [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

+ È anche possibile usare il client Python o R preferito e scrivere script che eseguono il push dell'esecuzione (denominata *contesto di calcolo remoto*) a un'istanza di SQL Server remota. Per altre informazioni, vedere come configurare un client di data science per lo [sviluppo in Python](python/setup-python-client-tools-sql.md) e lo [sviluppo in R](r/set-up-a-data-science-client.md).

<a name="versions"></a>

## <a name="python-and-r-versions"></a>Versioni di Python e R

La versione di Python e R inclusa in Machine Learning Services dipende dalla versione di SQL Server in uso. 

| Versione di SQL Server | Versione Python | Versione di R |
|-|-|-|
| SQL Server 2017 | 3.5.2 | 3.3.3 |
| SQL Server 2019 | 3.7.3 | 3.5.2 |

Per la versione di R in SQL Server 2016, vedere la sezione [Versione di R in Che cos'è R Services?](r/sql-server-r-services.md#version)

<a name="packages"></a>

## <a name="python-and-r-packages"></a>Pacchetti Python e R

È possibile usare pacchetti e framework open source, oltre ai pacchetti aziendali Microsoft. I pacchetti Python e R open source più comuni sono preinstallati in Machine Learning Services. Sono inclusi anche i pacchetti Python e R di Microsoft seguenti:

| Linguaggio | Pacchetto | Descrizione |
|-|-|-|
| Python | [revoscalepy](python/ref-py-revoscalepy.md) | Pacchetto principale per Python scalabile. Trasformazioni e manipolazione di dati, riepilogo statistico, visualizzazione e molte forme di modellazione. Inoltre, le funzioni di questo pacchetto distribuiscono automaticamente i carichi di lavoro tra i core disponibili per l'elaborazione parallela. |
| Python | [microsoftml](python/ref-py-microsoftml.md) | Aggiunge algoritmi di Machine Learning per creare modelli personalizzati per l'analisi del testo, l'analisi delle immagini e l'analisi del sentiment. | 
| R | [RevoScaleR](r/ref-r-revoscaler.md) | Pacchetto principale per R scalabile. Trasformazioni e manipolazione di dati, riepilogo statistico, visualizzazione e molte forme di modellazione. Inoltre, le funzioni di questo pacchetto distribuiscono automaticamente i carichi di lavoro tra i core disponibili per l'elaborazione parallela. |
| R | [MicrosoftML (R)](r/ref-r-microsoftml.md) | Aggiunge algoritmi di Machine Learning per creare modelli personalizzati per l'analisi del testo, l'analisi delle immagini e l'analisi del sentiment. |
| R | [olapR](r/ref-r-olapr.md) | Funzioni R usate per le query MDX su un cubo OLAP di SQL Server Analysis Services. |
| R | [sqlrutils](r/ref-r-sqlrutils.md) | Meccanismo per usare gli script R in una stored procedure T-SQL, registrare la stored procedure con un database ed eseguirla da un [ambiente di sviluppo R](r/set-up-a-data-science-client.md). |
| R | [Microsoft R Open](https://mran.microsoft.com/rro) | Microsoft R Open (MRO) è la distribuzione avanzata di R di Microsoft. Si tratta di una piattaforma open source completa per analisi statistica e data science. Basata su R e compatibile al 100% con questo linguaggio, include funzionalità aggiuntive per migliorare le prestazioni e la riproducibilità. |

Per altre informazioni sui pacchetti installati con Machine Learning Services e su come installare altri pacchetti, vedere:

+ [Ottenere informazioni sui pacchetti Python](package-management/python-package-information.md)
+ [Installare pacchetti Python con sqlmlutils](package-management/install-additional-python-packages-on-sql-server.md)
+ [Ottenere informazioni sui pacchetti R](package-management/r-package-information.md)
+ [Installare nuovi pacchetti R con sqlmlutils](package-management/install-additional-r-packages-on-sql-server.md)

## <a name="how-do-i-get-started-with-machine-learning-services"></a>Come iniziare a usare Machine Learning Services

1. [Installare Machine Learning Services per SQL Server](install/sql-machine-learning-services-windows-install.md)

1. Configurare gli strumenti di sviluppo. È possibile usare:

    + [Azure Data Studio](../azure-data-studio/what-is.md) o [SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md) per usare T-SQL e la stored procedure [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) per l'esecuzione dello script Python o R.
    + Python o R sulla workstation o il portatile di sviluppo per l'esecuzione degli script. È possibile eseguire il pull dei dati localmente o eseguire il push dell'esecuzione in modalità remota per SQL Server con [revoscalepy](python/ref-py-revoscalepy.md) e [RevoScaleR](r/ref-r-revoscaler.md). Per altre informazioni, vedere come configurare un client di data science per lo [sviluppo in Python](python/setup-python-client-tools-sql.md) e lo [sviluppo in R](r/set-up-a-data-science-client.md).

1. Scrivere il primo script Python o R

    + Guida introduttiva: [Eseguire script Python semplici](tutorials/quickstart-python-create-script.md)
    + Guida introduttiva: [Eseguire script R semplici](tutorials/quickstart-r-create-script.md)
    + Esercitazione: [Usare Python in T-SQL](tutorials/sqldev-in-database-python-for-sql-developers.md): esplorare dati, progettare caratteristiche, eseguire il training e la distribuzione di modelli ed eseguire stime (serie in cinque parti)
    + Esercitazione: [Usare R in T-SQL](tutorials/sqldev-in-database-r-for-sql-developers.md): esplorare dati, progettare caratteristiche, eseguire il training e la distribuzione di modelli ed eseguire stime (serie in cinque parti)

## <a name="next-steps"></a>Passaggi successivi

+ [Installare Machine Learning Services per SQL Server](install/sql-machine-learning-services-windows-install.md)
+ Configurare un client di data science per lo [sviluppo in Python](python/setup-python-client-tools-sql.md) e lo [sviluppo in R](r/set-up-a-data-science-client.md)
