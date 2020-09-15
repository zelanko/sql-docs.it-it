---
title: Creare estensioni
description: È possibile aggiungere funzionalità ad Azure Data Studio con un'estensione. Informazioni su come crearne una e come pubblicarla nella raccolta delle estensioni.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu
ms.custom: seodec18
ms.date: 08/26/2020
ms.openlocfilehash: 477e93dc272c4a26e40333b02728c643299161ce
ms.sourcegitcommit: 5da46e16b2c9710414fe36af9670461fb07555dc
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/01/2020
ms.locfileid: "89283718"
---
# <a name="extend-the-functionality-by-creating-azure-data-studio-extensions"></a>Estendere le funzionalità creando estensioni per Azure Data Studio

Le estensioni di Azure Data Studio consentono di aggiungere facilmente nuove funzionalità all'installazione di base di questo strumento.

Le estensioni vengono fornite sia dal team di Azure Data Studio (Microsoft) sia dalla community di terze parti.

## <a name="author-an-extension"></a>Creare un'estensione

Se si è interessati a estendere Azure Data Studio, è possibile creare un'estensione personalizzata e pubblicarla nella raccolta di estensioni.

**Scrittura di un'estensione**

***Prerequisiti***

Per sviluppare un'estensione, è necessario che [Node.js](https://nodejs.org/) sia installato e disponibile in `$PATH`. Node.js include npm, lo strumento di gestione dei pacchetti di Node.js, che verrà usato per installare il generatore di estensioni.

Per creare la nuova estensione, è possibile usare il generatore di estensioni di Azure Data Studio. Il [generatore di estensioni](https://www.npmjs.com/package/generator-azuredatastudio) Yeoman è un utile punto di partenza per i progetti di estensioni. Per avviare il generatore, digitare quanto segue in un prompt dei comandi:

```console
npm install -g yo generator-azuredatastudio # Install the generator
yo azuredatastudio
```

Per una guida approfondita su come iniziare a usare il modello di estensione, vedere [Creazione di un'estensione](./tutorial-create-extension.md?view=sql-server-ver15), che illustra la creazione di un'estensione per la mappatura della tastiera.

**Riferimenti di estendibilità**

Per informazioni sull'estendibilità di Azure Data Studio, vedere [Panoramica dell'estendibilità](extensibility.md). È anche possibile vedere esempi di come usare l'API negli [esempi](https://github.com/Microsoft/azuredatastudio/tree/main/samples) esistenti.

## <a name="debug-an-extension"></a>Eseguire il debug di un'estensione

È possibile eseguire il debug della nuova estensione usando l'estensione [Azure Data Studio Debug](https://github.com/kevcunnane/sqlops-debug) di Visual Studio Code.

Passaggi:

1. Aprire l'estensione con [Visual Studio Code](https://code.visualstudio.com/).
2. Installare l'estensione Azure Data Studio Debug.
3. Premere **F5** o fare clic sull'icona Debug e quindi su **Avvia**.
4. Una nuova istanza di Azure Data Studio viene avviata in una modalità speciale (Host di sviluppo estensione) e riconosce ora l'estensione.

## <a name="create-an-extension-package"></a>Creare un pacchetto di estensioni

Dopo aver scritto l'estensione, è necessario creare un pacchetto VSIX per poterlo installare in Azure Data Studio. È possibile usare [vsce](https://github.com/Microsoft/vscode-vsce) (Visual Studio Code Extension) per creare il pacchetto VSIX.

```console
npm install -g vsce
cd myExtensionName
vsce package
# The myExtensionName.vsix file has now been generated
```

Con un pacchetto VSIX, è possibile condividere l'estensione in locale e in privato condividendo il file `.vsix` e usando il comando **Estensioni: Install From VSIX File** (Installa da file VSIX) del riquadro comandi per installare l'estensione in Azure Data Studio.

## <a name="publish-an-extension"></a>Pubblicare un'estensione

Per pubblicare la nuova estensione in Azure Data Studio:

1. Aggiungere l'estensione a https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json
2. Non è attualmente disponibile il supporto per l'hosting di estensioni di terze parti; anziché scaricare l'estensione, quindi, è possibile reindirizzare Azure Data Studio su una pagina di download. Per impostare una pagina di download per l'estensione, impostare il valore di asset "Microsoft.AzureDataStudio.DownloadPage".
3. Creare una richiesta pull per il ramo Release/Extensions.
4. Inviare una richiesta di revisione al team.

L'estensione verrà esaminata e aggiunta alla raccolta di estensioni.

**Pubblicazione degli aggiornamenti delle estensioni**

Il processo di pubblicazione degli aggiornamenti è simile alla pubblicazione dell'estensione. Assicurarsi che la versione sia aggiornata in package.json.

## <a name="next-steps"></a>Passaggi successivi

Per istruzioni dettagliate su come iniziare, fare riferimento a una delle esercitazioni seguenti sulla creazione di estensioni:

- [Esercitazione per l'estensione di tipo mappatura della tastiera](extensions/keymap-extension.md)
- [Esercitazione per l'estensione di tipo dashboard](extensions/dashboard-extension.md)
- [Esercitazione per l'estensione di tipo notebook](extensions/notebook-extension.md)
- [Esercitazione per l'estensione di tipo book Jupyter](extensions/jupyter-book-extension.md)
- [Esercitazione per l'estensione di tipo procedura guidata](extensions/wizard-extension.md)