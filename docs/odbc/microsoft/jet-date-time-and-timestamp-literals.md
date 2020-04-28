---
title: 'Jet: valori letterali data, ora e timestamp | Microsoft Docs'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 372b7c1dab1ad8ff000fb88729c3b02e05d4a21c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299936"
---
# <a name="jet-date-time-and-timestamp-literals"></a>Jet: valori letterali data, ora e timestamp
Per garantire la massima interoperabilità, le applicazioni devono passare i valori letterali di data nel formato canonico ODBC utilizzando la sintassi della clausola di escape:  
  
-   Per i valori letterali data, {d'*value*'}, dove *Valor*e è nel formato "aaaa-mm-gg"  
  
-   Per i valori letterali temporali, {t'*value*'}, dove *Valor*e è nel formato "HH: mm: SS"  
  
 Per i valori letterali timestamp {TS '*value*'}, dove *Valor*e è nel formato "aaaa-mm-gg hh: mm: SS [. f...]".
