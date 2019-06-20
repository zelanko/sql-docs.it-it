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
manager: craigg
ms.openlocfilehash: 7b33bc399646a6d274c875abd36d53219a2814e1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63200512"
---
# <a name="procedure-invocation"></a>Chiamata di procedura
Quando viene usato il driver Microsoft Access, le procedure possono essere richiamate dal driver tramite il **SQLExecDirect** oppure **SQLPrepare** funzione con la sintassi seguente: {CHIAMARE *nome procedura*  [(*parametro*[,*parametro*]...)]}. Si noti che le espressioni non sono supportate come parametri per una routine chiamata.  
  
 Se un nome di procedure include un trattino, il nome deve essere delimitato tra virgolette back (').  
  
 Una query con parametri può essere chiamata utilizzando l'istruzione precedente.
