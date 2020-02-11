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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d7fb67171a796755bf8d6229b9d562f69bd588ed
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68096513"
---
# <a name="data-truncation-detection-enabled-using-extendedansisql"></a>Rilevamento dei dati troncati abilitato con ExtendedAnsiSQL
Quando il flag ExtendedAnsiSQL è attivato e l'applicazione inserisce dati in una colonna char o binary e i dati vengono troncati, il troncamento verrà rilevato. Quando il flag ExtendedAnsiSQL è disattivato, i dati vengono troncati senza avviso, come nelle versioni precedenti dei driver del database desktop ODBC.
