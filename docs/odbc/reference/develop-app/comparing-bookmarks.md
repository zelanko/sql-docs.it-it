---
title: Confronto tra segnalibri | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], bookmarks
- comparing bookmarks [ODBC]
- bookmarks [ODBC]
ms.assetid: ea347635-fbe3-41c1-b537-4048b7c0f7da
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 44da652ad1e52934fa48f32b1b2f88b30212ad3b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68083297"
---
# <a name="comparing-bookmarks"></a>Confronto tra segnalibri
Poiché i segnalibri sono confrontabili con i byte, possono essere confrontati per verificarne l'uguaglianza o la disuguaglianza. A tale scopo, un'applicazione considera ogni segnalibro come una matrice di byte e confronta due segnalibri byte per byte. Poiché è garantito che i segnalibri siano distinti solo all'interno di un set di risultati, non è sensato confrontare i segnalibri ottenuti da set di risultati diversi.
