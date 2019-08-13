---
title: Che cos'è SQL Server Machine Learning Services (Python e R)?
titleSuffix: ''
description: Machine Learning Services è una funzionalità di SQL Server che offre la possibilità di eseguire script Python e R con dati relazionali. È possibile usare i pacchetti e i framework open source e i pacchetti Microsoft Python e R per l'analisi predittiva e l'apprendimento automatico. Gli script vengono eseguiti nel database senza trasferire i dati all'esterno di SQL Server o in rete. Questo articolo illustra le nozioni di base di SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/07/2019
ms.topic: overview
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4a1a9a3b0f712458466051ce2c67c0a725ef0a76
ms.sourcegitcommit: 12b7e3447ca2154ec2782fddcf207b903f82c2c0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/12/2019
ms.locfileid: "68957434"
---
# <a name="what-is-sql-server-machine-learning-services-python-and-r"></a>Che cos'è SQL Server Machine Learning Services (Python e R)?
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Machine Learning Services è una funzionalità di SQL Server che offre la possibilità di eseguire script Python e R con dati relazionali. È possibile usare i pacchetti e i framework open source e i [pacchetti Microsoft Python e R](#packages) per l'analisi predittiva e l'apprendimento automatico. Gli script vengono eseguiti nel database senza trasferire i dati all'esterno di SQL Server o in rete. Questo articolo illustra le nozioni di base di SQL Server Machine Learning Services.

Nel database SQL di Azure [Machine Learning Services](https://docs.microsoft.com/azure/sql-database/sql-database-machine-learning-services-overview) è attualmente disponibile in anteprima pubblica.

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
> [!NOTE]
> Per l'esecuzione di Java in SQL Server, vedere la [documentazione sulle estensioni del linguaggio](../language-extensions/language-extensions-overview.md).
::: moniker-end

## <a name="what-is-machine-learning-services"></a>Che cos'è Machine Learning Services?

SQL Server Machine Learning Services consente di eseguire script Python e R nel database. È possibile usarlo per preparare e pulire i dati, eseguire la progettazione delle funzionalità e il training, la valutazione e la distribuzione di modelli di machine learning all'interno di un database. La funzionalità esegue gli script in cui risiedono i dati ed Elimina il trasferimento dei dati attraverso la rete a un altro server.

Le distribuzioni di base di Python e R sono incluse in Machine Learning Services. È possibile usare i pacchetti e i framework open source, ad esempio PyTorch, TensorFlow e Scikit-learn, oltre ai pacchetti Microsoft [revoscalepy](python/ref-py-revoscalepy.md) e [microsoftml](python/ref-py-microsoftml.md) per Python e [RevoScaleR](r/ref-r-revoscaler.md), [microsoftml](r/ref-r-microsoftml.md), [olapr ](r/ref-r-olapr.md)e [Sqlrutils](r/ref-r-sqlrutils.md) per R.

Machine Learning Services usa un Framework di estendibilità per eseguire gli script Python e R in SQL Server. Altre informazioni sul funzionamento:

+ [Framework di estendibilità](concepts/extensibility-framework.md)
+ [Estensione Python](concepts/extension-python.md)
+ [Estensione R](concepts/extension-r.md)

## <a name="what-can-i-do-with-machine-learning-services"></a>Che cosa è possibile fare con Machine Learning Services?

È possibile usare Machine Learning Services per compilare ed eseguire il training di modelli di apprendimento automatico e apprendimento avanzato all'interno SQL Server. È inoltre possibile distribuire modelli esistenti per Machine Learning Services e utilizzare dati relazionali per le stime.

Esempi del tipo di stime che è possibile utilizzare SQL Server Machine Learning Services per, tra cui:

|||
|-|-|
|Classificazione/categorizzazione|Suddivide automaticamente i commenti dei clienti in categorie positive e negative|
|Regressione/stima valori continui|Prevedere il prezzo delle case in base alle dimensioni e alla posizione|
|Rilevamento di anomalie|Rilevare transazioni bancarie fraudolente |
|Consigli|Suggerisci i prodotti che gli acquirenti online potrebbero voler acquistare, in base agli acquisti precedenti|

### <a name="how-to-execute-python-and-r-scripts"></a>Come eseguire gli script Python e R

Esistono due modi per eseguire gli script Python e R in Machine Learning Services:

+ Il modo più comune consiste nell'usare T-SQL stored procedure [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

+ È anche possibile usare il client Python o R preferito e scrivere script che effettuano il push dell'esecuzione (denominata *contesto di calcolo remoto*) a una SQL Server remota. Per altre informazioni, vedere come configurare un client data science per [lo sviluppo Python](python/setup-python-client-tools-sql.md) e [lo sviluppo R](r/set-up-a-data-science-client.md) .

<a name="packages"></a>

## <a name="python-and-r-packages"></a>Pacchetti Python e R

È possibile usare i pacchetti e i framework open source, oltre ai pacchetti aziendali Microsoft. I pacchetti R e Python open source più comuni sono pre-installati in Machine Learning Services. Sono inclusi anche i pacchetti Python e R seguenti di Microsoft:

| Linguaggio | Pacchetto | Descrizione |
|-|-|-|
| Python | [revoscalepy](python/ref-py-revoscalepy.md) | Pacchetto primario per Python scalabile. Trasformazioni e manipolazione di dati, riepilogo statistico, visualizzazione e molte forme di modellazione. Inoltre, le funzioni in questo pacchetto distribuiscono automaticamente i carichi di lavoro tra i core disponibili per l'elaborazione parallela. |
| Python | [microsoftml](python/ref-py-microsoftml.md) | Aggiunge algoritmi di machine learning per creare modelli personalizzati per l'analisi del testo, l'analisi delle immagini e l'analisi dei sentimenti. | 
| R | [RevoScaleR](r/ref-r-revoscaler.md) | Il pacchetto principale per le trasformazioni e le trasformazioni dei dati scalabili di R., il riepilogo statistico, la visualizzazione e molte forme di modellazione. Inoltre, le funzioni in questo pacchetto distribuiscono automaticamente i carichi di lavoro tra i core disponibili per l'elaborazione parallela. |
| R | [MicrosoftML (R)](r/ref-r-microsoftml.md) | Aggiunge algoritmi di machine learning per creare modelli personalizzati per l'analisi del testo, l'analisi delle immagini e l'analisi dei sentimenti. |
| R | [olapR](r/ref-r-olapr.md) | Funzioni R utilizzate per le query MDX su un cubo OLAP SQL Server Analysis Services. |
| R | [sqlrutils](r/ref-r-sqlrutils.md) | Un meccanismo per usare gli script R in una stored procedure T-SQL, registrare stored procedure con un database ed eseguire il stored procedure da un [ambiente di sviluppo r](r/set-up-a-data-science-client.md). |
| R | [Microsoft R Open](https://mran.microsoft.com/rro) | Microsoft R Open (riparazione) è la distribuzione avanzata di R da Microsoft. Si tratta di una piattaforma open source completa per l'analisi statistica e data science. Si basa su e 100% compatibile con R e include funzionalità aggiuntive per migliorare le prestazioni e la riproducibilità. |

## <a name="how-do-i-get-started-with-machine-learning-services"></a>Ricerca per categorie iniziare a usare Machine Learning Services?

1. [Installare SQL Server Machine Learning Services](install/sql-machine-learning-services-windows-install.md)

1. Configurare gli strumenti di sviluppo. È possibile usare:

    + [Azure Data Studio](../azure-data-studio/what-is.md) o [SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md) per usare T-SQL e il stored procedure [Sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) per eseguire lo script Python o R.
    + Python o R sul computer portatile o sulla workstation di sviluppo per l'esecuzione di script. È possibile estrarre i dati localmente o eseguire il push dell'esecuzione in modalità remota per SQL Server con [revoscalepy](python/ref-py-revoscalepy.md) e [RevoScaleR](r/ref-r-revoscaler.md). Per altre informazioni, vedere come configurare un client data science per [lo sviluppo Python](python/setup-python-client-tools-sql.md) e [lo sviluppo R](r/set-up-a-data-science-client.md) .

1. Scrivere il primo script Python o R

    + Avvio rapido: Eseguire uno script "Hello World" [in Python](tutorials/quickstart-python-run-using-t-sql.md) o [in R](tutorials/quickstart-r-run-using-tsql.md)
    + Avvio rapido: Creare un modello predittivo [in Python](tutorials/quickstart-python-train-score-in-tsql.md) o [in R](tutorials/quickstart-r-create-predictive-model.md)
    + Esercitazione: [Usare Python in T-SQL](tutorials/sqldev-in-database-python-for-sql-developers.md): Esplorazione dei dati, progettazione di funzionalità, training e distribuzione di modelli ed esecuzione di stime (serie in cinque parti)
    + Esercitazione: [Usare R in T-SQL](tutorials/sqldev-in-database-r-for-sql-developers.md): Esplorazione dei dati, progettazione di funzionalità, training e distribuzione di modelli ed esecuzione di stime (serie in cinque parti)
    + Esercitazione: [Usare Machine Learning Services in R Tools](tutorials/walkthrough-data-science-end-to-end-walkthrough.md): Esplora i dati, crea grafici e tracciati, Esegui la progettazione delle funzionalità, Esegui il training e Distribuisci modelli ed Esegui stime (serie in sei parti)

## <a name="next-steps"></a>Passaggi successivi

+ [Installare SQL Server Machine Learning Services](install/sql-machine-learning-services-windows-install.md)
+ Configurare un client di data science per lo sviluppo di [Python](python/setup-python-client-tools-sql.md) e [R](r/set-up-a-data-science-client.md)
