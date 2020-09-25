---
title: Creare un'estensione di tipo book Jupyter
description: Informazioni su come creare un pacchetto per un book Jupyter in un'estensione usando il generatore di estensioni
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: how-to
author: yualan
ms.author: alayu
ms.reviewer: alayu, maghan
ms.custom: ''
ms.date: 08/28/2020
ms.openlocfilehash: a781affee2db40dbd7636c25712ca622c881650e
ms.sourcegitcommit: 8f062015c2a033f5a0d805ee4adabbe15e7c8f94
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/25/2020
ms.locfileid: "91226838"
---
# <a name="create-a-jupyter-book-extension"></a>Creare un'estensione di tipo book Jupyter

Questa esercitazione illustra come creare una nuova estensione di Azure Data Studio di tipo book Jupyter. L'estensione fornisce un book Jupyter di esempio che può essere aperto ed eseguito in Azure Data Studio. 

In questa esercitazione verranno illustrate le procedure per:
> [!div class="checklist"]
> - Creare un progetto di estensione
> - Installare il generatore di estensioni
> - Creare l'estensione di tipo book Jupyter
> - Eseguire l'estensione
> - Creare il pacchetto dell'estensione
> - Pubblicare l'estensione nel marketplace

## <a name="apis-used"></a>API usate

- `bookTreeView.openBook`

### <a name="extension-use-cases"></a>Casi d'uso dell'estensione

Esistono diversi motivi per cui può essere utile creare un'estensione di tipo book Jupyter:

- Condividere documentazione interattiva organizzata e suddivisa in sezioni
- Condividere un book completo (simile a un e-book ma distribuito tramite Azure Data Studio)
- Controllare le versioni e tenere traccia degli aggiornamenti di book Jupyter

La differenza principale tra un'estensione di tipo book Jupyter e di tipo notebook è che un book Jupyter supporta l'organizzazione. Decine di notebook possono essere suddivisi in capitoli diversi in un book, ma l'estensione di tipo notebook è progettata per distribuire un numero ridotto di singoli notebook.

## <a name="prerequisites"></a>Prerequisiti

Azure Data Studio si basa sullo stesso framework di Visual Studio Code, quindi le estensioni per Azure Data Studio vengono compilate usando Visual Studio Code. Per iniziare, sono necessari i componenti seguenti:

