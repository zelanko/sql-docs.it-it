---
title: Chiamata di routine | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68070487"
---
# <a name="procedure-invocation"></a>Chiamata di procedura
Quando si utilizza il driver Microsoft Access, le procedure possono essere richiamate dal driver utilizzando la funzione **SQLExecDirect** o **SQLPrepare** con la sintassi seguente: {Call *procedure-name* [(*Parameter*[,*Parameter*]...)]}. Si noti che le espressioni non sono supportate come parametri di una stored procedure chiamata.  
  
 Se il nome di una stored procedure include un trattino, il nome deve essere delimitato da virgolette inverso (').  
  
 Una query con parametri può essere chiamata usando l'istruzione precedente.
