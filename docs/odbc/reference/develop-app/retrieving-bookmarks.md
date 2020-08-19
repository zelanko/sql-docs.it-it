---
description: Recupero di segnalibri
title: Recupero di segnalibri | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- retrieving bookmarks [ODBC]
- result sets [ODBC], bookmarks
- bookmarks [ODBC]
ms.assetid: a34c8f09-b786-4835-a44b-b7294c970aff
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 22fba0ccc900d221e915fea939736aa87b101e80
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429093"
---
# <a name="retrieving-bookmarks"></a>Recupero di segnalibri
Se l'applicazione utilizzerà segnalibri, è necessario impostare l'attributo SQL_ATTR_USE_BOOKMARKS istruzione su SQL_UB_VARIABLE prima di preparare o eseguire l'istruzione. Questa operazione è necessaria perché la compilazione e la gestione dei segnalibri può essere un'operazione costosa, quindi i segnalibri devono essere abilitati solo quando un'applicazione può utilizzarli in modo corretto.  
  
 I segnalibri vengono restituiti come colonna 0 del set di risultati. Un'applicazione può recuperarle in tre modi:  
  
-   Associare la colonna 0 del set di risultati. **SQLFetch** o **SQLFetchScroll** restituisce i segnalibri per ogni riga nel set di righe insieme ai dati relativi ad altre colonne associate.  
  
-   Chiamare **SQLSetPos** per posizionare in una riga del set di righe e quindi chiamare **SQLGetData** per la colonna 0. Se un driver supporta i segnalibri, deve sempre supportare la possibilità di chiamare **SQLGetData** per la colonna 0, anche se non consente alle applicazioni di chiamare **SQLGetData** per altre colonne prima dell'ultima colonna associata.  
  
-   Chiamare **SQLBulkOperations** con l'argomento *Operation* impostato su SQL_ADD e il limite della colonna 0. Il cursore inserisce la riga e restituisce il segnalibro per la riga nel buffer associato.
