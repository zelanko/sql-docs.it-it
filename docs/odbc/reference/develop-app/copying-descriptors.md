---
title: Copia dei descrittori Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], copying
- copying descriptors [ODBC]
ms.assetid: 949a860d-6579-4218-882e-8c061688dd87
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2e2e5897afc3673a21396e256df04d25008c8cdf
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301670"
---
# <a name="copying-descriptors"></a>Copia di descrittori
La funzione **SQLCopyDesc** viene chiamata per copiare i campi di un descrittore in un altro descrittore. I campi possono essere copiati solo in un descrittore dell'applicazione o in un IPD, ma non in un IRD. I campi possono essere copiati da qualsiasi tipo di descrittore. Vengono copiati solo i campi definiti sia per i descrittori di origine che per quelli di destinazione. **SQLCopyDesc** non copia il campo SQL_DESC_ALLOC_TYPE, perché il tipo di allocazione di un descrittore non può essere modificato. I campi copiati sovrascrivono i campi esistenti.  
  
 Un ARD su un handle di istruzione può fungere da aPD su un altro handle di istruzione. Ciò consente a un'applicazione di copiare righe tra tabelle senza copiare dati a livello di applicazione. A tale scopo, un descrittore di riga che descrive una riga recuperata di una tabella viene riutilizzato come descrittore di parametro per un parametro in un'istruzione INSERT. Affinché l'operazione abbia esito positivo, il tipo di informazioni SQL_MAX_CONCURRENT_ACTIVITIES deve essere maggiore di 1.
