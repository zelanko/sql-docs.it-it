---
title: Aggiornamento, eliminazione o recupero tramite segnalibro Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating by bookmarks [ODBC]
- result sets [ODBC], bookmarks
- fetches [ODBC], by bookmarks [ODBC]
- deleting by bookmarks [ODBC]
- bookmarks [ODBC]
ms.assetid: e2ee58d7-c28f-435f-b537-06207215dd2f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5e94a98bb577ef906afbb04539761fd07d15f772
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286151"
---
# <a name="updating-deleting-or-fetching-by-bookmark"></a>Aggiornamento, eliminazione o recupero tramite segnalibro
I segnalibri possono essere utilizzati per identificare i dati da aggiornare nel set di risultati, eliminati dal set di risultati o recuperati dal set di risultati ai buffer del set di righe. Queste operazioni vengono eseguite da una chiamata a **SQLBulkOperations** con un *Option* argomento di SQL_UPDATE_BY_BOOKMARK, SQL_DELETE_BY_BOOKMARK o SQL_FETCH_BY_BOOKMARK. I segnalibri utilizzati in queste operazioni vengono archiviati nella colonna 0 dei buffer del set di righe. Quando si esegue l'aggiornamento tramite segnalibro, i dati a cui vengono aggiornate le colonne del set di risultati vengono recuperati dai buffer del set di righe. Per ulteriori informazioni, vedere [Aggiornamento dei dati con SQLBulkOperations](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md).
