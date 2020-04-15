---
title: Tipi di applicazioni Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- upgrading applications [ODBC], application types
- backward compatibility [ODBC], application and driver compatibility
- compatibility [ODBC], application and driver compatibility
- application upgrades [ODBC], application types
- application compatibility issues [ODBC]
ms.assetid: d346a64e-a32c-4153-a40f-5b53c2f57ef2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f14326c9cec1eb89e431154c91b680e4688fcdfa
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305532"
---
# <a name="types-of-applications"></a>Tipi di applicazioni
Le applicazioni ODBC possono essere classificate come segue:  
  
-   **ODBC puro 2.**  
     ** _x_ Applicazione** Un'applicazione a 32 bit che:  
  
    -   Chiama solo ODBC 2. *x* (inclusa la funzione ODBC 1.0 **SQLSetParam**). Questi includono ODBC 1. *x* applicazioni di cui è stato eseguito il porting a 32 bit.  
  
    -   Prevede ODBC 2. *x* per le funzionalità che hanno subito modifiche comportamentali. Per ulteriori informazioni, vedere [Modifiche comportamentali.](../../../odbc/reference/develop-app/behavioral-changes.md)  
  
    -   Non è stato ricompilato con intestazioni ODBC 3.5.  
  
-   **ODBC puro 2.**  
     **_x_ Applicazione ricompilata** A ODBC 2 puro. *x* applicazione che è stata ricompilata utilizzando i file di intestazione ODBC 3.5, impostando ODBCVER-0x0250.  
  
-   **ODBC puro 2.**  
     **_x_ Applicazione Unicode** A ODBC puro 2. *x* applicazione ricompilata che è conforme a Unicode e utilizza il tipo di dati SQL_WCHAR.  
  
-   **Pure Open Group e ISO**-**compatibile Applicazione ODBC** Un'applicazione a 32 bit che:  
  
    -   Chiama le funzioni definite negli standard Open Group o ISO CLI. Queste funzioni possono includere funzioni 3.0 deprecate.  
  
    -   Non utilizza i tipi di dati Unicode.  
  
    -   Si aspetta il comportamento di ODBC 3.0 per le funzionalità che hanno subito modifiche comportamentali.  
  
-   **Applicazione ODBC 3.0 pure** Un'applicazione a 32 bit che:  
  
    -   Viene compilato con intestazioni 3.0.  
  
    -   Chiama qualsiasi funzione ODBC 3.0, inclusi quelli deprecati.  
  
    -   Si aspetta il comportamento di ODBC 3.0 per le funzionalità che hanno subito modifiche comportamentali.  
  
-   **Applicazione PURE ODBC 3.5** Un'applicazione a 32 o 64 bit che:  
  
    -   Può utilizzare tipi di dati Unicode.  
  
    -   Chiama qualsiasi funzione ODBC 3.5, inclusi quelli deprecati.  
  
    -   Si aspetta il comportamento di ODBC 3.5 per le funzionalità che hanno subito modifiche comportamentali.  
  
-   **Applicazione ODBC 3.8 (o versione successiva) pure** Un'applicazione a 32 bit o a 64 bit che:  
  
    -   Può utilizzare tipi di dati Unicode.  
  
    -   Chiama qualsiasi funzione ODBC 3.8, inclusi quelli deprecati.  
  
    -   Si aspetta il comportamento di ODBC 3.8 per le funzionalità che hanno subito modifiche comportamentali.  
  
-   **Applicazione sostituita** Un'applicazione a 32 o 64 bit che:  
  
    -   Implementa un nuovo comportamento per la funzionalità duplicata.  
  
    -   Utilizza tutte le nuove funzionalità di una versione successiva di ODBC solo all'interno del codice condizionale.  
  
    -   Ha codice condizionale limitato per gestire le modifiche comportamentali o si è registrato come una versione precedente dell'applicazione ODBC.
