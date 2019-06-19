---
title: Gli errori aritmetici | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- arithmetic errors [ODBC]
- desktop database drivers [ODBC], arithmetic errors
ms.assetid: 1c47bfac-7455-4487-b673-6b47d2a2d756
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c0d957d6091dc5fa29ee8a0b707c0e7fe7dfc7c8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63302035"
---
# <a name="arithmetic-errors"></a>Errori aritmetici
Il driver ODBC restituisca la clausola WHERE in un'istruzione SELECT recupera ciascuna riga. Se una riga contiene un valore che provoca un errore aritmetico, ad esempio overflow numerico o di divisione per zero, il driver restituisce tutte le righe, ma restituisce errori per le colonne con gli errori aritmetici. Durante l'inserimento o aggiornamento, tuttavia, il driver ODBC arresta inserendo o aggiornando dati quando viene rilevato il primo errore aritmetico.
