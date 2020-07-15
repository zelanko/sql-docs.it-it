---
title: Creare e personalizzare scelte rapide da tastiera
description: Informazioni su come creare e personalizzare scelte rapide da tastiera in Azure Data Studio
ms.prod: azure-data-studio
ms.technology: ''
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu, maghan, sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: da7ca6132a8727d4ea77b3549f1e4d6199741b3a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85774572"
---
# <a name="keyboard-shortcuts-in-azure-data-studio"></a>Tasti di scelta rapida in Azure Data Studio

Questo articolo illustra la procedura per visualizzare, modificare e creare rapidamente scelte rapide da tastiera in Azure Data Studio.

Azure Data Studio ha ereditato le funzionalità dei tasti di scelta rapida da Visual Studio Code. Per informazioni dettagliate sulle personalizzazioni avanzate, l'uso dei vari layout di tastiera e così via, è quindi possibile vedere l'articolo [Tasti di scelta rapida per Visual Studio Code](https://code.visualstudio.com/docs/getstarted/keybindings). È possibile che alcune funzionalità dei tasti di scelta rapida non siano disponibili (le estensioni di mappatura della tastiera, ad esempio, non sono supportate in Azure Data Studio).

## <a name="open-the-keyboard-shortcuts-editor"></a>Aprire l'editor delle scelte rapide da tastiera

Per visualizzare tutte le scelte rapide da tastiera attualmente definite:

Aprire l'editor **Scelte rapide da tastiera** dal menu **File**: **File** > **Preferenze** > **Scelte rapide da tastiera** (**Azure Data Studio** > **Preferenze** > **Scelte rapide da tastiera** in Mac).

Oltre a visualizzare i tasti di scelta rapida correnti, l'editor **Scelte rapide da tastiera** elenca i comandi disponibili per i quali non sono ancora stati definiti tasti di scelta rapida. L'editor **Scelte rapide da tastiera** consente di modificare, rimuovere o reimpostare facilmente tasti di scelta rapida, nonché definirne di nuovi.  

## <a name="edit-existing-keyboard-shortcuts"></a>Modificare scelte rapide da tastiera esistenti

Per modificare il tasto di scelta rapida per una scelta rapida da tastiera esistente:

1. Individuare la scelta rapida da tastiera che si vuole modificare usando la casella di ricerca o scorrendo l'elenco.
   > [!TIP]
   > Cercare per chiave, comando, origine e così via per restituire tutte le scelte rapide da tastiera pertinenti.

2. Fare clic con il pulsante destro del mouse sulla voce desiderata e scegliere **Change Key binding** (Modifica tasto di scelta rapida).

   ![modifica scelta rapida da tastiera](media/keyboard-shortcuts/change-keybinding.png)

3. Premere la combinazione di tasti desiderata e quindi premere **Invio** per salvarla. 

   ![salva scelta rapida da tastiera](media/keyboard-shortcuts/save-keybinding.png)

## <a name="create-new-keyboard-shortcuts"></a>Creare nuove scelte rapide da tastiera

Per creare nuove scelte rapide da tastiera:

1. Fare clic con il pulsante destro del mouse su un comando a cui non è ancora associato un tasto di scelta rapida e selezionare **Add Key binding** (Aggiunti tasto di scelta rapida).

   ![crea scelta rapida da tastiera](media/keyboard-shortcuts/add-keybinding.png)

2. Premere la combinazione di tasti desiderata e quindi premere **Invio** per salvarla.