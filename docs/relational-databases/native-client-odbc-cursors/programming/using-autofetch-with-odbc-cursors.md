---
title: Utilizzo del recupero automatico con i cursori ODBC . Documenti Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC cursors, autofetch
- autofetch option
- cursors [ODBC], autofetch
ms.assetid: 57bd55f4-8945-4d8d-9f58-d30c81d2a514
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 812f4742dfe8273c4e96fc5205626fe1f6c07347
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298414"
---
# <a name="using-autofetch-with-odbc-cursors"></a>Utilizzo del recupero automatico con i cursori ODBC
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Quando si è [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]connessi [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a un'istanza di , il driver ODBC Native Client supporta un'opzione di lettura automatica quando si utilizza qualsiasi tipo di cursore del server. Con il recupero automatico, la funzione **SQLExecute** o **SQLExecDirect** che apre il cursore ha anche una funzione [SQLFetchScroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)(SQL_FIRST) implicita. Le righe incluse nel primo set di righe vengono restituite alle variabili di applicazione associate come parte dell'esecuzione dell'istruzione, evitando in questo modo un altro round trip del server nella rete. [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) non è supportato quando l'opzione di lettura automatica è abilitata. Le colonne del set di risultati devono essere associate alle variabili di programma.  
  
 Le applicazioni richiedono il recupero automatico impostando l'attributo di istruzione SQL_SOPT_SS_CURSOR_OPTIONS specifico del driver su SQL_CO_AF.  
  
## <a name="see-also"></a>Vedere anche  
 [Dettagli di programmazione del cursore &#40;&#41;ODBCCursor Programming Details to ODBC&#41;](../../../relational-databases/native-client-odbc-cursors/programming/cursor-programming-details-odbc.md)  
  
  
