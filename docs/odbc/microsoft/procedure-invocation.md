---
title: Chiamata di procedura | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL grammar [ODBC], procedure invocation
- procedure invocation [ODBC]
ms.assetid: b9ff2c3a-2003-4832-adbe-08dd0f5ad948
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bc37ef6d268dba71f8270909ea9c5b938ef3ee75
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68070487"
---
# <a name="procedure-invocation"></a>Chiamata di procedura
Quando viene usato il driver Microsoft Access, le procedure possono essere richiamate dal driver tramite il **SQLExecDirect** oppure **SQLPrepare** funzione con la sintassi seguente: {CHIAMARE *nome procedura*  [(*parametro*[,*parametro*]...)]}. Si noti che le espressioni non sono supportate come parametri per una routine chiamata.  
  
 Se un nome di procedure include un trattino, il nome deve essere delimitato tra virgolette back (').  
  
 Una query con parametri può essere chiamata utilizzando l'istruzione precedente.
