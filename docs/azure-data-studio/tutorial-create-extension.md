---
title: "Esercitazione: Creare un'estensione"
titleSuffix: Azure Data Studio
description: Questa esercitazione illustra come creare un'estensione per aggiungere funzionalità personalizzate a Data Studio di Azure.
ms.custom: seodec18
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: tutorial
author: kevcunnane
ms.author: kcunnane
manager: craigg
ms.openlocfilehash: 0a4e877a91cad978bb62747bd50e40adaa69ef1c
ms.sourcegitcommit: 189a28785075cd7018c98e9625c69225a7ae0777
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/07/2018
ms.locfileid: "53030605"
---
# <a name="tutorial-create-an-azure-data-studio-extension"></a>Esercitazione: Creare un'estensione di Studio dei dati di Azure

Questa esercitazione illustra come creare una nuova estensione di Studio dei dati di Azure. L'estensione crea familiare SSMS tasti di scelta rapida in Azure Data Studio.

Durante questa esercitazione si apprenderà come:
> [!div class="checklist"]
> * Creare un progetto di estensione
> * Installare il generatore di estensione
> * Creare l'estensione
> * Testare l'estensione
> * Creare un pacchetto di estensione
> * Pubblicare l'estensione nel marketplace

## <a name="prerequisites"></a>Prerequisiti

Azure Data Studio viene compilato nello stesso framework come Visual Studio Code, in modo che le estensioni per Azure Data Studio vengono compilate usando Visual Studio Code. Per iniziare, sono necessari i componenti seguenti:

