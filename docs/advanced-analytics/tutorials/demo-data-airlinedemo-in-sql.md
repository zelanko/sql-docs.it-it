---
title: Set di dati dimostrativo dei voli delle compagnie aeree per SQL Server Python e R - esercitazioni di SQL Server Machine Learning
Description: Creare un database che contiene il set di dati relativi alle compagnie aeree da R e Python. Questo set di dati viene utilizzata negli esercizi che illustra come eseguire il wrapping di codice Python o linguaggio R in una stored procedure SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/22/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: d317053721d3c3288e58bcfbd467bb282020db48
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962128"
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
