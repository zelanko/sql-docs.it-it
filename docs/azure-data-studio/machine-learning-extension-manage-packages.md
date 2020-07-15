---
title: Gestire pacchetti con l'estensione Machine Learning
titleSuffix: Azure Data Studio
description: Informazioni su come gestire i pacchetti Python o R nel database con l'[estensione Machine Learning per Azure Data Studio.
ms.date: 05/19/2020
ms.reviewer: sstein
ms.prod: azure-data-studio
ms.technology: machine-learning
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 234c7493852afb4667f9c97b2cb4bb81e119af63
ms.sourcegitcommit: 48d60fe6b6991303a88936fb32322c005dfca2d8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/25/2020
ms.locfileid: "85352398"
---
# <a name="manage-packages-in-database-with-machine-learning-extension-preview-for-azure-data-studio"></a>Gestire i pacchetti nel database con l'estensione Machine Learning (anteprima) per Azure Data Studio

Informazioni su come gestire i pacchetti Python o R nel database con l'[estensione Machine Learning per Azure Data Studio](machine-learning-extension.md).

> [!IMPORTANT]
> La gestione dei pacchetti nel database con l'estensione Machine Learning supporta attualmente solo [Machine Learning Services](../machine-learning/sql-server-machine-learning-services.md) in SQL Server 2019.

## <a name="prerequisites"></a>Prerequisiti

- Installare e configurare l'[estensione Machine Learning per Azure Data Studio](machine-learning-extension.md). Per consentire il funzionamento della gestione dei pacchetti, è necessario specificare i [percorsi di installazione di Python o R in Impostazioni estensione](machine-learning-extension.md#settings).

- Pacchetto **sqlmlutils**. Se il pacchetto non è ancora installato, l'estensione Machine Learning richiederà di installarlo.

- Per SQL Server in Linux, l'autenticazione di Windows non è supportata. Per connettersi a SQL Server in Linux, è quindi necessario usare l'autenticazione SQL.

## <a name="manage-python-packages"></a>Gestire pacchetti Python

È possibile installare e disinstallare pacchetti Python con l'estensione Machine Learning.

### <a name="install-new-python-package"></a>Installare nuovi pacchetti Python

Attenersi alla procedura seguente per installare pacchetti Python nel database.

1. Fare clic su **Manage packages in database** (Gestisci pacchetti nel database).

1. Se viene richiesto di installare **sqlmlutils**, fare clic su **Sì**.

1. Nella scheda **Installati** selezionare **Python** in **Tipo di pacchetto** e selezionare il database in **Posizione**.

1. Fare clic sulla scheda **Aggiungi nuovo**.

1. Immettere il pacchetto Python che si vuole installare in **Search Python packages** (Cerca pacchetti Python) e fare clic su **Cerca**.

1. Verificare che il pacchetto sia presente in **Nome del pacchetto** e che la versione desiderata sia presente in **Versione del pacchetto**.

1. Fare clic su **Installa**.

1. Fare clic su **Chiudi** e verificare che il pacchetto sia stato installato correttamente in **Attività**.

### <a name="uninstall-a-python-package"></a>Disinstallare un pacchetto Python

Attenersi alla procedura seguente per disinstallare pacchetti Python nel database.

> [!NOTE]
> È possibile disinstallare solo pacchetti che sono stati installati nel database. Non è possibile disinstallare un pacchetto preinstallato con SQL Server Machine Learning Services.

1. Fare clic su **Manage packages in database** (Gestisci pacchetti nel database).

1. Se viene richiesto di installare **sqlmlutils**, fare clic su **Sì**.

1. Nella scheda **Installati** selezionare **Python** in **Tipo di pacchetto** e selezionare il database in **Posizione**.

1. Selezionare i pacchetti che si vogliono disinstallare.

1. Fare clic su **Disinstalla i pacchetti selezionati**.

1. Fare clic su **Chiudi** e verificare che il pacchetto sia stato installato correttamente in **Attività**.

## <a name="manage-r-packages"></a>Gestire pacchetti R

È possibile installare e disinstallare pacchetti R con l'estensione Machine Learning.

### <a name="install-new-r-package"></a>Installare un nuovo pacchetto R

Attenersi alla procedura seguente per installare pacchetti Python nel database.

1. Fare clic su **Manage packages in database** (Gestisci pacchetti nel database).

1. Se viene richiesto di installare **sqlmlutils**, fare clic su **Sì**.

1. Nella scheda **Installati** selezionare **R** in **Tipo di pacchetto** e selezionare il database in **Posizione**.

1. Fare clic sulla scheda **Aggiungi nuovo**.

1. Immettere il pacchetto R che si vuole installare in **Search R packages** (Cerca pacchetti R) e fare clic su **Cerca**.

1. Verificare che il pacchetto sia presente in **Nome del pacchetto** e che la versione desiderata sia presente in **Versione del pacchetto**.

1. Fare clic su **Installa**.

1. Fare clic su **Chiudi** e verificare che il pacchetto sia stato installato correttamente in **Attività**.

### <a name="uninstall-an-r-package"></a>Disinstallare un pacchetto R

Attenersi alla procedura seguente per disinstallare pacchetti R nel database.

> [!NOTE]
> È possibile disinstallare solo pacchetti che sono stati installati nel database. Non è possibile disinstallare un pacchetto preinstallato con SQL Server Machine Learning Services.

1. Fare clic su **Manage packages in database** (Gestisci pacchetti nel database).

1. Se viene richiesto di installare **sqlmlutils**, fare clic su **Sì**.

1. Nella scheda **Installati** selezionare **R** in **Tipo di pacchetto** e selezionare il database in **Posizione**.

1. Selezionare i pacchetti che si vogliono disinstallare.

1. Fare clic su **Disinstalla i pacchetti selezionati**.

1. Fare clic su **Chiudi** e verificare che il pacchetto sia stato installato correttamente in **Attività**.

## <a name="next-steps"></a>Passaggi successivi

- [Estensione Machine Learning in Azure Data Studio](machine-learning-extension.md)
- [Eseguire stime](machine-learning-extension-predictions.md)
- [Importare o visualizzare modelli](machine-learning-extension-import-view-models.md)
- [Notebook in Azure Data Studio](notebooks-guidance.md)
- [Documentazione per Machine Learning in SQL](../machine-learning/index.yml)
