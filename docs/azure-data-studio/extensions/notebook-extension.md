---
title: Creare un'estensione di tipo notebook di Jupyter
description: Informazioni su come creare un pacchetto di notebook in un'estensione usando il generatore di estensioni
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: how-to
author: yualan
ms.author: alayu
ms.reviewer: alayu, maghan
ms.custom: ''
ms.date: 08/28/2020
ms.openlocfilehash: 52a38a8074814737a30cb2f31d22da922eb76901
ms.sourcegitcommit: b6ee0d434b3e42384b5d94f1585731fd7d0eff6f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/02/2020
ms.locfileid: "89288153"
---
# <a name="create-a-jupyter-notebook-extension"></a>Creare un'estensione di tipo notebook di Jupyter

Questa esercitazione illustra come creare una nuova estensione di Azure Data Studio per notebook. L'estensione rende disponibile un Jupyter Notebook di esempio che può essere aperto ed eseguito in Azure Data Studio.

In questa esercitazione verranno illustrate le procedure per:
> [!div class="checklist"]
> - Creare un progetto di estensione
> - Installare il generatore di estensioni
> - Creare l'estensione di tipo notebook
> - Eseguire l'estensione
> - Creare il pacchetto dell'estensione
> - Pubblicare l'estensione nel marketplace

## <a name="apis-used"></a>API usate

- `azdata.nb.showNotebookDocument`

### <a name="extension-use-cases"></a>Casi d'uso dell'estensione

Esistono diversi motivi per cui può essere utile creare un'estensione di tipo notebook: 
- Condividere documentazione interattiva 
- Salvare e avere accesso costante a tale notebook
- Presentare problemi di scrittura del codice che gli utenti possono seguire
- Controllare le versioni e tenere traccia degli aggiornamenti dei notebook

## <a name="prerequisites"></a>Prerequisiti

Azure Data Studio si basa sullo stesso framework di Visual Studio Code, quindi le estensioni per Azure Data Studio vengono compilate usando Visual Studio Code. Per iniziare, sono necessari i componenti seguenti:

