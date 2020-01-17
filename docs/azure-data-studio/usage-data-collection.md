---
title: Abilitare o disabilitare la raccolta dei dati di utilizzo e la segnalazione di arresti anomali
titleSuffix: Azure Data Studio
description: Questo articolo illustra come controllare se i dati di utilizzo e di segnalazioni di arresti anomali vengono raccolti e inviati a Microsoft.
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18; seo-lt-2019
ms.date: 09/24/2018
ms.openlocfilehash: 416c22aa04e289e7959e41924344666e4329ecf1
ms.sourcegitcommit: 39ea690996a7390e3d13d6fb8f39d8641cd5f710
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/10/2019
ms.locfileid: "74957005"
---
# <a name="enable-or-disable-usage-data-collection-for-includename-sosincludesname-sos-shortmd"></a>Abilitare o disabilitare la raccolta dei dati di utilizzo per [!INCLUDE[name-sos](../includes/name-sos-short.md)]

## <a name="how-to-disable-telemetry-reporting"></a>Come disabilitare la creazione di report di telemetria

[!INCLUDE[name-sos](../includes/name-sos-short.md)] raccoglie i dati di utilizzo e li invia a Microsoft per contribuire a migliorare i prodotti e i servizi offerti. Per altre informazioni, leggere l'[informativa sulla privacy](https://go.microsoft.com/fwlink/?LinkID=528096&clcid=0x409).

Se non si vuole inviare i dati di utilizzo a Microsoft, è possibile impostare l'opzione *telemetry.enableTelemetry* su *false*.

Per disattivare tutti gli eventi di telemetria da [!INCLUDE[name-sos](../includes/name-sos-short.md)], in **File** > **Preferenze** > **Impostazioni** aggiungere l'opzione seguente:

```json
    "telemetry.enableTelemetry": false
```

**Avviso importante**: per rendere effettiva questa opzione, è necessario riavviare [!INCLUDE[name-sos](../includes/name-sos-short.md)]. 

## <a name="how-to-disable-crash-reporting"></a>Come disabilitare la segnalazione di arresti anomali

Per disabilitare la segnalazione di arresti anomali, in **File** > **Preferenze** > **Impostazioni** aggiungere l'opzione seguente:

```json
    "telemetry.enableCrashReporter": false
```

**Avviso importante**: per rendere effettiva questa opzione, è necessario riavviare [!INCLUDE[name-sos](../includes/name-sos-short.md)].

## <a name="additional-resources"></a>Risorse aggiuntive
- [Impostazioni utente e dell'area di lavoro](settings.md)
