---
title: Che cos'è SQL Server 2016 R Services?
titleSuffix: ''
description: R Services è una funzionalità di SQL Server 2016 che offre la possibilità di eseguire script R con dati relazionali. È possibile usare i pacchetti e i framework open source e i pacchetti Microsoft R per l'analisi predittiva e l'apprendimento automatico. Gli script vengono eseguiti nel database senza trasferire i dati all'esterno di SQL Server o in rete. Questo articolo illustra le nozioni di base di R Services per SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/12/2019
ms.topic: overview
author: dphansen
ms.author: davidph
monikerRange: =sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 99aba9748e7ee6d53aabb18919324243740d996a
ms.sourcegitcommit: 1661c3e1bb38ed12f8485c3860fc2d2b97dd2c9d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/20/2019
ms.locfileid: "71149928"
---
# <a name="what-is-sql-server-2016-r-services"></a>Che cos'è SQL Server 2016 R Services?
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

R Services è una funzionalità di SQL Server 2016 che offre la possibilità di eseguire script R con dati relazionali. È possibile usare i pacchetti e i framework open source e i [pacchetti Microsoft R](#packages) per l'analisi predittiva e l'apprendimento automatico. Gli script vengono eseguiti nel database senza trasferire i dati all'esterno di SQL Server o in rete. Questo articolo illustra le nozioni di base di R Services per SQL Server.

> [!Note]
> R Services è stato rinominato in [Machine Learning Services](../what-is-sql-server-machine-learning.md) SQL Server 2017 e versioni successive e supporta sia Python che r.

## <a name="what-is-r-services"></a>Che cos'è R Services?

R Services per SQL Server consente di eseguire gli script R nel database. È possibile usarlo per preparare e pulire i dati, eseguire la progettazione delle funzionalità e il training, la valutazione e la distribuzione di modelli di machine learning all'interno di un database. La funzionalità esegue gli script in cui risiedono i dati ed Elimina il trasferimento dei dati attraverso la rete a un altro server.

Le distribuzioni di base di R sono incluse in R Services. È possibile usare i pacchetti e i framework open source oltre ai pacchetti Microsoft [RevoScaleR](../r/ref-r-revoscaler.md), [MicrosoftML](../r/ref-r-microsoftml.md), [olapr].. /r/Ref-r-olapr.MD) e [sqlrutils](../r/ref-r-sqlrutils.md) per r.

R Services usa un Framework di estendibilità per eseguire gli script R in SQL Server. Altre informazioni sul funzionamento:

+ [Framework di estendibilità](../concepts/extensibility-framework.md)
+ [Estensione R](../concepts/extension-r.md)

## <a name="what-can-i-do-with-r-services"></a>Che cosa è possibile fare con R Services?

È possibile usare R Services per compilare ed eseguire il training di modelli di apprendimento automatico e apprendimento avanzato all'interno SQL Server. È anche possibile distribuire i modelli esistenti in R Services e usare i dati relazionali per le stime.

Esempi del tipo di stime che è possibile utilizzare R Services per SQL Server per, includono:

|||
|-|-|
|Classificazione/categorizzazione|Suddivide automaticamente i commenti dei clienti in categorie positive e negative|
|Regressione/stima valori continui|Prevedere il prezzo delle case in base alle dimensioni e alla posizione|
|Rilevamento di anomalie|Rilevare transazioni bancarie fraudolente |
|Consigli|Suggerisci i prodotti che gli acquirenti online potrebbero voler acquistare, in base agli acquisti precedenti|

### <a name="how-to-execute-r-scripts"></a>Come eseguire gli script R

Esistono due modi per eseguire gli script R in R Services:

+ Il modo più comune consiste nell'usare T-SQL stored procedure [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

+ È anche possibile usare il client R preferito e scrivere script che effettuano il push dell'esecuzione (denominata *contesto di calcolo remoto*) a una SQL Server remota. Per altre informazioni, vedere come [configurare uno sviluppo R per client Data Science](../r/set-up-a-data-science-client.md) .

<a name="packages"></a>

## <a name="r-packages"></a>Pacchetti R

È possibile usare i pacchetti e i framework open source, oltre ai pacchetti aziendali Microsoft. I pacchetti R open source più comuni sono pre-installati in R Services. Sono inclusi anche i pacchetti R seguenti di Microsoft:

| Pacchetto | Descrizione |
|-|-|
| [RevoScaleR](../r/ref-r-revoscaler.md) | Il pacchetto principale per le trasformazioni e le trasformazioni dei dati scalabili di R., il riepilogo statistico, la visualizzazione e molte forme di modellazione. Inoltre, le funzioni in questo pacchetto distribuiscono automaticamente i carichi di lavoro tra i core disponibili per l'elaborazione parallela. |
| [MicrosoftML (R)](../r/ref-r-microsoftml.md) | Aggiunge algoritmi di machine learning per creare modelli personalizzati per l'analisi del testo, l'analisi delle immagini e l'analisi dei sentimenti. |
| [olapR](../r/ref-r-olapr.md) | Funzioni R utilizzate per le query MDX su un cubo OLAP SQL Server Analysis Services. |
| [sqlrutils](../r/ref-r-sqlrutils.md) | Un meccanismo per usare gli script R in una stored procedure T-SQL, registrare stored procedure con un database ed eseguire il stored procedure da un [ambiente di sviluppo r](../r/set-up-a-data-science-client.md). |
| [Microsoft R Open](https://mran.microsoft.com/rro) | Microsoft R Open (riparazione) è la distribuzione avanzata di R da Microsoft. Si tratta di una piattaforma open source completa per l'analisi statistica e data science. Si basa su e 100% compatibile con R e include funzionalità aggiuntive per migliorare le prestazioni e la riproducibilità. |

## <a name="how-do-i-get-started-with-rservices"></a>Ricerca per categorie iniziare a usare RServices?

1. [Installare SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)

1. Configurare gli strumenti di sviluppo. È possibile usare:

    + [Azure Data Studio](../../azure-data-studio/what-is.md) o [SQL Server Management Studio (SSMS)](../../ssms/sql-server-management-studio-ssms.md) per usare T-SQL e il stored procedure [Sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) per eseguire lo script R.
    + R sul computer portatile o sulla workstation di sviluppo per eseguire gli script. È possibile estrarre i dati localmente o eseguire il push dell'esecuzione in modalità remota per SQL Server con [RevoScaleR](../r/ref-r-revoscaler.md). Per altre informazioni, vedere come [configurare uno sviluppo R per client Data Science](../r/set-up-a-data-science-client.md) .

1. Scrivere il primo script R

    + Avvio rapido: [Creare ed eseguire script R semplici in SQL Server](../tutorials/quickstart-r-create-script.md)
    + Avvio rapido: [Creare ed eseguire il training di un modello predittivo in R](../tutorials/quickstart-r-train-score-model.md)
    + Esercitazione: [Usare R in T-SQL](../tutorials/sqldev-in-database-r-for-sql-developers.md): Esplorazione dei dati, progettazione di funzionalità, training e distribuzione di modelli ed esecuzione di stime (serie in cinque parti)
    + Esercitazione: [Usare r Services in r Tools](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md): Esplora i dati, crea grafici e tracciati, Esegui la progettazione delle funzionalità, Esegui il training e Distribuisci modelli ed Esegui stime (serie in sei parti)

## <a name="next-steps"></a>Passaggi successivi

+ [Installare SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)
+ [Configurare un client di data science per lo sviluppo R](../r/set-up-a-data-science-client.md)