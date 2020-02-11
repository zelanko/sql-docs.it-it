---
title: Sequenze di escape intervallo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interval literals [ODBC]
- escape sequences [ODBC], interval
- ODBC escape sequences [ODBC], interval
ms.assetid: 303e8dab-8f13-4fa5-857f-15cc1f75bdd6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 69c674ee8838273af9bf4ed91ddcead7e1768fb9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68041645"
---
# <a name="interval-escape-sequences"></a>Sequenze di escape intervallo
ODBC utilizza sequenze di escape per i valori letterali di intervallo. La sintassi di questa sequenza di escape è la seguente:  
  
 {*intervallo-valore letterale*}  
  
 Per la sintassi BNF di *Interval-Literal*, vedere la sezione relativa alla [sintassi dei valori letterali Interval](../../../odbc/reference/appendixes/interval-literal-syntax.md) più avanti in questa appendice.  
  
 La sequenza di escape letterale intervallo è supportata se i tipi di dati intervallo sono supportati dall'origine dati. Un'applicazione deve chiamare **SQLGetTypeInfo** per determinare se questi tipi di dati sono supportati.
