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
ms.openlocfilehash: 7d41cd744d39113c556c4ee8bc17411b7992e596
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68002147"
---
# <a name="copying-descriptors"></a>Copia di descrittori
Il **SQLCopyDesc** funzione viene chiamata per copiare i campi di un descrittore del descrittore di un altro. I campi possono essere copiati solo a un descrittore applicazione o un IPD, ma non a un'implementazione. I campi possono essere copiati da qualsiasi tipo di descrittore. Vengono copiati solo i campi definiti per i descrittori di origine e di destinazione. **SQLCopyDesc** non copia il campo SQL_DESC_ALLOC_TYPE, perché non è possibile modificare il tipo di allocazione del descrittore. Campi copiati sovrascrivono i campi esistenti.  
  
 Un ARD sull'handle di un'unica istruzione può essere utilizzato come APD su un altro handle di istruzione. In questo modo un'applicazione per copiare le righe tra le tabelle senza copiare i dati a livello di applicazione. A tale scopo, viene riutilizzato un descrittore della riga che descrive una riga recuperata di una tabella come un descrittore di parametri per un parametro in un'istruzione INSERT. Il tipo di informazioni SQL_MAX_CONCURRENT_ACTIVITIES deve essere maggiore di 1 per eseguire questa operazione.
