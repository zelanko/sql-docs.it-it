---
title: Compatibilità con i driver di database per il desktop Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 89eea7ab112eaefdc73c7cbc72ee3555797c7efd
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303522"
---
# <a name="desktop-database-driver-compatibility"></a>Compatibilità dei driver di database desktop
Unicode è un metodo di codifica dei caratteri software che considera tutti i caratteri con una larghezza fissa di due byte. Questo metodo viene utilizzato come alternativa alla codifica dei caratteri ANSI di Windows, che, poiché rappresenta i caratteri in un byte, è limitata a 256 caratteri. Poiché Unicode può rappresentare oltre 65.000 caratteri, supporta molte lingue i cui caratteri non sono rappresentati nella codifica ANSI.  
  
 Gestione Driver ODBC 3.5 (o versione successiva) è abilitato per Unicode. Ciò influisce su due aree principali: chiamate di funzione e tipi di dati stringa. Gestione Driver esegue il mapping di argomenti di stringa di funzione e dati di stringa come richiesto dall'applicazione e dal driver, entrambi i quali possono essere abilitati per Unicode o ANSI.  
  
 Gestione driver ODBC 3.5 (o versione successiva) supporta l'utilizzo di un driver Unicode con un'applicazione Unicode e un'applicazione ANSI. Supporta inoltre l'utilizzo di un driver ANSI con un'applicazione ANSI. Gestione Driver fornisce un mapping Unicode-ANSI limitato per un'applicazione Unicode che utilizza un driver ANSI. Ciò consente l'accesso ai database Jet 3.5 e il supporto di tutti i tipi di file ISAM esistenti.  
  
 Quando un'applicazione ANSI utilizza il driver di database Desktop ODBC 4.0 e accede a Microsoft Access 4.0 o versione successiva, il driver espone il tipo di dati come SQL_CHAR, SQL_VARCHAR o SQL_LONGVARCHAR anche se Jet 4.0 supporta la versione wide. Le versioni precedenti di Jet non supportano SQL_WCHAR, SQL_WVARCHAR e SQL_WLONGVARCHAR. Questa restrizione si applica anche nei casi in cui i formati precedenti vengono utilizzati con il motore di database Jet 4.0.This restriction also app in cases where the old formats are used with the Jet 4.0 Database Engine.  
  
 Per altre informazioni sui problemi Unicode con ODBC, vedere [Unicode](../../odbc/reference/develop-app/unicode.md) in Considerazioni sulla programmazione.
