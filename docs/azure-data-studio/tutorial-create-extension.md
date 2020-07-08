---
title: "Esercitazione: Creare un'estensione"
description: Questa esercitazione illustra come creare un'estensione per aggiungere funzionalità personalizzate ad Azure Data Studio.
ms.custom: seodec18
ms.date: 12/10/2019
ms.prod: azure-data-studio
ms.technology: ''
ms.reviewer: alayu, maghan, sstein
ms.topic: tutorial
author: rothja
ms.author: jroth
ms.openlocfilehash: 668e2f4292fb20a85329bbb0716e6945d44e8e02
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85719046"
---
# <a name="tutorial-create-an-azure-data-studio-extension"></a>Esercitazione: Creare un'estensione di Azure Data Studio

Questa esercitazione illustra come creare una nuova estensione di Azure Data Studio. L'estensione crea i familiari tasti di scelta rapida di SSMS in Azure Data Studio.

In questa esercitazione verranno illustrate le procedure per:
> [!div class="checklist"]
> * Creare un progetto di estensione
> * Installare il generatore di estensioni
> * Creare l'estensione
> * Testare l'estensione
> * Creare il pacchetto dell'estensione
> * Pubblicare l'estensione nel marketplace

## <a name="prerequisites"></a>Prerequisiti

Azure Data Studio si basa sullo stesso framework di Visual Studio Code, quindi le estensioni per Azure Data Studio vengono compilate usando Visual Studio Code. Per iniziare, sono necessari i componenti seguenti:

