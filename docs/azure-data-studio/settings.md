---
title: Utente e le impostazioni dell'area di lavoro
titleSuffix: Azure Data Studio
description: Come personalizzare Azure dati Studio modificando le impostazioni dell'area di lavoro e utente.
ms.custom: seodec18
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: 8983e874e9f1a7a5dc875774304c87ad23fa60ea
ms.sourcegitcommit: cebfa2610ea36e3c5ad510c214590035ecb499c2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/04/2019
ms.locfileid: "55689854"
---
# <a name="modify-user-and-workspace-settings"></a>Modificare le impostazioni dell'area di lavoro e utente

È facile da configurare [!INCLUDE[name-sos](../includes/name-sos-short.md)] in base alle esigenze tramite le impostazioni. Quasi tutte le parti di [!INCLUDE[name-sos](../includes/name-sos-short.md)]dell'editor, interfaccia utente e comportamento funzionale sono disponibili opzioni è possibile modificare.

[!INCLUDE[name-sos](../includes/name-sos-short.md)] fornisce due ambiti diversi per le impostazioni:

* **Utente** : queste impostazioni si applicano globalmente a qualsiasi istanza di[!INCLUDE[name-sos](../includes/name-sos-short.md)].
* **Area di lavoro**: sono impostazioni specifiche di una cartella nel computer e sono disponibili solo quando la cartella è aperta in Esplora risorse dalla barra laterale. Le impostazioni definite in questo ambito ridefiniscono quelle di ambito utente.

## <a name="creating-user-and-workspace-settings"></a>Creazione di impostazioni utente e dell'area di lavoro

Il comando di menu **File** > **Preferenze** > **Impostazioni** (**sqlops**  >  **Preferenze** > **Impostazioni** su Mac) fornisce il punto di ingresso per configurare le impostazioni utente e dell'area di lavoro. Esse vengono fornite con un elenco di impostazioni predefinite. Copiare qualsiasi impostazione si desideri modificare nell'appropriato file `settings.json`. Le schede a destra consentono di passare rapidamente tra i file delle impostazioni utente e dell'area di lavoro.

È anche possibile aprire le impostazioni utente e dell'area di lavoro dal **riquadro comandi** (**Ctrl + MAIUSC + P**) con **preferenze: Aprire le impostazioni utente** e **preferenze: Aprire le impostazioni dell'area di lavoro** oppure usare il tasto di scelta rapida (**Ctrl +,**).

Nell'esempio seguente disabilita i numeri di riga nell'editor e configura le righe di codice per essere rientrate automaticamente.

![Impostazioni di esempio](media/settings/sample-settings.png)

Le modifiche alle impostazioni vengono ricaricate da [!INCLUDE[name-sos](../includes/name-sos-short.md)] dopo aver modificato e salvato il file `settings.json`.

>**Nota:** Le impostazioni dell'area di lavoro sono utili per la condivisione delle impostazioni specifiche del progetto in un team.

## <a name="settings-file-locations"></a>Percorsi dei file delle impostazioni

A seconda della piattaforma, il file delle impostazioni utente si trova nei percorsi seguenti:

* **Windows** `%APPDATA%\azuredatastudio\User\settings.json`
* **Mac** `$HOME/Library/Application Support/azuredatastudio/User/settings.json`
* **Linux** `$HOME/.config/azuredatastudio/User/settings.json`

Il file delle impostazioni dell'area di lavoro si trova sotto la cartella `.[!INCLUDE[name-sos](../includes/name-sos-short.md)]` nel progetto.

## <a name="hot-exit"></a>Esci da accesso frequente

Azure Data Studio memorizza le modifiche non salvate ai file quando si esce per impostazione predefinita. Questo è lo stesso come la funzionalità di uscita frequente in Visual Studio Code.

Per impostazione predefinita, a caldo exit è disattivata. Abilitare uscita hot modificando il `files.hotExit` impostazione. Per informazioni dettagliate, vedere [Esci da accesso frequente (nella documentazione di Visual Studio Code)](https://code.visualstudio.com/docs/editor/codebasics#_hot-exit).


## <a name="tab-color"></a>Colore della scheda

Per semplificare l'identificazione delle connessioni utilizzate, le schede aperte nell'editor possono essere impostate con un proprio colore in modo che esso corrisponda a quello definito nel gruppo di Server a cui appartiene la connessione. Per impostazione predefinita, i colori delle schede sono disattivati. Abilitare i colori delle schede modificando l'impostazione `sql.tabColorMode`.

## <a name="additional-resources"></a>Risorse aggiuntive

Poiché [!INCLUDE[name-sos](../includes/name-sos-short.md)] eredita le impostazioni utente e dell'area di lavoro da Visual Studio Code, informazioni dettagliate sono incluse nell'articolo sulle [impostazioni per Visual Studio Code](https://code.visualstudio.com/docs/getstarted/settings).
