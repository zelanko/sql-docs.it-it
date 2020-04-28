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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5d9589230183b198cb7d59cf9739dab75625441e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298711"
---
# <a name="escape-sequences"></a>Sequenza di escape
ODBC definisce sequenze di escape che contengono la grammatica standard per i valori letterali di data, ora, timestamp e intervallo DateTime, le chiamate di funzioni scalari, **come** i caratteri di escape dei predicati, gli outer join e le chiamate di routine. Le applicazioni interoperative devono usare queste sequenze quando possibile.  
  
 Per determinare se un driver supporta le sequenze di escape per i valori letterali di data, ora, timestamp o intervallo di tempo DateTime, un'applicazione chiama **SQLGetTypeInfo**. Se l'origine dati supporta un tipo di dati date, Time, timestamp o DateTime Interval, deve supportare anche la sequenza di escape corrispondente. Per determinare se sono supportate le altre sequenze di escape, un'applicazione chiama **SQLGetInfo**.  
  
 Per ulteriori informazioni, vedere [sequenze di escape in ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md), più avanti in questa sezione.
