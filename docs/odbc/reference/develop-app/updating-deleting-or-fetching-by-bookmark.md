---
description: Aggiornamento, eliminazione o recupero tramite segnalibro
title: Aggiornamento, eliminazione o recupero tramite segnalibro | Microsoft Docs
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
ms.openlocfilehash: 2202e3483e13848ccac7f7e6f21145ba9704a8b7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448948"
---
# <a name="updating-deleting-or-fetching-by-bookmark"></a>Aggiornamento, eliminazione o recupero tramite segnalibro
I segnalibri possono essere utilizzati per identificare i dati da aggiornare nel set di risultati, eliminati dal set di risultati o recuperati dal set di risultati ai buffer dei set di righe. Queste operazioni vengono eseguite da una chiamata a **SQLBulkOperations** con un argomento *Option* di SQL_UPDATE_BY_BOOKMARK, SQL_DELETE_BY_BOOKMARK o SQL_FETCH_BY_BOOKMARK. I segnalibri utilizzati in queste operazioni vengono archiviati nella colonna 0 dei buffer del set di righe. Quando si esegue l'aggiornamento tramite segnalibro, i dati a cui vengono aggiornate le colonne del set di risultati vengono recuperati dai buffer del set di righe. Per ulteriori informazioni, vedere [aggiornamento dei dati con SQLBulkOperations](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md).
