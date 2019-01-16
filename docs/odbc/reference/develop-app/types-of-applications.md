---
title: Tipi di applicazioni | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 50e3e733a4ddd4855da2ea7722407e5f061eee47
ms.sourcegitcommit: bfa10c54e871700de285d7f819095d51ef70d997
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2019
ms.locfileid: "54255796"
---
# <a name="types-of-applications"></a>Tipi di applicazioni
Le applicazioni ODBC possono essere classificate come segue:  
  
-   **Pure ODBC 2.**  
     **_x_ applicazione** applicazione A 32 bit che:  
  
    -   Chiama solo ODBC 2. *x* funzioni (inclusa la funzione ODBC 1.0 **SQLSetParam**). Ad esempio ODBC 1. *x* le applicazioni che sono state trasferite a 32 bit.  
  
    -   Si aspetta che ODBC 2. *x* comportamento per le funzionalità che hanno subito modifiche del comportamento. (Vedere [modifiche del comportamento](../../../odbc/reference/develop-app/behavioral-changes.md) per altre informazioni.)  
  
    -   Non è stato ricompilato con le intestazioni di ODBC 3.5.  
  
-   **Pure ODBC 2.**  
     **_x_ dell'applicazione ricompilata** un puro di ODBC 2. *x* applicazione che è stato ricompilato utilizzando i file di intestazione ODBC 3.5, impostando ODBCVER = 0x0250.  
  
-   **Pure ODBC 2.**  
     **_x_ Unicode Application** un puro di ODBC 2. *x* ricompilato l'applicazione che è conforme a Unicode e Usa il tipo di dati SQL_WCHAR.  
  
-   **Gruppo aperta pure e ISO**-**applicazione conforme a ODBC** applicazione A 32 bit che:  
  
    -   Chiama le funzioni definite negli standard Open Group o ISO CLI. (Queste funzioni possono includere funzioni deprecate 3.0).  
  
    -   Non usa i tipi di dati Unicode.  
  
    -   È previsto il comportamento ODBC 3.0 per le funzionalità che hanno subito modifiche del comportamento.  
  
-   **Applicazione di pura ODBC 3.0** applicazione A 32 bit che:  
  
    -   Viene compilato con le 3.0 intestazioni.  
  
    -   Chiama qualsiasi funzione ODBC 3.0, magari con quelli che sono deprecati.  
  
    -   È previsto il comportamento ODBC 3.0 per le funzionalità che hanno subito modifiche del comportamento.  
  
-   **Applicazione di pura ODBC 3.5** A 32 o 64 bit dell'applicazione che:  
  
    -   Può usare tipi di dati Unicode.  
  
    -   Chiama qualsiasi funzione ODBC 3.5, magari con quelli che sono deprecati.  
  
    -   Comportamento di ODBC 3.5 per le funzionalità che hanno subito modifiche del comportamento è previsto.  
  
-   **Applicazione di pura ODBC 3.8 (o versioni successive)** applicazione A 32 bit o 64 bit che:  
  
    -   Può usare tipi di dati Unicode.  
  
    -   Chiama qualsiasi funzione ODBC 3.8, magari con quelli che sono deprecati.  
  
    -   Comportamento di ODBC 3.8 per le funzionalità che hanno subito modifiche del comportamento è previsto.  
  
-   **Sostituito applicazione** A 32 o 64 bit dell'applicazione che:  
  
    -   Nuovo comportamento implementa per funzionalità duplicate.  
  
    -   Utilizza tutte le nuove funzionalità in una versione successiva di ODBC solo all'interno di codice condizionale.  
  
    -   Ha limitato il codice condizionale per gestire modifiche del comportamento o ha eseguito la registrazione per una versione precedente dell'applicazione ODBC.
