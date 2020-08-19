---
description: Sequenze di escape intervallo
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e2ef792403352568ce5f8d92c07a5b0e1027b507
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483294"
---
# <a name="interval-escape-sequences"></a>Sequenze di escape intervallo
ODBC utilizza sequenze di escape per i valori letterali di intervallo. La sintassi di questa sequenza di escape è la seguente:  
  
 {*intervallo-valore letterale*}  
  
 Per la sintassi BNF di *Interval-Literal*, vedere la sezione relativa alla [sintassi dei valori letterali Interval](../../../odbc/reference/appendixes/interval-literal-syntax.md) più avanti in questa appendice.  
  
 La sequenza di escape letterale intervallo è supportata se i tipi di dati intervallo sono supportati dall'origine dati. Un'applicazione deve chiamare **SQLGetTypeInfo** per determinare se questi tipi di dati sono supportati.
