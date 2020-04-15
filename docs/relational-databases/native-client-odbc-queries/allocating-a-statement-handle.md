---
title: Allocazione di un handle di istruzione Documenti Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLSetStmtAttr function
- statements [ODBC], statement handles
- ODBC applications, executing queries
- SQLGetStmtAttr function
- SQL Server Native Client ODBC driver, statements
- allocating statement handles
- ODBC applications, statements
- statement handles [ODBC]
- SQLAllocHandle function
ms.assetid: 9ee207f3-2667-45f5-87ca-e6efa1fd7a5c
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 85678c5b03a77910c73bd5b8bac8d0e40d52c252
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81291606"
---
# <a name="allocating-a-statement-handle"></a>Allocazione di un handle di istruzione
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Prima che un'applicazione possa eseguire un'istruzione, deve allocare un handle di istruzione. Questa operazione viene eseguito chiamando **SQLAllocHandle** con il parametro *HandleType* impostato su SQL_HANDLE_STMT e *InputHandle* che punta a un handle di connessione.  
  
 Gli attributi di istruzione sono caratteristiche dell'handle di istruzione. Attributi di istruzione di esempio possono includere l'utilizzo di segnalibri e il tipo di cursore da utilizzare con il set di risultati dell'istruzione. Gli attributi dell'istruzione vengono impostati con [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)e le relative impostazioni correnti vengono recuperate tramite [SQLGetStmtAttr](../../relational-databases/native-client-odbc-api/sqlgetstmtattr.md). Non vi è alcun requisito che stabilisce che un'applicazione debba impostare tutti gli attributi di istruzione. Per tutti gli attributi di istruzione sono disponibili valori predefiniti, alcuni dei quali specifici del driver.  
  
 Prestare particolare attenzione nell'utilizzare molte delle opzioni di istruzione e connessione ODBC. La chiamata a [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) con *fOption* impostato su SQL_ATTR_LOGIN_TIMEOUT controlla il tempo di attesa di un tentativo di connessione durante l'attesa di stabilire una connessione (0 specifica un'attesa infinita). Per i siti con tempi di risposta prolungati è possibile impostare un valore elevato per garantire che le connessioni dispongano di tempo sufficiente per il completamento. L'intervallo, tuttavia, deve essere sempre sufficientemente ridotto per consentire all'utente di ricevere una risposta entro un periodo di tempo ragionevole se il driver non è in grado di connettersi.  
  
 La chiamata a **SQLSetStmtAttr** *conopzione* set su SQL_ATTR_QUERY_TIMEOUT imposta un intervallo di timeout delle query per proteggere il server e l'utente dalle query a esecuzione prolungata.  
  
 La chiamata a **SQLSetStmtAttr** con *fOption* impostato su SQL_ATTR_MAX_LENGTH limita la quantità di dati di **tipo text** e **image** che una singola istruzione può recuperare. La chiamata a **SQLSetStmtAttr** con *fOption* impostato su SQL_ATTR_MAX_ROWS limita anche un set di righe alle prime *n* righe se questo è tutto l'applicazione richiede. Si noti che impostando SQL_ATTR_MAX_ROWS, il driver esegue un'istruzione SET ROWCOUNT nel server. Ciò [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] influisce su tutte le istruzioni, inclusi i trigger e gli aggiornamenti.  
  
 Utilizzare particolare attenzione quando si impostano queste opzioni. È preferibile che tutti gli handle di istruzione in un handle di connessione specifichino le stesse impostazioni per SQL_ATTR_MAX_LENGTH e SQL_ATTR_MAX_ROWS. Se il driver passa da un handle di istruzione a un altro con valori diversi per queste opzioni, il driver deve generare le istruzioni SET TEXTSIZE e SET ROWCOUNT appropriate per modificare le impostazioni. Il driver non può inserire queste istruzioni nello stesso batch dell'istruzione SQL dell'utente perché l'istruzione SQL dell'utente può contenere un'istruzione che deve essere la prima in un batch. Il driver deve inviare le istruzioni SET TEXTSIZE e SET ROWCOUNT in un batch distinto, che genera automaticamente un round trip aggiuntivo al server.  
  
## <a name="see-also"></a>Vedere anche  
 [Esecuzione di query &#40;&#41;ODBC](../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
  
