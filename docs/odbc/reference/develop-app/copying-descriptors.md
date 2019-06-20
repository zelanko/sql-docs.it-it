---
title: Copia di descrittori | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: da22ba86ea49532f460b081b13e18d6b7d95211c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63042757"
---
# <a name="copying-descriptors"></a>Copia di descrittori
Il **SQLCopyDesc** funzione viene chiamata per copiare i campi di un descrittore del descrittore di un altro. I campi possono essere copiati solo a un descrittore applicazione o un IPD, ma non a un'implementazione. I campi possono essere copiati da qualsiasi tipo di descrittore. Vengono copiati solo i campi definiti per i descrittori di origine e di destinazione. **SQLCopyDesc** non copia il campo SQL_DESC_ALLOC_TYPE, perché non è possibile modificare il tipo di allocazione del descrittore. Campi copiati sovrascrivono i campi esistenti.  
  
 Un ARD sull'handle di un'unica istruzione può essere utilizzato come APD su un altro handle di istruzione. In questo modo un'applicazione per copiare le righe tra le tabelle senza copiare i dati a livello di applicazione. A tale scopo, viene riutilizzato un descrittore della riga che descrive una riga recuperata di una tabella come un descrittore di parametri per un parametro in un'istruzione INSERT. Il tipo di informazioni SQL_MAX_CONCURRENT_ACTIVITIES deve essere maggiore di 1 per eseguire questa operazione.
