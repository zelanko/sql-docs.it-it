---
title: Esplorazione dei dati e modellazione predittiva con R - servizi di SQL Server Machine Learning
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: c6c0e07f48dee271fee61bc59b47f49683ff8832
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/15/2018
ms.locfileid: "53432344"
---
# <a name="data-exploration-and-predictive-modeling-with-r-in-sql-server"></a>Esplorazione dei dati e modellazione predittiva con R in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo descrive i miglioramenti al processo di analisi scientifica dei dati che sono possibili grazie all'integrazione con SQL Server.

Si applica a: SQL Server 2016 R Services, servizi SQL Server 2017 macchine al meglio

## <a name="the-data-science-process"></a>Il processo di analisi scientifica dei dati

Gli esperti dei dati spesso usano R per esplorare i dati e compilare modelli predittivi. Si tratta in genere di un processo iterativo di prove ed errori fino a ottenere un modello predittivo soddisfacente. Gli esperti di dati possono connettersi al database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e recuperare i dati nella workstation locale usando il pacchetto RODBC, esplorare i dati e compilare un modello predittivo tramite pacchetti R standard.

Tuttavia, questo approccio presenta numerosi svantaggi, tale georgiano rallentato l'adozione più ampio di R nell'organizzazione. 

+ Lo spostamento dei dati può essere lento, inefficiente o non sicuri
+ Lo stesso R presenta le limitazioni delle prestazioni e scalabilità

Questi svantaggi diventano più evidenti quando si desidera spostare e analizzare grandi quantità di dati oppure usare il set di dati che non rientrano nella memoria disponibile nel computer.

Pacchetti nuova, scalabili e le funzioni R incluse con [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] consentono di risolvere molti di questi problemi. 

## <a name="whats-different-about-revoscaler"></a>Che cos'è diverso su RevoScaleR?

Il pacchetto **RevoScaleR** contiene le implementazioni di alcune delle funzioni R più diffuse, riprogettate per garantire parallelismo e scalabilità. Per altre informazioni, vedere [Distributed Computing con RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler-distributed-computing).

Il pacchetto RevoScaleR fornisce anche supporto per la modifica del *contesto di esecuzione*. Ciò significa che, per un'intera soluzione o per una sola funzione, è possibile indicare che è necessario eseguire calcoli usando le risorse del computer che ospita l’istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , invece della workstation locale. Questa procedura offre numerosi vantaggi: evitare lo spostamento dei dati non necessari e usare risorse di calcolo più grandi nel computer del server.

## <a name="r-environment-and-packages"></a>Ambiente e pacchetti R

L'ambiente R supportato in [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] è costituito da un runtime, dal linguaggio open source e da un motore grafico supportato ed esteso da più pacchetti. Il linguaggio consente di usare un'ampia gamma di estensioni implementate con i pacchetti.  

### <a name="using-other-r-packages"></a>Uso di altri pacchetti R

Oltre alle librerie R proprietari incluse con Microsoft Machine Learning, è possibile usare quasi tutti i pacchetti R nella soluzione, tra cui:

+ Pacchetti R per utilizzo generico da repository pubblici. È possibile ottenere i pacchetti R open source più diffusi da repository pubblici, ad esempio CRAN, che ospita oltre 6000 pacchetti, usabili dagli esperti di dati.
  
  Per la piattaforma Windows, i pacchetti R vengono forniti come file con estensione zip e possono essere scaricati e installati con la licenza GPL.  
  
  Per informazioni su come installare i pacchetti di terze parti per l'uso con [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], vedere [Install Additional R Packages on SQL Server](../../advanced-analytics/r/install-additional-r-packages-on-sql-server.md)  
  
+ Pacchetti e librerie aggiuntivi forniti da [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)].   
  
     Il pacchetto **RevoScaleR** include analisi di Big Data ad alte prestazioni, versioni migliorate delle funzioni che supportano le attività comuni di data science, strumenti di apprendimento ottimizzati per Naive Bayes, regressione lineare, modelli Time Series, reti neurali e librerie matematiche avanzate.  
  
     Il pacchetto **RevoPemaR** consente di sviluppare algoritmi paralleli di memoria esterna in R.  
  
     Per altre informazioni su questi pacchetti e come usarli, vedere [What ' s RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-introduction) e [Introduzione a RevoPemaR](https://msdn.microsoft.com/microsoft-r/pemar-getting-started). 

+ **MicrosoftML** contiene una raccolta di algoritmi di apprendimento altamente ottimizzata e trasformazioni dei dati dal team di analisi scientifica dei dati di Microsoft. Molti degli algoritmi utilizzati anche in Azure Machine Learning. Per altre informazioni, vedere [MicrosoftML in SQL Server](ref-r-microsoftml.md).

### <a name="r-development-tools"></a>Strumenti di sviluppo di R

Quando si sviluppa la soluzione di R, assicurarsi di scaricare Microsoft R Client. Questo download gratuito include le librerie necessari per supportare contesti di calcolo remoti e alorithms scalabile:

+ **[!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)]:** Distribuzione del runtime di R e un set di pacchetti, ad esempio la libreria del kernel matematico di Intel, che migliorano le prestazioni delle operazioni standard di R.  
  
