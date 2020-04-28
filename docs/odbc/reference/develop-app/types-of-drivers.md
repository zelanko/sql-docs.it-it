---
title: Tipi di driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver compatibility issues [ODBC]
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], application and driver compatibility
- compatibility [ODBC], application and driver compatibility
ms.assetid: 864c53c1-b68a-48b6-b6bc-5ecb520bb9dc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: de6d8e1473f127d28c69969e0fc298afd69d3023
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304872"
---
# <a name="types-of-drivers"></a>Tipi di driver
I driver ODBC possono essere classificati come segue:  
  
-   **ODBC 2 a 32 bit.**  
     **driver _x_ ** un driver a 32 bit che:  
  
    -   Esporta solo le funzioni ODBC *2. x* .  
  
    -   Mostra il comportamento di ODBC *2. x* per le modifiche comportamentali.  
  
-   **Driver conformi a ISO e Apri gruppo** Driver a 32 bit che:  
  
    -   Esporta tutte le funzioni documentate nel gruppo Open o nei documenti dell'interfaccia della riga di comando ISO. Verranno incluse alcune funzioni deprecate in ODBC.  
  
    -   Presenta il comportamento ODBC 3,0 per le modifiche comportamentali.  
  
    -   Non passa necessariamente attraverso Gestione driver ODBC 3,0.  
  
-   **Driver ODBC 3,0** Driver a 32 bit che:  
  
    -   Esporta solo le funzioni presenti in ODBC 3,0 meno funzioni deprecate.  
  
    -   È in grado di esporre il comportamento ODBC *2. x* o ODBC 3,0 in relazione alle modifiche comportamentali, in base all'attributo SQL_ATTR_APP_ODBC_VERSION Environment.  
  
-   **Driver ANSI 3,5 (o versione successiva) ODBC** Driver a 32 bit che:  
  
    -   Esporta solo le funzioni presenti in ODBC 3,5 meno funzioni deprecate.  
  
    -   È in grado di esporre il comportamento ODBC *2. x* o ODBC 3,0 o il comportamento ODBC 3,5 rispetto alle modifiche comportamentali, in base all'attributo SQL_ATTR_APP_ODBC_VERSION Environment.  
  
-   **Driver Unicode ODBC 3,5 (o versione successiva)** Driver a 32 bit che:  
  
    -   Supporta tutte le funzionalità di un driver ODBC 3,5 ANSI.  
  
    -   Esporta versioni Unicode di tutte le API stringa ODBC.  
  
    -   Consente di archiviare ed elaborare dati Unicode nell'origine dati.  
  
> [!NOTE]  
>  i driver ODBC a 16 bit non funzioneranno direttamente con Gestione driver ODBC *3. x* . Tuttavia, è possibile che i driver a 16 bit funzionino con Gestione driver ODBC 2,0, che successivamente consente di eseguire il thunk fino alla gestione driver *3. x* .
