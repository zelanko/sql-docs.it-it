---
title: Utilizzo del recupero automatico con i cursori ODBC | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298414"
---
# <a name="using-autofetch-with-odbc-cursors"></a>Utilizzo del recupero automatico con i cursori ODBC
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Quando si è connessi a un' [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , il driver ODBC di Native Client supporta un'opzione di recupero automatico quando si utilizza qualsiasi tipo di cursore del server. Con il recupero automatico, la funzione **SQLExecute** o **SQLExecDirect** che apre il cursore dispone anche di una funzione implicita [SQLFetchScroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)(SQL_FIRST). Le righe incluse nel primo set di righe vengono restituite alle variabili di applicazione associate come parte dell'esecuzione dell'istruzione, evitando in questo modo un altro round trip del server nella rete. [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) non è supportato quando è abilitata l'opzione di recupero automatico; è necessario associare le colonne del set di risultati alle variabili di programma.  
  
 Le applicazioni richiedono il recupero automatico impostando l'attributo di istruzione SQL_SOPT_SS_CURSOR_OPTIONS specifico del driver su SQL_CO_AF.  
  
## <a name="see-also"></a>Vedere anche  
 [Dettagli sulla programmazione dei cursori &#40;&#41;ODBC](../../../relational-databases/native-client-odbc-cursors/programming/cursor-programming-details-odbc.md)  
  
  
