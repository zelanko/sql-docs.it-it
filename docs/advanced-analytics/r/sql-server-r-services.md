---
title: 'R Services in SQL Server 2016: SQL Server Machine Learning Services'
description: R in SQL Server per le attività R integrate su dati relazionali, tra cui analisi scientifica dei dati e modellazione statistica, analitica predittiva, visualizzazione dei dati e altro ancora.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/10/2018
ms.topic: overview
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 14be74e19219fee834a4ab82e74c004a4e426483
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58510528"
---
# <a name="r-services-in-sql-server-2016"></a>R Services in SQL Server 2016
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

R Services è un componente aggiuntivo a un'istanza del motore del database SQL Server 2016, utilizzato per l'esecuzione di funzioni e codice R in SQL Server. Codice viene eseguito in un framework di estendibilità, isolata da processi del motore di base, ma è completamente disponibile ai dati relazionali come stored procedure, come script T-SQL contenente le istruzioni di R o come codice R che contiene di T-SQL. 

R Services include una distribuzione di base di R, da sovrapporre i pacchetti R aziendali da Microsoft in modo che è possibile caricare e di elaborare grandi quantità di dati su più core e aggregare i risultati in un singolo output consolidato. Le funzioni R e gli algoritmi di Microsoft sono progettati per operare sia scalabilità che utilità: recapito di analitica predittiva, modellazione statistica, visualizzazioni dei dati e avanguardia algoritmi di machine learning in un prodotto commerciale server progettato e supportato da Microsoft. 

Le librerie R includono [ **RevoScaleR**](ref-r-revoscaler.md), [ **MicrosoftML (R)**](ref-r-microsoftml.md)e così via. Poiché R Services è integrato con il motore di database, puoi mantenere analitica vicino ai dati ed eliminare i costi e rischi di sicurezza associati allo spostamento dei dati.

> [!Note]
> R Services è stato rinominato in SQL Server 2017 da [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md), che riflette l'aggiunta di Python.

## <a name="components"></a>Componenti

SQL Server 2016 è solo R. La tabella seguente descrive le funzionalità di SQL Server 2016.

| Componente | Descrizione |
|-----------|-------------|
| Servizio Launchpad di SQL Server | Un servizio che gestisce le comunicazioni tra i runtime R esterni e l'istanza di SQL Server. |
| Pacchetti R | [**RevoScaleR** ](ref-r-revoscaler.md) è la libreria primaria per funzioni R. scalabile in questa raccolta sono tra i più diffusi. Le trasformazioni dei dati e la manipolazione, riepilogo statistico, visualizzazione e molte forme di analisi e modellazione sono disponibili in queste librerie. Inoltre, le funzioni in queste librerie distribuisce automaticamente i carichi di lavoro tra memorie centrali disponibili per l'elaborazione parallela, con la possibilità di operare su blocchi di dati coordinati e gestiti dal motore di calcolo.  <br/>[**MicrosoftML (R)** ](ref-r-microsoftml.md) aggiunge algoritmi di machine learning per creare modelli personalizzati per l'analisi del sentiment, analisi delle immagini e analisi del testo. <br/>[**sqlRUtils** ](ref-r-sqlrutils.md) fornisce funzioni helper per l'inserimento di script R in una stored procedure T-SQL archiviate, la registrazione di una stored procedure con un database e l'esecuzione della stored procedure da un ambiente di sviluppo R.<br/>[**olapR** ](ref-r-olapr.md) di specificare le query MDX in R.|
| Microsoft R Open (MRO) | [**MRO** ](https://mran.microsoft.com/open) è distribuzione open source di Microsoft di R. Sono inclusi il pacchetto e dell'interprete. Usare sempre la versione di MRO installato dal programma di installazione. |
| Strumenti R | Prompt dei comandi e le finestre della console R sono gli strumenti standard in una distribuzione di R.  |
| Esempi di R e gli script |  Pacchetti open source di R e RevoScaleR includono set di dati incorporato in modo che è possibile creare ed eseguire lo script usando i dati pre-installati |
| Modelli con training preliminare in R | I modelli con training preliminare vengono creati per casi d'uso specifici e gestiti per il team di progettazione di analisi scientifica dei dati in Microsoft. È possibile usare i modelli con training preliminare come-consiste nell'assegnare un punteggio del sentiment negativo positivo in testo o funzionalità vengono rilevati in immagini usando nuovi input di dati fornito. I modelli eseguiti in R Services, ma non possono essere installati tramite il programma di installazione di SQL Server. Per altre informazioni, vedere [Install con training preliminare modelli di machine learning in SQL Server](../install/sql-pretrained-models-install.md). |

## <a name="using-r-services"></a>Usando i servizi R

Analisti e sviluppatori hanno spesso il codice in esecuzione su un'istanza di SQL Server locale. Aggiunta di servizi di Machine Learning e abilitando l'esecuzione dello script esterno, si ottengono la possibilità di eseguire codice R in SQL Server tramite: eseguire il wrapping dello script in stored procedure, l'archiviazione dei modelli in una tabella di SQL Server o combinando le funzioni nelle query T-SQL e R.

L'approccio più comune per analitica nel database consiste nell'usare [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), il passaggio di script R come parametro di input.

Le interazioni classiche client-server sono un altro approccio. Da qualsiasi workstation client che dispone di un IDE, è possibile installare [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)e quindi scrivere codice che effettua il push di esecuzione (definito come una *contesto di calcolo remoto*) ai dati e delle operazioni SQL remoto Server. 

Infine, se si usa un' [server autonomo](r-server-standalone.md) e l'edizione Developer, è possibile creare soluzioni in una workstation client utilizzando le stesse librerie e gli interpreti e quindi distribuire codice di produzione in SQL Server Machine Learning Servizi (In-Database). 

## <a name="how-to-get-started"></a>Come iniziare a usare

Iniziare con il programma di installazione, collegare i file binari dello strumento di sviluppo preferito e scrivere il primo script.

**Passaggio 1:** Installare e configurare il software. 

+ [Installare SQL Server 2016 R Services (In-Database)](../install/sql-r-services-windows-install.md)

**Passaggio 2:** Ottieni esperienza pratica usando una delle esercitazioni seguenti:

+ [Esercitazione: Informazioni su analitica nel database con R](../tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [Esercitazione: Procedura dettagliata end-to-end con R](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

**Passaggio 3:** Aggiungere i pacchetti R Preferiti e usarli insieme a pacchetti forniti da Microsoft

+ [Gestione dei pacchetti R per SQL Server](install-additional-r-packages-on-sql-server.md)


## <a name="see-also"></a>Vedere anche

 [Installare SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)
