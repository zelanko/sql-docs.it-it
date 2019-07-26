---
title: Creare grafici e tracciati con funzioni SQL e R-SQL Server Machine Learning
description: Esercitazione che illustra come creare grafici e tracciati usando le funzioni del linguaggio R su SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: f14005b8ba9d6f05d2b69deba29d83af5695f657
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470506"
---
# <a name="create-graphs-and-plots-using-sql-and-r-walkthrough"></a>Creare grafici e tracciati con SQL e R (procedura dettagliata)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

In questa parte della procedura dettagliata vengono illustrate le tecniche per la generazione di grafici e mappe usando R con dati SQL Server. Si crea un istogramma semplice e quindi si sviluppa un tracciato mappa più complesso.

## <a name="prerequisites"></a>Prerequisiti

Questo passaggio presuppone una sessione R in corso in base ai passaggi precedenti di questa procedura dettagliata. Usa le stringhe di connessione e gli oggetti origine dati creati in questi passaggi. Per eseguire lo script vengono usati gli strumenti e i pacchetti seguenti.

+ Rgui. exe per l'esecuzione di comandi R
+ Management Studio per eseguire T-SQL
+ googMap
+ pacchetto ggmap
+ pacchetto mapproj

## <a name="create-a-histogram"></a>Creare un istogramma

1. Generare il primo tracciato usando la funzione [rxHistogram](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatasource) .  La funzione rxHistogram fornisce una funzionalità simile a quella nei pacchetti R Open Source, ma può essere eseguita in un contesto di esecuzione remoto.

    ```R
    # Plot fare amount on SQL Server and return the plot
    start.time <- proc.time()
    rxHistogram(~fare_amount, data = inDataSource, title = "Fare Amount Histogram")
    used.time <- proc.time() - start.time
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2), " seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate plot.", sep=""))
    ```

2. L'immagine viene restituita nel dispositivo grafico R per l'ambiente di sviluppo.  Ad esempio, in RStudio fare clic sulla finestra **Plot** .  In [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)]viene aperta una finestra grafica separata.

    ![uso di rxHistogram per tracciare gli importi delle tariffe](media/rsql-e2e-rxhistogramresult.png "uso di rxHistogram per tracciare gli importi delle tariffe")

    > [!NOTE]
    > Il grafico ha un aspetto diverso?
    >  
    > Questo perché _indatasource_ usa solo le prime 1000 righe. L'ordinamento delle righe che utilizzano TOP è non deterministico in assenza di una clausola ORDER BY, quindi è previsto che i dati e il grafico risultante potrebbero variare.
    > Questa particolare immagine è stata generata usando circa 10.000 righe di dati. È consigliabile provare con diversi numeri di righe per ottenere grafici differenti, osservando il tempo necessario alla restituzione dei risultati nell'ambiente in uso.

## <a name="create-a-map-plot"></a>Creare un tracciato mappa

In genere, i server di database bloccano l'accesso a Internet. Questo può risultare scomodo quando si usano pacchetti R che devono scaricare mappe o altre immagini per generare i tracciati. Tuttavia, esiste una soluzione alternativa che può risultare utile quando si sviluppano applicazioni personalizzate. In sostanza, si genera la rappresentazione della mappa nel client e quindi si sovrappone alla mappa i punti archiviati come attributi nella tabella SQL Server.

1. Definire la funzione che crea l'oggetto tracciato R. La funzione personalizzata *mapPlot* crea un grafico a dispersione che usa i percorsi di prelievo dei taxi e traccia il numero di corse avviate da ogni posizione. USA i pacchetti **ggplot2** e **ggmap** , che devono essere già [installati e caricati](walkthrough-data-science-end-to-end-walkthrough.md#add-packages).

    ```R
    mapPlot <- function(inDataSource, googMap){
        library(ggmap)
        library(mapproj)
        ds <- rxImport(inDataSource)
        p <- ggmap(googMap)+
        geom_point(aes(x = pickup_longitude, y =pickup_latitude ), data=ds, alpha =.5,
    color="darkred", size = 1.5)
        return(list(myplot=p))
    }
    ```

    + La funzione *mapPlot* accetta due argomenti: un oggetto dati esistente definito in precedenza mediante RxSqlServerData e la rappresentazione della mappa passata dal client.
    + Nella riga che inizia con la variabile *DS* , viene usato rxImport per caricare i dati in memoria dall'origine dati creata in precedenza , indatasource. (L'origine dati contiene solo 1000 righe; se si desidera creare una mappa con più punti dati, è possibile sostituire un'origine dati diversa).
    + Quando si usano funzioni R Open Source, i dati devono essere caricati in frame di dati nella memoria locale. Tuttavia, chiamando la funzione [rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rximport) , è possibile eseguire nella memoria del contesto di calcolo remoto.

2. Modificare il contesto di calcolo in locale e caricare le librerie necessarie per la creazione delle mappe.

    ```R
    rxSetComputeContext("local")
    library(ggmap)
    library(mapproj)
    gc <- geocode("Times Square", source = "google")
    googMap <- get_googlemap(center = as.numeric(gc), zoom = 12, maptype = 'roadmap', color = 'color');
    ```

    + La variabile `gc` memorizza un set di coordinate per Times Square, New York.

    + La riga che inizia con `googmap` genera una mappa con al centro le coordinate specificate.

3. Passare al contesto di calcolo SQL Server ed eseguire il rendering dei risultati eseguendo il wrapping della funzione Plot in [rxExec](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxexec) , come illustrato di seguito. La funzione rxExec fa parte del pacchetto **RevoScaleR** e supporta l'esecuzione di funzioni R arbitrarie in un contesto di calcolo remoto.

    ```R
    rxSetComputeContext(sqlcc)
    myplots <- rxExec(mapPlot, inDataSource, googMap, timesToRun = 1)
    plot(myplots[[1]][["myplot"]]);
    ````

    + I dati `googMap` della mappa vengono passati come argomento alla funzione eseguita in remoto *mapPlot*. Poiché le mappe sono state generate nell'ambiente locale, devono essere passate alla funzione per creare il tracciato nel contesto di SQL Server.

    + Quando la riga che inizia `plot` con viene eseguita, i dati di cui è stato eseguito il rendering vengono serializzati nell'ambiente r locale, in modo che sia possibile visualizzarli nel client r.

    > [!NOTE]
    > Se si usa SQL Server in una macchina virtuale di Azure, si potrebbe ricevere un errore a questo punto. Si verifica un errore quando la regola del firewall predefinita in Azure blocca l'accesso alla rete da parte del codice R. Per informazioni dettagliate su come correggere questo errore, vedere [installazione di servizi di Machine Learning (R) in una macchina virtuale di Azure](../install/sql-machine-learning-azure-virtual-machine.md).

4. La figura seguente mostra il tracciato di output. I punti di inizio corsa dei taxi vengono aggiunti alla mappa come punti rossi. L'immagine potrebbe essere diversa, a seconda del numero di posizioni presenti nell'origine dati usata.

    ![creazione del tracciato delle corse in taxi con una funzione R personalizzata](media/rsql-e2e-mapplot.png "creazione del tracciato delle corse in taxi con una funzione R personalizzata")

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Creare funzionalità di dati usando R e SQL](walkthrough-create-data-features.md)
