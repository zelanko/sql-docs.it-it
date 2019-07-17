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
ms.openlocfilehash: fdc7728fe06df708efd973423f5c8c05333ce189
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041606"
---
# <a name="loading-by-ordinal"></a>Caricamento per ordinale
In ODBC *2.x*, è possibile eseguire il caricamento per ordinale per migliorare le prestazioni del processo di connessione. Un database ODBC *2.x* driver Esporta una funzione fittizia con l'ordinale 199; quando Gestione Driver lo rileva, risolve gli indirizzi delle funzioni ODBC dall'ordinale, non dal nome. Questa funzionalità è ancora supportata per ODBC *2.x* i driver, ma non è supportata per ODBC *3.x* driver.
