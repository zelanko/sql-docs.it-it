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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 32617cdb753f5fc1b9c52520cb609d2902137b54
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81290772"
---
# <a name="procedure-invocation"></a>Chiamata di procedura
Quando si utilizza il driver Microsoft Access, le procedure possono essere richiamate dal driver utilizzando la funzione **SQLExecDirect** o **SQLPrepare** con la sintassi seguente: {Call *procedure-name* [(*Parameter*[,*Parameter*]...)]}. Si noti che le espressioni non sono supportate come parametri di una stored procedure chiamata.  
  
 Se il nome di una stored procedure include un trattino, il nome deve essere delimitato da virgolette inverso (').  
  
 Una query con parametri può essere chiamata usando l'istruzione precedente.
