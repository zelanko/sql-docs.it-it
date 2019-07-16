---
title: Limitazioni di Word riservato | Microsoft Docs
ms.custom: ''
ms.date: 05/01/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: ed42f083-c9e8-4ee4-9d64-d879bf955c78
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c884d8594c3c4511bed0e24f9b3dd43092176b4e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67988023"
---
# <a name="reserved-keyword-limitations"></a>Limitazioni della parola chiave riservata

Evitare l'utilizzo delle parole chiave riservate di ODBC come identificatori nel tabelle SQL o gli oggetti correlati. Se un caso dispari in cui è necessario usare una parola chiave riservata come identificatore, è necessario racchiudere l'identificatore tra parentesi *apici* ('). Un altro nome per *apice inverso* viene *virgolette inverse*.

La limitazione della parola chiave riservata si applica anche a qualsiasi forma abbreviata delle parole chiave riservate.

Un elenco delle parole chiave riservate di ODBC è disponibile all'indirizzo:

- [Parole chiave riservate di ODBC](https://docs.microsoft.com/sql/odbc/reference/appendixes/reserved-keywords).

- Nel *Guida di riferimento per programmatori ODBC*, vedere [appendice c: Grammatica SQL](https://docs.microsoft.com/sql/odbc/reference/appendixes/appendix-c-sql-grammar).

