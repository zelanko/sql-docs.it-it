---
title: Copia bulk di dati di testo e immagine | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- bulk copy [ODBC], text data
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [ODBC], image data
- ODBC, bulk copy operations
ms.assetid: 87155bfa-3a73-4158-9d4d-cb7435dac201
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5243c862e07ad8b4f5a0b3b33ea292cecc1cb0a9
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2019
ms.locfileid: "71707904"
---
# <a name="bulk-copying-text-and-image-data"></a>Copia bulk di dati di tipo text e image
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  I valori di grandi dimensioni di tipo **Text**, **ntext**e **Image** vengono copiati in blocco utilizzando la funzione [bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md) . È possibile scrivere il codice [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) per la colonna di tipo **Text**, **ntext**o **Image** con un puntatore *pData* impostato su null che indica che i dati verranno forniti con **bcp_moretext**. È importante specificare la lunghezza esatta dei dati forniti per ogni colonna di tipo **Text**, **ntext**o **Image** in ogni riga di cui è stata eseguita la copia bulk. Se la lunghezza dei dati per una colonna è diversa dalla lunghezza della colonna specificata in [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md), utilizzare [bcp_collen](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md) per impostare la lunghezza sul valore appropriato. Un [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md) Invia tutti i dati non di tipo**Text**, non di tipo**ntext**e non di**immagine** ; si chiama quindi **bcp_moretext** per inviare i dati di tipo **Text**, **ntext**o **Image** in unità separate. Le funzioni di copia bulk determinano che tutti i dati sono stati inviati per la colonna di tipo **Text**, **ntext**o **Image** corrente quando la somma delle lunghezze dei dati inviati tramite **bcp_moretext** è uguale alla lunghezza specificata nel bcp_collen più recenteo **bcp_bind**.  
  
 **bcp_moretext** non dispone di un parametro per identificare una colonna. Quando sono presenti più colonne di tipo **Text**, **ntext**o **Image** in una riga, **bcp_moretext** opera sulle colonne **Text**, **ntext**o **Image** a partire dalla colonna con il numero ordinale più basso e si procede alla colonna con il numero ordinale più alto. **bcp_moretext** passa da una colonna a quella successiva quando la somma delle lunghezze dei dati inviati è uguale alla lunghezza specificata nell'ultima **bcp_collen** o **bcp_bind** per la colonna corrente.  
  
## <a name="see-also"></a>Vedere anche  
 [Esecuzione di operazioni &#40;di copia bulk ODBC&#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
  
