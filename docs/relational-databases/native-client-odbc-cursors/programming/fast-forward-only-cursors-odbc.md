---
title: Cursori di inoltro rapido (ODBC) Documenti Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- fast forward-only cursors
- forward-only cursors
- cursors [ODBC], fast forward-only
- ODBC cursors, fast forward-only
ms.assetid: 0707d07e-fc95-42ed-9280-b7e508ac8c62
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 50d79875e0f3f661c0a959f50ce68c4f2761d186
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298419"
---
# <a name="fast-forward-only-cursors-odbc"></a>Cursori fast forward only (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Quando si è [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]connessi [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a un'istanza di , il driver ODBC Native Client supporta le ottimizzazioni delle prestazioni per i cursori forward-only di sola lettura. I cursori fast forward only vengono implementati internamente dal driver e dal server in modo molto simile ai set di risultati predefiniti. Oltre a offrire prestazioni elevate, i cursori fast forward only possono presentare anche le caratteristiche seguenti:  
  
-   [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) non è supportato. Le colonne del set di risultati devono essere associate a variabili di programma.  
  
-   Quando viene rilevata la fine del cursore, questo viene chiuso automaticamente dal server. L'applicazione deve comunque chiamare [SQLCloseCursor](../../../relational-databases/native-client-odbc-api/sqlclosecursor.md) o [SQLFreeStmt](../../../relational-databases/native-client-odbc-api/sqlfreestmt.md)(SQL_CLOSE), ma il driver non deve inviare la richiesta di chiusura al server. In questo modo viene evitato un round trip del server nella rete.  
  
 L'applicazione richiede cursori fast forward only mediante l'attributo dell'istruzione SQL_SOPT_SS_CURSOR_OPTIONS specifica del driver. Quando l'attributo è impostato su SQL_CO_FFO, i cursori fast forward only vengono abilitati senza recupero automatico. Quando l'attributo è impostato su SQL_CO_FFO_AF, viene abilitata anche l'opzione per il recupero automatico. Per ulteriori informazioni sulla lettura automatica, vedere [Utilizzo della lettura automatica con i cursori ODBC](../../../relational-databases/native-client-odbc-cursors/programming/using-autofetch-with-odbc-cursors.md).  
  
 I cursori fast forward only con recupero automatico possono essere utilizzati per recuperare un set di risultati di piccole dimensioni con un solo round trip del server. In questi passaggi, n è il numero di righe da restituire:In these steps, *n* is the number of rows to be returned:  
  
1.  Impostare SQL_SOPT_SS_CURSOR_OPTIONS su SQL_CO_FFO_AF.  
  
2.  Impostare SQL_ATTR_ROW_ARRAY_SIZE su *n* .  
  
3.  Associare le colonne dei risultati a matrici di *n* e 1 elementi (per essere sicuri se *n* x 1 righe vengono effettivamente recuperate).  
  
4.  Aprire il cursore con **SQLExecDirect** o **SQLExecute**.  
  
5.  Se lo stato restituito è SQL_SUCCESS, chiamare **SQLFreeStmt** o **SQLCloseCursor** per chiudere il cursore. Tutti i dati delle righe si troveranno nelle variabili di programma associate.  
  
 Con questi passaggi, **SQLExecDirect** o **SQLExecute** invia una richiesta di apertura cursore con l'opzione di recupero automatico abilitata. Nella singola richiesta proveniente dal client il server:  
  
-   Apre il cursore.  
  
-   Compila il set di risultati e invia le righe al client.  
  
-   Poiché le dimensioni del set di righe sono impostate sul numero di righe del set di risultati più uno, il server rileva la fine del cursore e lo chiude.  
  
## <a name="see-also"></a>Vedere anche  
 [Dettagli di programmazione del cursore &#40;&#41;ODBCCursor Programming Details to ODBC&#41;](../../../relational-databases/native-client-odbc-cursors/programming/cursor-programming-details-odbc.md)  
  
  
