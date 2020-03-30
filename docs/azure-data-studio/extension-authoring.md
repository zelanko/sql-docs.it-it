---
title: Creare estensioni
titleSuffix: Azure Data Studio
description: Informazioni sulla creazione e l'aggiunta di estensioni in Azure Data Studio
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: d0c43df8b24a33f3763dc5ff3a80e989b9b85038
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "67959600"
---
# <a name="extend-the-functionality-by-creating-azure-data-studio-extensions"></a>Estendere le funzionalità creando estensioni per Azure Data Studio

Le estensioni di [!INCLUDE[name-sos](../includes/name-sos-short.md)] consentono di aggiungere facilmente nuove funzionalità all'installazione di base di [!INCLUDE[name-sos](../includes/name-sos-short.md)].

Le estensioni vengono fornite sia dal team di Azure Data Studio (Microsoft) sia dalla community di terze parti.


## <a name="author-an-extension"></a>Creare un'estensione

Se si è interessati a estendere Azure Data Studio, è possibile creare un'estensione personalizzata e pubblicarla nella raccolta di estensioni.

**Scrittura di un'estensione**

***Prerequisiti***

Per sviluppare un'estensione, è necessario che Node.js sia installato e disponibile in $PATH. Node.js include npm, lo strumento di gestione dei pacchetti di Node.js, che verrà usato per installare il generatore di estensioni.

Per avviare la nuova estensione, è possibile usare il generatore di estensioni di Azure Data Studio. Il [generatore di estensioni](https://www.npmjs.com/package/generator-azuredatastudio) Yeoman consente di creare semplici progetti di estensione con estrema semplicità. Per avviare il generatore, digitare quanto segue in un prompt dei comandi:

`npm install -g yo generator-azuredatastudio`

`yo azuredatastudio`


**Riferimenti di estendibilità**

Per informazioni sull'estendibilità di Azure Data Studio, vedere [Panoramica dell'estendibilità](extensibility.md). È anche possibile vedere esempi di come usare l'API negli [esempi](https://github.com/Microsoft/azuredatastudio/tree/master/samples) esistenti.


## <a name="debug-an-extension"></a>Eseguire il debug di un'estensione

È possibile eseguire il debug della nuova estensione usando l'estensione [Azure Data Studio Debug](https://github.com/kevcunnane/sqlops-debug) di Visual Studio Code.

Passaggi
- Aprire l'estensione con [Visual Studio Code](https://code.visualstudio.com/)
- Installare l'estensione Azure Data Studio Debug
- Premere **F5** o fare clic sull'icona Debug e quindi su **Avvia**.
- Una nuova istanza di Azure Data Studio viene avviata in una modalità speciale (Host di sviluppo estensione) e riconosce ora l'estensione.


## <a name="create-an-extension-package"></a>Creare un pacchetto di estensioni

Dopo aver scritto l'estensione, è necessario creare un pacchetto VSIX per poterlo installare in Azure Data Studio. È possibile usare [vsce](https://github.com/Microsoft/vscode-vsce) per creare il pacchetto VSIX.

`npm install -g vsce`

`vsce package`


## <a name="publish-an-extension"></a>Pubblicare un'estensione

Per pubblicare la nuova estensione in Azure Data Studio:

1. Aggiungere l'estensione a https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json
2. Non è attualmente disponibile il supporto per l'hosting di estensioni di terze parti; anziché scaricare l'estensione, quindi, è possibile reindirizzare Azure Data Studio su una pagina di download. Per impostare una pagina di download per l'estensione, impostare il valore di asset "Microsoft.AzureDataStudio.DownloadPage".
3. Creare una richiesta pull per il ramo Release/Extensions.
4. Inviare una richiesta di revisione al team.

L'estensione verrà esaminata e aggiunta alla raccolta di estensioni.

**Pubblicazioni di aggiornamenti alle estensioni** Il processo di pubblicazione degli aggiornamenti è simile alla pubblicazione dell'estensione. Assicurarsi che la versione sia aggiornata in package.json
