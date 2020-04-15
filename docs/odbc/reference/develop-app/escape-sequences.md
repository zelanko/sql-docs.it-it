---
title: Sequenze di escape | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- escape sequences [ODBC], determining if supported
- interoperability of SQL statements [ODBC], escape sequences
ms.assetid: 5913abfa-d280-43e4-a2f1-05a924388bf9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5d9589230183b198cb7d59cf9739dab75625441e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298711"
---
# <a name="escape-sequences"></a>Sequenza di escape
ODBC definisce sequenze di escape contenenti grammatica standard per valori letterali di intervallo di data, ora, timestamp e datetime, chiamate di funzione scalari, caratteri di escape predicati **LIKE,** outer join e chiamate di routine. Le applicazioni interoperabili devono utilizzare queste sequenze quando possibile.  
  
 Per determinare se un driver supporta le sequenze di escape per i valori letterali di intervallo di data, ora, timestamp o datetime, un'applicazione chiama **SQLGetTypeInfo**. Se l'origine dati supporta un tipo di dati di data, ora, timestamp o intervallo di date-ora, deve supportare anche la sequenza di escape corrispondente. Per determinare se le altre sequenze di escape sono supportate, un'applicazione chiama **SQLGetInfo**.  
  
 Per ulteriori informazioni, vedere [Sequenze](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)di escape in ODBC , più avanti in questa sezione.
