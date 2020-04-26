---
title: SQLGetCursorName | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLGetCursorName function
ms.assetid: 3a427a23-28ef-49aa-b9ec-6cab0914bdf3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 603a2b5be4ca75495f094aa838d0373a9689a523
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/25/2020
ms.locfileid: "62657780"
---
# <a name="sqlgetcursorname"></a>SQLGetCursorName
  Se l'applicazione non specifica un nome di cursore, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC di Native client ne genera uno per l'applicazione durante la generazione del cursore. L'applicazione può utilizzare **SQLGetCursorName** per recuperare il nome del cursore definito dal driver per le istruzioni Update e Delete posizionate. Non è necessario che l'applicazione chiami **SQLSetCursorName** per sfruttare le istruzioni di manipolazione dei dati posizionate.  
  
## <a name="see-also"></a>Vedi anche  
 [SQLGetCursorName (funzione)](https://go.microsoft.com/fwlink/?LinkId=59349)   
 [Dettagli di implementazione dell'API ODBC](odbc-api-implementation-details.md)  
  
  
