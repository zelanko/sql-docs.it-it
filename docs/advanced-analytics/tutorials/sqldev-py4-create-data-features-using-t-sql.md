---
title: Creare funzionalità di dati mediante le funzioni T-SQL e Python, SQL Server Machine Learning
description: Esercitazione che illustra come aggiungere calcoli per le stored procedure per l'utilizzo in modelli di Python di machine learning.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/01/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: dccc9afa9961d5ce8f2e9de75b4e8b34f28e0438
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58513358"
---
# <a name="create-data-features-using-t-sql"></a>Creare funzionalità di dati mediante T-SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Dopo l'esplorazione dei dati, si sono raccolte alcune informazioni dettagliate dai dati e si è pronti per passare alla *progettazione di funzionalità*. Questo processo di creazione di funzionalità da dati non elaborati può essere un passaggio critico nella analitica avanzata di modellazione.

Questo articolo fa parte di un'esercitazione [analitica di Python nel database per sviluppatori SQL](sqldev-in-database-python-for-sql-developers.md). 

In questo passaggio si apprenderà come creare funzionalità dai dati non elaborati tramite una funzione [!INCLUDE[tsql](../../includes/tsql-md.md)] . Tale funzione verrà quindi chiamata da una stored procedure per creare una tabella contenente i valori della funzionalità.

## <a name="define-the-function"></a>Definire la funzione

I valori di distanza inclusi nei dati originali si basano sulla distanza registrata dal tassametro e non rappresentano necessariamente la distanza geografica o la distanza percorsa. Pertanto è necessario calcolare la distanza diretta tra i punti di inizio e fine della corsa, usando le coordinate disponibili nel set di dati di origine NYC Taxi. È possibile farlo usando la [formula dell'emisenoverso](https://en.wikipedia.org/wiki/Haversine_formula) in una funzione [!INCLUDE[tsql](../../includes/tsql-md.md)] personalizzata.

Si userà una funzione T-SQL personalizzata, _fnCalculateDistance_, per calcolare la distanza con la formula dell'emisenoverso e una seconda funzione T-SQL personalizzata, _fnEngineerFeatures_, per creare una tabella contenente tutte le funzionalità.

### <a name="calculate-trip-distance-using-fncalculatedistance"></a>Calcolare distanza della corsa mediante fnCalculateDistance

1.  La funzione _fnCalculateDistance_ va scaricata e registrata con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] come parte della preparazione per questa procedura dettagliata. È opportuno esaminare il codice.
  
    In [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]espandere **Programmabilità**, **Funzioni** e quindi **Funzioni a valori scalari**.
    Fare clic con il pulsante destro del mouse su _fnCalculateDistance_e selezionare **Modifica** per aprire lo script [!INCLUDE[tsql](../../includes/tsql-md.md)] in una nuova finestra Query.
  
    ```sql
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)
    -- User-defined function that calculates the direct distance between two geographical coordinates
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
**Note:**

- La funzione è una funzione con valori scalari che restituisce un singolo valore di dati di un tipo predefinito.
- Accetta come input valori di latitudine e longitudine, ottenuti dalle località di inizio e fine della corsa. La formula dell'emisenoverso converte le posizioni in radianti e usa tali valori per calcolare la distanza diretta in miglia tra queste due posizioni.

Per aggiungere il valore calcolato a una tabella da usare per il training del modello è possibile usare un'altra funzione, _fnEngineerFeatures_.

### <a name="save-the-features-using-fnengineerfeatures"></a>Salvare le funzionalità con _fnEngineerFeatures_

1.  Osservare il codice della funzione T-SQL personalizzata _fnEngineerFeatures_, creata in preparazione a questa procedura dettagliata.
  
    È una funzione con valori di tabella che accetta come input più colonne e restituisce una tabella con più colonne di funzionalità.  Lo scopo della funzione è la creazione di un set di funzionalità da usare per la compilazione di un modello. La funzione _fnEngineerFeatures_ chiama la funzione T-SQL _fnCalculateDistance_creata in precedenza per ottenere la distanza diretta tra i punti di inizio e fine della corsa.
  
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
  
2. Per verificare che la funzione operi in modo corretto è possibile usarla per calcolare la distanza geografica per i viaggi in cui la distanza sul tassametro era pari a 0 ma i punti di inizio e fine corsa erano diversi.
  
    ```sql
        SELECT tipped, fare_amount, passenger_count,(trip_time_in_secs/60) as TripMinutes,
        trip_distance, pickup_datetime, dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) AS direct_distance
        FROM nyctaxi_sample
        WHERE pickup_longitude != dropoff_longitude and pickup_latitude != dropoff_latitude and trip_distance = 0
        ORDER BY trip_time_in_secs DESC
    ```
  
    Come si può notare, la distanza indicata dal tassametro non corrisponde sempre alla distanza geografica. Ecco perché la progettazione di funzionalità è importante.

Nel passaggio successivo si apprenderà come usare queste funzionalità di dati per creare ed eseguire il training di un modello di machine learning tramite Python.

## <a name="next-step"></a>Passaggio successivo

[Eseguire il training e salvataggio di un modello Python con T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="previous-step"></a>Passaggio precedente

[Esplorare e visualizzare i dati](sqldev-py3-explore-and-visualize-the-data.md)


