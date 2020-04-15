---
title: Confronto dei segnalibri Documenti Microsoft
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
ms.openlocfilehash: c28392c0d48984b4aaf8a8df442b6a4054a7eced
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307476"
---
# <a name="comparing-bookmarks"></a>Confronto tra segnalibri
Poiché i segnalibri sono byte-comparable, possono essere confrontati per l'uguaglianza o la disuguaglianza. A tale scopo, un'applicazione considera ogni segnalibro come una matrice di byte e confronta due segnalibri byte per byte. Poiché è garantito che i segnalibri siano distinti solo all'interno di un set di risultati, non ha senso confrontare i segnalibri ottenuti da set di risultati diversi.
