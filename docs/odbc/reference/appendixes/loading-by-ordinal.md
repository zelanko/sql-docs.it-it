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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fdc7728fe06df708efd973423f5c8c05333ce189
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68041606"
---
# <a name="loading-by-ordinal"></a>Caricamento per ordinale
In ODBC *2. x*è possibile eseguire il caricamento in base al numero ordinale per migliorare le prestazioni del processo di connessione. Un driver ODBC *2. x* esporta una funzione fittizia con l'ordinale 199; Quando la gestione driver la rileva, risolve gli indirizzi delle funzioni ODBC in base al numero ordinale, non in base al nome. Questa funzionalità è ancora supportata per i driver ODBC *2. x* , ma non è supportata per i driver ODBC *3. x* .
