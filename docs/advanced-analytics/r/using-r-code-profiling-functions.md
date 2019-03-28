---
title: Usare funzioni - servizi di SQL Server Machine Learning di analisi del codice R
description: Migliorare le prestazioni e ottenere risultati più veloci in calcoli R in SQL Server usando funzioni di profiling R per restituire informazioni sulle chiamate di funzione interna.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/12/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: c9195a6c2b9a2192e9d8fd04ce3e5d2592b1b23e
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58510948"
---
# <a name="use-r-code-profiling-functions-to-improve-performance"></a>Usare funzioni di profiling del codice R per migliorare le prestazioni
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Oltre a usare risorse e strumenti di SQL Server per monitorare l'esecuzione di script R, è possibile usare gli strumenti per le prestazioni forniti da altri pacchetti R per ottenere altre informazioni sulle chiamate di funzioni interne. 

> [!TIP]
> Questo articolo fornisce risorse di base per iniziare a usare. Per indicazioni di esperti, è consigliabile la *Performance* sezione ["Advanced R" di Hadley Wickham](http://adv-r.had.co.nz).

## <a name="using-rprof"></a>Uso di RPROF

[*rprof* ](https://www.rdocumentation.org/packages/utils/versions/3.5.1/topics/Rprof) è una funzione inclusa nel pacchetto di base [ **utils**](https://www.rdocumentation.org/packages/utils/versions/3.5.1), che viene caricato per impostazione predefinita. 

In generale, la funzione *rprof* opera scrivendo lo stack di chiamate in un file a intervalli specificati. È quindi possibile usare la [ *summaryRprof* ](https://www.rdocumentation.org/packages/utils/versions/3.5.1/topics/summaryRprof) funzione per elaborare il file di output. Un vantaggio di *rprof* è il fatto di eseguire il campionamento, riducendo il carico delle prestazioni sul monitoraggio.

Per usare il profiling R nel codice, chiamare questa funzione e specificarne i parametri, incluso il percorso del file di log che verrà scritto. È possibile attivare o disattivare il profiling nel codice. La sintassi seguente viene illustrato l'utilizzo di base: 

```R
# Specify profiling output file.
varOutputFile <- "C:/TEMP/run001.log")
Rprof(varOutputFile)

# Turn off profiling
Rprof(NULL)
    
# Restart profiling
Rprof(append=TRUE)
```

> [!NOTE]
> Per poter usare questa funzione, è necessario che Windows Perl sia installato nel computer in cui viene eseguito il codice. Di conseguenza, è consigliabile profilare il codice durante lo sviluppo in un ambiente R e quindi distribuire il codice sottoposto a debug in SQL Server.  


## <a name="r-system-functions"></a>Funzioni di sistema R

Il linguaggio R include molte funzioni di pacchetto di base per la restituzione del contenuto delle variabili di sistema. Come parte del codice R, ad esempio, è possibile usare `Sys.timezone` per ottenere il fuso orario corrente o `Sys.Time` per ottenere l'ora di sistema da R. 

Per ottenere informazioni su singole funzioni di sistema R, digitare il nome della funzione come argomento per la funzione R `help()` da un prompt dei comandi di R.

```R
help("Sys.time")
```

## <a name="debugging-and-profiling-in-r"></a>Debug e profiling in R

La documentazione per Microsoft R Open, che viene installato per impostazione predefinita, include un manuale sullo sviluppo di estensioni per il linguaggio R che illustra [debug e profilatura](https://cran.r-project.org/doc/manuals/r-release/R-exts.html#Debugging) in modo dettagliato. È possibile trovare la stessa documentazione nel computer in C:\Program Files\Microsoft SQL Server\MSSQL13. MSSQLSERVER\R_SERVICES\doc\manual.

## <a name="see-also"></a>Vedere anche

+ [pacchetto di utilità R](https://www.rdocumentation.org/packages/utils/versions/3.5.1)
+ ["Advanced R" by Hadley Wickham](http://adv-r.had.co.nz)
