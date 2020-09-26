---
title: Abilitare o disabilitare la raccolta dei dati di utilizzo e la segnalazione di arresti anomali
description: Questo articolo illustra come controllare se i dati di utilizzo e di segnalazioni di arresti anomali vengono raccolti e inviati a Microsoft.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: how-to
author: markingmyname
ms.author: maghan
ms.reviewer: alayu, maghan, sstein
ms.custom: seodec18; seo-lt-2019
ms.date: 09/24/2018
ms.openlocfilehash: 5ef44a7e2981d98c749e25692e667ae71b42843d
ms.sourcegitcommit: 63aef5a96905f0b026322abc9ccb862ee497eebe
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/25/2020
ms.locfileid: "91363888"
---
# <a name="enable-or-disable-usage-data-collection-for-azure-data-studio"></a>Abilitare o disabilitare la raccolta dei dati di utilizzo per Azure Data Studio

## <a name="how-to-disable-telemetry-reporting"></a>Come disabilitare la creazione di report di telemetria

Azure Data Studio raccoglie i dati di utilizzo e li invia a Microsoft per contribuire a migliorare i prodotti e i servizi offerti. Per altre informazioni, leggere l'[informativa sulla privacy](https://go.microsoft.com/fwlink/?LinkID=528096&clcid=0x409).

Se non si vuole inviare i dati di utilizzo a Microsoft, è possibile impostare l'opzione *telemetry.enableTelemetry* su *false*.

Per disattivare tutti gli eventi di telemetria da Azure Data Studio, in **File** > **Preferenze** > **Impostazioni** aggiungere l'opzione seguente:

```json
    "telemetry.enableTelemetry": false
```

**Avviso importante**: Per rendere effettiva questa opzione è necessario riavviare Azure Data Studio. 

## <a name="how-to-disable-crash-reporting"></a>Come disabilitare la segnalazione di arresti anomali

Per disabilitare la segnalazione di arresti anomali, in **File** > **Preferenze** > **Impostazioni** aggiungere l'opzione seguente:

```json
    "telemetry.enableCrashReporter": false
```

**Avviso importante**: Per rendere effettiva questa opzione è necessario riavviare Azure Data Studio.

## <a name="additional-resources"></a>Risorse aggiuntive
- [Impostazioni utente e dell'area di lavoro](settings.md)
