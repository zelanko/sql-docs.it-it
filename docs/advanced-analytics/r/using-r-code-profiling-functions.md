---
title: Usare le funzioni di profiling del codice R
description: Migliorare le prestazioni e ottenere risultati più veloci sui calcoli R su SQL Server usando le funzioni di profilatura R per restituire informazioni sulle chiamate di funzione interne.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/12/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: f4a68c19813b31164947f6d04a8c54c2a54eec34
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345687"
---
# <a name="use-r-code-profiling-functions-to-improve-performance"></a>Usare le funzioni di profiling del codice R per migliorare le prestazioni
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Oltre a usare risorse e strumenti di SQL Server per monitorare l'esecuzione di script R, è possibile usare gli strumenti per le prestazioni forniti da altri pacchetti R per ottenere altre informazioni sulle chiamate di funzioni interne. 

> [!TIP]
> Questo articolo fornisce le risorse di base per iniziare. Per indicazioni di esperti, è consigliabile usare la sezione relativa alle *prestazioni* in ["Advanced R" di Hadley Wickham](http://adv-r.had.co.nz).

## <a name="using-rprof"></a>Uso di RPROF

[*rprof*](https://www.rdocumentation.org/packages/utils/versions/3.5.1/topics/Rprof) è una funzione inclusa nel pacchetto di base [**utils**](https://www.rdocumentation.org/packages/utils/versions/3.5.1), che viene caricato per impostazione predefinita. 

In generale, la funzione *rprof* opera scrivendo lo stack di chiamate in un file a intervalli specificati. È quindi possibile usare la funzione [*summaryRprof*](https://www.rdocumentation.org/packages/utils/versions/3.5.1/topics/summaryRprof) per elaborare il file di output. Un vantaggio di *rprof* è il fatto di eseguire il campionamento, riducendo il carico delle prestazioni sul monitoraggio.

Per usare il profiling R nel codice, chiamare questa funzione e specificarne i parametri, incluso il percorso del file di log che verrà scritto. È possibile attivare o disattivare il profiling nel codice. Nella sintassi seguente viene illustrato l'utilizzo di base: 

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

La documentazione per Microsoft R Open, che è installata per impostazione predefinita, include un manuale sullo sviluppo di estensioni per il linguaggio R che illustra in dettaglio la profilatura [e il debug](https://cran.r-project.org/doc/manuals/r-release/R-exts.html#Debugging) . È possibile trovare la stessa documentazione nel computer in C:\Programmi\Microsoft SQL Server\MSSQL13. MSSQLSERVER\R_SERVICES\doc\manual.

## <a name="see-also"></a>Vedere anche

+ [pacchetto utils R](https://www.rdocumentation.org/packages/utils/versions/3.5.1)
+ ["Advanced R" di Hadley Wickham](http://adv-r.had.co.nz)
