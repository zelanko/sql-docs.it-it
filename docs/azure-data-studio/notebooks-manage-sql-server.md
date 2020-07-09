---
title: Come gestire un notebook
description: Informazioni su come gestire notebook in Azure Data Studio, inclusi l'apertura di un notebook, il relativo salvataggio e la modifica della connessione SQL o del kernel Python.
author: markingmyname
ms.author: maghan
ms.reviewer: achatter, alayu, mikeray
ms.metadata: seo-lt-2019
ms.topic: conceptual
ms.prod: azure-data-studio
ms.technology: ''
ms.custom: ''
ms.date: 04/27/2020
ms.openlocfilehash: 326e0b0afc4809d13cf2fdfdbd76f53dafe1cbb9
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85774584"
---
# <a name="how-to-manage-notebooks-in-azure-data-studio"></a>Come gestire notebook in Azure Data Studio

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

Questo articolo descrive come aprire e salvare file di notebook in Azure Data Studio. Illustra inoltre come modificare la connessione a SQL Server o al kernel Python.

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

## <a name="change-the-sql-connection"></a>Modificare la connessione SQL

Per modificare la connessione SQL per un notebook:

1. Selezionare il menu **Collega a** dalla barra degli strumenti del notebook e quindi selezionare **Cambia connessione**.

   ![Fare clic sul menu "Associa a" sulla barra degli strumenti del notebook](./media/notebooks-manage-sql-server/select-attach-to-1.png)

2. A questo punto è possibile selezionare un server di connessione recente oppure immettere i dettagli della nuova connessione per la connessione.

   ![Selezionare un server dal menu Associa a.](./media/notebooks-manage-sql-server/select-attach-to-2.png)

## <a name="change-the-python-kernel"></a>Modificare il kernel Python

La prima volta che si apre Azure Data Studio viene visualizzata la pagina **Configura Python per Notebooks**. È possibile selezionare:

- **Nuova installazione di Python** per installare una nuova copia di Python per Azure Data Studio o
- **Usa l'installazione esistente di Python** per specificare il percorso di un'installazione esistente di Python da usare in Azure Data Studio

Per visualizzare il percorso e la versione del kernel Python attivo, creare una cella di codice ed eseguire i comandi Python seguenti:

```python
import os
import sys
print(sys.version_info)
print(os.path.dirname(sys.executable))
```

Per passare a un'installazione diversa di Python:

1. Scegliere **Preferenze** dal menu **File** e quindi **Impostazioni**.
1. Scorrere fino a **Configurazione di Notebook** in **Estensioni**.
1. In **Usa l'installazione esistente di Python** deselezionare l'opzione "Percorso locale di un'installazione preesistente di Python usata da Notebooks."
1. Riavviare Azure Data Studio.

Quando viene visualizzata la pagina **Configura Python per Notebooks** è possibile scegliere di creare una nuova installazione di Python o specificare il percorso di un'installazione esistente.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui notebook SQL in Azure Data Studio, vedere [Come usare i notebook in SQL Server 2019](notebooks-guidance.md).
