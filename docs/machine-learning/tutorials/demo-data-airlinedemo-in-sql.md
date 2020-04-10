---
title: Dati demo di una compagnia aerea per le esercitazioni
Description: Creare un database contenente il set di dati della compagnia aerea da R e Python. Questo set di dati viene usato nelle esercitazioni di R e Python per Machine Learning Services per SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/22/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 9bb8d26acb21ff38725c6e993c0b6080a35410f1
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/04/2020
ms.locfileid: "81116684"
---
#  <a name="airline-flight-arrival-demo-data-for-sql-server-python-and-r-tutorials"></a>Dati demo sugli arrivi di una compagnia aerea per le esercitazioni su Python e R in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

In questo esercizio si creerà un database SQL Server in cui archiviare i dati importati dal set di dati demo della compagnia aerea incorporati in R o Python. Le distribuzioni R e Python forniscono dati equivalenti, che è possibile importare in un database SQL Server usando Management Studio.

Per completare questo esercizio, è necessario avere [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017) o un altro strumento in grado di eseguire query T-SQL.

Le esercitazioni e le guide di avvio rapido che usano questo set di dati includono:

+  [Creare un modello Python usando revoscalepy](use-python-revoscalepy-to-create-model.md)

## <a name="create-the-database"></a>Creare il database

1. Avviare SQL Server Management Studio e connettersi a un'istanza del motore di database con integrazione R o Python.  

2. In Esplora oggetti fare clic con il pulsante destro del mouse su **Database** e creare un nuovo database denominato **flightdata**.

3. Fare clic con il pulsante destro del mouse su **flightdata**, scegliere **Attività** e fare clic su **Importa file flat**.

4. Aprire il file AirlineDemoData.csv disponibile nella distribuzione R o Python, a seconda del linguaggio installato.

   Per R, cercare **AirlineDemoSmall.csv** in C:\Programmi\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR\SampleData
   
   Per Python, cercare **AirlineDemoSmall.csv** in C:\Programmi\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\Lib\site-packages\revoscalepy\data\sample_data
  
Quando si seleziona il file, per il nome della tabella e lo schema vengono visualizzati i valori predefiniti.

  ![Procedura guidata Importa file flat che illustra i valori demo predefiniti della compagnia aerea](media/import-airlinedemosmall.png)

Scorrere le pagine rimanenti, accettando le impostazioni predefinite, per importare i dati.


## <a name="query-the-data"></a>Eseguire una query sui dati

Come passaggio di convalida, eseguire una query per confermare che i dati sono stati caricati.

1. In Esplora oggetti fare clic con il pulsante destro del mouse sul database **flightdata** in Database e avviare una nuova query.

2. Eseguire alcune query semplici:

    ```sql
    SELECT TOP(10) * FROM AirlineDemoSmall;
    SELECT COUNT(*) FROM AirlineDemoSmall;
    ```

## <a name="next-steps"></a>Passaggi successivi

Nella lezione seguente verrà creato un modello di regressione lineare basato su questi dati.

+ [Creare un modello Python usando revoscalepy](use-python-revoscalepy-to-create-model.md)