- [Node.js](https://nodejs.org) installato e disponibile in `$PATH`. Node.js include [npm](https://www.npmjs.com/), lo strumento di gestione dei pacchetti di Node.js, che viene usato per installare il generatore di estensioni.
- [Visual Studio Code](https://code.visualstudio.com) per apportare modifiche all'estensione ed eseguire il debug dell'estensione.
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

2. Scegliere **New book Jupyter** (Nuovo book Jupyter) nell'elenco dei tipi di estensione:

   :::image type="content" source="media/jupyter-book-extension/jupyter-book-extension-generator.png" alt-text="Generatore di estensioni":::

3. Seguire i passaggi per specificare il nome dell'estensione (per questa esercitazione, usare **Test Book**), il nome dell'editore (per questa esercitazione, usare **Microsoft**) e aggiungere una descrizione.

È possibile scegliere di specificare un book Jupyter esistente, usare un book di esempio specificato o creare un nuovo book Jupyter. Queste tre opzioni sono illustrate di seguito.

### <a name="providing-an-existing-book"></a>Specificare un book esistente

Se si vuole distribuire un book già creato, specificare il percorso di file assoluto della cartella in cui si trova il contenuto del book. Sarà quindi possibile procedere per scoprire di più sull'estensione e la distribuzione.

:::image type="content" source="media/jupyter-book-extension/jupyter-book-existing-book.png" alt-text="Book esistente":::

### <a name="using-the-sample-book"></a>Usare il book di esempio

Se non sono già disponibili book o notebook esistenti, è possibile usare l'esempio fornito nel generatore.

:::image type="content" source="media/jupyter-book-extension/jupyter-book-sample-path.png" alt-text="Book di Jupyter di esempio":::

Il book di esempio dimostra l'aspetto di un semplice book Jupyter. Per informazioni sulla personalizzazione di un book Jupyter, vedere la sezione seguente relativa alla creazione di un nuovo book con notebook esistenti.

### <a name="creating-a-new-book"></a>Creazione di un nuovo book

È possibile raccogliere in un book Jupyter eventuali notebook esistenti. Il generatore chiede se si vogliono creare capitoli nel book e, in caso affermativo, il numero e i titoli. Il processo di selezione è illustrato di seguito. Usare la barra spaziatrice per selezionare i notebook da inserire in ogni capitolo.

:::image type="content" source="media/jupyter-book-extension/jupyter-book-create-book.png" alt-text="Creare un book Jupyter":::

Il completamento dei passaggi precedenti consente di creare una nuova cartella con il nuovo book Jupyter. Aprire la cartella in Visual Studio Code e si è pronti per distribuire l'estensione book Jupyter.

## <a name="understanding-your-extension"></a>Informazioni sull'estensione

Il progetto dovrebbe essere simile al seguente:

   :::image type="content" source="media/jupyter-book-extension/jupyter-book-file-structure-generator.png" alt-text="Struttura del file dell'estensione":::

`vsc-extension-quickstart.md` fornisce informazioni di riferimento sui file importanti. `README.md` è la posizione in cui è possibile fornire documentazione per la nuova estensione. Si notino i file `package.json`, `jupyter-book.ts`, `content` e `toc.yml`. La cartella `content` include tutti i notebook o i file markdown. Il file `toc.yml` definisce la struttura del book Jupyter e viene generato automaticamente se si è scelto di creare un book Jupyter personalizzato tramite il generatore di estensioni.

Se è stato creato un book usando il generatore e si è scelto di usare i capitoli nel book, la struttura di cartelle avrà un aspetto leggermente diverso. Invece dei file markdown e di Jupyter Notebook nella cartella `content`, saranno presenti sottocartelle corrispondenti ai titoli scelti per i capitoli. 

Se sono presenti file o cartelle che non si desidera pubblicare, è possibile includere i relativi nomi nel file `.vscodeignore`.

Verrà ora esaminato il file `jupyter-book.ts` per comprendere le funzioni dell'estensione appena creata.

```javascript
// This function is called when you run the command `Launch Book: Test Book` from
// command palette in Azure Data Studio. If you would like any additional functionality
// to occur when you launch the book, add to the activate function.
export function activate(context: vscode.ExtensionContext) {
    context.subscriptions.push(vscode.commands.registerCommand('launchBook.test-book', () => {
        processNotebooks();
    }));

    // Add other code here if you want to register another command
}
```

La funzione `activate` è l'azione principale dell'estensione. Tutti i comandi da registrare devono essere specificati all'interno della funzione `activate`, in modo analogo al comando `launchBook.test-book`. All'interno della funzione `processNotebooks` è possibile trovare la cartella dell'estensione che contiene il book Jupyter e chiamare `bookTreeView.openBook` usando la cartella dell'estensione come parametro. 

Anche il file `package.json` ha un ruolo importante per la registrazione del comando dell'estensione:

```json
"activationEvents": [
        "onCommand:launchBook.test-book"
    ],
    "main": "./out/notebook.js",
    "contributes": {
        "commands": [
            {
                "command": "launchBook.test-book",
                "title": "Launch Book: Test Book"
            }
        ]
    }
```

L'evento di attivazione `onCommand` attiva la funzione registrata quando si richiama il comando. Esistono alcuni altri eventi di attivazione possibili per personalizzazioni aggiuntive. Per altre informazioni, vedere [Eventi di attivazione](https://code.visualstudio.com/api/references/activation-events).

## <a name="package-your-extension"></a>Creare il pacchetto dell'estensione

Per condividere l'estensione con altri utenti, è necessario inserirla in un pacchetto costituito da un unico file. Questo può essere pubblicato nel marketplace delle estensioni di Azure Data Studio o condiviso all'interno del team o della community. A tale scopo, è necessario installare un altro pacchetto npm dalla riga di comando:

```console
`npm install -g vsce`
```

Modificare il file `README.md` in base alla proprie esigenze e quindi passare alla directory di base dell'estensione ed eseguire `vsce package`. Facoltativamente, è possibile collegare un repository con l'estensione o continuare senza. Per aggiungerne uno, aggiungere una riga simile al file `package.json`.

```json
"repository": {
    "type": "git",
    "url": "https://github.com/laurajjiang/testbook.git"
}
```

Dopo l'aggiunta di queste righe è stato creato un file my test-book-0.0.1.vsix pronto per l'installazione in Azure Data Studio.

## <a name="run-your-extension"></a>Eseguire l'estensione

Per eseguire e testare l'estensione, aprire Azure Data Studio e aprire il riquadro comandi (`Ctrl + Shift + P`). Trovare il comando **Extensions: Install from VSIX** (Estensioni: Installa da VSIX) e passare alla cartella che contiene la nuova estensione. L'estensione dovrebbe ora comparire nel pannello delle estensioni in Azure Data Studio.

   :::image type="content" source="media/jupyter-book-extension/install-vsix.png" alt-text="Installare VSIX":::

Aprire di nuovo il riquadro comandi e trovare il comando registrato **Launch Book: Test Book**. Eseguendo questo comando verrà aperto il book Jupyter per il quale è stato creato un pacchetto con l'estensione.

   :::image type="content" source="media/jupyter-book-extension/jupyter-book-launch-ads.png" alt-text="Comando Launch Book: Test Book":::

Congratulazioni. È stata creata la prima estensione di tipo book Jupyter ed è ora possibile distribuirla. Per altre informazioni sui book Jupyter, vedere [Books with Jupyter](https://jupyterbook.org/intro.html) (Book con Jupyter).

## <a name="publish-your-extension-to-the-marketplace"></a>Pubblicare l'estensione nel marketplace

L'implementazione del marketplace delle estensioni di Azure Data Studio non è ancora stata completata. Per eseguire la pubblicazione, ospitare l'estensione VSIX nella posizione preferita, ad esempio una pagina di rilascio di GitHub, e inviare una richiesta pull aggiornando [questo file JSON](https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json) con le informazioni sull'estensione.

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione sono state illustrate le procedure per:
> [!div class="checklist"]
> - Creare un progetto di estensione
> - Installare il generatore di estensioni
> - Creare l'estensione di tipo book Jupyter
> - Creare il pacchetto dell'estensione
> - Pubblicare l'estensione nel marketplace

Dopo aver completato questa esercitazione è possibile dare spazio alle proprie idee e condividere nuovi book Jupyter con la community di Azure Data Studio. 

Se si ha un'idea, ma non si è certi di come iniziare, aprire un problema o inviare un tweet al team: [azuredatastudio](https://twitter.com/azuredatastudio).

È sempre possibile fare riferimento alla [Guida delle estensioni di Visual Studio Code](https://code.visualstudio.com/docs/extensions/overview) perché copre tutte le API e i modelli esistenti.
