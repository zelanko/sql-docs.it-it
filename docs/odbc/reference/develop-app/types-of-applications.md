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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f14326c9cec1eb89e431154c91b680e4688fcdfa
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305532"
---
# <a name="types-of-applications"></a>Tipi di applicazioni
Le applicazioni ODBC possono essere classificate come segue:  
  
-   **ODBC pure 2.**  
     ** _x_ applicazione** un'applicazione a 32 bit che:  
  
    -   Chiama solo ODBC 2. funzioni *x* (inclusa la funzione ODBC 1,0 **SQLSetParam**). Che includono ODBC 1. *x* applicazioni che sono state trasferite a 32 bit.  
  
    -   Prevede ODBC 2. comportamento *x* per le funzionalità che hanno modificato il comportamento. Per ulteriori informazioni, vedere [modifiche del comportamento](../../../odbc/reference/develop-app/behavioral-changes.md) .  
  
    -   Non è stato ricompilato con le intestazioni ODBC 3,5.  
  
-   **ODBC pure 2.**  
     **_x_ applicazione ricompilata** ODBC 2 puro. applicazione *x* ricompilata utilizzando i file di intestazione ODBC 3,5, impostando ODBCVer = 0x0250.  
  
-   **ODBC pure 2.**  
     **_x_ applicazione Unicode** un ODBC 2 puro. *x* applicazione ricompilata che è conforme a Unicode e utilizza il tipo di dati SQL_WCHAR.  
  
-   **Applicazione ODBC Open Group e**-**conforme allo standard** ISO un'applicazione a 32 bit che:  
  
    -   Chiama funzioni definite negli standard del gruppo aperto o dell'interfaccia della riga di comando ISO. Queste funzioni possono includere funzioni 3,0 deprecate.  
  
    -   Non utilizza i tipi di dati Unicode.  
  
    -   Prevede il comportamento di ODBC 3,0 per le funzionalità che hanno modificato il comportamento.  
  
-   **Applicazione ODBC 3,0 pure** Applicazione a 32 bit che:  
  
    -   Viene compilato con le intestazioni 3,0.  
  
    -   Chiama qualsiasi funzione ODBC 3,0, eventualmente includendo gli elementi deprecati.  
  
    -   Prevede il comportamento di ODBC 3,0 per le funzionalità che hanno modificato il comportamento.  
  
-   **Applicazione ODBC 3,5 pure** Un'applicazione 32 o a 64 bit che:  
  
    -   Può utilizzare tipi di dati Unicode.  
  
    -   Chiama qualsiasi funzione ODBC 3,5, eventualmente includendo gli elementi deprecati.  
  
    -   Prevede il comportamento di ODBC 3,5 per le funzionalità che hanno modificato il comportamento.  
  
-   **Applicazione ODBC 3,8 (o versione successiva)** Applicazione a 32 bit o a 64 bit che:  
  
    -   Può utilizzare tipi di dati Unicode.  
  
    -   Chiama qualsiasi funzione ODBC 3,8, eventualmente includendo gli elementi deprecati.  
  
    -   Prevede il comportamento di ODBC 3,8 per le funzionalità che hanno modificato il comportamento.  
  
-   **Applicazione sostituita** Un'applicazione 32 o a 64 bit che:  
  
    -   Implementa un nuovo comportamento per la funzionalità duplicata.  
  
    -   Utilizza tutte le nuove funzionalità di una versione successiva di ODBC solo all'interno del codice condizionale.  
  
    -   Dispone di un codice condizionale limitato per gestire le modifiche comportamentali o si è registrato come versione precedente dell'applicazione ODBC.
