---
description: Rilevamento dei dati troncati abilitato con ExtendedAnsiSQL
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
ms.openlocfilehash: 26965093caecbc11e94ef738ba6b8ff757b43258
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412889"
---
# <a name="data-truncation-detection-enabled-using-extendedansisql"></a>Rilevamento dei dati troncati abilitato con ExtendedAnsiSQL
Quando il flag ExtendedAnsiSQL è attivato e l'applicazione inserisce dati in una colonna char o binary e i dati vengono troncati, il troncamento verrà rilevato. Quando il flag ExtendedAnsiSQL è disattivato, i dati vengono troncati senza avviso, come nelle versioni precedenti dei driver del database desktop ODBC.
