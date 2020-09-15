---
title: Migliorare le prestazioni usando la funzione di profilatura del codice R
description: Raccogliere informazioni utili per migliorare le prestazioni e ottenere risultati più veloci per i calcoli R in SQL Server usando le funzioni di profilatura di R. La funzione *rprof* raccoglie e restituisce informazioni sulle chiamate di funzione interne.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 12/12/2018
ms.topic: how-to
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e65171fa0222c0c581f692bede727dc4366c9c53
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/13/2020
ms.locfileid: "88180440"
---
# <a name="use-r-code-profiling-functions-to-improve-performance"></a>Migliorare le prestazioni tramite le funzioni di profilatura di R
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

Oltre a usare risorse e strumenti di SQL Server per monitorare l'esecuzione di script R, è possibile usare gli strumenti per le prestazioni forniti da altri pacchetti R per ottenere altre informazioni sulle chiamate di funzioni interne. 

> [!TIP]
> Questo articolo presenta alcune risorse di base per iniziare. Per linee guida per utenti esperti, è consigliabile vedere la sezione *Performance* (Prestazioni) in ["Advanced R" (R avanzato) di Hadley Wickham](http://adv-r.had.co.nz).

## <a name="using-rprof"></a>Uso di RPROF

[*rprof*](https://www.rdocumentation.org/packages/utils/versions/3.5.1/topics/Rprof) è una funzione inclusa nel pacchetto di base [**utils**](https://www.rdocumentation.org/packages/utils/versions/3.5.1), caricato per impostazione predefinita. 

In generale, la funzione *rprof* opera scrivendo lo stack di chiamate in un file a intervalli specificati. È quindi possibile usare la funzione [*summaryRprof*](https://www.rdocumentation.org/packages/utils/versions/3.5.1/topics/summaryRprof) per elaborare il file di output. Un vantaggio di *rprof* è il fatto di eseguire il campionamento, riducendo il carico delle prestazioni sul monitoraggio.

Per usare il profiling R nel codice, chiamare questa funzione e specificarne i parametri, incluso il percorso del file di log che verrà scritto. È possibile attivare o disattivare il profiling nel codice. La sintassi seguente illustra l'utilizzo di base: 

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

La documentazione per Microsoft R Open, installata per impostazione predefinita, include un manuale sullo sviluppo di estensioni per il linguaggio R che descrive [profilatura e debug](https://cran.r-project.org/doc/manuals/r-release/R-exts.html#Debugging) in modo dettagliato. È possibile trovare la stessa documentazione nel computer in C:\Programmi\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\doc\manual.

## <a name="see-also"></a>Vedere anche

+ [Pacchetto utils di R](https://www.rdocumentation.org/packages/utils/versions/3.5.1)
+ ["Advanced R" (R avanzato) di Hadley Wickham](http://adv-r.had.co.nz)
