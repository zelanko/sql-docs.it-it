---
title: Eseguire stime con l'estensione Machine Learning
titleSuffix: Azure Data Studio
description: Informazioni su come usare l'estensione Machine Learning per Azure Data Studio per eseguire stime con un modello ONNX nel database.
ms.date: 06/09/2020
ms.reviewer: sstein
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 5472f4ff32a807b58091fd56f3382aa73ead142e
ms.sourcegitcommit: dc8a30a4a27e15fc6671ca2674da9b7c637ec255
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2020
ms.locfileid: "88745491"
---
# <a name="make-predictions-with-machine-learning-extension-preview-for-azure-data-studio"></a>Eseguire stime con l'estensione Machine Learning (anteprima) per Azure Data Studio

Informazioni su come usare l'[estensione Machine Learning per Azure Data Studio](machine-learning-extension.md) per eseguire stime con un modello ONNX nel database. L'estensione genera uno script T-SQL tramite l'istruzione [PREDICT](../t-sql/queries/predict-transact-sql.md) per eseguire stime sul set di dati archiviato nella tabella con un modello importato in precedenza, che risiede in un file locale o proveniente da Azure Machine Learning.

> [!IMPORTANT]
> L'esecuzione di stime con l'estensione Machine Learning supporta attualmente solo [Machine Learning Services in Istanza gestita di SQL di Azure](/azure/azure-sql/managed-instance/machine-learning-services-overview) e [SQL Edge di Azure con ONNX](/azure/azure-sql-edge/onnx-overview).

## <a name="prerequisites"></a>Prerequisiti

- Installare e configurare l'[estensione Machine Learning per Azure Data Studio](machine-learning-extension.md). È necessario specificare i [percorsi di installazione di Python in Impostazioni estensione](machine-learning-extension.md#settings).

- I pacchetti Python **onnxruntime**, **mlflow** e **mlflow-dbstore**. Se i pacchetti non sono ancora installati, l'estensione Machine Learning richiederà di installarli.

## <a name="make-predictions-from-onnx-model"></a>Eseguire stime dal modello ONNX

Attenersi alla procedura seguente per usare un modello ONNX per eseguire stime.

1. Fare clic su **Make predictions** (Esegui stime).

1. Se viene richiesto di installare **onnxruntime**, **mlflow**e **mlflow-dbstore**, fare clic su **Sì**.

1. Scegliere la posizione del modello e fare clic su **Avanti**. È possibile usare:
    - **Modelli importati**. Scegliere questa opzione per usare un modello già archiviato nel database. Scegliere il **database** e la **tabella** in cui si trova il modello, selezionare il modello che si vuole usare e fare clic su **Avanti**.
    - **Caricamento file**. Scegliere questa opzione per usare un modello da un file. Selezionare il file di modello in **File di origine** e fare clic su **Avanti**.
    - **Azure Machine Learning**. Scegliere questa opzione per usare un modello proveniente da Azure Machine Learning. Per prima cosa, **accedere ad Azure**. Selezionare quindi l'**account**, la **sottoscrizione**, il **gruppo di risorse** e l'**area di lavoro ML** di Azure. Selezionare il modello che si vuole usare e fare clic su **Avanti**.

1. Eseguire il mapping dei dati di origine al modello.
    - Selezionare il **database di origine** e la **tabella di origine** contenenti il set di dati a cui si vuole applicare la stima.
    - Eseguire il mapping delle colonne in **Model Input mapping** (Mapping input modello) e **Model output** (Output modello). L'estensione eseguirà automaticamente il mapping delle colonne con lo stesso nome e lo stesso tipo di dati.

1. Fare clic su **Stima**.

Azure Data Studio creerà una nuova query T-SQL con l'istruzione [PREDICT](../t-sql/queries/predict-transact-sql.md), utilizzabile per eseguire stime sui dati.

## <a name="next-steps"></a>Passaggi successivi

- [Estensione Machine Learning in Azure Data Studio](machine-learning-extension.md)
- [Gestire i pacchetti nel database](machine-learning-extension-manage-packages.md)
- [Importare o visualizzare modelli](machine-learning-extension-import-view-models.md)
- [Notebook in Azure Data Studio](notebooks-guidance.md)
- [Documentazione per Machine Learning in SQL](../machine-learning/index.yml)
- [Machine Learning Services in Istanza gestita di SQL di Azure](/azure/azure-sql/managed-instance/machine-learning-services-overview)
- [Machine Learning e intelligenza artificiale con ONNX in SQL Edge (anteprima)](/azure/azure-sql-edge/onnx-overview)
