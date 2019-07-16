---
title: Gestire i notebook in Azure Data Studio
titleSuffix: SQL Server big data clusters
description: Informazioni su come gestire i notebook in Azure Data Studio. Ciò include l'apertura di notebook, essi un notevole risparmio e modificando la connessione di cluster di big data.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5417166ea69abe726f47b6bf2adede4b937d5b00
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67958285"
---
# <a name="how-to-manage-notebooks-in-azure-data-studio"></a>Come gestire i notebook in Azure Data Studio

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo illustra come aprire e salvare i file di notebook in Azure Data Studio con l'anteprima di SQL Server 2019. Viene inoltre illustrato come modificare la connessione al cluster SQL Server i big Data.

## <a name="prerequisites"></a>Prerequisiti

Questo articolo presuppone che si disponga già di un notebook che si desidera usare in Azure Data Studio. Se si desidera creare un notebook, vedere [come usare i notebook in fase di anteprima di SQL Server 2019](notebooks-guidance.md). Per usare i notebook in Azure Data Studio, è necessario soddisfare i prerequisiti seguenti:

- [Distribuire un cluster di big data](quickstart-big-data-cluster-deploy.md).
- [Strumenti di big data di SQL Server 2019](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **Estensione di SQL Server 2019**
   - **kubectl**

## <a name="open-a-notebook"></a>Apre un notebook

Esistono diversi modi per aprire la **aprire Notebook** finestra di dialogo. È possibile usare il menu File, il Dashboard e il riquadro comandi. Le sezioni seguenti descrivono ogni metodo.

### <a name="file-menu"></a>Menu file

Selezionare **Apri File** dal menu File Cmd + O (nel Mac) e Ctrl + O (in Windows).

![Aprire la finestra di dialogo Apri File selezionare Apri File](./media/notebooks-how-to-manage/open-file-1.png) 

### <a name="dashboard"></a>dashboard

Fare clic su **aprire Notebook** nel dashboard per aprire la finestra di dialogo Apri File.

![Aprire la finestra di dialogo Apri File selezionare aprire Notebook nel dashboard](./media/notebooks-how-to-manage/open-file-2.png) 

### <a name="command-palette"></a>Riquadro comandi

Usare comandi **File: Apri** nel riquadro comandi digitando Cmd + MAIUSC + P (nel Mac) e Ctrl + MAIUSC + P (in Windows).

![Aprire la finestra di dialogo Apri File immettendo File:Open nel riquadro comandi](./media/notebooks-how-to-manage/open-file-3.png)

## <a name="save-a-notebook"></a>Salva un notebook

È attualmente un modo per salvare un notebook. È necessario selezionare **salvare** nella barra degli strumenti del blocco appunti.

![Salva File, fare clic su Salva nella barra degli strumenti del blocco appunti](./media/notebooks-how-to-manage/save-file-1.png)

> [!NOTE]
> I metodi seguenti attualmente non salvano le modifiche ai blocchi appunti:
>
> - **Salva file**, **Salva File con nome...**  e **File Salva tutto** comandi dal menu File.
> - **File: Salvare** comandi immessi nel riquadro comandi.

## <a name="change-the-big-data-cluster"></a>Modificare i cluster di big data

Per modificare i cluster di big data di SQL Server per un notebook:

1. Fare clic sui **Collega a** menu nella barra degli strumenti del blocco appunti.

   ![Fare clic su Connetti a menu sulla barra degli strumenti del blocco appunti](./media/notebooks-how-to-manage/select-attach-to-1.png)

2. Fare clic su un server dal **Collega a** menu.

   ![Selezionare un server dal collegamento al menu](./media/notebooks-how-to-manage/select-attach-to-2.png)

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su notebook in Azure Data Studio, vedere [come usare i notebook in fase di anteprima di SQL Server 2019](notebooks-guidance.md).