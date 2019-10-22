---
title: Estensione Confronto schema
titleSuffix: Azure Data Studio
description: Installare e usare l'estensione Confronto schema (anteprima) per Azure Data Studio
ms.custom: seodec18
ms.date: 10/03/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: 031bdc19762213ff2c85e6fe4612ded294fcaaa9
ms.sourcegitcommit: 4c75b49599018124f05f91c1df3271d473827e4d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72381786"
---
# <a name="schema-compare-extension-preview"></a>Estensione Confronto schema (anteprima)
L'estensione Confronto schema consente di confrontare facilmente due definizioni di database e di applicare le differenze dall'origine alla destinazione.

Questa funzionalità è attualmente disponibile in versione di anteprima iniziale. Segnalare eventuali problemi e richieste di funzionalità [qui](https://github.com/microsoft/azuredatastudio/issues).


## <a name="features"></a>Funzionalità

* Confrontare gli schemi di due file con estensione dacpac o database
* Visualizzare i risultati come un set di azioni che devono essere eseguite sulla destinazione affinché corrisponda all'origine
* Escludere selettivamente le azioni elencate nei risultati
* Impostare le opzioni che controllano l'ambito del confronto
* Applicare le modifiche alla destinazione o generare uno script con lo stesso effetto
* Salvare il confronto

![Confronto schema: Confronto di esempio](media/extensions/schema-compare-extension/schema-compare.png)


## <a name="why-would-i-use-the-schema-compare-extension"></a>Perché usare l'estensione Confronto schema?

Può essere noioso gestire e sincronizzare manualmente versioni di database diverse. L'estensione Confronto schema semplifica il processo di confronto dei database e offre il controllo completo durante la loro sincronizzazione. È possibile filtrare in modo selettivo differenze e categorie di differenze specifiche prima di applicare le modifiche. L'estensione Confronto schema è uno strumento affidabile che consente di risparmiare tempo e codice.

![Confronto schema: Finestra di dialogo Opzioni](media/extensions/schema-compare-extension/schema-compare-options.png)


## <a name="install-the-extension"></a>Installare l'estensione

1. Selezionare l'icona Estensioni per visualizzare le estensioni disponibili.

    ![icona Gestione estensioni](media/extensions/extension-manager-icon.png)

2. Cercare l'estensione **Confronto schema** e selezionarla per visualizzarne i dettagli. Fare clic su **Installa** per aggiungere l'estensione.

3. Dopo l'installazione, **ricaricare** per abilitare l'estensione in Azure Data Studio (necessario solo quando si installa un'estensione per la prima volta).


## <a name="launch-a-schema-compare"></a>Avviare Confronto di schema

1. Per aprire la finestra di dialogo Confronto schema, **fare clic con il pulsante destro del mouse** su un database in Esplora oggetti e quindi scegliere **Confronto schema**. Il database selezionato verrà impostato come database di origine nel confronto.

    ![menu di avvio confronto schema](media/extensions/schema-compare-extension/schema-compare-launch.png)


2. Selezionare uno dei puntini di sospensione (...) per modificare l'origine e la destinazione del confronto dello schema e fare clic su OK.

    ![confronto schema - selezione di origine/destinazione](media/extensions/schema-compare-extension/schema-compare-select-source-target.png)

3. Per personalizzare il confronto, fare clic sul pulsante **Opzioni** sulla barra degli strumenti.

4. Fare clic su **Confronta** per visualizzare i risultati del confronto.


## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su Confronto schema, [consultare la documentazione di riferimento](https://docs.microsoft.com/sql/ssdt/how-to-use-schema-compare-to-compare-different-database-definitions).