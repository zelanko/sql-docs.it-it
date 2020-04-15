---
title: 'Jet: valori letterali di data, ora e timestamp Documenti Microsoft'
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299936"
---
# <a name="jet-date-time-and-timestamp-literals"></a>Jet: valori letterali data, ora e timestamp
Per la massima interoperabilità, le applicazioni devono passare valori letterali data nel formato canonico ODBC utilizzando la sintassi della clausola di escape:For maximum interoperability, applications should pass date literals in the ODBC canonical format using escape-clause syntax:  
  
-   Per i valori letterali di data, il*valore*'d' , dove *valu*e è nel formato "aaaa-mm-gg"  
  
-   Per i valori letterali di tempo, il*valore*'-0, dove *valu*e è nel formato "hh:mm:ss"  
  
 Per i valori letterali timestamp '*ts*' valore ' , dove *valu*e è nel formato "aaaa-mm-gg hh:mm:ss[.f...]".
