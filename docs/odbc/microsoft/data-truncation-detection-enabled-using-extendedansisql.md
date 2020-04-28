---
title: Rilevamento del troncamento dei dati abilitato con ExtendedAnsiSQL | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81280699"
---
# <a name="data-truncation-detection-enabled-using-extendedansisql"></a>Rilevamento dei dati troncati abilitato con ExtendedAnsiSQL
Quando il flag ExtendedAnsiSQL è attivato e l'applicazione inserisce dati in una colonna char o binary e i dati vengono troncati, il troncamento verrà rilevato. Quando il flag ExtendedAnsiSQL è disattivato, i dati vengono troncati senza avviso, come nelle versioni precedenti dei driver del database desktop ODBC.
