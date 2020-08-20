---
description: Errori aritmetici
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3e2fa142b43f1e96693390f777c90ea6f10705f6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500404"
---
# <a name="arithmetic-errors"></a>Errori aritmetici
Il driver ODBC valuta la clausola WHERE in un'istruzione SELECT durante il recupero di ogni riga. Se una riga contiene un valore che causa un errore aritmetico, ad esempio la divisione per zero o l'overflow numerico, il driver restituisce tutte le righe, ma restituisce errori per le colonne con errori aritmetici. Quando si inserisce o si aggiorna, tuttavia, il driver ODBC interrompe l'inserimento o l'aggiornamento dei dati quando viene rilevato il primo errore aritmetico.