- [Node.js](https://nodejs.org) installato e disponibile in `$PATH`. Node.js include [npm](https://www.npmjs.com/), lo strumento di gestione dei pacchetti di Node.js, che viene usato per installare il generatore di estensioni.
- [Visual Studio Code](https://code.visualstudio.com) per eseguire il debug dell'estensione.
- [Estensione di debug](https://marketplace.visualstudio.com/items?itemName=ms-mssql.sqlops-debug) di Azure Data Studio (facoltativo). In questo modo è possibile testare l'estensione senza dover creare il pacchetto e installarla in Azure Data Studio.
- Assicurarsi che `azuredatastudio` sia nel percorso. Per Windows, assicurarsi di scegliere l'opzione `Add to Path` in setup.exe. Per Mac o Linux, eseguire l'opzione *Installa il comando 'azuredatastudio' in PATH*.


## <a name="install-the-extension-generator"></a>Installare il generatore di estensioni

Per semplificare il processo di creazione delle estensioni, abbiamo creato un [generatore di estensioni](https://code.visualstudio.com/docs/extensions/yocode) con Yeoman. Per installarlo, eseguire il comando seguente dal prompt dei comandi:

`npm install -g yo generator-azuredatastudio`

## <a name="create-your-extension"></a>Creare l'estensione

Per creare un'estensione:

1. Avviare il generatore di estensioni con il comando seguente:

   `yo azuredatastudio`

2. Scegliere **New Keymap** (Nuova mappatura tastiera) dall'elenco dei tipi di estensione:

   ![generatore di estensioni](./media/tutorial-create-extension/extension-generator.png)

3. Seguire i passaggi per compilare il nome dell'estensione (per questa esercitazione, usare **ssmskeymap2**) e aggiungere una descrizione.

Il completamento dei passaggi precedenti consente di creare una nuova cartella. Aprire la cartella in Visual Studio Code ed è tutto pronto per creare un'estensione per i tasti di scelta rapida personalizzati.


### <a name="add-a-keyboard-shortcut"></a>Aggiungere una scelta rapida da tastiera

**Passaggio 1: Trovare le scelte rapide da tastiera da sostituire**

Ora che l'estensione è pronta, aggiungere alcune scelte rapide da tastiera (o tasti di scelta rapida) di SSMS in Azure Data Studio. Qui ci si è ispirati alla [scheda di riferimento rapido di Andy Mallon](https://am2.co/2018/02/updated-cheat-sheet/) e all'elenco di scelte rapide da tastiera di RedGate.

Ecco le principali combinazioni mancanti:

- Eseguire una query con il piano di esecuzione effettivo abilitato. In SSMS corrisponde a **CTRL+M** e non ha una scelta rapida da tastiera in Azure Data Studio.
- **CTRL+MAIUSC+E** come secondo modo per eseguire una query. Il feedback degli utenti indica che questa scelta rapida da tastiera è mancante.
- **ALT+F1** per l'esecuzione di `sp_help`. Questa opzione è stata aggiunta in Azure Data Studio ma poiché questa scelta rapida da tastiera era già in uso, è stato eseguito il mapping a **ALT+F2**.
- Attiva/Disattiva schermo intero (**MAIUSC+ALT+INVIO**).
- **F8** per mostrare **Esplora oggetti** / **visualizzazione Server**.

È facile trovare e sostituire questi tasti di scelta rapida. Eseguire *Apri tasti di scelta rapida* per visualizzare la scheda **Scelte rapide da tastiera** in Azure Data Studio, cercare *query*, quindi scegliere **Cambia tasto di scelta rapida**. Una volta modificato il tasto di scelta rapida, è possibile visualizzare il mapping aggiornato nel file keybindings.json (eseguire *Apri tasti di scelta rapida* per visualizzarlo).

![tasti di scelta rapida](./media/tutorial-create-extension/keyboard-shortcuts.png)

![Estensione keybindings.json](./media/tutorial-create-extension/keybindings-json.png)


**Passaggio 2: Aggiungere collegamenti all'estensione**

Per aggiungere collegamenti all'estensione, aprire il file *package.json* (nell'estensione) e sostituire la sezione `contributes` con il codice seguente:

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

Assicurarsi che `azuredatastudio` sia in PATH eseguendo il comando Installa il comando 'azuredatastudio' in PATH in Azure Data Studio.

Verificare che in Visual Studio Code sia installata l'estensione di debug di Azure Data Studio.

Selezionare **F5** per avviare Azure Data Studio in modalità di debug con l'estensione in esecuzione:

![installare l'estensione](./media/tutorial-create-extension/install-extension.png)

![testare l'estensione](./media/tutorial-create-extension/test-extension.png)

Le mappature della tastiera sono tra le estensioni più veloci da creare, quindi la nuova estensione dovrebbe ora funzionare correttamente ed essere pronta per la condivisione.

## <a name="package-your-extension"></a>Creare il pacchetto dell'estensione

Per condividere l'estensione con altri utenti, è necessario inserirla in un pacchetto costituito da un unico file. Questo può essere pubblicato nel marketplace delle estensioni di Azure Data Studio o condiviso all'interno del team o della community. A tale scopo, è necessario installare un altro pacchetto npm dalla riga di comando:

`npm install -g vsce`

Passare alla directory di base dell'estensione ed eseguire `vsce package`. Qui sono state aggiunte un paio di righe extra perché lo strumento *vsce* mostrava errori:

```json
"repository": {
    "type": "git",
    "url": "https://github.com/kevcunnane/ssmskeymap.git"
},
"bugs": {
    "url": "https://github.com/kevcunnane/ssmskeymap/issues"
},
```

Al termine di questa operazione, il file sssmskeymap-0.1.0.vsix è stato creato ed è pronto per l'installazione e la condivisione.

![installare l'estensione](./media/tutorial-create-extension/extensions.png)


## <a name="publish-your-extension-to-the-marketplace"></a>Pubblicare l'estensione nel marketplace

Il marketplace delle estensioni di Azure Data Studio non è ancora completamente implementato, ma il processo corrente consiste nell'ospitare il pacchetto VSIX dell'estensione in una posizione qualsiasi (ad esempio, una pagina delle versioni di GitHub), quindi inviare una richiesta pull per aggiornare [questo file JSON](https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json) con le informazioni sull'estensione.


## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione sono state illustrate le procedure per:
> [!div class="checklist"]
> * Creare un progetto di estensione
> * Installare il generatore di estensioni
> * Creare l'estensione
> * Testare l'estensione
> * Creare il pacchetto dell'estensione
> * Pubblicare l'estensione nel marketplace


Ci auguriamo che la lettura di questo articolo sia di ispirazione per creare un'estensione personalizzata per Azure Data Studio. Sono disponibili il supporto per dashboard di informazioni dettagliate (utili grafici eseguiti in SQL Server), una serie di API specifiche di SQL e un enorme set di punti di estensione ereditati da Visual Studio Code.

Se si ha un'idea, ma non si è certi di come iniziare, aprire un problema o inviare un tweet al team: [azuredatastudio](https://twitter.com/azuredatastudio).

È sempre possibile fare riferimento alla [Guida delle estensioni di Visual Studio Code](https://code.visualstudio.com/docs/extensions/overview) perché copre tutte le API e i modelli esistenti.


Per informazioni su come usare T-SQL in Azure Data Studio, completare l'esercitazione sull'editor T-SQL:

> [!div class="nextstepaction"]
> [Usare l'editor Transact-SQL per creare oggetti di database](tutorial-sql-editor.md).
