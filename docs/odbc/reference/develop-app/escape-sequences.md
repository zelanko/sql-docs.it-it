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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d73282cde4d0598d7e6a35ac6273935626b96969
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68001377"
---
# <a name="escape-sequences"></a>Sequenza di escape
ODBC definisce sequenze di escape che contengono la grammatica standard per i valori letterali di data, ora, timestamp e intervallo DateTime, le chiamate di funzioni scalari, **come** i caratteri di escape dei predicati, gli outer join e le chiamate di routine. Le applicazioni interoperative devono usare queste sequenze quando possibile.  
  
 Per determinare se un driver supporta le sequenze di escape per i valori letterali di data, ora, timestamp o intervallo di tempo DateTime, un'applicazione chiama **SQLGetTypeInfo**. Se l'origine dati supporta un tipo di dati date, Time, timestamp o DateTime Interval, deve supportare anche la sequenza di escape corrispondente. Per determinare se sono supportate le altre sequenze di escape, un'applicazione chiama **SQLGetInfo**.  
  
 Per ulteriori informazioni, vedere [sequenze di escape in ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md), più avanti in questa sezione.
