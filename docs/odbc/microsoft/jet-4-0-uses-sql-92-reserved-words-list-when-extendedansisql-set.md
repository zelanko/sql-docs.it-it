---
title: Jet 4,0 utilizza l'elenco di parole riservate SQL-92 quando ExtendedAnsiSQL_Set | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 93d23216db950ed861449061f3e35e5e88a637fb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68058793"
---
# <a name="jet-40-uses-sql-92-reserved-words-list-when-extendedansisql_set"></a>Jet 4.0 usa l'elenco di parole riservate SQL-92 con ExtendedAnsiSQL_Set
Quando il flag ExtendedAnsiSQL è attivato, Jet 4,0 utilizza l'elenco di parole riservate di SQL-92. Se si tenta di utilizzare una parola riservata SQL-92 come nome di oggetto non racchiuso tra virgolette, verrà generato un errore di sintassi. Quando il flag ExtendedAnsiSQL è disattivato, le nuove parole riservate possono essere usate come nomi di oggetto come prima.
