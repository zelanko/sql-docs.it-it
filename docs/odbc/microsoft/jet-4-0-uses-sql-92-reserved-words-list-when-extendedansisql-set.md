---
title: Jet 4.0 utilizza l'elenco delle parole riservate SQL-92 quando ExtendedAnsiSQL_Set Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- extendedANSISQL [ODBC], reserved words
ms.assetid: 7645187e-7777-4c07-9686-0a80d5c5834d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6988e0da1ecb881e0f6e88e35b66f1a6284f9b7a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299961"
---
# <a name="jet-40-uses-sql-92-reserved-words-list-when-extendedansisql_set"></a>Jet 4.0 usa l'elenco di parole riservate SQL-92 con ExtendedAnsiSQL_Set
Quando il flag ExtendedAnsiSQL è attivato, Jet 4.0 utilizza l'elenco di parole riservate SQL-92. Se si tenta di utilizzare una parola riservata SQL-92 come nome di oggetto senza virgolette, verrà generato un errore di sintassi. Quando il flag ExtendedAnsiSQL è disattivato, le nuove parole riservate possono essere utilizzate come nomi di oggetto come in precedenza.
