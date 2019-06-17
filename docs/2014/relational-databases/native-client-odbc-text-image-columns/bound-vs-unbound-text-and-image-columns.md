---
title: Colonne di Annullare l'associazione di colonne Text e Image | Microsoft Docs
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
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62626584"
---
# <a name="bound-vs-unbound-text-and-image-columns"></a>Colonne di tipo text e image associate e non associate
  Quando si utilizzano i cursori server, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client è ottimizzato per non trasmettere i dati per annullare l'associazione **testo**, **ntext**, o **immagine** colonne di tempo **SQLFetch** viene eseguita. Il **testo**, **ntext**, o **immagine** dati non vengono effettivamente recuperati dal server finché i problemi dell'applicazione [SQLGetData](../native-client-odbc-api/sqlgetdata.md) per il colonna.  
  
 Molte applicazioni possono essere scritti in modo che nessun **testo**, **ntext**, o **immagine** dati vengono visualizzati anche se un utente viene semplicemente effettuato uno scorrimento verticale in un cursore. Quando un utente seleziona una riga per ottenere altri dettagli, l'applicazione può quindi chiamare **SQLGetData** per recuperare le **testo**, **ntext**, oppure **immagine** dati. Sarà in grado di trasmettere il **testo**, **ntext**, o **immagine** dati per tutte le righe, l'utente non seleziona e può pertanto impediscono la trasmissione di dimensioni molto grandi quantità di dati.  
  
## <a name="see-also"></a>Vedere anche  
 [La gestione di colonne Text e Image](managing-text-and-image-columns.md)   
 [Comportamenti del cursore](../native-client-odbc-cursors/cursor-behaviors.md)  
  
  
