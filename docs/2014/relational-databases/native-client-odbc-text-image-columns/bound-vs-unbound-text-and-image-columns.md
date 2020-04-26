---
title: Colonne di testo e di immagine non associato e associato | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- text columns [ODBC]
- SQL Server Native Client ODBC driver, image columns
- SQL Server Native Client ODBC driver, text columns
- data types [ODBC], image
- data types [ODBC], text
- columns [ODBC]
- ODBC data types, image columns
- ODBC data types, text columns
- image columns [ODBC]
ms.assetid: ffd3442e-d880-46e9-b848-2365a09a2406
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1bf8ac0cf868394d9aa8063220939feee69ac2f6
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/25/2020
ms.locfileid: "62626584"
---
# <a name="bound-vs-unbound-text-and-image-columns"></a>Colonne di tipo text e image associate e non associate
  Quando si utilizzano i cursori server [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , il driver ODBC di Native Client è ottimizzato per non trasmettere i dati per le colonne di tipo **Text**, **ntext**o **Image** non associato al momento dell'esecuzione di **SQLFetch** . I dati di tipo **Text**, **ntext**o **Image** non vengono effettivamente recuperati dal server fino a quando l'applicazione non rilascia [SQLGetData](../native-client-odbc-api/sqlgetdata.md) per la colonna.  
  
 Molte applicazioni possono essere scritte in modo che non vengano visualizzati dati di tipo **Text**, **ntext**o **Image** quando un utente scorre verso l'alto e verso il basso un cursore. Quando un utente seleziona una riga per ottenere maggiori dettagli, l'applicazione può quindi chiamare **SQLGetData** per recuperare i dati di tipo **Text**, **ntext**o **Image** . In questo modo si impedisce la trasmissione dei dati di tipo **Text**, **ntext**o **Image** per le righe non selezionate dall'utente e pertanto è possibile impedire la trasmissione di grandi quantità di dati.  
  
## <a name="see-also"></a>Vedi anche  
 [Gestione delle colonne di testo e immagini](managing-text-and-image-columns.md)   
 [Comportamenti dei cursori](../native-client-odbc-cursors/cursor-behaviors.md)  
  
  
