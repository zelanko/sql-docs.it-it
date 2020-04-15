---
title: Limitazioni delle parole riservate Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bf536e06556e6b2e7b27f220d09a51f91b44d23c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304009"
---
# <a name="reserved-keyword-limitations"></a>Limitazioni delle parole chiave riservate

Evitare di utilizzare parole chiave riservate ODBC come identificatori nelle tabelle SQL o negli oggetti correlati. Se si verifica un caso dispari in cui è necessario utilizzare una parola chiave riservata come identificatore, è necessario racchiudere l'identificatore con una coppia di *backtick* ('). Un altro nome per *backtick* è *back quote*.

La limitazione delle parole chiave riservate si applica anche a qualsiasi forma abbreviata delle parole chiave riservate.

Un elenco delle parole chiave riservate ODBC è disponibile all'indirizzo:

- [Parole chiave riservate ODBC](https://docs.microsoft.com/sql/odbc/reference/appendixes/reserved-keywords).

- Nella Guida di riferimento per programmatori *ODBC,* vedere [Appendice C: Grammatica SQL](https://docs.microsoft.com/sql/odbc/reference/appendixes/appendix-c-sql-grammar).

