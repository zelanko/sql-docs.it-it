---
title: R Services in SQL Server 2016
description: R in SQL Server per attività R integrate su dati relazionali, tra cui data science e modellazione statistica, analisi predittiva, visualizzazione dei dati e altro ancora.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/10/2018
ms.topic: overview
author: dphansen
ms.author: davidph
monikerRange: =sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 32487d8c1a6c87c9ad916e4cfd517f9ba4cba6e2
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469904"
---
# <a name="r-services-in-sql-server-2016"></a>R Services in SQL Server 2016
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

R Services è un componente aggiuntivo di un'istanza del motore di database SQL Server 2016, usato per l'esecuzione di codice R e funzioni su SQL Server. Il codice viene eseguito in un Framework di estendibilità, isolato dai processi del motore di base, ma completamente disponibile per i dati relazionali come stored procedure, come script T-SQL che contiene istruzioni R o come codice R contenente T-SQL. 

R Services include una distribuzione di base di R, sovrapposta ai pacchetti R aziendali di Microsoft, in modo da poter caricare ed elaborare grandi quantità di dati in più core e aggregare i risultati in un unico output consolidato. Le funzioni e gli algoritmi R di Microsoft sono progettati per la scalabilità e l'utilità: distribuzione di analisi predittive, modellazione statistica, visualizzazioni di dati e algoritmi di machine learning all'avanguardia in un prodotto server commerciale progettato e supportato da Microsoft. 

Le librerie R includono [**RevoScaleR**](ref-r-revoscaler.md), [**MicrosoftML (r)** ](ref-r-microsoftml.md)e altre. Poiché R Services è integrato con il motore di database, è possibile gestire le analisi vicine ai dati ed eliminare i costi e i rischi di protezione associati allo spostamento dei dati.

> [!Note]
> R Services è stato rinominato in SQL Server 2017 e versioni successive per [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md), riflettendo l'aggiunta di Python.

## <a name="components"></a>Componenti

SQL Server 2016 è solo R. Nella tabella seguente vengono descritte le funzionalità di SQL Server 2016.

| Componente | Descrizione |
|-----------|-------------|
| Servizio Launchpad di SQL Server | Un servizio che gestisce le comunicazioni tra i runtime R esterni e l'istanza di SQL Server. |
| Pacchetti R | [**RevoScaleR**](ref-r-revoscaler.md) è la libreria primaria per R scalabile. le funzioni in questa libreria sono tra i più diffusi. In queste librerie sono disponibili le trasformazioni e la manipolazione dei dati, il riepilogo statistico, la visualizzazione e molte forme di modellazione e analisi. Inoltre, le funzioni in queste librerie distribuiscono automaticamente i carichi di lavoro tra i core disponibili per l'elaborazione parallela, con la possibilità di lavorare su blocchi di dati coordinati e gestiti dal motore di calcolo.  <br/>[**MicrosoftML (R)** ](ref-r-microsoftml.md) aggiunge algoritmi di apprendimento automatico per creare modelli personalizzati per l'analisi del testo, l'analisi delle immagini e l'analisi dei sentimenti. <br/>[**sqlRUtils**](ref-r-sqlrutils.md) fornisce funzioni di supporto per l'inserimento di script R in un stored procedure T-SQL, la registrazione di una stored procedure con un database e l'esecuzione del stored procedure da un ambiente di sviluppo r.<br/>[**olapr**](ref-r-olapr.md) è per la specifica di query MDX in R.|
| Microsoft R Open (MRO) | [**Riparazione**](https://mran.microsoft.com/open) è una distribuzione open source di Microsoft di R. Il pacchetto e l'interprete sono inclusi. Usare sempre la versione di installazione di installazione. |
| Strumenti R | Le finestre della console R e i prompt dei comandi sono strumenti standard in una distribuzione R.  |
| Esempi e script R |  I pacchetti R e RevoScaleR Open Source includono set di dati predefiniti che consentono di creare ed eseguire script con dati pre-installati |
| Modelli con training preliminare in R | I modelli con training preliminare vengono creati per casi d'uso specifici e gestiti dal team di progettazione di data science in Microsoft. È possibile usare i modelli con training preliminare così come sono per assegnare punteggi positivi negativi nel testo o per rilevare le funzionalità nelle immagini, usando i nuovi input di dati forniti. I modelli vengono eseguiti in R Services, ma non possono essere installati tramite il programma di installazione di SQL Server. Per altre informazioni, vedere [installare modelli di apprendimento automatico pre-addestrati in SQL Server](../install/sql-pretrained-models-install.md). |

## <a name="using-r-services"></a>Uso di R Services

Gli sviluppatori e gli analisti spesso hanno codice in esecuzione su un'istanza di SQL Server locale. Aggiungendo Machine Learning Services e abilitando l'esecuzione di script esterni, è possibile eseguire il codice R in modalità SQL Server: wrapping di script nelle stored procedure, archiviazione di modelli in una tabella SQL Server o combinazione di funzioni T-SQL e R nelle query.

L'approccio più comune per l'analisi nel database consiste nell'usare [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), passando lo script R come parametro di input.

Le interazioni client-server classiche sono un altro approccio. Da qualsiasi workstation client che dispone di un IDE, è possibile installare [Microsoft R client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)e quindi scrivere il codice che esegue il push dell'esecuzione (definita *contesto di calcolo remoto*) ai dati e alle operazioni in una SQL Server remota. 

Infine, se si usa un [server autonomo](r-server-standalone.md) e l'edizione Developer, è possibile compilare soluzioni in una workstation client usando le stesse librerie e gli stessi interpreti e quindi distribuire il codice di produzione in SQL Server Machine Learning Services (in-database). 

## <a name="how-to-get-started"></a>Come iniziare

Iniziare con il programma di installazione, associare i file binari allo strumento di sviluppo preferito e scrivere il primo script.

**Passaggio 1:** Installare e configurare il software. 

+ [Installare SQL Server 2016 R Services (in-database)](../install/sql-r-services-windows-install.md)

**Passaggio 2:** Acquisire esperienza pratica usando una di queste esercitazioni:

+ [Esercitazione: Informazioni sulle analisi nel database con R](../tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [Esercitazione: Procedura dettagliata end-to-end con R](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

**Passaggio 3:** Aggiungere i pacchetti R preferiti e usarli insieme ai pacchetti forniti da Microsoft

+ [Gestione dei pacchetti R per SQL Server](install-additional-r-packages-on-sql-server.md)


## <a name="see-also"></a>Vedere anche

 [Installare SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)
