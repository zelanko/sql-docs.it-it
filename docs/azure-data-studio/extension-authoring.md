---
title: Creazione di estensioni
titleSuffix: Azure Data Studio
description: Informazioni sulla creazione e aggiunta di estensioni alle Data Studio di Azure
ms.custom: seodec18
ms.date: 09/24/2018
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a939770ba7b362e2601ecb45b126066341c7c34e
ms.sourcegitcommit: 189a28785075cd7018c98e9625c69225a7ae0777
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/07/2018
ms.locfileid: "53030516"
---
# <a name="extend-the-functionality-by-creating-azure-data-studio-extensions"></a>Estendere la funzionalità tramite la creazione di estensioni di Azure Data Studio

Le estensioni in [!INCLUDE[name-sos](../includes/name-sos-short.md)] forniscono un modo semplice per aggiungere ulteriori funzionalità all'installazione di base di [!INCLUDE[name-sos](../includes/name-sos-short.md)].

Le estensioni sono fornite dal team di Studio di Azure Data (Microsoft), nonché la community di terze parti 3rd (l'utente).


## <a name="author-an-extension"></a>Creare un'estensione

Se si è interessati a estendere Azure Data Studio, è possibile creare estensioni personalizzate e pubblicarlo in raccolta di estensioni.

**Creazione di un'estensione**

***Prerequisiti***

Per sviluppare un'estensione è necessario Node. js installato e disponibile nel $PATH. Node. js include npm, Node. js Package Manager, che verrà usato per installare il generatore di estensione.

Per avviare la nuova estensione, è possibile usare il generatore di estensione di Studio dei dati di Azure. Il Yeoman [generatore di estensione](https://www.npmjs.com/package/generator-sqlops) è molto semplice creare progetti di estensione semplice. Per avviare il generatore, digitare quanto segue al prompt dei comandi:

`npm install -g yo generator-sqlops`

`yo sqlops`


**Riferimenti di estendibilità**

Per informazioni su Extensibility di Studio dei dati di Azure, vedere [panoramica dell'estendibilità](extensibility.md). È anche possibile visualizzare esempi di come usare l'API esistente [esempi](https://github.com/Microsoft/azuredatastudio/tree/master/samples).


## <a name="debug-an-extension"></a>Eseguire il debug di un'estensione

È possibile eseguire il debug la nuova estensione con l'estensione di Visual Studio Code [eseguire il Debug di Azure Data Studio](https://github.com/kevcunnane/sqlops-debug).

Passaggi
- Aprire l'estensione con [Visual Studio Code](https://code.visualstudio.com/)
- Installare l'estensione Azure dati Studio eseguire il Debug
- Premere **F5** oppure fare clic sull'icona di Debug e fare clic su **avviare**.
- Una nuova istanza della Data Studio di Azure viene avviato in modalità speciale (estensione sviluppo Host) e questa nuova istanza a questo punto è a conoscenza dell'estensione.


## <a name="create-an-extension-package"></a>Creare un pacchetto di estensione

Dopo la scrittura dell'estensione, è necessario creare un pacchetto VSIX per essere in grado di installarlo in Studio dei dati di Azure. È possibile usare [vsce](https://github.com/Microsoft/vscode-vsce) per creare il pacchetto VSIX.

`npm install -g vsce`

`vsce package`


## <a name="publish-an-extension"></a>Pubblicare un'estensione

Per pubblicare la nuova estensione per Azure Data Studio:

1. Aggiungere l'estensione https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json
2. Attualmente non è disponibile il supporto per le estensioni di terze parti di host, in modo invece di scaricare l'estensione, Azure Data Studio ha la possibilità di passare a una pagina di download. Per impostare una pagina di download per l'estensione, impostare il valore dell'asset "Microsoft.AzureDataStudio.DownloadPage".
3. Creare una richiesta pull con il ramo di rilascio/le estensioni.
4. Inviare una richiesta di revisione al team.

L'estensione verrà esaminata e aggiunto alla raccolta di estensioni.

**La pubblicazione degli aggiornamenti di estensione** il processo di pubblicazione di aggiornamenti è simile alla pubblicazione dell'estensione. Assicurarsi che la versione viene aggiornata in package. JSON