+ **RevoScaleR:** Un pacchetto R che consente di trasferire i calcoli a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[rsql_rre-noversion](../../includes/rsql-rre-noversion-md.md)] (Indici per tabelle con ottimizzazione per la memoria). Include anche un set di funzioni R comuni riprogettate per offrire scalabilità e prestazioni migliori. È possibile identificare queste funzioni migliorate dal prefisso **rx** . Include anche provider di dati avanzati per diverse origini. Queste funzioni sono precedute dal prefisso **Rx**.

È possibile usare qualsiasi editor di codice basato su Windows che supporti R, ad esempio [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] o RStudio. Il download di [!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)] include anche strumenti comuni della riga di comando per R, ad esempio RGui.exe.

## <a name="use-new-data-sources-and-compute-contexts"></a>Uso di nuove origini dati e contesti di calcolo

Quando si usa il pacchetto RevoScaleR per connettersi a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], cercare queste funzioni da usare nel codice R:

+ **RxSqlServerData** è una funzione fornita nel pacchetto RevoScaleR a supporto della migliorata connettività dei dati a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
     Usare questa funzione nel codice R per definire l’ *origine dei dati*. L'oggetto di origine dei dati specifica il server e le tabelle in cui i dati si trovano e gestisce le attività di lettura dei dati e scrittura di dati su [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
-   Il pacchetto **RxInSqlServer** può essere usata per specificare il *contesto di calcolo*.  In altre parole, è possibile indicare la posizione in cui deve essere eseguito il codice R: nella workstation locale o nel computer che ospita l’istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  Per altre informazioni, vedere [funzioni RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler).
  
     Quando si imposta il contesto di calcolo, questo interessa solo i calcoli che supportano il contesto di esecuzione remota, ovvero le operazioni R fornite dal pacchetto RevoScaleR e le funzioni correlate. Le soluzioni R basate su pacchetti CRAN standard in genere non possono essere eseguite in un contesto di calcolo remoto, anche se possono essere eseguite nel computer [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] se avviate da T-SQL. È tuttavia possibile usare la funzione `rxExec` per chiamare singole funzioni R ed eseguirle in remoto in [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].

Per esempi di come creare e usare origini dati e contesti di esecuzione, vedere queste esercitazioni:

+ [Procedura approfondita per l'analisi scientifica dei dati](../../advanced-analytics/tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)  
+  [Analisi dei dati usando Microsoft R](https://msdn.microsoft.com/microsoft-r/data-analysis-in-microsoft-r)

## <a name="deploy-r-code-to-production"></a>Distribuire il codice R nell'ambiente di produzione

Una parte importante dell'analisi scientifica dei dati è la distribuzione dell'analisi ad altri utenti o l’uso di modelli predittivi per migliorare i risultati e i processi aziendali. In [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], è facile passare alla produzione quando lo script R o il modello è pronto.

Per altre informazioni sul trasferimento del codice per l'esecuzione in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Operationalizing Your R Code](../../advanced-analytics/r/operationalizing-your-r-code.md).

Il processo di distribuzione inizia in genere con pulizia dello script in uso al fine di eliminare il codice non necessario nell'ambiente di produzione. Quando si spostano i calcoli più vicino ai dati, è possibile adottare modi per spostare in modo più efficiente, riepilogare o presentare i dati invece operazioni vengono eseguite in R.  È consigliabile che il data scientist consultare uno sviluppatore di database sui modi per migliorare le prestazioni, soprattutto se la soluzione non pulizia dei dati o una funzionalità di progettazione che può essere più efficace in SQL. Potrebbero essere necessarie modifiche ai processi ETL per garantire che i flussi di lavoro per la compilazione o la valutazione di un modello non abbiano esito negativo e che i dati di input siano disponibili nel formato corretto.

## <a name="see-also"></a>Vedere anche

[Confronto tra funzioni R di base e ScaleR](https://msdn.microsoft.com/microsoft-r/scaler/compare-base-r-scaler-functions)

[Libreria RevoScaleR in SQL Server](ref-r-revoscaler.md)
