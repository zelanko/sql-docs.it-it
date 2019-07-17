---
title: Compatibilità dei Driver di Database desktop | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], Unicode
- Unicode [ODBC], desktop database drivers
- ODBC desktop database drivers [ODBC], Unicode
- backward compatibility [ODBC], Unicode
- desktop database drivers [ODBC], Unicode
- Jet-based ODBC drivers [ODBC], Unicode
ms.assetid: dd695638-1a0b-4e27-8a6a-9510ebb5a5ee
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 31263162526b6bd2e0a116a473f09f9e2caeba94
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077277"
---
# <a name="desktop-database-driver-compatibility"></a>Compatibilità dei driver di database desktop
Unicode è un metodo di codifica dei caratteri software considera tutti i caratteri con una larghezza fissa di due byte. Questo metodo viene utilizzato come alternativa alla codifica dei caratteri ANSI di Windows che, poiché rappresenta caratteri in un byte, è limitata a 256 caratteri. Poiché Unicode può rappresentare oltre 65.000 caratteri, avviene per molti linguaggi cui caratteri non sono rappresentati nella codifica ANSI.  
  
 La gestione Driver ODBC 3.5 (o versioni successive) è abilitata per Unicode. Ciò influisce su due aree principali: chiamate di funzione e tipi di dati stringa. Gli argomenti di stringa funzione di gestione Driver mappe e dati di tipo stringa come richiesto dall'applicazione e driver, entrambi possono essere abilitata per Unicode o ANSI abilitati.  
  
 La gestione Driver ODBC 3.5 (o versioni successive) supporta l'utilizzo di un driver di Unicode con un'applicazione Unicode e nelle applicazioni ANSI. Supporta inoltre l'utilizzo di un driver ANSI con applicazioni ANSI. Gestione Driver fornisce mapping Unicode-to-ANSI limitato per un'applicazione Unicode funziona con un driver ANSI. Ciò consente l'accesso ai database Jet 3.5 e supporto di tutti i tipi di file ISAM esistenti.  
  
 Quando nelle applicazioni ANSI Usa la 4.0 del Driver di Database Desktop ODBC e accede a Microsoft Access 4.0 o versioni successive, il driver espone il tipo di dati come SQL_CHAR, SQL_VARCHAR o SQL_LONGVARCHAR anche se Jet 4.0 supporta la versione grande. Le versioni precedenti di Jet non supportano SQL_WCHAR, SQL_WVARCHAR e SQL_WLONGVARCHAR. Questa restrizione si applica anche nei casi in cui i vecchi formati vengono utilizzati con il motore di Database Jet 4.0.  
  
 Per altre informazioni relative ai problemi di Unicode con ODBC, vedere [Unicode](../../odbc/reference/develop-app/unicode.md) in considerazioni sulla programmazione.
