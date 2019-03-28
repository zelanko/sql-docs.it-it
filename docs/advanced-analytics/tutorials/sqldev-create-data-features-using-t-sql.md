---
title: Funzionalità di dati crea lezione 2 usando funzioni R e T-SQL - SQL Server Machine Learning
description: Esercitazione che illustra come aggiungere calcoli per le stored procedure per l'utilizzo in modelli di machine learning R.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/19/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 32f762de13a844f12144e89f4742409c3afcbab0
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58511968"
---
# <a name="lesson-2-create-data-features-using-r-and-t-sql"></a>Lezione 2: Creare funzionalità di dati con R e T-SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo fa parte di un'esercitazione per sviluppatori SQL su come usare R in SQL Server.

In questo passaggio si apprenderà come creare funzionalità dai dati non elaborati tramite una funzione [!INCLUDE[tsql](../../includes/tsql-md.md)] . Tale funzione verrà quindi chiamata da una stored procedure per creare una tabella contenente i valori della funzionalità.

## <a name="about-feature-engineering"></a>Sulla progettazione di funzionalità

Dopo varie sessioni di esplorazione dei dati si sono raccolte alcune informazioni relative ai dati e si è pronti a passare alla *progettazione di funzionalità*. Questo processo di creazione di funzionalità significative dai dati non elaborati è un passaggio critico nella creazione di modelli analitici.

In questo set di dati, i valori di distanza sono basati sul tassametro e non rappresentano necessariamente la distanza geografica o la distanza effettiva percorsa. Pertanto è necessario calcolare la distanza diretta tra i punti di inizio e fine della corsa, usando le coordinate disponibili nel set di dati di origine NYC Taxi. È possibile farlo usando la [formula dell'emisenoverso](https://en.wikipedia.org/wiki/Haversine_formula) in una funzione [!INCLUDE[tsql](../../includes/tsql-md.md)] personalizzata.

Si userà una funzione T-SQL personalizzata, _fnCalculateDistance_, per calcolare la distanza con la formula dell'emisenoverso e una seconda funzione T-SQL personalizzata, _fnEngineerFeatures_, per creare una tabella contenente tutte le funzionalità.

Il processo complessivo è come segue:

- Creare la funzione T-SQL che esegue i calcoli

- Chiamare la funzione per generare i dati della funzionalità

- Salvare i dati della funzionalità in una tabella

## <a name="calculate-trip-distance-using-fncalculatedistance"></a>Calcolare distanza della corsa mediante fnCalculateDistance

La funzione _fnCalculateDistance_ deve avere scaricata e registrata con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] come parte della preparazione per questa esercitazione. È opportuno esaminare il codice.
  
1. In [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]espandere **Programmabilità**, **Funzioni** e quindi **Funzioni a valori scalari**.   

2. Fare clic con il pulsante destro del mouse su _fnCalculateDistance_e selezionare **Modifica** per aprire lo script [!INCLUDE[tsql](../../includes/tsql-md.md)] in una nuova finestra Query.
  
    ```sql
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)  
    -- User-defined function that calculates the direct distance between two geographical coordinates.  
    RETURNS float  
    AS  
    BEGIN  
      DECLARE @distance decimal(28, 10)  
      -- Convert to radians  
      SET @Lat1 = @Lat1 / 57.2958  
      SET @Long1 = @Long1 / 57.2958  
      SET @Lat2 = @Lat2 / 57.2958  
      SET @Long2 = @Long2 / 57.2958  
      -- Calculate distance  
      SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))  
      --Convert to miles  
      IF @distance <> 0  
      BEGIN  
        SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);  
      END  
      RETURN @distance  
    END
    GO
    ```
  
    - La funzione è una funzione con valori scalari che restituisce un singolo valore di dati di un tipo predefinito.
  
    - Accetta come input valori di latitudine e longitudine, ottenuti dalle località di inizio e fine della corsa. La formula dell'emisenoverso converte le posizioni in radianti e usa tali valori per calcolare la distanza diretta in miglia tra queste due posizioni.

## <a name="generate-the-features-using-fnengineerfeatures"></a>Generare le funzionalità usando _fnEngineerFeatures_

Per aggiungere i valori calcolati in una tabella che può essere usata per il training del modello, si userà un'altra funzione, _fnEngineerFeatures_. La nuova funzione chiama la funzione T-SQL creata in precedenza _fnCalculateDistance_, per ottenere la distanza diretta tra le posizioni e fine della corsa. 

1. Osservare il codice della funzione T-SQL personalizzata _fnEngineerFeatures_, creata in preparazione a questa procedura dettagliata.
  
    ```sql
    CREATE FUNCTION [dbo].[fnEngineerFeatures] (  
    @passenger_count int = 0,  
    @trip_distance float = 0,  
    @trip_time_in_secs int = 0,  
    @pickup_latitude float = 0,  
    @pickup_longitude float = 0,  
    @dropoff_latitude float = 0,  
    @dropoff_longitude float = 0)  
    RETURNS TABLE  
    AS
      RETURN
      (
      -- Add the SELECT statement with parameter references here
      SELECT
        @passenger_count AS passenger_count,
        @trip_distance AS trip_distance,
        @trip_time_in_secs AS trip_time_in_secs,
        [dbo].[fnCalculateDistance](@pickup_latitude, @pickup_longitude, @dropoff_latitude, @dropoff_longitude) AS direct_distance
  
      )
    GO
    ```

    + Questa funzione con valori di tabella che accetta come input più colonne e restituisce una tabella con più colonne di funzionalità.

    + Lo scopo di questa funzione consiste nel creare nuove funzionalità per l'uso nella creazione di un modello.

2.  Per verificare che questa funzione funziona, usarlo per calcolare la distanza geografica per i viaggi in cui la distanza a consumo è 0 ma le posizioni di inizio e fine corsa erano diverse.
  
    ```sql
        SELECT tipped, fare_amount, passenger_count,(trip_time_in_secs/60) as TripMinutes,
        trip_distance, pickup_datetime, dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) AS direct_distance
        FROM nyctaxi_sample
        WHERE pickup_longitude != dropoff_longitude and pickup_latitude != dropoff_latitude and trip_distance = 0
        ORDER BY trip_time_in_secs DESC
    ```
  
    Come si può notare, la distanza indicata dal tassametro non corrisponde sempre alla distanza geografica. Ecco perché la progettazione delle funzionalità è così importante. È possibile usare queste funzionalità di dati migliorate per il training di un modello di machine learning tramite R.

## <a name="next-lesson"></a>Lezione successiva

[Lezione 3: Eseguire il training e salvataggio di un modello usando T-SQL](sqldev-train-and-save-a-model-using-t-sql.md)

## <a name="previous-lesson"></a>Lezione precedente

[Lezione 1: Esplorare e visualizzare i dati usando R e le stored procedure](sqldev-explore-and-visualize-the-data.md)
