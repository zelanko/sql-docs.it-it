---
title: Aggiungere estensioni
titleSuffix: Azure Data Studio
description: Aggiungere estensioni ad Azure Data Studio dal Marketplace di estensioni
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 10/03/2019
ms.openlocfilehash: 6f0a2ab021873a2a9414bfbcdb7aed63c2d31056
ms.sourcegitcommit: cf268c4e39edf00a8552466e9440e79e6a5d0084
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/09/2019
ms.locfileid: "72166729"
---
# <a name="extend-the-functionality-of-includename-sosincludesname-sos-shortmd"></a>Estendere le funzionali di [!INCLUDE[name-sos](../includes/name-sos-short.md)]

Le estensioni di [!INCLUDE[name-sos](../includes/name-sos-short.md)] consentono di aggiungere facilmente nuove funzionalità all'installazione di base di [!INCLUDE[name-sos](../includes/name-sos-short.md)]. 

Le estensioni vengono fornite sia dal team di Azure Data Studio (Microsoft) sia dalla community di terze parti. Per altre informazioni sulla creazione di estensioni, vedere [Creazione di estensioni](extension-authoring.md).


## <a name="add-azure-data-studio-extensions"></a>Aggiungere estensioni ad Azure Data Studio

1. Accedere alle estensioni disponibili selezionando l'icona Estensioni o scegliendo **Estensioni** dal menu **Visualizza**.

    ![icona Gestione estensioni](media/extensions/extension-manager-icon.png)

    È anche possibile accedere rapidamente a Gestione estensioni premendo `Ctrl+Shift+X` (Windows/Linux) o `Command+Shift+X` (Mac).

2. Selezionare un'estensione disponibile per visualizzarne i dettagli.
    ![dettagli dell'estensione](media/extensions/extension-details.png)

3. Selezionare l'estensione desiderata e **installarla**.

4. Dopo l'installazione, **ricaricare** per abilitare l'estensione in Azure Data Studio (necessario solo quando si installa un'estensione per la prima volta).

Se si verificano problemi durante l'accesso a Gestione estensioni in Azure Data Studio, è possibile scaricare l'estensione necessaria nella [Wiki di GitHub](https://github.com/microsoft/azuredatastudio/wiki/List-of-Extensions).


## <a name="access-installed-azure-data-studio-extensions"></a>Accedere alle estensioni di Azure Data Studio installate

Ogni estensione migliora l'esperienza in Azure Data Studio in modo diverso. Di conseguenza, il punto di ingresso per le estensioni può variare. Vedere la documentazione specifica per l'estensione installata per informazioni sul modo in cui è possibile accedere alle relative funzionalità dopo l'installazione.
