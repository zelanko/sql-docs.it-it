---
title: Creare estensioni
description: È possibile aggiungere funzionalità ad Azure Data Studio con un'estensione. Informazioni su come crearne una e come pubblicarla nella raccolta delle estensioni.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu, maghan, sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: bd2a20857c8f16ea2b2d71ebfcb620bcea3f0190
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88778420"
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

```
npm install -g yo generator-azuredatastudio # Install the generator
yo azuredatastudio
```

Per una guida approfondita su come iniziare a usare il modello di estensione, vedere [Creazione di un'estensione](./tutorial-create-extension.md?view=sql-server-ver15), che illustra la creazione di un'estensione per la mappatura della tastiera.

**Riferimenti di estendibilità**

Per informazioni sull'estendibilità di Azure Data Studio, vedere [Panoramica dell'estendibilità](extensibility.md). È anche possibile vedere esempi di come usare l'API negli [esempi](https://github.com/Microsoft/azuredatastudio/tree/main/samples) esistenti.


## <a name="debug-an-extension"></a>Eseguire il debug di un'estensione

È possibile eseguire il debug della nuova estensione usando l'estensione [Azure Data Studio Debug](https://github.com/kevcunnane/sqlops-debug) di Visual Studio Code.

Passaggi
1. Aprire l'estensione con [Visual Studio Code](https://code.visualstudio.com/).
1. Installare l'estensione Azure Data Studio Debug.
1. Premere **F5** o fare clic sull'icona Debug e quindi su **Avvia**.
1. Una nuova istanza di Azure Data Studio viene avviata in una modalità speciale (Host di sviluppo estensione) e riconosce ora l'estensione.


## <a name="create-an-extension-package"></a>Creare un pacchetto di estensioni

Dopo aver scritto l'estensione, è necessario creare un pacchetto VSIX per poterlo installare in Azure Data Studio. È possibile usare [vsce](https://github.com/Microsoft/vscode-vsce) (Visual Studio Code Extension) per creare il pacchetto VSIX. 

```
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