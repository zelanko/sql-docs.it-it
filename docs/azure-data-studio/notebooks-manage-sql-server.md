---
title: Gestire un notebook di SQL Server
description: Informazioni su come gestire notebook in Azure Data Studio, inclusi l'apertura di un notebook, il relativo salvataggio e la modifica della connessione del cluster Big Data.
author: markingmyname
ms.author: maghan
ms.reviewer: achatter, alayu, mikeray
ms.metadata: seo-lt-2019
ms.topic: conceptual
ms.prod: sql
ms.technology: azure-data-studio
ms.custom: ''
ms.date: 03/30/2020
ms.openlocfilehash: 9b071a9d1b9e770e1443e5df539208baa4399a30
ms.sourcegitcommit: 1124b91a3b1a3d30424ae0fec04cfaa4b1f361b6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/01/2020
ms.locfileid: "80531594"
---
# <a name="how-to-manage-notebooks-in-azure-data-studio"></a>Come gestire notebook in Azure Data Studio

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo descrive come aprire e salvare file di notebook in Azure Data Studio con SQL Server. Illustra anche come modificare la connessione a SQL Server.

## <a name="open-a-notebook"></a>Aprire un notebook

Sono disponibili vari modi per aprire la finestra di dialogo **Open Notebook** (Apri notebook): è possibile usare il menu file, il dashboard e il riquadro comandi. Nelle sezioni seguenti vengono descritti i vari metodi.

### <a name="file-menu"></a>Menu File

Selezionare **Apri file** dal menu File: CTRL + O (in Windows) e Cmd+O (in Mac).

![Aprire la finestra di dialogo Apri file selezionando Apri file](./media/notebooks-manage-sql-server/open-file-1.png)

### <a name="dashboard"></a>Dashboard

Fare clic su **Open Notebook** (Apri notebook) nel dashboard per aprire la finestra di dialogo Apri file.

![Aprire la finestra di dialogo Apri file selezionando Open Notebook (Apri notebook) nel dashboard](./media/notebooks-manage-sql-server/open-file-2.png) 

### <a name="command-palette"></a>Riquadro comandi

Usare il comando **File: Aprire**  dal riquadro comandi digitando CTRL+MAIUSC+P (in Windows) o CMD+MAIUSC+P (in Mac).

![Aprire la finestra di dialogo Apri file immettendo File: Apri nel riquadro comandi](./media/notebooks-manage-sql-server/open-file-3.png)

## <a name="save-a-notebook"></a>Salvare un notebook

È attualmente disponibile un solo modo per salvare un notebook. Selezionare **Salva** sulla barra degli strumenti del notebook.

![Salvare il file selezionando Salva sulla barra degli strumenti del notebook](./media/notebooks-manage-sql-server/save-file-1.png)

> [!NOTE]
> I metodi seguenti non consentono attualmente di salvare modifiche sui notebook:
>
> - Comandi **Salva file**, **Salva file con nome...** e **Salva tutto** dal menu File.
> - Comando **File: Salva** immessi nel riquadro comandi.

## <a name="change-the-connection"></a>Modificare la connessione

Per modificare la connessione per un notebook:

1. Selezionare il menu **Collega a** dalla barra degli strumenti del notebook e quindi selezionare **Cambia connessione**.

   ![Fare clic sul menu "Associa a" sulla barra degli strumenti del notebook](./media/notebooks-manage-sql-server/select-attach-to-1.png)

2. A questo punto è possibile selezionare un server di connessione recente oppure immettere i dettagli della nuova connessione per la connessione.

   ![Selezionare un server dal menu Associa a.](./media/notebooks-manage-sql-server/select-attach-to-2.png)

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui notebook in Azure Data Studio, vedere [Come usare i notebook in SQL Server 2019](notebooks-guidance.md).
