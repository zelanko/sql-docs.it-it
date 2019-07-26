---
title: Set di dati della Demo Flight Airline per SQL Server esercitazioni su Python e R
Description: Creare un database contenente il set di dati della compagnia aerea da R e Python. Questo set di dati viene usato in esercizi che illustrano come eseguire il wrapping del linguaggio R o del codice Python in un SQL Server stored procedure.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/22/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 38e61bcbf3a5ff5ed44f85d5ad28406550e5a726
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469678"
---
#  <a name="airline-flight-arrival-demo-data-for-sql-server-python-and-r-tutorials"></a>Dati dimostrativi di arrivo del volo aereo per SQL Server esercitazioni su Python e R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

In questo esercizio viene creato un database di SQL Server per archiviare i dati importati da set di dati demo della compagnia aerea incorporata di R o Python. Le distribuzioni R e Python forniscono dati equivalenti, che è possibile importare in un database di SQL Server usando Management Studio.

Per completare questo esercizio, è necessario disporre di [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017) o un altro strumento in grado di eseguire query T-SQL.

Le esercitazioni e le guide introduttive che usano questo set di dati includono quanto segue:

+  [Creare un modello Python usando revoscalepy](use-python-revoscalepy-to-create-model.md)

## <a name="create-the-database"></a>Creare il database

1. Avviare SQL Server Management Studio, connettersi a un'istanza del motore di database con integrazione R o Python.  

2. In Esplora oggetti fare clic con il pulsante destro del mouse su **database** e creare un nuovo database denominato **FlightData**.

3. Fare clic con il pulsante destro del mouse su **FlightData**, scegliere **attività**, quindi **Importa file flat**.

4. Aprire il file AirlineDemoData. CSV fornito nella distribuzione di R o Python, a seconda della lingua installata.

   Per R, cercare **AirlineDemoSmall. csv** in C:\Programmi\Microsoft SQL Server\MSSQL14. MSSQLSERVER\R_SERVICES\library\RevoScaleR\SampleData
   
   Per Python, cercare **AirlineDemoSmall. csv** in C:\Programmi\Microsoft SQL Server\MSSQL14. MSSQLSERVER\PYTHON_SERVICES\Lib\site-packages\revoscalepy\data\sample_data
  
Quando si seleziona il file, i valori predefiniti vengono inseriti per nome tabella e schema.

  ![Importazione guidata file flat che mostra le impostazioni predefinite delle demo aeree](media/import-airlinedemosmall.png)

Fare clic sulle pagine rimanenti, accettando le impostazioni predefinite, per importare i dati.


## <a name="query-the-data"></a>Eseguire query sui dati

Come passaggio di convalida, eseguire una query per confermare che i dati sono stati caricati.

1. In Esplora oggetti, in database, fare clic con il pulsante destro del mouse sul database **FlightData** e avviare una nuova query.

2. Eseguire alcune query semplici:

    ```sql
    SELECT TOP(10) * FROM AirlineDemoSmall;
    SELECT COUNT(*) FROM AirlineDemoSmall;
    ```

## <a name="next-steps"></a>Passaggi successivi

Nella lezione seguente verrà creato un modello di regressione lineare basato su questi dati.

+ [Creare un modello Python usando revoscalepy](use-python-revoscalepy-to-create-model.md)
