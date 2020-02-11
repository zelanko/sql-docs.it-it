---
title: Compatibilità del driver del database desktop | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68077277"
---
# <a name="desktop-database-driver-compatibility"></a>Compatibilità dei driver di database desktop
Unicode è un metodo di codifica dei caratteri software che considera tutti i caratteri con una larghezza fissa di due byte. Questo metodo viene usato come alternativa alla codifica dei caratteri ANSI di Windows, che, poiché rappresenta i caratteri in un byte, è limitato a 256 caratteri. Poiché Unicode può rappresentare più di 65.000 caratteri, include molti linguaggi i cui caratteri non sono rappresentati nella codifica ANSI.  
  
 La gestione driver ODBC 3,5 (o versione successiva) è abilitata per Unicode. Questo effetto riguarda due aree principali: le chiamate di funzione e i tipi di dati stringa. Gestione driver esegue il mapping degli argomenti della stringa di funzione e dei dati di tipo stringa come richiesto dall'applicazione e dal driver, che possono essere abilitati per Unicode o ANSI.  
  
 Gestione driver ODBC 3,5 (o versione successiva) supporta l'utilizzo di un driver Unicode con un'applicazione Unicode e un'applicazione ANSI. Supporta inoltre l'utilizzo di un driver ANSI con un'applicazione ANSI. Gestione driver fornisce un mapping da Unicode a ANSI limitato per un'applicazione Unicode che utilizza un driver ANSI. In questo modo è possibile accedere ai database Jet 3,5 e supportare tutti i tipi di file ISAM esistenti.  
  
 Quando un'applicazione ANSI utilizza il driver del database desktop ODBC 4,0 e accede a Microsoft Access 4,0 o versione successiva, il driver espone il tipo di dati come SQL_CHAR, SQL_VARCHAR o SQL_LONGVARCHAR anche se Jet 4,0 supporta la versione estesa. Le versioni precedenti di Jet non supportano SQL_WCHAR, SQL_WVARCHAR e SQL_WLONGVARCHAR. Questa restrizione si applica anche nei casi in cui i formati precedenti vengono usati con la motore di database Jet 4,0.  
  
 Per ulteriori informazioni sui problemi Unicode con ODBC, vedere la pagina relativa alle considerazioni sulla programmazione in [Unicode](../../odbc/reference/develop-app/unicode.md) .