- [Node. js](https://nodejs.org) installato e disponibile nel `$PATH`. Include Node. js [npm](https://www.npmjs.com/), Node. js Package Manager, che consente di installare il generatore di estensione.
- [Visual Studio Code](https://code.visualstudio.com) per eseguire il debug dell'estensione.
- Azure Data Studio [estensione di Debug](https://marketplace.visualstudio.com/items?itemName=ms-mssql.sqlops-debug).
- Assicurarsi che `sqlops` sia presente nel percorso. Per Windows, assicurarsi di scegliere il `Add to Path` opzione setup.exe. Per Mac o Linux, eseguire la *installare il comando 'sqlops' nel percorso* opzione.
- Estensione eseguire il Debug di SQL Operations Studio (facoltativo). Ciò consente di testare l'estensione senza la necessità di creare un pacchetto e installarlo in Azure Data Studio.


## <a name="install-the-extension-generator"></a>Installare il generatore di estensione

Per semplificare il processo di creazione di estensioni, abbiamo creato un [generatore di estensione](https://code.visualstudio.com/docs/extensions/yocode) usando Yeoman. Per installarlo, eseguire il comando seguente dal prompt dei comandi:

`npm install -g yo generator-sqlops`

## <a name="create-your-extension"></a>Creare l'estensione

Per creare un'estensione:

1. Avviare il generatore di estensione con il comando seguente:

   `yo sqlops`

2. Scegli **nuova mappatura** dall'elenco dei tipi di estensione:

   ![Generatore di estensione](./media/tutorial-create-extension/extension-generator.png)

3. Seguire i passaggi necessari per inserire il nome di estensione (per questa esercitazione, usare **ssmskeymap**) e aggiungere una descrizione.

Completare i passaggi precedenti, viene creata una nuova cartella. Aprire la cartella in Visual Studio Code e si è pronti per creare tasti di scelta rapida estensioni personalizzate!


### <a name="add-a-keyboard-shortcut"></a>Aggiungere un tasto di scelta rapida

**Passaggio 1: Trovare le scelte rapide da sostituire**

Ora che abbiamo nostra estensione pronto per iniziare, aggiungere alcuni SSMS tastiera tasti di scelta rapida (o tasti di scelta rapida) in Azure Data Studio. Ho utilizzato [foglio informativo di Andy Mallon](https://am2.co/2018/02/updated-cheat-sheet/) e un elenco di tasti di scelta rapida da tastiera di RedGate per trovare l'ispirazione.

Sono stati le cose che ho visto mancanti:

- Eseguire una query con il piano di esecuzione effettivo attivato. Si tratta **Ctrl + M** in SQL Server Management Studio e non dispone di un'associazione in Data Studio di Azure.
- Visto **CTRL + MAIUSC + E** come secondo modalità di esecuzione di una query. Feedback dell'utente indicato che questa era manca.
- Visto **ALT+F1** eseguire `sp_help`. È stato aggiunto in Studio di Azure Data ma dal momento che l'associazione è stata già in uso, viene eseguito il mapping a **ALT + F2** invece.
- Attiva/Disattiva schermo (**MAIUSC + ALT + INVIO**).
- **F8** per mostrare **Esplora oggetti** / **visualizzazione server**.

È facile trovare e sostituire questi tasti di scelta rapida. Eseguire *tasti di scelta rapida Open* per visualizzare i **tasti di scelta rapida** scheda in Azure Data Studio, cercare *query* e quindi scegliere **associazione Cambia chiave**. Dopo aver modificato il tasto di scelta rapida, è possibile visualizzare il mapping aggiornato nel file KeyBindings. JSON (eseguire *tasti di scelta rapida Open* per visualizzarlo).

![tasti di scelta rapida](./media/tutorial-create-extension/keyboard-shortcuts.png)

![estensione di file KeyBindings. JSON](./media/tutorial-create-extension/keybindings-json.png)


**Passaggio 2: Aggiungere tasti di scelta rapida per l'estensione**

Per aggiungere tasti di scelta rapida per l'estensione, aprire il *package. JSON* del file (nell'estensione) e sostituire il `contributes` sezione con il codice seguente:

```json
"contributes": {
  "keybindings": [
    {
      "key": "shift+cmd+e",
      "command": "runQueryKeyboardAction"
    },
    {
      "key": "ctrl+cmd+e",
      "command": "workbench.view.explorer"
    },
    {
      "key": "alt+f1",
      "command": "workbench.action.query.shortcut1"
    },
    {
      "key": "shift+alt+enter",
      "command": "workbench.action.toggleFullScreen"
    },
    {
      "key": "f8",
      "command": "workbench.view.connections"
    },
    {
      "key": "ctrl+m",
      "command": "runCurrentQueryWithActualPlanKeyboardAction"
    }
  ]
}
```

## <a name="test-your-extension"></a>Testare l'estensione

Assicurarsi che `azuredatastudio` sia presente nel percorso eseguendo il comando di installazione azuredatastudio nel comando di percorso in Studio di Azure Data.

Verificare che sia installata l'estensione Azure dati Studio eseguire il Debug in Visual Studio Code.

Selezionare **F5** per avviare Studio dei dati di Azure in modalità di debug con l'estensione in esecuzione:

![installare l'estensione](./media/tutorial-create-extension/install-extension.png)

![estensione di test](./media/tutorial-create-extension/test-extension.png)

Mappe delle chiavi sono una delle estensioni più rapida per creare, in modo che la nuova estensione di questo punto dovrebbe essere pronti per condividere e funzionino correttamente.

## <a name="package-your-extension"></a>Creare un pacchetto di estensione

Per condividere con altri utenti è necessario creare un pacchetto di estensione in un unico file. Questo può essere pubblicato in marketplace delle estensioni di Studio di Azure Data o condiviso tra il team o della community. A tale scopo, è necessario installare un altro pacchetto npm dalla riga di comando:

`npm install -g vsce`

Passare alla directory di base dell'estensione ed eseguire `vsce package`. Devo aggiungere un paio di righe aggiuntive per arrestare il *vsce* strumento che segnala che:

```json
"repository": {
    "type": "git",
    "url": "https://github.com/kevcunnane/ssmskeymap.git"
},
"bugs": {
    "url": "https://github.com/kevcunnane/ssmskeymap/issues"
},
```

Dopo questa operazione è stata eseguita, il file ssmskeymap 0.1.0.vsix è stato creato e pronto per installare e condividere con tutto il mondo!

![installare l'estensione](./media/tutorial-create-extension/extensions.png)


## <a name="publish-your-extension-to-the-marketplace"></a>Pubblicare l'estensione nel marketplace

Il marketplace delle estensioni Studio di Azure Data non è completamente ancora implementato, ma il processo corrente è per ospitare l'estensione VSIX in una posizione (ad esempio, una pagina di GitHub Release) quindi inviare per l'aggiornamento di una richiesta pull [questo file JSON](https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json) con di informazioni sull'estensione.


## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione si è appreso come:
> [!div class="checklist"]
> * Creare un progetto di estensione
> * Installare il generatore di estensione
> * Creare l'estensione
> * Testare l'estensione
> * Creare un pacchetto di estensione
> * Pubblicare l'estensione nel marketplace


Ci auguriamo che dopo aver letto questo che sarà ispirazione per creare un'estensione personalizzata per Azure Data Studio. È disponibile il supporto per Dashboard Insights (grafici piuttosto che eseguire in SQL Server), una serie di API specifiche di SQL e un vastissimo insieme esistente di punti di estensione ereditata da Visual Studio Code.

Se si è fatti un'idea ma non conoscono come iniziare, aprire un problema o un tweet di team: [azuredatastudio](https://twitter.com/azuredatastudio).

È sempre possibile fare riferimento al [Guida all'estensione di Visual Studio Code](https://code.visualstudio.com/docs/extensions/overview) poiché concerne tutte le API esistenti e i modelli.


Per informazioni su come lavorare con T-SQL Studio di dati di Azure, completare l'esercitazione Editor T-SQL:

> [!div class="nextstepaction"]
> [Usare l'editor Transact-SQL per creare oggetti di database](tutorial-sql-editor.md).
