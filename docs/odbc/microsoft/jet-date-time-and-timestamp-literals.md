---
title: 'Jet: Date, Time e Timestamp valori letterali | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- literals [ODBC], SQL grammar
- SQL grammar [ODBC], literals
- date literals [ODBC]
- timestamp literals [ODBC]
- time literals [ODBC]
ms.assetid: 37db1ae1-ca4e-4cd8-9b47-7f1a38e7fcad
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2325cd7e4a10e91f351aa2107c64c0978b843fa6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63224584"
---
# <a name="jet-date-time-and-timestamp-literals"></a>Jet: Valori letterali data, ora e timestamp
Per garantire la massima interoperabilità, le applicazioni devono passare valori letterali di data nel formato canonico ODBC usando la sintassi della clausola di escape:  
  
-   Per i valori letterali data, {1!d»*valore*'}, dove *valor*e è nel formato "aaaa-mm-gg"  
  
-   Per i valori letterali ora, {t '*valore*'}, dove *valor*e è nel formato "hh"  
  
 Per i valori letterali timestamp {ts'*valore*'}, dove *valor*e è nel formato "aaaa-mm-gg hh.mm.ss [. f...]".
