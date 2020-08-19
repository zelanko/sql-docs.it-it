---
description: Confronto tra segnalibri
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 939c3780fc9c6738a307e9a969a346951cfac5e7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476783"
---
# <a name="comparing-bookmarks"></a>Confronto tra segnalibri
Poiché i segnalibri sono confrontabili con i byte, possono essere confrontati per verificarne l'uguaglianza o la disuguaglianza. A tale scopo, un'applicazione considera ogni segnalibro come una matrice di byte e confronta due segnalibri byte per byte. Poiché è garantito che i segnalibri siano distinti solo all'interno di un set di risultati, non è sensato confrontare i segnalibri ottenuti da set di risultati diversi.
