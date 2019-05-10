---
title: Abilitare o disabilitare la raccolta dati di utilizzo e segnalazione degli arresti anomali
titleSuffix: Azure Data Studio
description: In questo articolo viene illustrato come controllare se vengono raccolti e inviati a Microsoft informazioni sull'utilizzo e dati di segnalazione arresto anomalo del sistema.
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
manager: craigg
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 7eeebe22f73815b053c0b9d1adfb53259732695f
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/06/2019
ms.locfileid: "65089538"
---
# <a name="enable-or-disable-usage-data-collection-for-includename-sosincludesname-sos-shortmd"></a>Abilitare o disabilitare la raccolta di dati di utilizzo per [!INCLUDE[name-sos](../includes/name-sos-short.md)]

## <a name="how-to-disable-telemetry-reporting"></a>Come disabilitare la segnalazione di dati di telemetria

[!INCLUDE[name-sos](../includes/name-sos-short.md)]raccoglie dati sull'utilizzo e li invia a Microsoft per contribuire a migliorare i prodotti e i servizi. Per altre informazioni, leggere l'[informativa sulla privacy](https://go.microsoft.com/fwlink/?LinkID=528096&clcid=0x409).

Se non si vuole inviare i dati di utilizzo a Microsoft, è possibile impostare il *telemetry.enableTelemetry* se si imposta su *false*.

Per tutti gli eventi di telemetria da disattiva [!INCLUDE[name-sos](../includes/name-sos-short.md)], da **File** > **preferenze** > **impostazioni**, aggiungere la seguente opzione:

```json
    "telemetry.enableTelemetry": false
```

**Avviso importante**: Questa opzione richiede un riavvio del [!INCLUDE[name-sos](../includes/name-sos-short.md)] abbiano effetto. 

## <a name="how-to-disable-crash-reporting"></a>Come disabilitare la segnalazione degli arresti anomali

Per disabilitare la segnalazione di arresto anomalo del sistema, scegliere **File**  >  **Preferenze**  >  **Impostazioni** e aggiungere l'opzione seguente:

```json
    "telemetry.enableCrashReporter": false
```

**Avviso importante**: Questa opzione richiede un riavvio del [!INCLUDE[name-sos](../includes/name-sos-short.md)] abbiano effetto.

## <a name="additional-resources"></a>Risorse aggiuntive
- [Area di lavoro e impostazioni utente](settings.md)
