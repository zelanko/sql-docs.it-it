---
title: Creare grafici e tracciati con R funzioni SQL Server Machine Learning e SQL
description: Esercitazione che illustra come creare grafici e tracciati con le funzioni del linguaggio R in SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: b988105733d8e3a9ee2edae344947cbf9d377e5d
ms.sourcegitcommit: a91c3f4fe2587d474cd4d470bda93239ba2693bb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/14/2019
ms.locfileid: "67140391"
---
# <a name="create-graphs-and-plots-using-sql-and-r-walkthrough"></a>Creare grafici e tracciati con R (procedura dettagliata) e SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

In questa parte della procedura dettagliata descrive le tecniche per la generazione di grafici e mappe usando R con dati di SQL Server. Creare un istogramma semplice e quindi lo sviluppo di un tracciato a mappa più complesso.

## <a name="prerequisites"></a>Prerequisiti

Questo passaggio si presuppone una sessione di R in corso in base a quello precedente in questa procedura dettagliata. Usa connessione dati e stringhe di origine oggetti creati in tali passaggi. Gli strumenti e i pacchetti seguenti vengono utilizzati per eseguire lo script.

+ Rgui.exe per eseguire i comandi di R
+ Management Studio per eseguire T-SQL
+ googMap
+ pacchetto ggmap
+ pacchetto mapproj

## <a name="create-a-histogram"></a>Creare un istogramma

1. Generare il primo tracciato usando la funzione [rxHistogram](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatasource) .  La funzione di rxHistogram fornisce funzionalità simili a quelle nei pacchetti R open source, ma è possibile eseguire in un contesto di esecuzione in modalità remota.

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
    > Il grafico aspetto diverso?
    >  
    > Infatti _inDataSource_ Usa solo le prime 1000 righe. L'ordinamento delle righe mediante TOP non è deterministico in assenza di una clausola ORDER BY, in modo che si prevede che i dati e il grafico risultante potrebbe variare.
    > Questa particolare immagine è stata generata usando circa 10.000 righe di dati. È consigliabile provare con diversi numeri di righe per ottenere grafici differenti, osservando il tempo necessario alla restituzione dei risultati nell'ambiente in uso.

## <a name="create-a-map-plot"></a>Creare un tracciato mappa

In genere, i server di database bloccano l'accesso a Internet. Ciò può risultare poco pratico quando si usano i pacchetti R che è necessario scaricare mappe o altre immagini da generare tracciati. Tuttavia, vi è una soluzione alternativa che possono risultare utili durante lo sviluppo di applicazioni personalizzate. In pratica, si genera la rappresentazione della mappa nel client e quindi sovrappongono sulla mappa i punti archiviati come attributi nella tabella di SQL Server.

1. Definire la funzione che crea l'oggetto tracciato di R. La funzione personalizzata *mapPlot* crea un grafico a dispersione che usa la corsa dei taxi e traccia il numero di corse avviate da ogni posizione. Usa il **ggplot2** e **ggmap** pacchetti che devono essere già [installati e caricati](walkthrough-data-science-end-to-end-walkthrough.md#add-packages).

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

    + Il *mapPlot* funzione accetta due argomenti: un oggetto dati esistente, che è definita in precedenza usando RxSqlServerData e la rappresentazione della mappa passata dal client.
    + Nella riga che inizia con la *ds* variabile rxImport viene usato per caricare dati di memoria dall'origine dati creata in precedenza, in *inDataSource*. (Tale origine dati contiene solo 1000 righe, se si desidera creare una mappa con più punti dati, è possibile sostituire un'origine dati diversa).
    + Quando si usano funzioni R open source, i dati devono essere caricati nel frame di dati nella memoria locale. Tuttavia, chiamando il [rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rximport) (funzione), è possibile eseguire nella memoria del contesto di calcolo remoto.

2. Modificare il contesto di calcolo locale e caricare le librerie necessarie per la creazione delle mappe.

    ```R
    rxSetComputeContext("local")
    library(ggmap)
    library(mapproj)
    gc <- geocode("Times Square", source = "google")
    googMap <- get_googlemap(center = as.numeric(gc), zoom = 12, maptype = 'roadmap', color = 'color');
    ```

    + La variabile `gc` memorizza un set di coordinate per Times Square, New York.

    + La riga che inizia con `googmap` genera una mappa con al centro le coordinate specificate.

3. Passare al contesto di calcolo di SQL Server ed eseguire il rendering dei risultati, eseguendo il wrapping della funzione tracciato in [rxExec](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxexec) come illustrato di seguito. La funzione rxExec fa parte il **RevoScaleR** pacchetto e supporta l'esecuzione di funzioni R arbitrarie in un contesto di calcolo remoto.

    ```R
    rxSetComputeContext(sqlcc)
    myplots <- rxExec(mapPlot, inDataSource, googMap, timesToRun = 1)
    plot(myplots[[1]][["myplot"]]);
    ````

    + I dati della mappa nel `googMap` viene passato come argomento alla funzione eseguita in modalità remota *mapPlot*. Poiché le mappe sono state generate nell'ambiente locale, deve essere passati alla funzione per creare il tracciato nel contesto di SQL Server.

    + Quando la riga che inizia con `plot` esecuzioni, il rendering dei dati viene nuovamente serializzato nell'ambiente R locale in modo che è possibile visualizzarlo nel client di R.

    > [!NOTE]
    > Se si usa SQL Server in una macchina virtuale di Azure, si potrebbe ottenere un errore a questo punto. Si verifica un errore quando la regola del firewall predefinite in Azure blocca l'accesso alla rete dal codice R. Per informazioni dettagliate su come risolvere questo errore, vedere [(R) servizi di installazione di Machine Learning in una VM Azure](../install/sql-machine-learning-azure-virtual-machine.md).

4. La figura seguente mostra il tracciato di output. I punti di inizio corsa dei taxi vengono aggiunti alla mappa come punti rossi. L'immagine potrebbe apparire diverso, a seconda di quanti percorsi inclusi tra l'origine dati usata.

    ![creazione del tracciato delle corse in taxi con una funzione R personalizzata](media/rsql-e2e-mapplot.png "creazione del tracciato delle corse in taxi con una funzione R personalizzata")

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Creare funzionalità di dati con R e SQL](walkthrough-create-data-features.md)
