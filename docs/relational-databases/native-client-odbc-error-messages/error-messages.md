---
title: I messaggi di errore | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, errors
- messages [ODBC], types
- ODBC error handling, message types
- errors [ODBC], types
ms.assetid: 46c0c22e-d105-4d5b-bb9d-5694472e8651
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: cdf6421fa237333207b090c75d14ea57f9f9e02a
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53201860"
---
# <a name="error-messages"></a>messaggi di errore
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Il testo dei messaggi restituiti dal [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client viene inserito nella *MessageText* parametro **SQLGetDiagRec**. L'origine di un errore viene indicata dall'intestazione del messaggio:  
  
 [Microsoft][Gestione driver ODBC]  
 Questi errori vengono generati da Gestione driver ODBC.  
  
 [Microsoft][Libreria di cursori ODBC]  
 Questi errori vengono generati dalla libreria di cursori ODBC.  
  
 [Microsoft][SQL Server Native Client]  
 Questi errori vengono generati dal [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client. Se non sono presenti altri nodi con il nome di una libreria di rete o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], l'errore è stato rilevato nel driver.  
  
 [Microsoft] [SQL Server Native Client] [*Net-Transportname*]  
 Questi errori vengono generati dal [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] libreria di rete, in cui *Net-Transportname* è il nome visualizzato di un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trasporto di rete client (ad esempio, Named Pipes, Shared Memory, TCP/IP Sockets o VIA). Il resto del messaggio di errore contiene la funzione della libreria di rete chiamata e la funzione chiamata nell'API di rete sottostante dalla funzione TDS. Il *pfNative* codice di errore restituito con questi errori è il codice di errore dallo stack di protocollo di rete sottostante.  
  
 [Microsoft] [SQL Server Native Client] [ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]]  
 Questi errori vengono generati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il resto del messaggio di errore corrisponde al testo del messaggio di errore restituito da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il *pfNative* codice restituito con questi errori è il numero di errore [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni su un elenco di messaggi di errore (e i relativi numeri) che può essere restituito da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere le colonne descrizione ed errore del **sysmessages** tabella di sistema il **master** database in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione di errori e messaggi](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
