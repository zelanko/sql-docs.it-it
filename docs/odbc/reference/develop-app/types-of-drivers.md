---
title: Tipi di driver Documenti Microsoft
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304872"
---
# <a name="types-of-drivers"></a>Tipi di driver
I driver ODBC possono essere classificati come segue:  
  
-   **ODBC 2 a 32 bit.**  
     ** _x_ Driver** Un driver a 32 bit che:  
  
    -   Esporta solo le funzioni ODBC *2.x.*  
  
    -   Espone il comportamento di ODBC *2.x* per le modifiche comportamentali.  
  
-   **ISO e driver aperto conforme al gruppo** Un driver a 32 bit che:  
  
    -   Esporta tutte le funzioni documentate nei documenti Open Group o ISO CLI. Sono incluse alcune delle funzioni deprecate in ODBC.  
  
    -   Espone il comportamento di ODBC 3.0 per le modifiche comportamentali.  
  
    -   Non passa necessariamente attraverso Gestione driver ODBC 3.0.  
  
-   **Driver ODBC 3.0** Un driver a 32 bit che:  
  
    -   Esporta solo le funzioni che si trovano in ODBC 3.0 meno funzioni deprecate.  
  
    -   È in grado di esporre il comportamento ODBC *2.x* o ODBC 3.0 rispetto alle modifiche comportamentali, in base all'attributo di ambiente SQL_ATTR_APP_ODBC_VERSION.  
  
-   **Driver ANSI ODBC 3.5 (o versione successiva)** Un driver a 32 bit che:  
  
    -   Esporta solo le funzioni che si trovano in ODBC 3.5 meno funzioni deprecate.  
  
    -   È in grado di mostrare il comportamento ODBC *2.x* o il comportamento ODBC 3.0 o il comportamento ODBC 3.5 rispetto alle modifiche comportamentali, in base all'attributo di ambiente SQL_ATTR_APP_ODBC_VERSION.  
  
-   **Driver Unicode ODBC 3.5 (o versione successiva)** Un driver a 32 bit che:  
  
    -   Supporta tutte le funzionalità di un driver ANSI ODBC 3.5.  
  
    -   Esporta le versioni Unicode di tutte le API di stringa ODBC.  
  
    -   Può archiviare ed elaborare i dati Unicode nell'origine dati.  
  
> [!NOTE]  
>  I driver ODBC a 16 bit non funzioneranno direttamente con Gestione driver ODBC *3.x.* Tuttavia, è possibile che i driver a 16 bit funzionino con Gestione driver ODBC 2.0, che successivamente si è affiancato a Gestione driver *3.x.*
