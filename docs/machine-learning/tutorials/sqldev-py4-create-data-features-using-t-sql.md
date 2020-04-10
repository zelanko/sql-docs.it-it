---
title: 'Python + T-SQL: Caratteristiche dei dati'
description: Esercitazione che illustra come aggiungere calcoli alle stored procedure per l'uso nei modelli di Machine Learning Python.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/01/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: eb7f7b271c49922698058e396b69b91444c5b65a
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/04/2020
ms.locfileid: "81115924"
---
# <a name="create-data-features-using-t-sql"></a>Creare caratteristiche dei dati usando T-SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Dopo l'esplorazione dei dati sono state raccolte alcune informazioni dettagliate e si è pronti a passare alla *progettazione delle caratteristiche*. Questo processo di creazione di caratteristiche dai dati non elaborati è un passaggio critico nella modellazione dell'analisi avanzata.

Questo articolo fa parte dell'esercitazione [Analisi Python nel database per sviluppatori SQL](sqldev-in-database-python-for-sql-developers.md). 

In questo passaggio si apprenderà come creare funzionalità dai dati non elaborati tramite una funzione [!INCLUDE[tsql](../../includes/tsql-md.md)] . Tale funzione verrà quindi chiamata da una stored procedure per creare una tabella contenente i valori della funzionalità.

## <a name="define-the-function"></a>Definire la funzione

I valori di distanza inclusi nei dati originali si basano sulla distanza registrata dal tassametro e non rappresentano necessariamente la distanza geografica o la distanza percorsa. Pertanto è necessario calcolare la distanza diretta tra i punti di inizio e fine della corsa, usando le coordinate disponibili nel set di dati di origine NYC Taxi. È possibile farlo usando la [formula dell'emisenoverso](https://en.wikipedia.org/wiki/Haversine_formula) in una funzione [!INCLUDE[tsql](../../includes/tsql-md.md)] personalizzata.

Si userà una funzione T-SQL personalizzata, _fnCalculateDistance_, per calcolare la distanza con la formula dell'emisenoverso e una seconda funzione T-SQL personalizzata, _fnEngineerFeatures_, per creare una tabella contenente tutte le funzionalità.

### <a name="calculate-trip-distance-using-fncalculatedistance"></a>Calcolare la distanza della corsa usando fnCalculateDistance

1.  La funzione _fnCalculateDistance_ va scaricata e registrata con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] come parte della preparazione per questa procedura dettagliata. Dedicare un attimo di tempo a esaminare il codice.
  
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

### <a name="save-the-features-using-_fnengineerfeatures_"></a>Salvare le caratteristiche usando _fnEngineerFeatures_

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
  
    Come si può notare, la distanza indicata dal tassametro non corrisponde sempre alla distanza geografica. È per questo che la progettazione delle caratteristiche è importante.

Nel passaggio successivo si apprenderà come usare queste caratteristiche dei dati per la creazione e il training di un modello di Machine Learning con Python.

## <a name="next-step"></a>Passaggio successivo

[Eseguire il training e il salvataggio di un modello Python usando T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="previous-step"></a>Passaggio precedente

[Esplorare e visualizzare i dati](sqldev-py3-explore-and-visualize-the-data.md)


