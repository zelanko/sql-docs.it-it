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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1bb7f0fb02049b6d2f1897c4f495035aee2858f6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68085487"
---
# <a name="jet-date-time-and-timestamp-literals"></a>Jet: valori letterali data, ora e timestamp
Per garantire la massima interoperabilità, le applicazioni devono passare i valori letterali di data nel formato canonico ODBC utilizzando la sintassi della clausola di escape:  
  
-   Per i valori letterali data, {d'*value*'}, dove *Valor*e è nel formato "aaaa-mm-gg"  
  
-   Per i valori letterali temporali, {t'*value*'}, dove *Valor*e è nel formato "HH: mm: SS"  
  
 Per i valori letterali timestamp {TS '*value*'}, dove *Valor*e è nel formato "aaaa-mm-gg hh: mm: SS [. f...]".
