---
title: Caricamento per ordinale Documenti Microsoft
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288721"
---
# <a name="loading-by-ordinal"></a>Caricamento per ordinale
In ODBC *2.x*, il caricamento tramite ordinale può essere eseguito per migliorare le prestazioni del processo di connessione. Un driver ODBC *2.x* esporta una funzione fittizia con l'ordinale 199; quando Gestione Driver lo rileva, risolve gli indirizzi delle funzioni ODBC per ordinale, non per nome. Questa funzionalità è ancora supportata per i driver ODBC *2.x,* ma non per i driver ODBC *3.x.*
