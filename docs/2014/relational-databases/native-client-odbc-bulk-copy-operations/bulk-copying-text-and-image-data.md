---
title: Copia bulk di dati di testo e immagine | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- bulk copy [ODBC], text data
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [ODBC], image data
- ODBC, bulk copy operations
ms.assetid: 87155bfa-3a73-4158-9d4d-cb7435dac201
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c468ec3cf52526192893458055cde857aeaa864d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63067477"
---
# <a name="bulk-copying-text-and-image-data"></a>Copia bulk di dati di tipo text e image
  I valori di grandi dimensioni di tipo **Text**, **ntext**e **Image** vengono copiati in blocco utilizzando la funzione [bcp_moretext](../native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md) . Il codice [bcp_bind](../native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) per la colonna di tipo **Text**, **ntext**o **Image** con un puntatore *pData* impostato su null indicante che i dati verranno forniti con **bcp_moretext**. È importante specificare la lunghezza esatta dei dati forniti per ogni colonna di tipo **Text**, **ntext**o **Image** in ogni riga di cui è stata eseguita la copia bulk. Se la lunghezza dei dati di una colonna è diversa dalla lunghezza della colonna specificata in [bcp_bind](../native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md), utilizzare [bcp_collen](../native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md) per impostare la lunghezza sul valore appropriato. Una [bcp_sendrow](../native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md) Invia tutti i dati non di tipo**Text**, non di tipo**ntext**e non di**immagine** ; si chiamerà quindi **bcp_moretext** per inviare i dati di tipo **Text**, **ntext**o **Image** in unità separate. Le funzioni di copia bulk determinano che tutti i dati sono stati inviati per la colonna di tipo **Text**, **ntext**o **Image** corrente quando la somma delle lunghezze dei dati inviati tramite **bcp_moretext** è uguale alla lunghezza specificata nell' **bcp_collen** o **bcp_bind**più recente.  
  
 **bcp_moretext** non dispone di un parametro per identificare una colonna. Quando in una riga sono presenti più colonne di tipo **Text**, **ntext**o **Image** , **bcp_moretext** opera sulle colonne **Text**, **ntext**o **Image** a partire dalla colonna con il numero ordinale più basso e procedendo alla colonna con il numero ordinale più alto. **bcp_moretext** passa da una colonna a quella successiva quando la somma delle lunghezze dei dati inviati è uguale alla lunghezza specificata nell' **bcp_collen** o **bcp_bind** più recente per la colonna corrente.  
  
## <a name="see-also"></a>Vedere anche  
 [Esecuzione di operazioni di copia bulk &#40;ODBC&#41;](performing-bulk-copy-operations-odbc.md)  
  
  
