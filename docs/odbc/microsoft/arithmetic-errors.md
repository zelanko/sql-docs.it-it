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
ms.openlocfilehash: 2e0880e1746b4b65070fb28bf8d83aadec301aa4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138184"
---
# <a name="arithmetic-errors"></a>Errori aritmetici
Il driver ODBC restituisca la clausola WHERE in un'istruzione SELECT recupera ciascuna riga. Se una riga contiene un valore che provoca un errore aritmetico, ad esempio overflow numerico o di divisione per zero, il driver restituisce tutte le righe, ma restituisce errori per le colonne con gli errori aritmetici. Durante l'inserimento o aggiornamento, tuttavia, il driver ODBC arresta inserendo o aggiornando dati quando viene rilevato il primo errore aritmetico.