- [Node.js](https://nodejs.org) installato e disponibile in `$PATH`. Node.js include [npm](https://www.npmjs.com/), lo strumento di gestione dei pacchetti di Node.js, che viene usato per installare il generatore di estensioni.
- [Visual Studio Code](https://code.visualstudio.com) per eseguire il debug dell'estensione.
- Assicurarsi che `azuredatastudio` sia nel percorso. Per Windows, assicurarsi di scegliere l'opzione `Add to Path` in setup.exe. Per Mac o Linux, eseguire l'opzione *Installa il comando 'azuredatastudio' in PATH*.

## <a name="install-the-extension-generator"></a>Installare il generatore di estensioni

Per semplificare il processo di creazione delle estensioni, abbiamo creato un [generatore di estensioni](https://www.npmjs.com/package/generator-azuredatastudio) con Yeoman. Per installarlo, eseguire il comando seguente dal prompt dei comandi:

```console
`npm install -g yo generator-azuredatastudio`
```

## <a name="create-your-extension"></a>Creare l'estensione

Per creare un'estensione:

1. Avviare il generatore di estensioni con il comando seguente:

   `yo azuredatastudio`

2. Scegliere **New Notebooks (Individual)** (Nuovi notebook - singoli) nell'elenco dei tipi di estensione:

   :::image type="content" source="media/notebook-extension/notebook-extension-generator.png" alt-text="Generatore dell'estensione di tipo notebook":::

3. Seguire i passaggi per specificare il nome dell'estensione (per questa esercitazione, usare **Test Notebook**), il nome dell'editore (per questa esercitazione, usare **Microsoft**) e aggiungere una descrizione.

A questo punto, è possibile procedere in modi diversi: aggiungere notebook di Jupyter già creati oppure usare i notebook di esempio forniti tramite il generatore.

Per questa esercitazione verrà usato un notebook Python di esempio:

   :::image type="content" source="media/notebook-extension/notebook-sample-generator.png" alt-text="Selezionare l'esempio Python":::

Se esistono notebook che si è interessati a distribuire, rispondere che si desidera distribuire notebook esistenti e specificare il percorso di file assoluto in cui risiedono tutti i notebook o i file markdown.

Il completamento dei passaggi precedenti consente di creare una nuova cartella con il notebook di esempio. Aprire la cartella in Visual Studio Code e si è pronti per distribuire la nuova estensione per i notebook.

## <a name="understanding-your-extension"></a>Informazioni sull'estensione

Il progetto dovrebbe essere simile al seguente:

   :::image type="content" source="media/notebook-extension/notebook-file-structure-generator.png" alt-text="Struttura del file dell'estensione":::

`vsc-extension-quickstart.md` fornisce informazioni di riferimento sui file importanti. `README.md` è la posizione in cui è possibile fornire documentazione per la nuova estensione. Si notino i file `package.json`, `notebook.ts` e `pySample.ipynb`.

Se sono presenti file o cartelle che non si desidera pubblicare, è possibile includere i relativi nomi nel file `.vscodeignore`.

Verrà ora esaminato il file `notebook.ts` per comprendere le funzioni dell'estensione appena creata.

```javascript
// This function is called when you run the command `Launch Notebooks: Test Notebook` from
// command palette in Azure Data Studio. If you would like any additional functionality
// to occur when you launch the book, add to the activate function.
export function activate(context: vscode.ExtensionContext) {
    context.subscriptions.push(vscode.commands.registerCommand('launchNotebooks.test-notebook', () => {
        let notebooksToDisplay: Array<string> = processNotebooks();
        notebooksToDisplay.forEach(name => {
            azdata.nb.showNotebookDocument(vscode.Uri.file(name));
        });
    }));

    // Add other code here if you want to register another command
}
```

Questa è la funzione principale in `notebook.ts` chiamata ogni volta che si esegue l'estensione tramite il comando **Launch Notebooks: Test Notebook**. Il nuovo comando viene creato usando l'API `vscode.commands.registerCommand` e la definizione seguente all'interno delle parentesi graffe è il codice eseguito ogni volta che viene chiamato il comando. Ogni notebook trovato dalla funzione `processNotebooks` viene aperto in Azure Data Studio tramite `azdata.nb.showNotebookDocument`. 

Il file `package.json` ha anche un ruolo importante per la registrazione del comando **Launch Notebooks: Test Notebook**.

```json
"activationEvents": [
        "onCommand:launchNotebooks.test-notebook"
    ],
    "main": "./out/notebook.js",
    "contributes": {
        "commands": [
            {
                "command": "launchNotebooks.test-notebook",
                "title": "Launch Notebooks: Test Notebook"
            }
        ]
    }
```

È presente un evento di attivazione per il comando e sono stati anche aggiunti punti di aggiunta contributi specifici. Questi vengono visualizzati nel marketplace in cui vengono pubblicate le estensioni, quando gli utenti esaminano l'estensione. Se si vogliono aggiungere altri comandi, assicurarsi di aggiungerli nel campo `activationEvents`. Per altre opzioni, vedere [Eventi di attivazione](https://code.visualstudio.com/api/references/activation-events).

## <a name="package-your-extension"></a>Creare il pacchetto dell'estensione

Per condividere l'estensione con altri utenti, è necessario inserirla in un pacchetto costituito da un unico file. Questo può essere pubblicato nel marketplace delle estensioni di Azure Data Studio o condiviso all'interno del team o della community. A tale scopo, è necessario installare un altro pacchetto npm dalla riga di comando:

```console
`npm install -g vsce`
```

Modificare il file `README.md` in base alla proprie esigenze e quindi passare alla directory di base dell'estensione ed eseguire `vsce package`. Facoltativamente, è possibile collegare un repository con l'estensione o continuare senza. Per aggiungerne uno, aggiungere una riga simile al file `package.json`.

```json
"repository": {
    "type": "git",
    "url": "https://github.com/laurajjiang/testnotebook.git"
}
```

Al termine di questa operazione, il file my test-notebook-0.0.1.vsix è stato creato ed è pronto per l'installazione e la condivisione.

## <a name="run-your-extension"></a>Eseguire l'estensione

Per eseguire e testare l'estensione, aprire Azure Data Studio e aprire il riquadro comandi (`Ctrl + Shift + P`). Trovare il comando **Extensions: Install from VSIX** (Estensioni: Installa da VSIX) e passare alla cartella che contiene la nuova estensione.

   :::image type="content" source="media/notebook-extension/install-vsix.png" alt-text="Installare VSIX":::

L'estensione dovrebbe ora comparire nel pannello delle estensioni in Azure Data Studio. Aprire di nuovo il riquadro comandi e notare che è disponibile il nuovo comando creato con l'estensione **Launch Notebooks: Test Notebook**. Eseguendo questo comando verrà aperto il notebook di Jupyter per il quale è stato creato un pacchetto con l'estensione.

   :::image type="content" source="media/notebook-extension/notebook-launch-ads.png" alt-text="Comando Launch Notebooks: Test Notebook":::

Congratulazioni. È stata creata la prima estensione per notebook di Jupyter ed è ora possibile distribuirla.

## <a name="publish-your-extension-to-the-marketplace"></a>Pubblicare l'estensione nel marketplace

L'implementazione del marketplace delle estensioni di Azure Data Studio non è ancora stata completata. Per eseguire la pubblicazione, ospitare l'estensione VSIX nella posizione preferita, ad esempio una pagina di rilascio di GitHub, e inviare una richiesta pull aggiornando [questo file JSON](https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json) con le informazioni sull'estensione.

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione sono state illustrate le procedure per:
> [!div class="checklist"]
> - Creare un progetto di estensione
> - Installare il generatore di estensioni - Creare l'estensione di tipo notebook
> - Creare l'estensione
> - Creare il pacchetto dell'estensione
> - Pubblicare l'estensione nel marketplace

Ci auguriamo che la lettura di questo articolo sia di ispirazione per creare un'estensione personalizzata per Azure Data Studio.

Se si ha un'idea, ma non si è certi di come iniziare, aprire un problema o inviare un tweet al team: [azuredatastudio](https://twitter.com/azuredatastudio).

È sempre possibile fare riferimento alla [Guida delle estensioni di Visual Studio Code](https://code.visualstudio.com/docs/extensions/overview) perché copre tutte le API e i modelli esistenti.