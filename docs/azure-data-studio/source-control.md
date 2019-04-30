---
title: Controllo del codice sorgente
titleSuffix: Azure Data Studio
description: Informazioni su come configurare controllo del codice sorgente in Azure Data Studio
ms.custom: seodec18
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5fb3c8dea11e570bba4452e181626625e31acbe0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63312040"
---
#  <a name="using-source-control-in-includename-sosincludesname-sos-shortmd"></a>Utilizzo del controllo del codice sorgente in [!INCLUDE[name-sos](../includes/name-sos-short.md)]

[!INCLUDE[name-sos](../includes/name-sos-short.md)] supporta Git per il controllo della versione/sorgente.


## <a name="git-support-in-includename-sosincludesname-sos-shortmd"></a>Supporto per GIT in [!INCLUDE[name-sos](../includes/name-sos-short.md)]

[!INCLUDE[name-sos](../includes/name-sos-short.md)] viene fornito con un manager di controllo di origine Git (SCM), ma è comunque necessario [installare Git (versione 2.0.0 o versione successiva)](https://git-scm.com/download) prima di queste funzionalità sono disponibili. 



## <a name="open-an-existing-git-repository"></a>Aprire un repository Git esistente

1. Nel menu **File** selezionare **Apri cartella...**
2. Passare alla cartella contenente i file tracciati da Git e fare clic su **Seleziona cartella**. È possibile selezionare anche le sottocartelle del repository locale.


## <a name="initialize-a-new-git-repository"></a>Inizializzare un nuovo repository Git

1. Selezionare **Controllo del codice sorgente** nella barra laterale sinistra, quindi selezionare l'icona di Git.


   ![Icona Git del controllo del codice sorgente](media/source-control/source-control.png)

1. Immettere il percorso della cartella in cui si desidera inizializzare un repository Git e premere **Invio**.

   ![inizializzare i repository Git](media/source-control/initialize-git-repository.png)

## <a name="working-with-git-repositories"></a>Utilizzo di un repository Git

[!INCLUDE[name-sos](../includes/name-sos-short.md)] eredita l'implementazione di Git da Visual Studio Code, ma attualmente non supporta altri provider di Gestione controllo servizi. Per i dettagli sull'uso di Git, dopo avere aperto o inizializzare un repository, vedere [supporto per Git in Visual Studio Code](https://code.visualstudio.com/docs/editor/versioncontrol#_git-support).


## <a name="additional-resources"></a>Risorse aggiuntive
- [Documentazione di Git](https://git-scm.com/documentation)
