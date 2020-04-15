---
title: Sequenze di escape di intervallo Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9fe7f6941e9ec9fba8b6698faaa18a678732dd6f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304956"
---
# <a name="interval-escape-sequences"></a>Sequenze di escape intervallo
ODBC utilizza sequenze di escape per i valori letterali di intervallo. La sintassi di questa sequenza di escape è la seguente:The syntax of this escape sequence is as follows:  
  
 -*intervallo-letterale*.  
  
 Per la sintassi BNF di *interval-literal*, vedere la sezione [Sintassi dei valori letterali](../../../odbc/reference/appendixes/interval-literal-syntax.md) di intervallo più avanti in questa appendice.  
  
 La sequenza di escape letterale intervallo è supportata se i tipi di dati intervallo sono supportati dall'origine dati. Un'applicazione deve chiamare **SQLGetTypeInfo** per determinare se questi tipi di dati sono supportati.
