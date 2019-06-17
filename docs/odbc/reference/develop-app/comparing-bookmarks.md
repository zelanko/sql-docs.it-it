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
manager: craigg
ms.openlocfilehash: 690acf80bfabdc04d5f70b780e41943337c18cb9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63026606"
---
# <a name="comparing-bookmarks"></a>Confronto tra segnalibri
I segnalibri sono paragonabili in termini di byte, essi possono essere confrontati per verificarne l'uguaglianza o disuguaglianza. A tale scopo, un'applicazione considera ogni segnalibro come una matrice di byte e consente di confrontare due segnalibri una byte per byte. Poiché i segnalibri sono garantiti essere univoci solo all'interno di un set di risultati, è opportuno non confrontare i segnalibri ottenuti da diversi set di risultati.
