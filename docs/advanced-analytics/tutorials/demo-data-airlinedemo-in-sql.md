---
title: Set di dati dimostrativo dei voli delle compagnie aeree per SQL Server Python e R - esercitazioni di SQL Server Machine Learning
Description: Create a database containing the Airline dataset from R and Python. This dataset is used in exercises showing how to wrap R language or Python code in a SQL Server stored procedure.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/22/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 10d2f013c103dee3de02335ca2acf82d4320b623
ms.sourcegitcommit: 33712a0587c1cdc90de6dada88d727f8623efd11
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/19/2018
ms.locfileid: "53596982"
---
#  <a name="airline-flight-arrival-demo-data-for-sql-server-python-and-r-tutorials"></a>Dati di demo arrivo dei voli delle compagnie aeree per le esercitazioni di SQL Server Python e R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

In questo esercizio, creare un database di SQL Server per archiviare i dati importati da R o Python incorporato Airline demo set di dati. Distribuzioni di R e Python forniscono dati equivalenti, che è possibile importare in un database di SQL Server usando Management Studio.

Per completare questo esercizio, è necessario disporre [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017) o un altro strumento che è possibile eseguire query T-SQL.

Esercitazioni e guide introduttive utilizzano questo set di dati seguenti:

+  [Creare un modello Python usando revoscalepy](use-python-revoscalepy-to-create-model.md)

## <a name="create-the-database"></a>Creare il database

1. Avviare SQL Server Management Studio, connettersi a un'istanza di motore di database che include l'integrazione di R o Python.  

2. In Esplora oggetti fare doppio clic su **database** e creare un nuovo database denominato **flightdata**.

3. Fare doppio clic su **flightdata**, fare clic su **attività**, fare clic su **Importa File Flat**.

4. Aprire il file AirlineDemoData.csv fornito nella distribuzione di R o Python, a seconda del linguaggio è stato installato.

   Per R, cercare **AirlineDemoSmall.csv** in C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\R_SERVICES\library\RevoScaleR\SampleData
   
   Per Python, cercare **AirlineDemoSmall.csv** in C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\PYTHON_SERVICES\Lib\site packages\revoscalepy\data\sample_data
  
Quando si seleziona il file, i valori predefiniti vengono compilati per lo schema e nome della tabella.

  ![Importazione guidata file flat che mostra le impostazioni predefinite di airline demo](media/import-airlinedemosmall.png)

Scegliere tra le pagine rimanenti, accettare le impostazioni predefinite, per importare i dati.


## <a name="query-the-data"></a>Eseguire query sui dati

Come passaggio di convalida, eseguire una query per verificare che i dati è stati caricati.

1. In Esplora oggetti, nel database, fare doppio clic il **flightdata** , del database e avviare una nuova query.

2. Eseguire alcune semplici query:

    ```sql
    SELECT TOP(10) * FROM AirlineDemoSmall;
    SELECT COUNT(*) FROM AirlineDemoSmall;
    ```

## <a name="next-steps"></a>Passaggi successivi

Nella lezione seguente si creerà un modello di regressione lineare basato su tali dati.

+ [Creare un modello Python usando revoscalepy](use-python-revoscalepy-to-create-model.md)
