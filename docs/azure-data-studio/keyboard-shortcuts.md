---
title: Creare e personalizzare i tasti di scelta rapida
titleSuffix: Azure Data Studio
description: Informazioni su come creare e personalizzare i tasti di scelta rapida in Azure Data Studio
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: b5a07ce70b57f5d62d53bf8ae9b570edcc78d7e6
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66800241"
---
# <a name="keyboard-shortcuts-in-includename-sosincludesname-sosmd"></a>Tasti di scelta rapida in [!INCLUDE[name-sos](../includes/name-sos.md)]

In questo articolo viene mostrata la procedura per visualizzare, modificare e creare tasti di scelta rapida in [!INCLUDE[name-sos](../includes/name-sos-short.md)].

Poiché [!INCLUDE[name-sos](../includes/name-sos-short.md)] eredita le associazioni dei tasti di Visual Studio Code, le informazioni dettagliate sulle personalizzazioni avanzate, l'utilizzo di diversi layout di tastiera e così via sono disponibili nell'articolo [associazione di tasti di Visual Studio Code](https://code.visualstudio.com/docs/getstarted/keybindings). Alcune funzionalità di tasti di scelta rapida potrebbero non essere disponibile (ad esempio, le estensioni di mappatura non sono supportate [!INCLUDE[name-sos](../includes/name-sos-short.md)]).


## <a name="open-the-keyboard-shortcuts-editor"></a>Aprire l'editor dei tasti di scelta rapida

Per visualizzare tutti i tasti di scelta rapida attualmente definiti:

Aprire il **tasti di scelta rapida** editor dalle **File** menu: **File** > **preferenze** > **scelte rapide da tastiera** ( **[!INCLUDE[name-sos](../includes/name-sos-short.md)]**  >   **Preferenze** > **tasti di scelta rapida** su Mac).

Oltre a visualizzare tasti corrente, il **tasti di scelta rapida** editor sono elencati i comandi disponibili privi di tasti di scelta rapida definiti. Il **tasti di scelta rapida** editor consente di modificare, rimuovere, reimpostare, e definire nuovi tasti di scelta rapida.  


## <a name="edit-existing-keyboard-shortcuts"></a>Modifica tasti di scelta rapida esistenti

Per modificare l'associazione di chiavi per un tasto di scelta rapida di esistente:

1. Individuare il tasto di scelta rapida che si desidera modificare usando la casella di ricerca o scorrere l'elenco.
   > [!TIP]
   > Cercare per chiave, per comando, per sorgente e così via per restituire tutti i tasti pertinenti.

1. Fare clic sulla voce desiderata e selezionare **associazione Modifica chiave**

   ![Modifica tasto di scelta rapida](media/keyboard-shortcuts/change-keybinding.png)

1. Premere la combinazione desiderata, quindi premere **Invio** per salvarla. 

   ![salvare i tasti di scelta rapida](media/keyboard-shortcuts/save-keybinding.png)

## <a name="create-new-keyboard-shortcuts"></a>Creare nuovi tasti di scelta rapida

Per creare nuovi tasti di scelta rapida:

1. Fare doppio clic su un comando che non dispone di un tasto qualsiasi associazione e seleziona **associazione di Aggiungi chiave**.

   ![creare tasti di scelta rapida](media/keyboard-shortcuts/add-keybinding.png)

1. Premere la combinazione desiderata, quindi premere **Invio** per salvarla.


