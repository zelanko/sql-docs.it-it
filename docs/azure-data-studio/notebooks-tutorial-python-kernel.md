---
title: Notebook con kernel Python in Azure Data Studio
description: Questa esercitazione illustra come è possibile creare ed eseguire un notebook Python.
author: garyericson
ms.author: garye
ms.reviewer: mikeray, alayu, maghan
ms.topic: tutorial
ms.prod: azure-data-studio
ms.technology: ''
ms.custom: ''
ms.date: 04/27/2020
ms.openlocfilehash: e4c431cba395b8e0c732fa7ac4ab96942cac7144
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85728864"
---
# <a name="create-and-run-a-python-notebook"></a>Creare ed eseguire un notebook Python

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

Questa esercitazione illustra come creare ed eseguire un notebook in Azure Data Studio usando il kernel Python.

## <a name="prerequisites"></a>Prerequisiti

- [Azure Data Studio installato](download-azure-data-studio.md)

## <a name="new-notebook"></a>Nuovo notebook

Questa procedura illustra come creare un file di notebook in Azure Data Studio:

1. Aprire Azure Data Studio. Se viene richiesto di connettersi a un'istanza di SQL Server è possibile connettersi o fare clic su **Annulla**.

1. Scegliere **Nuovo notebook** dal menu **File**.

1. Selezionare **Python 3** per **Kernel**.

   :::image type="content" source="media/notebook-tutorial-python/set-kernel-and-attach-to-python.png" alt-text="Impostare il kernel":::

1. Se viene richiesto di configurare Python, in **Configura Python per Notebooks** selezionare una delle opzioni seguenti:

   - **Nuova installazione di Python** per installare una nuova copia di Python per Azure Data Studio o
   - **Usa l'installazione esistente di Python** per specificare il percorso di un'installazione esistente di Python

## <a name="run-a-notebook-cell"></a>Eseguire una cella del notebook

È possibile creare celle contenenti codice o testo. È possibile eseguire una cella di codice e i risultati vengono visualizzati nel notebook al termine dell'esecuzione della cella. Le celle di testo consentono di inserire documentazione formattata all'interno del codice.

### <a name="code"></a>Codice

Aggiungere una nuova cella di codice Python selezionando il comando **+Codice** sulla barra degli strumenti.

:::image type="content" source="media/notebook-tutorial-python/notebook-toolbar-python.png" alt-text="Barra degli strumenti del notebook":::

Questo esempio esegue operazioni matematiche semplici.

```python
a = 1
b = 2
c = a/b
print(c)
```
Eseguire la cella facendo clic sul pulsante di riproduzione a sinistra della cella. I risultati vengono visualizzati di seguito.

:::image type="content" source="media/notebook-tutorial-python/run-notebook-cell-python.png" alt-text="Eseguire la cella del notebook":::

### <a name="text"></a>Text

Aggiungere una nuova cella di testo selezionando il comando **+Testo** sulla barra degli strumenti.

:::image type="content" source="media/notebook-tutorial-python/notebook-toolbar-python-text.png" alt-text="Barra degli strumenti del notebook":::

La cella passa alla modalità di modifica ed è quindi possibile digitare il codice markdown e, nello stesso tempo, visualizzare l'anteprima.

:::image type="content" source="media/notebook-tutorial-python/notebook-markdown-cell-python.png" alt-text="Cella di markdown":::

Se si fa clic all'esterno della cella di testo, viene visualizzato solo il testo markdown.

:::image type="content" source="media/notebook-tutorial-python/notebook-markdown-preview-python.png" alt-text="Testo markdown":::

## <a name="next-steps"></a>Passaggi successivi

Altre informazioni sui notebook:

- [Come usare i notebook con SQL Server](notebooks-guidance.md)

- [Creare ed eseguire un notebook di SQL Server](notebooks-tutorial-sql-kernel.md)

- [Come gestire i notebook in Azure Data Studio](notebooks-manage-sql-server.md)
