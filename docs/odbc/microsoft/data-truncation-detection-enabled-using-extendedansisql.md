---
title: Rilevamento dei dati abilitato con ExtendedAnsiSQL | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 95b7d538c2ace45b42c947b56ca5a5bd5f981ec5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62744273"
---
# <a name="data-truncation-detection-enabled-using-extendedansisql"></a>Rilevamento dei dati troncati abilitato con ExtendedAnsiSQL
Quando il flag ExtendedAnsiSQL è attivato e l'applicazione è di inserimento dei dati in un char o colonna di dati binari e i dati vengono troncati, il troncamento viene rilevato. Quando il flag ExtendedAnsiSQL è disattivato, i dati vengono troncati senza alcun avviso, come accadeva nelle versioni precedenti dei driver di Database Desktop ODBC.
