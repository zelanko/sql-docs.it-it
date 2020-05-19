---
title: Utilizzo del recupero automatico con i cursori ODBC | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC cursors, autofetch
- autofetch option
- cursors [ODBC], autofetch
ms.assetid: 57bd55f4-8945-4d8d-9f58-d30c81d2a514
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a15cc12787f5a7d05699737772e7478d57b6f6e8
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82705604"
---
# <a name="using-autofetch-with-odbc-cursors"></a>Utilizzo del recupero automatico con i cursori ODBC
  Quando si è connessi a un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC di Native Client supporta un'opzione di recupero automatico quando si utilizza qualsiasi tipo di cursore del server. Con il recupero automatico, la funzione **SQLExecute** o **SQLExecDirect** che apre il cursore dispone anche di una funzione implicita [SQLFetchScroll](../../native-client-odbc-api/sqlfetchscroll.md)(SQL_FIRST). Le righe incluse nel primo set di righe vengono restituite alle variabili di applicazione associate come parte dell'esecuzione dell'istruzione, evitando in questo modo un altro round trip del server nella rete. [SQLGetData](../../native-client-odbc-api/sqlgetdata.md) non è supportato quando è abilitata l'opzione di recupero automatico; è necessario associare le colonne del set di risultati alle variabili di programma.  
  
 Le applicazioni richiedono il recupero automatico impostando l'attributo di istruzione SQL_SOPT_SS_CURSOR_OPTIONS specifico del driver su SQL_CO_AF.  
  
## <a name="see-also"></a>Vedere anche  
 [Dettagli sulla programmazione dei cursori &#40;&#41;ODBC](cursor-programming-details-odbc.md)  
  
  
