---
title: Caricamento per ordinale | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 702e1fe58080cc370ab9a858c985a7744df85050
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63181337"
---
# <a name="loading-by-ordinal"></a>Caricamento per ordinale
In ODBC 2. *x*, è possibile eseguire il caricamento per ordinale per migliorare le prestazioni del processo di connessione. Un database ODBC 2. *x* driver Esporta una funzione fittizia con l'ordinale 199; quando Gestione Driver lo rileva, risolve gli indirizzi delle funzioni ODBC dall'ordinale, non dal nome. Questa funzionalità è ancora supportata per l'API ODBC 2. *x* i driver, ma non è supportata per ODBC 3*x* driver.
