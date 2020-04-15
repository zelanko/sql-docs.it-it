---
title: Limitazioni dell'utilizzo di cursori basati su keyset Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], cursors
- keyset-driven cursors [ODBC]
ms.assetid: 59d86fed-387c-4719-9550-36343e74da44
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2aeb5a0c50192118dfff8ed7d866c3911c2b4007
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284151"
---
# <a name="limitations-of-using-keyset-driven-cursors"></a>Limitazioni dell'uso dei cursori gestiti da keyset
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Utilizzare invece il driver ODBC fornito da Oracle.  
  
 È necessario essere in grado di recuperare una singola colonna ROWID per la tabella sottoposta a query. Un cursore basato su keyset non può essere utilizzato in join, query o istruzioni che contengono clausole DISTINCT, GROUP BY, UNION, INTERSECT o MINUS.  
  
 Inoltre, se l'applicazione utilizza alias di tabella, i cursori basati su keyset non funzioneranno; sono obbligatori tipi di cursore forward-only o statici. L'utilizzo del tipo di cursore keyset con alias di tabella causerà il seguente errore: "[Microsoft][ODBC driver for Oracle]Cannot use Keyset-driven cursor on join, with union, intersect or minus or on read only result set."  
  
> [!NOTE]  
>  A causa del modo in cui il driver gestisce l'istruzione SQL che viene inviata al server Oracle, Oracle restituisce internamente il seguente messaggio di errore: "ORA-00964: nome della tabella non nell'elenco FROM".
