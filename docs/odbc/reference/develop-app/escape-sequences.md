---
title: Le sequenze di escape | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c1423d7bcc0f0b943b490fdcf8f931efb6b533c6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63259272"
---
# <a name="escape-sequences"></a>Sequenza di escape
ODBC definisce sequenze di escape contenente grammatica standard per data, ora, timestamp e i valori letterali intervallo datetime, chiamate di funzioni scalari, **, ad esempio** predicato caratteri di escape outer join e le chiamate di procedura. Applicazioni interoperative utilizzino queste sequenze laddove possibile.  
  
 Per determinare se un driver supporta le sequenze di escape per data, ora, timestamp o valori letterali intervallo data/ora, un'applicazione chiama **SQLGetTypeInfo**. Se l'origine dati supporta una data, ora, timestamp o tipo di dati di intervallo datetime, deve anche supportare la sequenza di escape corrispondente. Per determinare se sono supportate le altre sequenze di escape, un'applicazione chiama **SQLGetInfo**.  
  
 Per altre informazioni, vedere [sequenze di Escape in ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md), più avanti in questa sezione.
