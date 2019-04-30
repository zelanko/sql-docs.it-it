---
title: Le sequenze di Escape intervallo | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 81481db74d973da0e54bc6bf9e70550fa3cc0c81
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63188892"
---
# <a name="interval-escape-sequences"></a>Sequenze di escape intervallo
ODBC Usa sequenze di escape per i valori letterali intervallo. La sintassi di questa sequenza di escape è come segue:  
  
 {*interval-literal*}  
  
 Relativa sintassi BNF *interval-literal*, vedere la [sintassi dei valori letterali intervallo](../../../odbc/reference/appendixes/interval-literal-syntax.md) sezione più avanti in questa appendice.  
  
 La sequenza di escape letterali di intervallo è supportata se i tipi di dati di intervallo sono supportati dall'origine dati. Un'applicazione deve chiamare **SQLGetTypeInfo** per determinare se sono supportati questi tipi di dati.
