---
title: Colonne di testo e immagine associate e non associate . Documenti Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0cfa05f7019342d63ab6f3092c3b6df5ae6e8daa
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297737"
---
# <a name="bound-vs-unbound-text-and-image-columns"></a>Colonne di tipo text e image associate e non associate
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Quando si utilizzano [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cursori del server, il driver ODBC Native Client è ottimizzato per non trasmettere i dati per le colonne **text,** **ntext**o **image** non associate al momento dell'esecuzione **di SQLFetch.** I dati **text**, **ntext**o **image** non vengono effettivamente recuperati dal server fino a quando l'applicazione non emette [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) per la colonna.  
  
 Molte applicazioni possono essere scritte in modo che non vengano visualizzati dati di **testo**, **ntext**o **immagine** mentre un utente scorre semplicemente verso l'alto e verso il basso in un cursore. Quando un utente seleziona una riga per ottenere maggiori dettagli, l'applicazione può quindi chiamare **SQLGetData** per recuperare i dati **text**, **ntext**o **image.** Ciò impedirà la trasmissione dei dati di **testo**, **ntext**o **immagine** per una qualsiasi delle righe che l'utente non seleziona e può quindi impedire la trasmissione di grandi quantità di dati.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione delle colonne di testo e immagini](../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)   
 [Comportamenti dei cursori](../../relational-databases/native-client-odbc-cursors/cursor-behaviors.md)  
  
  
