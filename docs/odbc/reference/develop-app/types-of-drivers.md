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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 445fe3a0b87e6ad8e35dbc585981d874f8e357bf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63306211"
---
# <a name="types-of-drivers"></a>Tipi di driver
Driver ODBC possono essere classificati come indicato di seguito:  
  
-   **32 bit ODBC 2.**  
     **_x_ Driver** driver A 32 bit che:  
  
    -   Consente di esportare solo l'API ODBC 2*x* funzioni.  
  
    -   Mostra ODBC 2.*x* comportamento per modifiche del comportamento.  
  
-   **ISO e aprire i Driver compatibili con gruppo** driver A 32 bit che:  
  
    -   Esporta tutte le funzioni che sono documentate nei documenti Open Group o ISO CLI. Ciò include alcune delle funzioni che sono deprecate in ODBC.  
  
    -   Presenta un comportamento ODBC 3.0 per modifiche del comportamento.  
  
    -   Non necessariamente esamina la gestione dei Driver ODBC 3.0.  
  
-   **Driver ODBC 3.0** driver A 32 bit che:  
  
    -   Esporta solo le funzioni che sono nella versione 3.0 di ODBC meno funzioni deprecate.  
  
    -   È in grado di che esibisce ODBC 2.*x* comportamento o il comportamento ODBC 3.0 rispetto alle modifiche di comportamento, basato sull'attributo SQL_ATTR_APP_ODBC_VERSION ambiente.  
  
-   **Driver ODBC 3.5 (o versioni successive) ANSI** driver A 32 bit che:  
  
    -   Esporta solo le funzioni che sono in ODBC 3.5 meno funzioni deprecate.  
  
    -   È in grado di che esibisce ODBC 2. *x* comportamento o il comportamento ODBC 3.0 o comportamento ODBC 3.5 rispetto alle modifiche del comportamento, basato sull'attributo SQL_ATTR_APP_ODBC_VERSION ambiente.  
  
-   **Driver ODBC 3.5 (o versioni successive) Unicode** driver A 32 bit che:  
  
    -   Supporta tutte le funzionalità di un driver ODBC 3.5 ANSI.  
  
    -   Esporta le versioni Unicode delle stringa ODBC tutte le API.  
  
    -   Può archiviare ed elaborare i dati Unicode nell'origine dati.  
  
> [!NOTE]  
>  driver ODBC a 16 bit non funziona direttamente con ODBC 3. *x* gestione Driver. Tuttavia, è possibile che i driver a 16 bit lavorare con la gestione di Driver ODBC 2.0, che successivamente thunk fino a 3. *x* gestione Driver.
