---
title: Gestire notebook in Azure Data Studio
titleSuffix: SQL Server big data clusters
description: Informazioni su come gestire notebook in Azure Data Studio, inclusi l'apertura di un notebook, il relativo salvataggio e la modifica della connessione del cluster Big Data.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5417166ea69abe726f47b6bf2adede4b937d5b00
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/25/2019
ms.locfileid: "67958285"
---
# <a name="how-to-manage-notebooks-in-azure-data-studio"></a>Come gestire notebook in Azure Data Studio

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo descrive come aprire e salvare file di notebook in Azure Data Studio con SQL Server 2019 (anteprima). Illustra inoltre come modificare la connessione al cluster Big Data di SQL Server.

## <a name="prerequisites"></a>Prerequisites

Questo articolo presuppone che si disponga già di un notebook che si vuole usare in Azure Data Studio. Se si vuole creare un notebook, vedere [Come usare i notebook in SQL Server 2019 (anteprima)](notebooks-guidance.md). Per poter usare i notebook in Azure Data Studio, è necessario soddisfare i prerequisiti seguenti:

- [Distribuire un cluster Big Data](quickstart-big-data-cluster-deploy.md).
- [Strumenti per Big Data di SQL Server 2019](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **Estensione di SQL Server 2019**
   - **kubectl**

## <a name="open-a-notebook"></a>Aprire un notebook

Sono disponibili vari modi per aprire la finestra di dialogo **Open Notebook** (Apri notebook): è possibile usare il menu file, il dashboard e il riquadro comandi. Nelle sezioni seguenti vengono descritti i vari metodi.

### <a name="file-menu"></a>Menu File

Selezionare **Apri file** dal menu File: CTRL + O (in Windows) e Cmd+O (in Mac).

![Aprire la finestra di dialogo Apri file selezionando Apri file](./media/notebooks-how-to-manage/open-file-1.png) 

### <a name="dashboard"></a>Dashboard

Fare clic su **Open Notebook** (Apri notebook) nel dashboard per aprire la finestra di dialogo Apri file.

![Aprire la finestra di dialogo Apri file selezionando Open Notebook (Apri notebook) nel dashboard](./media/notebooks-how-to-manage/open-file-2.png) 

### <a name="command-palette"></a>Riquadro comandi

Usare il comando **File: Aprire**  dal riquadro comandi digitando CTRL+MAIUSC+P (in Windows) o CMD+MAIUSC+P (in Mac).

![Aprire la finestra di dialogo Apri file digitando File:Apri nel riquadro comandi](./media/notebooks-how-to-manage/open-file-3.png)

## <a name="save-a-notebook"></a>Salvare un notebook

È attualmente disponibile un solo modo per salvare un notebook. È necessario selezionare **Salva** dalla barra degli strumenti del notebook.

![Salvare il file facendo clic su Salva sulla barra degli strumenti del notebook](./media/notebooks-how-to-manage/save-file-1.png)

> [!NOTE]
> I metodi seguenti non consentono attualmente di salvare modifiche sui notebook:
>
> - Comandi **Salva file**, **Salva file con nome...** e **Salva tutto** dal menu File.
> - Comando **File: Salva** immessi nel riquadro comandi.

## <a name="change-the-big-data-cluster"></a>Modificare il cluster Big Data

Per modificare il cluster Big Data di SQL Server per un notebook:

1. Fare clic sul menu **Associa a** sulla barra degli strumenti del notebook.

   ![Fare clic sul menu "Associa a" sulla barra degli strumenti del notebook](./media/notebooks-how-to-manage/select-attach-to-1.png)

2. Scegliere un server dal menu **Associa a**.

   ![Selezionare un server dal menu Associa a.](./media/notebooks-how-to-manage/select-attach-to-2.png)

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui notebook in Azure Data Studio, vedere [Come usare i notebook nella versione di anteprima di SQL Server 2019](notebooks-guidance.md).