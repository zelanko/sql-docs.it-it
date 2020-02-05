---
title: Controllo del codice sorgente
titleSuffix: Azure Data Studio
description: Informazioni su come configurare il controllo del codice sorgente in Azure Data Studio
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: c278bcf6cff451396b3d677b203f207b68fd6dc5
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "67959282"
---
#  <a name="using-source-control-in-includename-sosincludesname-sos-shortmd"></a>Utilizzo del controllo del codice sorgente in [!INCLUDE[name-sos](../includes/name-sos-short.md)]

[!INCLUDE[name-sos](../includes/name-sos-short.md)] supporta Git per il controllo della versione e del codice sorgente.


## <a name="git-support-in-includename-sosincludesname-sos-shortmd"></a>Supporto Git in [!INCLUDE[name-sos](../includes/name-sos-short.md)]

[!INCLUDE[name-sos](../includes/name-sos-short.md)] viene fornito con Gestione controllo del codice sorgente (SCM) di Git, ma è comunque necessario [installare Git (versione 2.0.0 o successiva)](https://git-scm.com/download) per rendere disponibili queste funzionalità. 



## <a name="open-an-existing-git-repository"></a>Aprire un repository Git esistente

1. Nel menu **File** selezionare **Apri cartella...**
2. Passare alla cartella contenente i file registrati da Git e quindi fare clic su **Seleziona cartella**. A questo punto è possibile selezionare le sottocartelle presenti nel repository locale.


## <a name="initialize-a-new-git-repository"></a>Inizializzare un nuovo repository Git

1. Selezionare **Controllo codice sorgente** e quindi l'icona di Git.

   ![Icona Git di Controllo codice sorgente](media/source-control/source-control.png)

1. Immettere il percorso della cartella che si vuole inizializzare come repository Git e premere **Invio**.

   ![Inizializzare repository Git](media/source-control/initialize-git-repository.png)

## <a name="working-with-git-repositories"></a>Uso dei repository Git

[!INCLUDE[name-sos](../includes/name-sos-short.md)] eredita l'implementazione di Git da VS Code ma non supporta attualmente altri provider di strumenti SCM. Per informazioni dettagliate sull'uso di Git dopo l'apertura o l'inizializzazione di un repository, vedere [Supporto di Git in VS Code](https://code.visualstudio.com/docs/editor/versioncontrol#_git-support).


## <a name="additional-resources"></a>Risorse aggiuntive
- [Documentazione di Git](https://git-scm.com/documentation)
