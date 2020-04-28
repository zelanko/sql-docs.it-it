---
title: Caricamento in base al numero ordinale | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], loading by ordinal
- compatibility [ODBC], loading by ordinal
- loading by ordinal [ODBC]
ms.assetid: 337d90ab-68eb-4940-a2f3-f7d5693ee766
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 64bff8dcdd3802f75dc402c9ada60f82580aca5c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81288721"
---
# <a name="loading-by-ordinal"></a>Caricamento per ordinale
In ODBC *2. x*è possibile eseguire il caricamento in base al numero ordinale per migliorare le prestazioni del processo di connessione. Un driver ODBC *2. x* esporta una funzione fittizia con l'ordinale 199; Quando la gestione driver la rileva, risolve gli indirizzi delle funzioni ODBC in base al numero ordinale, non in base al nome. Questa funzionalità è ancora supportata per i driver ODBC *2. x* , ma non è supportata per i driver ODBC *3. x* .
