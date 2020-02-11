---
title: Errori aritmetici | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68138184"
---
# <a name="arithmetic-errors"></a>Errori aritmetici
Il driver ODBC valuta la clausola WHERE in un'istruzione SELECT durante il recupero di ogni riga. Se una riga contiene un valore che causa un errore aritmetico, ad esempio la divisione per zero o l'overflow numerico, il driver restituisce tutte le righe, ma restituisce errori per le colonne con errori aritmetici. Quando si inserisce o si aggiorna, tuttavia, il driver ODBC interrompe l'inserimento o l'aggiornamento dei dati quando viene rilevato il primo errore aritmetico.
