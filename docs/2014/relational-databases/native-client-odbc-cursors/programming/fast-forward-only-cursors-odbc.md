---
title: Cursori Fast Forward-Only (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- fast forward-only cursors
- forward-only cursors
- cursors [ODBC], fast forward-only
- ODBC cursors, fast forward-only
ms.assetid: 0707d07e-fc95-42ed-9280-b7e508ac8c62
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: df3cea50a8800cdca7fe0a5c846bc32556299e0c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63209787"
---
# <a name="fast-forward-only-cursors-odbc"></a>Cursori fast forward only (ODBC)
  Quando si è connessi a un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client supporta ottimizzazioni delle prestazioni per i cursori forward-only di sola lettura. I cursori fast forward only vengono implementati internamente dal driver e dal server in modo molto simile ai set di risultati predefiniti. Oltre a offrire prestazioni elevate, i cursori fast forward only possono presentare anche le caratteristiche seguenti:  
  
-   [SQLGetData](../../native-client-odbc-api/sqlgetdata.md) non è supportato. Le colonne del set di risultati devono essere associate a variabili di programma.  
  
-   Quando viene rilevata la fine del cursore, questo viene chiuso automaticamente dal server. L'applicazione deve chiamare comunque [SQLCloseCursor](../../native-client-odbc-api/sqlclosecursor.md) oppure [SQLFreeStmt](../../native-client-odbc-api/sqlfreestmt.md)(SQL_CLOSE), ma il driver non deve inviare la richiesta di chiusura al server. In questo modo viene evitato un round trip del server nella rete.  
  
 L'applicazione richiede cursori fast forward only mediante l'attributo dell'istruzione SQL_SOPT_SS_CURSOR_OPTIONS specifica del driver. Quando l'attributo è impostato su SQL_CO_FFO, i cursori fast forward only vengono abilitati senza recupero automatico. Quando l'attributo è impostato su SQL_CO_FFO_AF, viene abilitata anche l'opzione per il recupero automatico. Per altre informazioni sul recupero automatico, vedere [utilizzo del recupero automatico con i cursori ODBC](using-autofetch-with-odbc-cursors.md).  
  
 I cursori fast forward only con recupero automatico possono essere utilizzati per recuperare un set di risultati di piccole dimensioni con un solo round trip del server. In questa procedura *n* è il numero di righe da restituire:  
  
1.  Impostare SQL_SOPT_SS_CURSOR_OPTIONS su SQL_CO_FFO_AF.  
  
2.  Impostare SQL_ATTR_ROW_ARRAY_SIZE *n* + 1.  
  
3.  Associare le colonne di risultati a matrici di *n* + 1 elementi (per essere sicuri se *n* + 1 righe vengano effettivamente recuperate).  
  
4.  Aprire il cursore con uno **SQLExecDirect** oppure **SQLExecute**.  
  
5.  Se lo stato restituito è SQL_SUCCESS, quindi chiamare **SQLFreeStmt** oppure **SQLCloseCursor** per chiudere il cursore. Tutti i dati delle righe si troveranno nelle variabili di programma associate.  
  
 Con questi passaggi, il **SQLExecDirect** oppure **SQLExecute** invia una richiesta di apertura del cursore con l'opzione di recupero automatico abilitata. Nella singola richiesta proveniente dal client il server:  
  
-   Apre il cursore.  
  
-   Compila il set di risultati e invia le righe al client.  
  
-   Poiché le dimensioni del set di righe sono impostate sul numero di righe del set di risultati più uno, il server rileva la fine del cursore e lo chiude.  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni sulla programmazione dei cursori &#40;ODBC&#41;](cursor-programming-details-odbc.md)  
  
  
