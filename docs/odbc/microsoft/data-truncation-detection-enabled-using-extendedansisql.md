---
title: Rilevamento del troncamento dei dati abilitato tramite ExtendedAnsiSQL Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- truncating data [ODBC]
- extendedANSISQL [ODBC], data truncation detection
ms.assetid: cec2359b-917d-4e1d-9625-5cd678b62f10
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ae1aa7a8a8b9ea2c3f3054717546506e660d5270
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280699"
---
# <a name="data-truncation-detection-enabled-using-extendedansisql"></a>Rilevamento dei dati troncati abilitato con ExtendedAnsiSQL
Quando il flag ExtendedAnsiSQL è attivato e l'applicazione inserisce dati in una colonna di tipo char o binario e i dati vengono troncati, il troncamento verrà rilevato. Quando il flag ExtendedAnsiSQL è disattivato, i dati vengono troncati senza avviso, come nelle versioni precedenti dei driver di database desktop ODBC.
