---
title: Chiamata di Routine Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 32617cdb753f5fc1b9c52520cb609d2902137b54
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81290772"
---
# <a name="procedure-invocation"></a>Chiamata di procedura
Quando viene utilizzato il driver di Microsoft Access, le procedure possono essere richiamate dal driver utilizzando la funzione **SQLExecDirect** o **SQLPrepare** con la sintassi seguente: .CALL *nome-procedura* [(*parametro*[,*parametro*]...)]. Si noti che le espressioni non sono supportate come parametri di una routine chiamata.  
  
 Se il nome di una routine include un trattino, il nome deve essere delimitato da virgolette rovesciate (').  
  
 Una query con parametri può essere chiamata utilizzando l'istruzione precedente.
